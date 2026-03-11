# Documentación del Proyecto: FoodBites API

[![English](https://img.icons8.com/color/48/great-britain.png )](README_EN.md)  [![Español](https://img.icons8.com/color/48/spain.png)](README.md)

---

## Resumen
El presente proyecto, denominado "FoodBites API", consiste en el desarrollo de un servicio web RESTful para la gestión integral de una plataforma de food trucks. El objetivo principal es facilitar la administración de los camiones de comida, sus menús, los pedidos de los clientes, y el seguimiento de ubicaciones e interacciones de usuario, todo centralizado en un sistema backend robusto.

El sistema se ha construido utilizando una arquitectura basada en Java. En el lado del servidor (Backend), se ha optado por **Spring Boot**, un framework que garantiza escalabilidad, mantenibilidad y rapidez en el desarrollo, junto con **MySQL** como sistema de gestión de base de datos relacional para asegurar la integridad y persistencia de la información bajo el esquema `proyectoad`.

La aplicación expone una serie de endpoints para gestionar entidades esenciales como: Food Trucks, Menús, Pedidos, Usuarios, Ubicaciones y Notificaciones. Las operaciones CRUD, junto con búsquedas geo-localizadas y análisis básicos de pedidos, están completamente implementadas.

Este proyecto fue creado por Andrés Caso Iglesias para la asignatura "Acceso a Datos" del grado "Técnico Superior en Desarrollo de Aplicaciones Multiplataforma" (DAM), demuestra la aplicación práctica de tecnologías de backend empresarial y el diseño de APIs eficientes.

---

## Palabras Clave
Food Trucks, Desarrollo Backend, Spring Boot, Java 17, MySQL, API REST, Gestión de Pedidos, DAM.

---

## Índice General

### CAPÍTULO 1. MEMORIA DEL PROYECTO
1.1 RESUMEN DE LA MOTIVACIÓN
1.2 OBJETIVOS

### CAPÍTULO 2. INTRODUCCIÓN
2.1 JUSTIFICACIÓN DEL PROYECTO
2.2 ESTUDIO DE LA SITUACIÓN ACTUAL

### CAPÍTULO 3. ASPECTOS TEÓRICOS
3.1 JAVA Y SPRING BOOT
3.2 ARQUITECTURA REST
3.3 MYSQL Y SPRING DATA JPA
3.4 MAVEN

### CAPÍTULO 4. ANÁLISIS
4.1 DEFINICIÓN DEL SISTEMA
4.2 CATÁLOGO DE REQUISITOS
4.3 IDENTIFICACIÓN DE ACTORES DEL SISTEMA
4.4 ESPECIFICACIÓN DE CASOS DE USO

### CAPÍTULO 5. PLAN DE PRUEBAS
5.1 INTRODUCCIÓN
5.2 DISEÑO Y PLANIFICACIÓN DEL PLAN DE PRUEBAS
5.3 ANÁLISIS E INTERPRETACIÓN DE RESULTADOS

### CAPÍTULO 6. DISEÑO DEL SISTEMA
6.1 ARQUITECTURA DEL SISTEMA
6.2 DISEÑO DE CLASES (MVC)
6.3 DISEÑO DE LA BASE DE DATOS

### CAPÍTULO 7. IMPLEMENTACIÓN DEL SISTEMA
7.1 LENGUAJES Y HERRAMIENTAS
7.2 ESTRUCTURA DEL PROYECTO

### CAPÍTULO 8. MANUALES DEL SISTEMA
8.1 MANUAL DE INSTALACIÓN
8.2 MANUAL DE USUARIO / ENDPOINTS API

### CAPÍTULO 9. CONCLUSIONES Y AMPLIACIONES
9.1 CONCLUSIONES
9.2 AMPLIACIONES

### CAPÍTULO 10. APÉNDICES
10.1 GLOSARIO

---

## Capítulo 1. Memoria del proyecto

### 1.1 Resumen de la motivación
La comida callejera y los food trucks representan un sector en auge. Sin embargo, su naturaleza móvil complica la fidelización con los clientes y la gestión centralizada de menús y pedidos. La motivación de este proyecto es proveer una infraestructura backend sólida (API) que permita a futuras aplicaciones móviles o web solucionar este problema, conectando a los dueños de los food trucks con hambrientos clientes en tiempo real.

### 1.2 Objetivos
1. Desarrollar una API RESTful funcional para la gestión de Food Trucks.
2. Permitir el registro y gestión de menús, así como la actualización de la ubicación actual de los camiones.
3. Procesar y gestionar los pedidos realizados por los usuarios.
4. Asegurar la persistencia de datos mediante una base de datos relacional MySQL (`proyectoad`).
5. Proveer endpoints de búsqueda por proximidad (ciudad/calle) y recomendaciones por tipo de cocina.

---

## Capítulo 2. Introducción

### 2.1 Justificación del proyecto
El sector de la restauración itinerante necesita herramientas digitales ágiles. Los perfiles en redes sociales estáticas no son suficientes para gestionar pedidos en tiempo real o informar de cambios súbitos de ubicación. FoodBites API se justifica como la pieza central que permite sincronizar la oferta gastronómica móvil con la demanda del consumidor, eliminando fricciones en el proceso de compra.

### 2.2 Estudio de la situación actual
Existen plataformas genéricas de entrega de comida (Glovo, Uber Eats), pero no están optimizadas para la inestabilidad de ubicación de los food trucks. FoodBites busca crear un ecosistema dedicado, donde la "ubicación actual" es un atributo dinámico de primera clase, y donde el catálogo se adapta a las particularidades de estos negocios.

---

## Capítulo 3. Aspectos teóricos

### 3.1 Java y Spring Boot
**Java 17** es el lenguaje principal. **Spring Boot (3.3.5)** es el framework elegido debido a su paradigma de "convención sobre configuración", facilitando el arranque rápido de aplicaciones basadas en Spring, con servidores web embebidos (Tomcat) y autoconfiguración de componentes.

### 3.2 Arquitectura REST
El sistema está diseñado bajo el estilo arquitectónico Representational State Transfer (REST), exponiendo recursos a través de URIs predecibles y utilizando los métodos HTTP estándar (GET, POST, PUT, DELETE) para semántica de operaciones CRUD.

### 3.3 MySQL y Spring Data JPA
**MySQL (8.x)** se utiliza como RDBMS. La capa de persistencia está gestionada mediante **Spring Data JPA** y **Hibernate**, lo que permite mapear las clases de Java (Entidades) directamente a las tablas de la base de datos, reduciendo el código repetitivo de acceso a datos.

### 3.4 Maven
Se usa **Apache Maven (3.6.x+)** para la gestión de dependencias y el ciclo de vida de construcción del proyecto (compilación, pruebas y empaquetado).

---

## Capítulo 4. Análisis

### 4.1 Definición del sistema
El sistema abarca las operaciones de backend necesarias para dar vida a la plataforma FoodBites. Recibe peticiones HTTP con cargas útiles en JSON, procesa la lógica de negocio, interactúa con la base de datos y devuelve respuestas JSON.

### 4.2 Catálogo de requisitos
*   **Gestión de Food Trucks**: Permitir registro, actualización, borrado y listado (CRUD). Búsquedas por ubicación y recomendaciones.
*   **Gestión de Menús**: CRUD de platos asociados a un Food Truck.
*   **Gestión de Pedidos**: Registro de ventas y cálculo de totales.
*   **Otras entidades**: Usuarios, Ubicaciones y Notificaciones completan el ecosistema.

### 4.3 Identificación de actores del sistema (A nivel API)
*   **Aplicación Cliente**: El frontend (web o móvil) que consume la API en nombre de Usuarios Finales o Dueños de Food Trucks.
*   **Desarrollador / Tester**: Utiliza curl o Postman para interactuar con los endpoints directamente.

### 4.4 Especificación de casos de uso principales
*   **Registrar un Food Truck**: El cliente envía un POST con nombre, tipo de cocina y ubicación preliminar.
*   **Listar Food Trucks Cercanos**: El cliente hace un GET con parámetros de ciudad y calle.
*   **Actualizar Ubicación**: Se envía un PUT al ID del Food Truck con la nueva información.

---

## Capítulo 5. Plan de pruebas

### 5.1 Introducción
Se evaluará la funcionalidad general de los endpoints utilizando herramientas de automatización y llamadas de red.

### 5.2 Diseño y planificación
*   **Pruebas Unitarias de Servicios**: El proyecto incluye un directorio `src/test/java` con tests para la capa de servicios (p.ej., `FoodTruckServiceTest.java`, `MenuServiceTest.java`).
*   **Pruebas Funcionales API**: Se utiliza una batería de scripts basados en comandos `curl` (documentada en `docs/Andres_CasoIglesias_testAPI.docx`).

### 5.3 Análisis de Resultados
La ejecución exitosa de los comandos curl devolviendo los códigos de estado HTTP correctos (200 OK, 201 Created) y la prevención de entradas erróneas (400 Bad Request) aseguran la robustez frente al cliente. Las pruebas unitarias cubren el ciclo de vida de las entidades.

---

## Capítulo 6. Diseño del sistema

### 6.1 Arquitectura del sistema
La API sigue un clásico modelo de arquitectura de tres capas:
1.  **Controlador (Controller)**: Maneja las llamadas HTTP, extrae parámetros superficiales y devuelve respuestas.
2.  **Servicio (Service)**: Contiene toda la lógica de negocio y validaciones.
3.  **Repositorio (Repository)**: Interfaces JPA que Spring instancia automáticamente para acceder a MySQL.

### 6.2 Diseño de Clases (MVC)
El diseño se refleja fielmente en los paquetes del proyecto (`com.foodbites.truck_bites.*`):
*   `model`: Clases anotadas con `@Entity` que representan tablas.
*   `dto`: Objetos de transferencia de datos utilizados en las peticiones/respuestas.
*   `repository`: Interfaces que extienden de `JpaRepository`.
*   `controller`: Clases anotadas con `@RestController`.

### 6.3 Diseño de la base de datos
Se asume un diseño relacional donde `FoodTrucks` es una entidad central. `Menus` tiene una clave foránea apuntando al food truck. `Pedidos` relaciona a los `Usuarios` con los `FoodTrucks` y sus platos.

---

## Capítulo 7. Implementación del sistema

### 7.1 Lenguajes y herramientas
*   Java SDK 17+
*   Spring Boot 3.3.5
*   IDE: IntelliJ IDEA / VS Code
*   Terminal y Apache Maven para ejecución de ciclos de vida.

### 7.2 Estructura del Proyecto
```text
FoodBites API
├── src/main/java/com/foodbites/truck_bites/
│   ├── controller/      # Endpoints de la API
│   ├── dto/             # Objetos de Datos (DTO)
│   ├── model/           # Entidades JPA
│   ├── repository/      # Acceso a Datos (Interfaces JPA)
│   ├── service/         # Lógica de Negocio
│   └── TruckBitesApplication.java
├── src/main/resources/
│   ├── application.properties
│   └── data.sql         # Para carga inicial si es necesario
├── src/test/java/       # Pruebas de Servicios (JUnit)
└── pom.xml              # Dependencias de Maven
```

---

## Capítulo 8. Manuales del sistema

### 8.1 Manual de instalación
1. Clonar: `git clone https://github.com/your-username/foodbites-api.git`
2. Base de datos: Ejecutar `CREATE DATABASE proyectoad;` en tu instancia MySQL.
3. Configurar: Editar `src/main/resources/application.properties` con tu usuario y contraseña de root de MySQL.
4. Arrancar: Ejecutar en terminal `mvn clean install` seguido de `mvn spring-boot:run`. El puerto por defecto es `8080`.

### 8.2 Manual de Usuario / Endpoints API
Resumen de los endpoints principales para Food Trucks (ver documentación completa del autor para el resto):
*   `GET /api/foodtrucks`: Listar todos los food trucks.
*   `POST /api/foodtrucks`: Crear uno nuevo (requiere JSON con nombre, tipoCocina, ubicacionActual).
*   `PUT /api/foodtrucks/{id}`: Actualizar.
*   `DELETE /api/foodtrucks/{id}`: Eliminar.
*   `GET /api/foodtrucks/cerca`: Buscar por ubicación.

Ejemplo de uso de Curl:
```bash
curl -X POST http://localhost:8080/api/foodtrucks \
-H "Content-Type: application/json" \
-d '{"nombre":"Pizza Palazzo","tipoCocina":"Italiana","ubicacionActual":"Nueva York, 10th St"}'
```

---

## Capítulo 9. Conclusiones y ampliaciones

### 9.1 Conclusiones
FoodBites API proporciona una base estable y escalable, gracias al ecosistema Spring, para soportar un negocio moderno de food trucks. Facilita la independencia entre el almacenamiento de datos y cualquier interfaz de usuario futura.

### 9.2 Ampliaciones
*   Implementar Spring Security con JWT para un consumo seguro y control de acceso por roles.
*   Agregar subida de imágenes (S3 o almacenamiento local) para fotos de los Food Trucks o Menús.
*   Integrar un sistema real de geolocalización de mapas (como Google Maps API).

---

## Capítulo 10. Apéndices

### 10.1 Glosario
*   **REST**: Transferencia de Estado Representacional.
*   **Endpoint**: URL expuesta por la API para que un cliente pueda interactuar con un recurso.
*   **JPA**: Java Persistence API, estándar de Java para mapeo objeto-relacional (ORM).
*   **CRUD**: Create, Read, Update, Delete. Las 4 operaciones básicas.
