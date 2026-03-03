# Spring Boot Microservice

A production-ready Spring Boot 3.2 microservice with JWT authentication, PostgreSQL, Spring Security, JPA, and Lombok.

## Tech Stack

- **Java 17** + **Spring Boot 3.2**
- **Spring Security** + **JWT (JJWT)**
- **Spring Data JPA** + **PostgreSQL 16**
- **Lombok** + **Bean Validation**
- **Spring Actuator** (health checks)

## Project Structure

```
src/main/java/com/example/microservice/
├── MicroserviceApplication.java
├── config/
│   └── SecurityConfig.java
├── controller/
│   └── AuthController.java
├── dto/
│   └── AuthDto.java
├── entity/
│   ├── Role.java
│   └── User.java
├── exception/
│   ├── EmailAlreadyExistsException.java
│   └── GlobalExceptionHandler.java
├── repository/
│   └── UserRepository.java
├── security/
│   ├── JwtAuthenticationFilter.java
│   └── JwtService.java
└── service/
    └── AuthService.java
```

## Getting Started

### With Docker Compose (Recommended)

```bash
docker-compose up --build
```

### Local Development

1. Start PostgreSQL and create database:
```sql
CREATE DATABASE microservice_db;
```

2. Configure environment variables:
```bash
export DB_USERNAME=postgres
export DB_PASSWORD=postgres
export JWT_SECRET=your-256-bit-secret
```

3. Run the application:
```bash
mvn spring-boot:run
```

## API Endpoints

| Method | URL | Description | Auth |
|--------|-----|-------------|------|
| POST | `/api/v1/auth/register` | Register new user | Public |
| POST | `/api/v1/auth/login` | Login and get JWT | Public |
| GET | `/actuator/health` | Health check | Public |

### Register
```bash
curl -X POST http://localhost:8080/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"secret123","firstName":"John","lastName":"Doe"}'
```

### Login
```bash
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"secret123"}'
```

### Use Token
```bash
curl http://localhost:8080/api/v1/protected-endpoint \
  -H "Authorization: Bearer <your-jwt-token>"
```

## Adding New Features

1. Create your **Entity** in `entity/`
2. Create **Repository** in `repository/`
3. Create **DTOs** in `dto/`
4. Create **Service** in `service/`
5. Create **Controller** in `controller/`
6. Secure endpoints using `@PreAuthorize("hasRole('ROLE_ADMIN')")` or update `SecurityConfig`
