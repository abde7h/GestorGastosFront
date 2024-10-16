# Expense Tracker Frontend - Vue.js + Vite

Este proyecto es la parte frontend del Expense Tracker, construido con **Vue 3** y **Vite**. El proyecto se conecta a un backend desarrollado en **Spring Boot** para proporcionar una aplicación completa de seguimiento de gastos.

## Características

- **Balance de gastos**: Visualiza el balance total de ingresos y gastos.
- **Agregar transacciones**: Permite agregar nuevas transacciones (ingresos o gastos).
- **Eliminar transacciones**: Elimina las transacciones no deseadas.
- **Interfaz moderna**: Usamos `vue-toastification` para mostrar notificaciones agradables.

## Requisitos Previos

Antes de comenzar, asegúrate de tener instalados los siguientes componentes:

- **Node.js** (v14 o superior)
- **NPM** (normalmente se incluye con Node.js)
- Un **backend** en **Spring Boot** corriendo en `http://localhost:8080`

## Instalación

Sigue los siguientes pasos para configurar e iniciar el proyecto:

1. Clona el repositorio del frontend:

   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd expense-tracker-frontend
   ```

2. Instala las dependencias necesarias:

   ```bash
   npm install
   ```

3. Instala **vue-toastification** para mostrar notificaciones y **axios** para realizar solicitudes HTTP:

   ```bash
   npm install vue-toastification@next axios
   ```

## Configuración

- Revisa el archivo **vite.config.js** para asegurarte de que está correctamente configurado el proxy para comunicarte con el backend:

  ```javascript
  import { defineConfig } from "vite";
  import vue from "@vitejs/plugin-vue";

  export default defineConfig({
    plugins: [vue()],
    server: {
      proxy: {
        "/api": {
          target: "http://localhost:8080",
          changeOrigin: true,
        },
      },
    },
  });
  ```

  Con esta configuración, todas las solicitudes a `/api` se redirigen al backend en el puerto `8080`.

- Asegúrate de que el backend de Spring Boot esté corriendo en `http://localhost:8080`.

## Ejecución

Para iniciar el servidor de desarrollo, ejecuta el siguiente comando:

```bash
npm run dev
```

Esto iniciará el servidor en `http://localhost:5173`, donde podrás ver la aplicación en acción.

## Estructura del Proyecto

```
expense-tracker-frontend/
 ├── public/
 ├── src/
 │    ├── assets/
 │    │    └── style.css        # Estilos de la aplicación
 │    ├── components/
 │    │    ├── Header.vue       # Componente del encabezado
 │    │    ├── Balance.vue      # Componente que muestra el balance
 │    │    ├── IncomeExpenses.vue # Componente para ingresos y gastos
 │    │    ├── TransactionList.vue # Componente que lista las transacciones
 │    │    └── AddTransaction.vue # Componente para agregar transacciones
 │    ├── App.vue               # Componente principal de la aplicación
 │    └── main.js               # Punto de entrada del proyecto
 ├── index.html                 # Archivo principal HTML
 └── package.json               # Configuración del proyecto y dependencias
```

## Uso

- **Agregar transacciones**: Utiliza el formulario "Add new transaction" para agregar una nueva transacción de ingreso o gasto.
- **Eliminar transacciones**: Haz clic en el botón "x" al lado de cada transacción para eliminarla.
- **Balance e Ingresos/Gastos**: Los totales se actualizan automáticamente según las transacciones registradas.

## Dependencias Clave

- **Vue 3**: Framework progresivo para construir interfaces de usuario.
- **Vite**: Herramienta de desarrollo rápido y construcción de proyectos para Vue.
- **Axios**: Biblioteca para realizar solicitudes HTTP al backend.
- **Vue-toastification**: Plugin para mostrar notificaciones agradables y personalizables.

## Estilos Personalizados

La aplicación utiliza la fuente **Lato** y define varias clases CSS para mantener un diseño limpio y moderno. Algunas de las clases destacadas incluyen:

- **.inc-exp-container**: Contenedor para mostrar ingresos y gastos con sombras sutiles.
- **.money.plus / .money.minus**: Define los colores para los ingresos (verde) y gastos (rojo).
- **.list li**: Cada transacción se muestra con una sombra distintiva y un borde lateral que indica si es un ingreso o un gasto.

## Errores Comunes

1. **CORS**: Asegúrate de tener configurado CORS en el backend de Spring Boot para permitir solicitudes del frontend (`http://localhost:5173`).

2. **Backend no disponible**: Si no puedes agregar transacciones o ver las transacciones actuales, verifica que el backend esté corriendo en el puerto `8080`. O en el indicado en tu proyecto back-end.

## Despliegue

Cuando estés listo para desplegar tu aplicación, sigue estos pasos:

1. Genera una versión optimizada para producción:

   ```bash
   npm run build
   ```

2. Los archivos optimizados se colocarán en la carpeta **dist/**, la cual puedes servir usando cualquier servidor web.

## Créditos

Este proyecto fue construido como ejemplo de una aplicación **full stack** utilizando **Vue.js + Vite** para el frontend y **Spring Boot** para el backend.

## Enlace al back end

[GestorGastosBack](https://github.com/abde7h/GestorGastosBack)

## Licencia

MIT License

# GestorGastos
