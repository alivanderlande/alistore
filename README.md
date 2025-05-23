# AliStore

AliStore is a modern book management and selling system built with Spring Boot, PostgreSQL, and OpenAPI. The system follows an API-first approach and provides a robust backend for managing books, customers, orders, and more.

## Features

- Book management (CRUD operations)
- Category management
- Customer registration and authentication
- Order processing
- Inventory management
- RESTful API with OpenAPI documentation
- Role-based access control
- JWT-based authentication

## Prerequisites

- JDK 17 or later
- Maven 3.8+
- PostgreSQL 15
- Docker (optional)

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/alivanderlande/alistore.git
   cd alistore
   ```

2. **Configure PostgreSQL**
   - Create a new database:
     ```sql
     CREATE DATABASE alistore;
     ```
   - Update database configuration in `src/main/resources/application.yml`

3. **Build the project**
   ```bash
   mvn clean install
   ```

4. **Run the application**
   ```bash
   mvn spring-boot:run
   ```

   The application will start on `http://localhost:8080`

## API Documentation

Once the application is running, you can access:
- Swagger UI: `http://localhost:8080/swagger-ui.html`
- OpenAPI specification: `http://localhost:8080/v3/api-docs`

## Project Structure

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
```

## Development

1. **Database Migrations**
   - Migrations are managed with Flyway
   - Add new migrations in `src/main/resources/db/migration`
   - Follow naming convention: `V{version}__{description}.sql`

2. **API Development**
   - Follow API-first approach
   - Update OpenAPI specifications first
   - Implement controllers and services
   - Add unit and integration tests

3. **Testing**
   ```bash
   # Run unit tests
   mvn test

   # Run integration tests
   mvn verify
   ```

## Security

- JWT-based authentication
- Role-based access control (ADMIN, CUSTOMER)
- Password encryption using BCrypt
- Protected endpoints require authentication

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Documentation

For more detailed information about the system design and architecture, please refer to the [design documentation](docs/design.md).