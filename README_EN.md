# Project Documentation: FoodBites API

[![English](https://img.icons8.com/color/48/great-britain.png )](README_EN.md)  [![Español](https://img.icons8.com/color/48/spain.png)](README.md)

---

## Summary
The current project, titled "FoodBites API", consists of the development of a RESTful web service for the comprehensive management of a food truck platform. The main objective is to facilitate the administration of food trucks, their menus, customer orders, and the tracking of locations and user interactions, all centralized in a robust backend system.

The system has been built using a Java-based architecture. On the server side (Backend), **Spring Boot** has been chosen, a framework that guarantees scalability, maintainability, and fast development, along with **MySQL** as a relational database management system to ensure data integrity and persistence under the `proyectoad` schema.

The application exposes a series of endpoints to manage essential entities such as: Food Trucks, Menus, Orders, Users, Locations, and Notifications. CRUD operations, along with geo-located searches and basic order analytics, are fully implemented.

This project, created by Andrés Caso Iglesias for the "Data Access" subject of the "Higher Technician in Multi-platform Applications Development" degree (DAM), demonstrates the practical application of enterprise backend technologies and efficient API design.

---

## Keywords
Food Trucks, Backend Development, Spring Boot, Java 17, MySQL, REST API, Order Management, DAM.

---

## General Index

### CHAPTER 1. PROJECT MEMORY
1.1 SUMMARY OF MOTIVATION
1.2 OBJECTIVES

### CHAPTER 2. INTRODUCTION
2.1 PROJECT JUSTIFICATION
2.2 STUDY OF CURRENT SITUATION

### CHAPTER 3. THEORETICAL ASPECTS
3.1 JAVA AND SPRING BOOT
3.2 REST ARCHITECTURE
3.3 MYSQL AND SPRING DATA JPA
3.4 MAVEN

### CHAPTER 4. ANALYSIS
4.1 SYSTEM DEFINITION
4.2 REQUIREMENTS CATALOG
4.3 IDENTIFICATION OF SYSTEM ACTORS
4.4 SPECIFICATION OF USE CASES

### CHAPTER 5. TEST PLAN
5.1 INTRODUCTION
5.2 TEST PLAN DESIGN AND PLANNING
5.3 ANALYSIS AND INTERPRETATION OF RESULTS

### CHAPTER 6. SYSTEM DESIGN
6.1 SYSTEM ARCHITECTURE
6.2 CLASS DESIGN (MVC)
6.3 DATABASE DESIGN

### CHAPTER 7. SYSTEM IMPLEMENTATION
7.1 LANGUAGES AND TOOLS
7.2 PROJECT STRUCTURE

### CHAPTER 8. SYSTEM MANUALS
8.1 INSTALLATION MANUAL
8.2 USER MANUAL / API ENDPOINTS

### CHAPTER 9. CONCLUSIONS AND EXTENSIONS
9.1 CONCLUSIONS
9.2 EXTENSIONS

### CHAPTER 10. APPENDICES
10.1 GLOSSARY

---

## Chapter 1. Project Memory

### 1.1 Summary of motivation
Street food and food trucks represent a growing sector. However, their mobile nature complicates customer loyalty and the centralized management of menus and orders. The motivation for this project is to provide a solid backend infrastructure (API) that allows future mobile or web applications to solve this problem, connecting food truck owners with hungry customers in real-time.

### 1.2 Objectives
1. Develop a functional RESTful API for Food Truck management.
2. Allow the registration and management of menus, as well as updating the current location of the trucks.
3. Process and manage orders placed by users.
4. Ensure data persistence through a robust MySQL relational database (`proyectoad`).
5. Provide search endpoints by proximity (city/street) and recommendations by cuisine type.

---

## Chapter 2. Introduction

### 2.1 Project justification
The mobile catering sector needs agile digital tools. Static social media profiles are not enough to manage orders in real-time or report sudden location changes. FoodBites API is justified as the central piece that synchronizes mobile gastronomic offerings with consumer demand, eliminating frictions in the purchasing process.

### 2.2 Study of current situation
There are generic food delivery platforms (Glovo, Uber Eats), but they are not optimized for the location instability of food trucks. FoodBites seeks to create a dedicated ecosystem where "current location" is a dynamic first-class attribute, and where the catalog adapts to the particularities of these businesses.

---

## Chapter 3. Theoretical aspects

### 3.1 Java and Spring Boot
**Java 17** is the primary language. **Spring Boot (3.3.5)** is the chosen framework due to its "convention over configuration" paradigm, facilitating the quick start of Spring-based applications, with embedded web servers (Tomcat) and auto-configuration of components.

### 3.2 REST Architecture
The system is designed under the Representational State Transfer (REST) architectural style, exposing resources through predictable URIs and using standard HTTP methods (GET, POST, PUT, DELETE) for CRUD operation semantics.

### 3.3 MySQL and Spring Data JPA
**MySQL (8.x)** is used as the RDBMS. The persistence layer is managed using **Spring Data JPA** and **Hibernate**, allowing Java classes (Entities) to be mapped directly to database tables, reducing repetitive data access code.

### 3.4 Maven
**Apache Maven (3.6.x+)** is used for dependency management and the project build lifecycle (compilation, testing, and packaging).

---

## Chapter 4. Analysis

### 4.1 System definition
The system encompasses the backend operations necessary to bring the FoodBites platform to life. It receives HTTP requests with JSON payloads, processes business logic, interacts with the database, and returns JSON responses.

### 4.2 Requirements catalog
*   **Food Truck Management**: Allow registration, update, deletion, and listing (CRUD). Searches by location and recommendations.
*   **Menu Management**: CRUD of dishes associated with a Food Truck.
*   **Order Management**: Registration of sales and sum of totals.
*   **Other entities**: Users, Locations, and Notifications complete the ecosystem.

### 4.3 Identification of system actors (At API Level)
*   **Client Application**: The frontend (web or mobile) that consumes the API on behalf of End Users or Food Truck Owners.
*   **Developer / Tester**: Uses curl or Postman to interact directly with the endpoints.

### 4.4 Specification of main use cases
*   **Register a Food Truck**: The client sends a POST with name, cuisine type, and preliminary location.
*   **List Nearby Food Trucks**: The client makes a GET with city and street parameters.
*   **Update Location**: A PUT is sent to the Food Truck ID with the new information.

---

## Chapter 5. Test Plan

### 5.1 Introduction
The overall functionality of the endpoints will be evaluated using automation tools and network calls.

### 5.2 Test Plan Design and Planning
*   **Unit Tests for Services**: The project includes a `src/test/java` directory with tests for the service layer (e.g., `FoodTruckServiceTest.java`, `MenuServiceTest.java`).
*   **Functional API Tests**: A battery of scripts based on `curl` commands is used (documented in `docs/Andres_CasoIglesias_testAPI.docx`).

### 5.3 Analysis of Results
The successful execution of curl commands returning the correct HTTP status codes (200 OK, 201 Created) and the prevention of erroneous inputs (400 Bad Request) ensure robustness against the client. The unit tests cover the lifecycle of the entities.

---

## Chapter 6. System Design

### 6.1 System Architecture
The API follows a classic three-tier architecture model:
1.  **Controller**: Handles HTTP calls, extracts surface parameters, and returns responses.
2.  **Service**: Contains all business logic and validations.
3.  **Repository**: JPA interfaces that Spring automatically instantiates to access MySQL.

### 6.2 Class Design (MVC)
The design is faithfully reflected in the project packages (`com.foodbites.truck_bites.*`):
*   `model`: Classes annotated with `@Entity` representing tables.
*   `dto`: Data Transfer Objects used in requests/responses.
*   `repository`: Interfaces extending `JpaRepository`.
*   `controller`: Classes annotated with `@RestController`.

### 6.3 Database Design
A relational design is assumed where `FoodTrucks` is a central entity. `Menus` has a foreign key pointing to the food truck. `Pedidos` relates `Usuarios` with `FoodTrucks` and their dishes.

---

## Chapter 7. System Implementation

### 7.1 Languages and Tools
*   Java SDK 17+
*   Spring Boot 3.3.5
*   IDE: IntelliJ IDEA / VS Code
*   Terminal and Apache Maven for execution lifecycles.

### 7.2 Project Structure
```text
FoodBites API
├── src/main/java/com/foodbites/truck_bites/
│   ├── controller/      # API Endpoints
│   ├── dto/             # Data Transfer Objects (DTO)
│   ├── model/           # JPA Entities
│   ├── repository/      # Data Access (JPA Interfaces)
│   ├── service/         # Business Logic
│   └── TruckBitesApplication.java
├── src/main/resources/
│   ├── application.properties
│   └── data.sql         # For initial load if necessary
├── src/test/java/       # Service Tests (JUnit)
└── pom.xml              # Maven Dependencies
```

---

## Chapter 8. System Manuals

### 8.1 Installation manual
1. Clone: `git clone https://github.com/your-username/foodbites-api.git`
2. Database: Execute `CREATE DATABASE proyectoad;` in your MySQL instance.
3. Configure: Edit `src/main/resources/application.properties` with your MySQL root username and password.
4. Run: Execute in terminal `mvn clean install` followed by `mvn spring-boot:run`. The default port is `8080`.

### 8.2 User Manual / API Endpoints
Summary of main endpoints for Food Trucks (see full author documentation for the rest):
*   `GET /api/foodtrucks`: List all food trucks.
*   `POST /api/foodtrucks`: Create a new one (requires JSON with nombre, tipoCocina, ubicacionActual).
*   `PUT /api/foodtrucks/{id}`: Update.
*   `DELETE /api/foodtrucks/{id}`: Delete.
*   `GET /api/foodtrucks/cerca`: Search by location.

Example Curl usage:
```bash
curl -X POST http://localhost:8080/api/foodtrucks \
-H "Content-Type: application/json" \
-d '{"nombre":"Pizza Palazzo","tipoCocina":"Italiana","ubicacionActual":"Nueva York, 10th St"}'
```

---

## Chapter 9. Conclusions and extensions

### 9.1 Conclusions
FoodBites API provides a stable and scalable base, thanks to the Spring ecosystem, to support a modern food truck business. It facilitates independence between data storage and any future user interface.

### 9.2 Extensions
*   Implement Spring Security with JWT for secure consumption and role-based access control.
*   Add image uploads (S3 or local storage) for Food Truck or Menu photos.
*   Integrate a real map geolocation system (such as Google Maps API).

---

## Chapter 10. Appendices

### 10.1 Glossary
*   **REST**: Representational State Transfer.
*   **Endpoint**: URL exposed by the API so a client can interact with a resource.
*   **JPA**: Java Persistence API, Java standard for object-relational mapping (ORM).
*   **CRUD**: Create, Read, Update, Delete. The 4 basic operations.
