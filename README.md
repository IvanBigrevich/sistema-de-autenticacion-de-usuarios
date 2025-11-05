# 🧩 Sistema de Autenticación de Usuarios — Node.js, Express, PostgreSQL & Sequelize

## 🔐 Descripción General

Este proyecto es un **sistema completo de autenticación y gestión de usuarios** desarrollado con **Node.js**, **Express**, **PostgreSQL** y **Sequelize ORM**.  

Permite:
- Registro y login de usuarios con contraseña encriptada (bcrypt).
- Generación y validación de tokens JWT.
- Gestión de roles (usuario y administrador).
- Creación de proyectos y tareas asociadas a usuarios.
- Control de acceso basado en roles (solo administradores pueden crear proyectos).
- API REST documentada y lista para probar con Postman.

El objetivo principal es **demostrar la implementación profesional de un sistema de autenticación backend** — modular, seguro y escalable — ideal para portafolios y entornos productivos.

---

## 🚀 Tecnologías Utilizadas

| Tecnología | Descripción |
|-------------|-------------|
| **Node.js** | Entorno de ejecución para JavaScript del lado del servidor |
| **Express.js** | Framework minimalista para construir la API REST |
| **PostgreSQL** | Base de datos relacional utilizada para persistencia |
| **Sequelize** | ORM para modelar y consultar datos de manera sencilla |
| **JWT (jsonwebtoken)** | Manejo de autenticación basada en tokens |
| **bcrypt** | Hash seguro para contraseñas |
| **dotenv** | Manejo de variables de entorno |
| **Nodemon** | Reinicio automático del servidor durante el desarrollo |

---

## 🛠️ Instalación y Configuración

### 1️⃣ Clonar el repositorio

```bash
git clone https://github.com/IvanBigrevich/sistema-de-autenticacion-de-usuarios.git
cd sistema-de-autenticacion-de-usuarios
2️⃣ Instalar dependencias

npm install
3️⃣ Configurar PostgreSQL
Asegúrate de tener PostgreSQL instalado y en ejecución.
Crea una base de datos llamada auth_db (o el nombre que prefieras):


CREATE DATABASE auth_db;
💡 Si tu instalación usa un puerto distinto (por ejemplo 5432 o 5433), asegúrate de reflejarlo en el archivo .env.

4️⃣ Crear el archivo .env
Crea un archivo .env en la raíz del proyecto con las siguientes variables (ajústalas según tu entorno):

.env:

PORT=4000
DB_HOST=localhost
DB_PORT=5433
DB_USER=postgres
DB_PASSWORD=TuContraseñaDePostgres
DB_NAME=auth_db
JWT_SECRET=supersecretkey
JWT_EXPIRES_IN=1h
🔑 Importante: No compartas tu .env públicamente.
Si usas otro puerto o contraseña, ajusta las variables en consecuencia.

```

5️⃣ Ejecutar el servidor

npm run dev
Si todo está correcto, deberías ver en la consola:


Database connection established.
Models synced.
Server listening on port 4000
🧱 Estructura del Proyecto

sistema-de-autenticacion-de-usuarios/
│
├── src/
│   ├── app.js                 # Configuración de Express y middlewares
│   ├── server.js              # Punto de entrada del servidor
│   ├── config/
│   │   └── database.js        # Configuración de Sequelize y conexión a PostgreSQL
│   ├── models/                # Definición de modelos Sequelize (User, Project, Task)
│   ├── routes/                # Rutas de la API (auth, users, projects, tasks)
│   ├── controllers/           # Lógica de cada endpoint
│   ├── middleware/            # Autenticación JWT y control de roles
│   └── utils/                 # Funciones auxiliares
│
├── .env                       # Variables de entorno (no subir a GitHub)
├── package.json               # Dependencias y scripts
└── README.md                  # Documentación del proyecto
📦 Dependencias Principales
Instaladas automáticamente con npm install:

# package.json:

"dependencies": {
  "bcrypt": "^5.1.1",
  "dotenv": "^17.2.3",
  "express": "^4.19.2",
  "jsonwebtoken": "^9.0.2",
  "pg": "^8.12.0",
  "sequelize": "^6.37.3"
},
"devDependencies": {
  "nodemon": "^3.1.10"
}
🧰 Endpoints Principales (Postman Ready)
Asegúrate de que el servidor esté ejecutándose (npm run dev).


🔸 Auth
Register
POST http://localhost:4000/api/auth/register

json
{
  "username": "ivan",
  "email": "ivan@example.com",
  "password": "secret123"
}


🔸 Login
POST http://localhost:4000/api/auth/login

json
{
  "email": "ivan@example.com",
  "password": "secret123"
}


json
{
  "user": { "id": "...", "username": "ivan", "email": "ivan@example.com" },
  "token": "<JWT_TOKEN>"
}


🔸 Usuarios
Get current user
GET http://localhost:4000/api/users/me
Header:
Authorization: Bearer <JWT_TOKEN>


🔸 Proyectos (solo admin)
Create project
POST http://localhost:4000/api/projects

json
{
  "name": "Website",
  "description": "Portfolio site"
}
Header:
Authorization: Bearer <ADMIN_JWT_TOKEN>


🔸 Tareas
Create task
POST http://localhost:4000/api/tasks

json
{
  "title": "Build auth",
  "description": "Implement login",
  "projectId": "997e9b43-89a4-4ad5-98af-394e87ebb545",
  "assigneeId": "c85f12a9-b4f3-4bb9-9f12-12f53a9f40f2"
}
⚠️ Usa IDs reales obtenidos desde tu base de datos (SELECT * FROM projects; y SELECT * FROM users;).


🔑 Roles y Permisos
Usuario normal: puede registrarse, iniciar sesión y ver su perfil.

Administrador: puede crear proyectos y asignar tareas a otros usuarios.

Los roles se definen en el modelo User y se pueden asignar directamente en la base de datos (role: 'admin').


🧠 Notas Técnicas
Las contraseñas se guardan encriptadas con bcrypt.

Los tokens JWT se firman con JWT_SECRET y expiran según JWT_EXPIRES_IN.

Sequelize sincroniza automáticamente los modelos con la base de datos (modo desarrollo).

Usa async/await y control de errores centralizado para mejor mantenibilidad.


🧪 Pruebas recomendadas
Registro y Login

Crea un nuevo usuario.

Inicia sesión y copia el token.

Acceso protegido

Usa el token en el header Authorization.

Prueba el endpoint /api/users/me.

Roles

Crea un usuario admin manualmente o desde SQL.

Crea un proyecto y asigna tareas a usuarios.


⚙️ Troubleshooting
Problema	Solución
FATAL: password authentication failed for user "postgres"	Verifica la contraseña y el puerto en .env.
Connection refused	PostgreSQL no está corriendo o puerto incorrecto.
no existe la base de datos "auth_db"	Crea la base de datos manualmente desde psql.
uuid error en creación de tareas	Usa IDs válidos de proyectos/usuarios.


👨‍💻 Autor
Iván Bigrevich
Desarrollador Full Stack — Node.js | React | PostgreSQL

⭐ Contribuciones y Uso
Este proyecto está diseñado con fines educativos y demostrativos.
Podés clonar, modificar o mejorar el código libremente, citando la fuente.

Si te gustó el proyecto, ¡dejá una ⭐ en el repositorio! 😄