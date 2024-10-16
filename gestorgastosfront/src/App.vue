<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="income" :expenses="expenses" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed, onMounted } from "vue";
import axios from "axios";
import { useToast } from "vue-toastification";

const toast = useToast();
const transactions = ref([]);

// Obtener todas las transacciones al montar la aplicación
onMounted(async () => {
  try {
    const response = await axios.get("http://localhost:8082/api/transactions");
    transactions.value = response.data;
  } catch (error) {
    toast.error("Failed to fetch transactions.");
  }
});

// Calcular el total del balance
const total = computed(() =>
  transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0)
);

// Calcular los ingresos
const income = computed(() =>
  transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
);

// Calcular los gastos
const expenses = computed(() =>
  transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
);

// Agregar nueva transacción
const handleTransactionSubmitted = async (transactionData) => {
  try {
    const response = await axios.post(
      "http://localhost:8082/api/transactions",
      transactionData
    );
    transactions.value.push(response.data);
    toast.success("Transaction added.");
  } catch (error) {
    toast.error("Failed to add transaction.");
  }
};

// Eliminar una transacción
const handleTransactionDeleted = async (id) => {
  try {
    await axios.delete(`http://localhost:8082/api/transactions/${id}`);
    transactions.value = transactions.value.filter(
      (transaction) => transaction.id !== id
    );
    toast.success("Transaction deleted.");
  } catch (error) {
    toast.error("Failed to delete transaction.");
  }
};
</script>

<style src="./assets/style.css"></style>
