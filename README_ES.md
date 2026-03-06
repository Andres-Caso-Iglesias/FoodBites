# TruckBites API

[![Español](https://img.icons8.com/color/48/spain.png)](README_ES.md)   [![English](https://img.icons8.com/color/48/great-britain.png )](README_EN.md)

La API de TruckBites es un servicio web RESTful construido con Spring Boot y Java, diseñado para gestionar food trucks, menús, pedidos, usuarios, ubicaciones y notificaciones para la plataforma TruckBites. Utiliza una base de datos MySQL con el esquema proyectoad y proporciona endpoints para operaciones CRUD, búsquedas basadas en ubicación y análisis de pedidos. La API soporta cargas útiles JSON y está probada con comandos curl tanto para su funcionalidad como para el manejo de errores.

Este proyecto sirve como backend para una aplicación de gestión de food trucks, accesible localmente en http://localhost:8080/api. 

Este proyecto fue creado por Andrés Caso Iglesias para la asignatura "Acceso a Datos" del grado "Técnico Superior en Desarrollo de Aplicaciones Multiplataforma" (DAM).

## Tabla de Contenidos

- Características
- Requisitos Previos
- Instrucciones de Configuración
- Endpoints de la API
- Prueba de la API
- Documentación de la API
- Estructura del Proyecto
- Extensión del Proyecto
- Contribución

## Características

- Food Trucks: Crear, leer, actualizar y eliminar food trucks; buscar por ubicación o tipo de cocina; obtener los mejores food trucks por cantidad de pedidos.
- Menús: Gestionar elementos del menú, incluida la creación masiva y el filtrado por food truck.
- Pedidos: Gestionar la creación, actualización y eliminación de pedidos; obtener pedidos pendientes o ventas totales.
- Usuarios: Gestionar cuentas de usuario con búsquedas por correo electrónico.
- Ubicaciones: Rastrear las ubicaciones de los food trucks por ciudad y calle.
- Notificaciones: Enviar y gestionar notificaciones de usuario.
- Manejo de Errores: Devuelve códigos de estado HTTP estándar (200, 400, 404, 500) con mensajes de error en formato JSON.

## Requisitos Previos

- Java: 17 o superior
- Maven: 3.6.x o superior
- MySQL: 8.x
- curl: Para probar los endpoints de la API (o usar Postman)
- Git: Para clonar el repositorio

## Instrucciones de Configuración

### 1. Clonar el Repositorio
Clonar el proyecto desde GitHub:

```bash
git clone https://github.com/your-username/foodbites-api.git
cd foodbites-api
```

### 2. Configurar la Base de Datos
1. Instalar e iniciar MySQL.
2. Crear una base de datos llamada proyectoad:
   ```sql
   CREATE DATABASE proyectoad;
   ```
3. Crear las tablas requeridas (FoodTrucks, Menus, Pedidos, Usuarios, Ubicaciones, Notificaciones).

### 3. Configurar las Propiedades de la Aplicación
Editar src/main/resources/application.properties para establecer las credenciales de MySQL:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/proyectoad?useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
server.port=8080
```

### 4. Construir y Ejecutar la Aplicación
Construir e iniciar la aplicación Spring Boot:

```bash
mvn clean install
mvn spring-boot:run
```

La API estará disponible en http://localhost:8080/api.

## Endpoints de la API

A continuación, se presenta un resumen de los endpoints clave para el recurso FoodTrucks.

| Método | Endpoint | Descripción |
|--------|--------------------------------|--------------------------------------|
| GET | /api/foodtrucks | Recuperar todos los food trucks |
| GET | /api/foodtrucks/{id} | Recuperar un food truck por ID |
| POST | /api/foodtrucks | Crear un nuevo food truck |
| PUT | /api/foodtrucks/{id} | Actualizar un food truck |
| DELETE | /api/foodtrucks/{id} | Eliminar un food truck |
| GET | /api/foodtrucks/cerca | Encontrar food trucks por ciudad y calle |
| GET | /api/foodtrucks/recomendar | Recomendar food trucks por ciudad y cocina|

### Solicitud de Ejemplo
Crear un nuevo food truck:

```bash
curl -X POST http://localhost:8080/api/foodtrucks \
-H "Content-Type: application/json" \
-d '{"nombre":"Pizza Palazzo","tipoCocina":"Italiana","ubicacionActual":"Nueva York, 10th St"}'
```

## Prueba de la API

Puedes probar la API usando comandos curl. Por ejemplo, para probar una entrada inválida:

```bash
curl -X POST http://localhost:8080/api/foodtrucks \
-H "Content-Type: application/json" \
-d '{"tipoCocina":"Italiana"}'
```

Respuesta Esperada (400 Bad Request):
```json
{
  "message": "Faltan campos requeridos: nombre, ubicacionActual"
}
```

## Documentación de la API

Notas clave para la implementación:
- URL Base: http://localhost:8080/api
- Tipo de Contenido: JSON (Content-Type: application/json) para solicitudes POST/PUT
- Formato de Fecha: ISO 8601 (p. ej., 2025-05-14T22:00:00)

## Estructura del Proyecto

```text
FoodBites API
├── src/main/java/com/foodbites/truck_bites/
│   ├── controller/      # Endpoints de la API
│   ├── dto/             # Objetos de Datos (DTO)
│   ├── model/           # Entidades JPA
│   ├── repository/      # Acceso a Datos
│   ├── service/         # Lógica de Negocio
│   └── TruckBitesApplication.java
├── src/main/resources/
│   ├── application.properties
│   └── data.sql
├── src/test/java/       # Pruebas de Servicios
└── pom.xml              # Configuración de Maven
```

## Extensión del Proyecto

Para agregar soporte a otros recursos:
1. Crear clases de entidades en el paquete model.
2. Definir repositorios JPA en el paquete repository.
3. Implementar clases de servicio en el paquete service.
4. Agregar controladores en el paquete controller.

Ejemplo: Para Menús, crear Menu.java, MenuRepository.java, MenuService.java y MenuController.java, siguiendo el patrón establecido.

## Contribución

¡Le damos la bienvenida a las contribuciones! Para contribuir:
1. Haz un fork del repositorio.
2. Crea una rama de características (git checkout -b feature/tu-caracteristica).
3. Confirma los cambios (git commit -m 'Agregar tu característica').
4. Sube la rama (git push origin feature/tu-caracteristica).
5. Abre un pull request.

---
