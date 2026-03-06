# TruckBites API

[![English](https://img.icons8.com/color/48/great-britain.png )](README_EN.md)  [![Español](https://img.icons8.com/color/48/spain.png)](README_ES.md)

The TruckBites API is a RESTful web service built with Spring Boot and Java, designed to manage food trucks, menus, orders, users, locations, and notifications for the TruckBites platform. It uses a MySQL database with the proyectoad schema and provides endpoints for CRUD operations, location-based searches, and order analytics. The API supports JSON payloads and is tested with curl commands for both functionality and error handling.

This project serves as the backend for a food truck management application, accessible locally at http://localhost:8080/api. 

This proyect was created by Andrés Caso Iglesias for the subject "Data Access" of the degree "Higher Technician in Multi-platform Applications Development".

## Table of Contents

- Features
- Prerequisites
- Setup Instructions
- API Endpoints
- Testing the API
- API Documentation
- Project Structure
- Extending the Project
- Contributing
- License
- Contact

## Features

- Food Trucks: Create, read, update, and delete food trucks; search by location or cuisine; retrieve top trucks by order count.
- Menus: Manage menu items, including bulk creation and filtering by food truck.
- Orders: Handle order creation, updates, and deletions; retrieve pending orders or total sales.
- Users: Manage user accounts with email-based lookups.
- Locations: Track food truck locations by city and street.
- Notifications: Send and manage user notifications.
- Error Handling: Returns standard HTTP status codes (200, 400, 404, 500) with JSON error messages.

## Prerequisites

- Java: 17 or higher
- Maven: 3.6.x or higher
- MySQL: 8.x
- curl: For testing API endpoints (or use Postman)
- Git: To clone the repository

## Setup Instructions

### 1. Clone the Repository
Clone the project from GitHub:

```bash
git clone https://github.com/your-username/foodbites-api.git
cd foodbites-api
```

### 2. Configure the Database
1. Install and start MySQL.
2. Create a database named proyectoad:
   ```sql
   CREATE DATABASE proyectoad;
   ```
3. Create the required tables (FoodTrucks, Menus, Pedidos, Usuarios, Ubicaciones, Notificaciones).

### 3. Configure Application Properties
Edit src/main/resources/application.properties to set your MySQL credentials:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/proyectoad?useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
server.port=8080
```

### 4. Build and Run the Application
Build and start the Spring Boot application:

```bash
mvn clean install
mvn spring-boot:run
```

The API will be available at http://localhost:8080/api.

## API Endpoints

Below is a summary of key endpoints for the FoodTrucks resource.

| Method | Endpoint | Description |
|--------|--------------------------------|--------------------------------------|
| GET | /api/foodtrucks | Retrieve all food trucks |
| GET | /api/foodtrucks/{id} | Retrieve a food truck by ID |
| POST | /api/foodtrucks | Create a new food truck |
| PUT | /api/foodtrucks/{id} | Update a food truck |
| DELETE | /api/foodtrucks/{id} | Delete a food truck |
| GET | /api/foodtrucks/cerca | Find trucks by city and street |
| GET | /api/foodtrucks/recomendar | Recommend trucks by city and cuisine|

### Example Request
Create a new food truck:

```bash
curl -X POST http://localhost:8080/api/foodtrucks \
-H "Content-Type: application/json" \
-d '{"nombre":"Pizza Palazzo","tipoCocina":"Italiana","ubicacionActual":"Nueva York, 10th St"}'
```

## Testing the API

You can test the API using curl commands. For example, to test invalid input:

```bash
curl -X POST http://localhost:8080/api/foodtrucks \
-H "Content-Type: application/json" \
-d '{"tipoCocina":"Italiana"}'
```

Expected Response (400 Bad Request):
```json
{
  "message": "Faltan campos requeridos: nombre, ubicacionActual"
}
```

## API Documentation

Key notes for implementation:
- Base URL: http://localhost:8080/api
- Content Type: JSON (Content-Type: application/json) for POST/PUT requests
- Date Format: ISO 8601 (e.g., 2025-05-14T22:00:00)

## Project Structure

```text
FoodBites API
├── src/main/java/com/foodbites/truck_bites/
│   ├── controller/      # API Endpoints
│   ├── dto/             # Data Objects
│   ├── model/           # JPA Entities
│   ├── repository/      # Data Access
│   ├── service/         # Business Logic
│   └── TruckBitesApplication.java
├── src/main/resources/
│   ├── application.properties
│   └── data.sql
├── src/test/java/       # Service Tests
└── pom.xml              # Maven Config
```

## Extending the Project

To add support for other resources:
1. Create entity classes in the model package.
2. Define JPA repositories in the repository package.
3. Implement service classes in the service package.
4. Add controllers in the controller package.

Example: For Menus, create Menu.java, MenuRepository.java, MenuService.java, and MenuController.java, following the established pattern.

## Contributing

We welcome contributions! To contribute:
1. Fork the repository.
2. Create a feature branch (git checkout -b feature/your-feature).
3. Commit changes (git commit -m 'Add your feature').
4. Push to the branch (git push origin feature/your-feature).
5. Open a pull request.

---
