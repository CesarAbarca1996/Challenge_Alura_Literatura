# Challenge_Alura_Literatura
Literalura es una aplicacion JAVA + Spring + JPA &amp; JPQL de manejo de base de datos relacional SQL de libros y autores.
# Proyecto API de Biblioteca

## Descripción
Este proyecto consiste en el desarrollo de una aplicación basada en **Java** y el framework **Spring**, orientada al manejo de una base de datos relacional para gestionar información de libros y autores. La API se conecta a una fuente de datos externa para obtener información relevante de libros.

## Funcionalidades Principales
1. Gestión de autores y libros mediante operaciones CRUD.
2. Validación de datos como fechas de nacimiento y muerte de autores.
3. Conexión con una API externa para la búsqueda de libros.
4. Integración con PostgreSQL para almacenamiento de datos.
5. Generación de datos iniciales mediante métodos preconfigurados.

---

## Configuración Inicial
### Requisitos Previos
- **Java 17** o superior.
- **PostgreSQL 14**.
- **PgAdmin4** para gestión de la base de datos.

### Variables de Entorno
Asegúrate de configurar las siguientes variables en el archivo `application.properties`:

```properties
spring.application.name=biblioteca
spring.datasource.url=jdbc:postgresql://${DB_HOST}/${DB_NOMBRE}
spring.datasource.username=${DB_USER}
spring.datasource.password=${DB_PASSWORD}
spring.datasource.driver-class-name=org.postgresql.Driver
hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.format-sql=false
```

---

## Estructura del Proyecto
### Paquetes Principales
- **controller**: Maneja las solicitudes HTTP y redirige las acciones correspondientes al servicio.
- **service**: Contiene la lógica de negocio.
- **repository**: Interactúa directamente con la base de datos utilizando JPA.
- **model**: Define las entidades del proyecto (Autor, Libro).

### Dependencias
El proyecto utiliza las siguientes librerías principales:

1. Spring Boot Starter Data JPA.
2. PostgreSQL Driver.
3. Hibernate ORM.

---

## Endpoints Disponibles
| Método | Endpoint                          | Descripción                       |
|--------|-----------------------------------|-----------------------------------|
| GET    | /libros                           | Obtiene una lista de todos los libros registrados. |
| GET    | /libros/{id}                      | Obtiene detalles de un libro por su ID. |
| POST   | /libros                           | Registra un nuevo libro. |
| DELETE | /libros/{id}                      | Elimina un libro existente por su ID. |
| GET    | /autores                          | Lista todos los autores. |
| GET    | /autores/{id}                     | Muestra información de un autor específico. |

---

## Ejemplo de Configuración Inicial
### Método init() para inicialización de datos:

```java
@PostConstruct
public void init() {
    if (repositorioAutor.count() == 0) {
        Autor autor = new Autor("Gabriel García Márquez", 1927, 2014);
        Libro libro = new Libro("Cien años de soledad", autor);
        repositorioAutor.save(autor);
        repositorioLibro.save(libro);
    }
}
```

---

## Manejo de Errores
El sistema implementa excepciones personalizadas para una mejor gestión de errores.

### Ejemplo: Excepción de Libro Existente
```java
package com.biblioteca.service;

public class LibroExistenteException extends RuntimeException {
    public LibroExistenteException(String mensaje) {
        super(mensaje);
    }
}
```

---

## Notas Adicionales
1. La conexión con la API externa se realiza a través de peticiones GET para obtener información adicional de libros.
2. Se recomienda manejar los datos sensibles, como las credenciales de la base de datos, utilizando un gestor de secretos.
3. Asegúrate de que la base de datos esté correctamente inicializada antes de ejecutar la aplicación.

