
# ForoHub API - Proyecto con Java y Spring Boot

## Descripción
**ForoHub API** es un proyecto desarrollado en **Java** utilizando el framework **Spring Boot**, que proporciona una API REST para la gestión de un foro. Este sistema permite a los usuarios autenticados crear, listar, actualizar y eliminar tópicos de discusión. Además, incluye autenticación mediante **JWT (JSON Web Tokens)** para garantizar la seguridad.

## Características principales
- Crear, listar, actualizar y eliminar tópicos.
- Autenticación y autorización mediante JWT.
- Documentación interactiva de la API con **Springdoc OpenAPI**.
- Implementación de códigos de estado HTTP para manejar las respuestas.
- Base de datos configurable (por defecto, **MySQL**).
- Migración de base de datos gestionada con **Flyway**.

## Tecnologías utilizadas
- **Java 17**
- **Spring Boot 3.x**
- **Maven**
- **JWT (JSON Web Tokens)**
- **Flyway** para la gestión de migraciones.
- **Springdoc OpenAPI** para documentación de la API.
- **Base de datos**: MySQL (configurable).
- **Insomnia/Postman** para pruebas de la API.

## Endpoints disponibles

### Authentication Controller
| Método | Endpoint    | Descripción                            |
|--------|-------------|-----------------------------------------|
| POST   | `/login`    | Genera un token JWT para el usuario.    |

### Tópico Controller
| Método | Endpoint          | Descripción                             |
|--------|-------------------|----------------------------------------|
| GET    | `/topicos`        | Lista todos los tópicos creados.        |
| POST   | `/topicos`        | Crea un nuevo tópico (requiere token).  |
| GET    | `/topicos/{id}`   | Obtiene un tópico por su ID.            |
| PUT    | `/topicos/{id}`   | Actualiza un tópico por su ID.          |
| DELETE | `/topicos/{id}`   | Elimina un tópico por su ID.            |

## Documentación de la API
El proyecto utiliza **Springdoc OpenAPI** para generar una documentación interactiva accesible desde:
```
http://localhost:8080/swagger-ui.html
```
Esta interfaz permite probar los endpoints directamente desde el navegador.

## Configuración del proyecto

### Requisitos previos
- Tener instalado **Java 17** o superior.
- Tener configurado **Maven**.
- Base de datos configurada (por defecto, se utiliza **MySQL**).

### Pasos para ejecutar
1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu_usuario/foro-api.git
   ```
2. Navega al directorio del proyecto:
   ```bash
   cd foro-api
   ```
3. Configura las credenciales de la base de datos en el archivo `application.properties` o `application.yml`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost/forohub_api
   spring.datasource.username=${DATASOURCE_USERNAME}
   spring.datasource.password=${DATASOURCE_PASSWORD}
   spring.jpa.show-sql=true
   spring.jpa.properties.hibernate.format_sql=true
   server.error.include-stacktrace=never
   api.security.secret=${JWT_SECRET}
   ```
4. Ejecuta las migraciones de base de datos con Flyway:
   ```bash
   mvn flyway:migrate
   ```
5. Construye y ejecuta el proyecto:
   ```bash
   mvn spring-boot:run
   ```
6. Accede a la documentación de la API en `http://localhost:8080/swagger-ui.html`.
7. Prueba la API utilizando Insomnia o Postman.

## Seguridad
Este proyecto utiliza **JWT** para la autenticación. Los usuarios deben autenticarse en el endpoint `/login` para obtener un token. Este token se debe incluir en el encabezado `Authorization` en las solicitudes protegidas, siguiendo el formato:
```
Authorization: Bearer <token>
```

## Pruebas con Insomnia/Postman
Se incluyen archivos de configuración para importar en Insomnia o Postman y facilitar las pruebas de la API. 

## Estructura del proyecto
```
src/
├── main/
│   ├── java/
│   │   └── com.alura.forohub/
│   │       ├── controllers/       # Controladores de la API
│   │       │   ├── AuthenticationController
│   │       │   └── TopicoController
│   │       ├── domain/            # Dominio del negocio
│   │       │   ├── dto/           # Objetos de transferencia de datos
│   │       │   │   ├── DatosAutenticacionUsuario
│   │       │   │   ├── DatosRegistroTopicoDTO
│   │       │   │   ├── DatosRegistroUsuarioDTO
│   │       │   │   ├── DatosRespuestaObtenerTopicoDTO
│   │       │   │   └── DatosRespuestaTopicoDTO
│   │       │   ├── entities/      # Entidades de la base de datos
│   │       │   │   ├── Status
│   │       │   │   ├── Topico
│   │       │   │   └── Usuario
|   |       |   ├── repositories/      # Repositorios para acceso a la BD
│   │       │   │   ├── TopicoRepository
│   │       │   │   └── UsuarioRepository
│   │       ├── infra/             # Infraestructura
│   │       │   ├── security/      # Seguridad y configuración de JWT
│   │       │   |   ├── services/      # Servicios de seguridad y autenticación
│   │       │   │   |   ├── AuthenticationService
│   │       │   │   |   └── TokenService
│   │       │   │   ├── DatosJWTToken
│   │       │   │   ├── SecurityConfigurations
│   │       │   │   ├── SecurityFilter
│   │       │   ├── springdoc/     # Configuración de Springdoc OpenAPI
│   │       │   │   └── SpringDocConfiguration
│   │       │   └── ForohubApplication
│   └── resources/
│       ├── db/migration/          # Migraciones de Flyway
│       │   └── V1__create-table-usuarios-topicos.sql
│       ├── static/
│       ├── templates/
│       └── application.properties
│   ├── test/
│       ├── java/
│           └── com.alura.forohub/
│               └── ForohubApplicationTests
```
## Futuras mejoras
- Implementar un front-end para el foro.
- Agregar la funcionalidad de respuestas a los tópicos.
- Paginación y filtrado en la lista de tópicos.
- Mejorar la validación de entradas.

## Contribuciones
Si deseas contribuir a este proyecto, no dudes en abrir un pull request o crear un issue para discutir posibles mejoras.

---
¡Gracias por revisar este proyecto! Espero que te sirva como inspiración para construir tus propias aplicaciones.
