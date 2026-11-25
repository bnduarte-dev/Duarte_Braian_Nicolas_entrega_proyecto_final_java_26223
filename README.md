# API de Gestión de Artículos

API REST desarrollada con Java 17 y Spring Boot 3.2.5 para administrar artículos mediante operaciones CRUD y persistencia en una base de datos MySQL/MariaDB.

## Tecnologías

- Java 17
- Spring Boot 3.2.5
- Spring Web
- Spring Data JPA / Hibernate
- MySQL Connector/J
- Maven
- MySQL o MariaDB

## Requisitos

- JDK 17
- Apache Maven
- MySQL o MariaDB en ejecución
- Postman (opcional, para probar los endpoints)

## Base de datos

Crear la base de datos antes de iniciar la aplicación:

```sql
CREATE DATABASE articulos_db;
```

La configuración de conexión se encuentra en `src/main/resources/application.properties`. La configuración original espera:

- Host: `localhost`
- Puerto: `3306`
- Base de datos: `articulos_db`
- Usuario: `root`
- Contraseña: vacía

Ajustar usuario y contraseña en `application.properties` si la instalación local utiliza credenciales diferentes. No publicar contraseñas reales en el repositorio.

## Ejecutar

Desde la carpeta que contiene `pom.xml`:

```bash
mvn spring-boot:run
```

La API queda disponible en:

```text
http://localhost:8080
```

## Endpoints

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/api/articulos` | Listar artículos |
| GET | `/api/articulos/{id}` | Consultar un artículo por ID |
| POST | `/api/articulos` | Crear un artículo |
| PUT | `/api/articulos/{id}` | Modificar un artículo |
| DELETE | `/api/articulos/{id}` | Eliminar un artículo |

### Ejemplo de creación

`POST http://localhost:8080/api/articulos`

```json
{
  "nombre": "Lapicera",
  "precio": 200.00
}
```

## Pruebas con Postman

Se puede importar la colección `articulo-api-mysql.postman_collection.json` (si se agrega al repositorio) o importar el archivo de colección entregado por separado. Ejecutar las solicitudes en orden: listar, crear, consultar, modificar, eliminar y verificar eliminación. La solicitud POST guarda automáticamente el ID creado para las solicitudes siguientes.
