# API REST de Gestión de Artículos

Proyecto integrador desarrollado con **Java 17**, **Spring Boot 3.2.5** y **Spring Data JPA**, que permite administrar artículos mediante una API REST y almacenar la información en una base de datos relacional.

## Objetivo

Exponer servicios HTTP para realizar las operaciones CRUD sobre artículos. Cada artículo contiene un identificador único, un nombre y un precio.

## Tecnologías utilizadas

- Java 17
- Spring Boot 3.2.5
- Spring Web
- Spring Data JPA
- Hibernate
- Maven
- MySQL Connector/J
- XAMPP para administrar el servicio de base de datos durante el desarrollo
- Postman para probar los endpoints
- Visual Studio Code

> **Entorno de base de datos utilizado:** la consigna de la cursada indica trabajar con XAMPP y su módulo identificado como **MySQL**. En la instalación utilizada para esta demostración, el comando `mysql --version` informa **MariaDB 10.4.32**. La aplicación se conecta mediante JDBC y MySQL Connector/J. Si se utiliza otra instalación local, se deben verificar el motor, el puerto y las credenciales.

## Arquitectura

La aplicación sigue una arquitectura monolítica organizada en capas:

- **Model:** contiene la entidad `Articulo`, que representa los datos persistidos.
- **Repository:** `ArticuloRepository` extiende `JpaRepository<Articulo, Long>` y proporciona las operaciones de acceso a datos.
- **Service:** `ArticuloService` define las operaciones disponibles.
- **ServiceImpl:** `ArticuloServiceImpl` implementa la lógica de servicio y utiliza el repositorio.
- **Controller:** `ArticuloController` recibe las solicitudes HTTP, invoca al servicio y devuelve las respuestas.

El recorrido de una solicitud es: **Postman → Controller → Service → ServiceImpl → Repository → base de datos**.

## Requisitos para ejecutar

- JDK 17.
- Apache Maven (se utilizó Maven 3.10.2 en el entorno de desarrollo).
- XAMPP con el servicio de base de datos iniciado.
- Postman, para realizar las pruebas (opcional para ejecutar el servidor).

## Configuración de la base de datos

1. Iniciar el módulo **MySQL** desde XAMPP Control Panel.
2. Crear la base de datos antes de iniciar la aplicación:

```sql
CREATE DATABASE IF NOT EXISTS articulos_db;
```

3. Revisar `src/main/resources/application.properties` y adaptar host, puerto, usuario y contraseña a la instalación local.

Configuración utilizada durante las pruebas locales:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/articulos_db?useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

La contraseña aparece vacía porque el usuario `root` de la instalación local utilizada no tenía contraseña. **No publiques contraseñas personales ni credenciales privadas.** Si tu instalación tiene contraseña, configurala localmente y no la incluyas en commits públicos.

Hibernate administra la creación o actualización de la tabla `articulo` mediante `spring.jpa.hibernate.ddl-auto=update`. La base de datos `articulos_db` debe existir previamente.

## Ejecución

Desde una terminal ubicada en la carpeta donde se encuentra `pom.xml`, y utilizando JDK 17:

```bash
mvn clean package
mvn spring-boot:run
```

Cuando Spring Boot inicia correctamente, la API queda disponible en:

```text
http://localhost:8080
```

## Endpoints disponibles

La ruta base es `http://localhost:8080/api/articulos`.

| Método HTTP | Endpoint | Descripción | Respuesta esperada |
|---|---|---|---|
| GET | `/api/articulos` | Lista todos los artículos | 200 OK |
| GET | `/api/articulos/{id}` | Consulta un artículo por ID | 200 OK o 404 Not Found |
| POST | `/api/articulos` | Crea un artículo | 200 OK |
| PUT | `/api/articulos/{id}` | Actualiza un artículo existente | 200 OK o 404 Not Found |
| DELETE | `/api/articulos/{id}` | Elimina un artículo | 204 No Content o 404 Not Found |

### Ejemplo de creación

Solicitud `POST http://localhost:8080/api/articulos`, con Body en formato raw / JSON:

```json
{
  "nombre": "Lapicera",
  "precio": 200.00
}
```

El identificador se genera automáticamente en la base de datos y se devuelve en la respuesta.

## Pruebas con Postman

Se incluye la colección exportada:

`articulo-api-mysql.postman_collection.json`

Para utilizarla, importar el archivo en Postman. La colección contiene solicitudes para listar, crear, consultar por ID, modificar, eliminar y verificar la eliminación de un artículo.

## Verificación de persistencia

Se pueden consultar los datos directamente en el administrador de base de datos o ejecutar:

```sql
USE articulos_db;
DESCRIBE articulo;
SELECT * FROM articulo;
```

Los registros se almacenan en la base de datos y no solamente en memoria.

## Video de demostración

**Video de funcionamiento y pruebas de la API:**

[Ver video de demostración en YouTube](https://youtu.be/fQFWEupU_cM)

