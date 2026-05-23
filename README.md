# Todo List Backend - Spring Boot

Una API REST completa para gestión de tareas (Todo List) construida con Spring Boot y MySQL, lista para desplegar en Railway.

## 🚀 Características

- CRUD completo para tareas (Crear, Leer, Actualizar, Eliminar)
- Base de datos MySQL con JPA/Hibernate
- Validación de datos con Jakarta Validation
- Endpoints RESTful
- Documentación de API con Swagger/OpenAPI
- Listo para despliegue en Railway
- Docker incluido

## 📋 Prerrequisitos

- Java 17 o superior
- Maven 3.6+
- MySQL 8.0+ (para desarrollo local)
- Cuenta en Railway (para despliegue en la nube)

## 🛠️ Instalación Local

1. **Clonar el repositorio**
   ```bash
   git clone <tu-repositorio>
   cd todolist
   ```

2. **Configurar la base de datos MySQL**
   ```sql
   CREATE DATABASE todolist;
   ```

3. **Configurar las credenciales de la base de datos**
   
   Edita `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/todolist
   spring.datasource.username=tu_usuario
   spring.datasource.password=tu_contraseña
   ```

4. **Ejecutar la aplicación**
   ```bash
   mvn spring-boot:run
   ```

   La aplicación estará disponible en `http://localhost:8080`

## � Documentación de API con Swagger

La aplicación incluye Swagger/OpenAPI para documentación interactiva de la API.

### Acceder a Swagger UI

- **Localmente**: `http://localhost:8080/swagger-ui.html`
- **En Railway**: `https://tu-url-railway.railway.app/swagger-ui.html`

### Acceder a OpenAPI JSON

- **Localmente**: `http://localhost:8080/api-docs`
- **En Railway**: `https://tu-url-railway.railway.app/api-docs`

Swagger UI te permite:
- Ver todos los endpoints disponibles
- Probar los endpoints directamente desde la interfaz
- Ver los modelos de datos y esquemas
- Descargar la especificación OpenAPI en formato JSON

## � API Endpoints

### Obtener todas las tareas
```http
GET /api/todos
```

### Obtener una tarea por ID
```http
GET /api/todos/{id}
```

### Obtener tareas por estado (completadas/pendientes)
```http
GET /api/todos/completed/{true|false}
```

### Buscar tareas por título
```http
GET /api/todos/search?title=texto
```

### Crear una nueva tarea
```http
POST /api/todos
Content-Type: application/json

{
  "title": "Nueva tarea",
  "description": "Descripción de la tarea",
  "completed": false
}
```

### Actualizar una tarea
```http
PUT /api/todos/{id}
Content-Type: application/json

{
  "title": "Título actualizado",
  "description": "Descripción actualizada",
  "completed": true
}
```

### Alternar estado de completado
```http
PATCH /api/todos/{id}/toggle
```

### Eliminar una tarea
```http
DELETE /api/todos/{id}
```

## 🚀 Despliegue en Railway

### 1. Preparar el repositorio

Asegúrate de tener todos los archivos en tu repositorio de Git:
- `pom.xml`
- `Dockerfile`
- `Procfile`
- Código fuente en `src/main/java/`
- Configuración en `src/main/resources/`

### 2. Crear proyecto en Railway

1. Ve a [railway.app](https://railway.app)
2. Crea una cuenta o inicia sesión
3. Haz clic en "New Project"
4. Selecciona "Deploy from GitHub repo"
5. Conecta tu repositorio

### 3. Configurar la base de datos MySQL en Railway

1. En tu proyecto de Railway, haz clic en "New Service"
2. Selecciona "Database"
3. Elige "MySQL"
4. Railway creará automáticamente la base de datos

### 4. Configurar variables de entorno

Railway configurará automáticamente las variables de entorno necesarias:
- `DATABASE_URL`
- `DATABASE_USERNAME`
- `DATABASE_PASSWORD`

La aplicación usará `application-railway.properties` que lee estas variables.

### 5. Desplegar

Railway detectará automáticamente el `Dockerfile` y `Procfile` y desplegará la aplicación.

### 6. Obtener la URL

Una vez desplegado, Railway te proporcionará una URL pública para tu API.

## 🐳 Docker Local

Para construir y ejecutar con Docker localmente:

```bash
# Construir la imagen
docker build -t todo-list-backend .

# Ejecutar el contenedor
docker run -p 8080:8080 \
  -e DATABASE_URL=jdbc:mysql://host.docker.internal:3306/todolist \
  -e DATABASE_USERNAME=root \
  -e DATABASE_PASSWORD=tu_contraseña \
  todo-list-backend
```

## 📁 Estructura del Proyecto

```
todolist/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── todolist/
│       │           ├── TodoListApplication.java
│       │           ├── controller/
│       │           │   └── TodoController.java
│       │           ├── service/
│       │           │   └── TodoService.java
│       │           ├── repository/
│       │           │   └── TodoRepository.java
│       │           └── entity/
│       │               └── Todo.java
│       └── resources/
│           ├── application.properties
│           └── application-railway.properties
├── Dockerfile
├── Procfile
├── pom.xml
└── README.md
```

## 🔧 Tecnologías Utilizadas

- **Spring Boot 3.2.5** - Framework principal
- **Spring Data JPA** - ORM y gestión de datos
- **MySQL Connector** - Driver de base de datos
- **Jakarta Validation** - Validación de datos
- **SpringDoc OpenAPI** - Documentación de API con Swagger UI
- **Maven** - Gestión de dependencias
- **Docker** - Contenedores para despliegue

## 📝 Notas Importantes

- La aplicación crea automáticamente la tabla `todos` si no existe
- Los campos `created_at` y `updated_at` se gestionan automáticamente
- La validación de datos está habilitada en los endpoints POST y PUT
- CORS está configurado para permitir acceso desde cualquier origen (ajustar para producción)

## 🤝 Contribuir

Si deseas contribuir a este proyecto:
1. Fork el repositorio
2. Crea una rama para tu feature
3. Commit tus cambios
4. Push a la rama
5. Abre un Pull Request

## 📄 Licencia

Este proyecto es de código abierto y está disponible bajo la licencia MIT.
