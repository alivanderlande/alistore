# AliStore - High-Level Design Document

## Overview
AliStore is a modern book management and selling system built using Java, Spring Boot, Maven, OpenAPI, and PostgreSQL. The system follows an API-first approach, ensuring clear contract definition and separation of concerns.

## Technology Stack
- **Language**: Java 17
- **Framework**: Spring Boot 3.2.x
- **Build Tool**: Maven
- **Database**: PostgreSQL 15
- **API Documentation**: OpenAPI 3.0
- **Authentication**: JWT (JSON Web Tokens)
- **Testing**: JUnit 5, Mockito
- **Code Quality**: SonarQube
- **Version Control**: Git

## Architecture

### System Architecture
The system follows a layered architecture pattern with the following components:
```
├── API Layer (Controllers)
├── Service Layer (Business Logic)
├── Repository Layer (Data Access)
└── Database Layer
```

### Database Design

#### Core Entities

1. **Book**
   ```sql
   CREATE TABLE books (
       id UUID PRIMARY KEY,
       isbn VARCHAR(13) UNIQUE NOT NULL,
       title VARCHAR(255) NOT NULL,
       author VARCHAR(255) NOT NULL,
       publisher VARCHAR(255),
       publication_date DATE,
       price DECIMAL(10,2) NOT NULL,
       quantity_in_stock INTEGER NOT NULL,
       category_id UUID,
       created_at TIMESTAMP,
       updated_at TIMESTAMP
   );
   ```

2. **Category**
   ```sql
   CREATE TABLE categories (
       id UUID PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       description TEXT,
       parent_id UUID,
       created_at TIMESTAMP,
       updated_at TIMESTAMP
   );
   ```

3. **Customer**
   ```sql
   CREATE TABLE customers (
       id UUID PRIMARY KEY,
       email VARCHAR(255) UNIQUE NOT NULL,
       password_hash VARCHAR(255) NOT NULL,
       first_name VARCHAR(100),
       last_name VARCHAR(100),
       phone VARCHAR(20),
       created_at TIMESTAMP,
       updated_at TIMESTAMP
   );
   ```

4. **Order**
   ```sql
   CREATE TABLE orders (
       id UUID PRIMARY KEY,
       customer_id UUID NOT NULL,
       status VARCHAR(20) NOT NULL,
       total_amount DECIMAL(10,2) NOT NULL,
       created_at TIMESTAMP,
       updated_at TIMESTAMP
   );
   ```

5. **OrderItem**
   ```sql
   CREATE TABLE order_items (
       id UUID PRIMARY KEY,
       order_id UUID NOT NULL,
       book_id UUID NOT NULL,
       quantity INTEGER NOT NULL,
       unit_price DECIMAL(10,2) NOT NULL,
       created_at TIMESTAMP
   );
   ```

### API Endpoints

#### Books API
- `GET /api/v1/books` - List all books with pagination
- `GET /api/v1/books/{id}` - Get book details
- `POST /api/v1/books` - Create a new book
- `PUT /api/v1/books/{id}` - Update book details
- `DELETE /api/v1/books/{id}` - Delete a book
- `GET /api/v1/books/search` - Search books by criteria

#### Categories API
- `GET /api/v1/categories` - List all categories
- `GET /api/v1/categories/{id}` - Get category details
- `POST /api/v1/categories` - Create a new category
- `PUT /api/v1/categories/{id}` - Update category
- `DELETE /api/v1/categories/{id}` - Delete category

#### Customers API
- `POST /api/v1/customers/register` - Register new customer
- `POST /api/v1/customers/login` - Customer login
- `GET /api/v1/customers/profile` - Get customer profile
- `PUT /api/v1/customers/profile` - Update customer profile

#### Orders API
- `POST /api/v1/orders` - Create new order
- `GET /api/v1/orders` - List customer orders
- `GET /api/v1/orders/{id}` - Get order details
- `PUT /api/v1/orders/{id}/status` - Update order status

### Security

1. **Authentication**
   - JWT-based authentication
   - Token expiration and refresh mechanism
   - Password hashing using BCrypt

2. **Authorization**
   - Role-based access control (ADMIN, CUSTOMER)
   - Method-level security using Spring Security

### Project Structure
```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── alistore/
│   │           ├── AliStoreApplication.java
│   │           ├── config/
│   │           ├── controller/
│   │           ├── dto/
│   │           ├── exception/
│   │           ├── model/
│   │           ├── repository/
│   │           ├── security/
│   │           └── service/
│   └── resources/
│       ├── application.yml
│       └── db/
│           └── migration/
└── test/
    └── java/
        └── com/
            └── alistore/
                ├── controller/
                ├── service/
                └── repository/
```

## Development Workflow

1. **API-First Development**
   - Define OpenAPI specifications
   - Generate API interfaces and models
   - Implement business logic
   - Write tests
   - Deploy and document

2. **Database Migrations**
   - Use Flyway for database version control
   - Maintain migration scripts in `db/migration`

3. **Testing Strategy**
   - Unit tests for services and utilities
   - Integration tests for repositories
   - API tests for controllers
   - End-to-end tests for critical flows

4. **CI/CD Pipeline**
   - Build and test
   - Static code analysis
   - Security scanning
   - Containerization
   - Deployment

## Monitoring and Logging

1. **Metrics**
   - Application metrics using Micrometer
   - JVM metrics
   - Custom business metrics

2. **Logging**
   - Structured logging using SLF4J
   - Correlation IDs for request tracing
   - Error logging and alerting

## Future Enhancements

1. **Features**
   - Book recommendations
   - Customer reviews and ratings
   - Discount management
   - Inventory alerts

2. **Technical**
   - Caching layer (Redis)
   - Full-text search (Elasticsearch)
   - Message queue for async operations
   - API rate limiting

## Getting Started

1. **Prerequisites**
   - JDK 17
   - Maven 3.8+
   - PostgreSQL 15
   - Docker (optional)

2. **Configuration**
   - Database connection
   - JWT secret
   - Mail server
   - External services

3. **Build and Run**
   ```bash
   mvn clean install
   java -jar target/alistore.jar
   ```

4. **API Documentation**
   - Swagger UI: `http://localhost:8080/swagger-ui.html`
   - OpenAPI spec: `http://localhost:8080/v3/api-docs`