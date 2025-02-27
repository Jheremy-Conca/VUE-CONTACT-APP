# Vue Contact App

## Descripción

Vue Contact App es una aplicación web construida con Vue 3 y Vite para gestionar contactos. La aplicación permite agregar, editar y eliminar contactos, proporcionando una interfaz responsiva basada en Bootstrap.

## Demo

Puedes acceder a la aplicación desplegada en Netlify desde el siguiente enlace:
[Vue Contact App](https://vue-contact-app.netlify.app/)

## Tecnologías Utilizadas

### Frontend

- **Vue 3**: Framework progresivo de JavaScript para la construcción de interfaces de usuario.
- **Vite**: Herramienta de construcción rápida para proyectos Vue.
- **Bootstrap 5**: Framework CSS para diseño responsivo y estilizado.
- **@popperjs/core**: Librería para la gestión de tooltips y popovers en Bootstrap.

### Backend

El backend de la aplicación proporciona una API para gestionar los contactos y está construido con las siguientes tecnologías:

- **Node.js** con **Express**: Servidor backend ligero y eficiente.
- **MongoDB**: Base de datos NoSQL para almacenar los contactos.
- **Mongoose**: ODM para manejar los datos en MongoDB.
- **CORS**: Middleware para permitir peticiones entre el frontend y el backend.
- **Dotenv**: Manejo de variables de entorno.

## Instalación y Configuración

Sigue estos pasos para ejecutar el proyecto en tu entorno local.

### Clonar el repositorio

```sh
git clone https://github.com/Jheremy-Conca/VUE-CONTACT-APP.git
cd vue-contact-app
```

### Instalación de dependencias

Ejecuta el siguiente comando para instalar las dependencias necesarias:

```sh
npm install
```

### Ejecución del proyecto en desarrollo

Para ejecutar el proyecto en modo desarrollo, usa:

```sh
npm run dev
```

Esto iniciará un servidor local y podrás acceder a la aplicación desde:

```
http://localhost:5173
```

### Construcción para producción

Para generar la versión optimizada para producción, ejecuta:

```sh
npm run build
```

### Scripts Disponibles

En el archivo `package.json` están definidos los siguientes scripts:

- **dev**: Inicia el entorno de desarrollo con Vite.
- **build**: Construye la aplicación para producción.
- **preview**: Previsualiza la aplicación construida.

## Configuración del Backend

Si deseas ejecutar el backend en local, sigue estos pasos:

1. Ve a la carpeta del backend:

```sh
cd backend
```

2. Instala las dependencias:

```sh
npm install
```

3. Configura las variables de entorno en un archivo `.env` con:

```
PORT=5000
MONGO_URI=mongodb+srv://usuario:contraseña@cluster.mongodb.net/contactos
```

4. Ejecuta el servidor:

```sh
npm start
```

El backend se ejecutará en:

```
http://localhost:5000
```

## Contribución

Si deseas contribuir al proyecto, puedes hacer un fork del repositorio, crear una rama con tus cambios y enviar un pull request.

## Licencia

Este proyecto está bajo la licencia MIT.
