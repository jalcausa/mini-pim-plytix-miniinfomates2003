# Mini PIM - Asset Management API

This repository contains my **first Spring Boot API**, developed for a **university Web Development subject**.

The project implements a small Product Information Management (PIM) style backend to manage:
- **Assets** (`Activo`)
- **Asset Categories** (`Categoria`)
- **Accounts and users** (`Cuenta`, `Usuario`)
- **JWT-based authentication and authorization**

---

## Academic context and learning goals

This project was built as part of a university learning process, so the objective was not only to deliver endpoints but to understand how a real backend is structured in layers.

Main learning goals covered in this API:

- Design and implementation of a **REST API** with Spring Boot
- Separation of concerns using **controller/service/repository** layers
- Persistence with **JPA/Hibernate** and relational modeling in MySQL
- Basic **authentication and authorization** with JWT and Spring Security
- Error handling through custom exceptions and HTTP status mapping
- Team workflow with feature branches, pull requests, and iterative improvement

---

## What this project teaches (pedagogical overview)

From an academic perspective, this repository is a compact example of how backend concepts connect in practice:

1. **HTTP layer (Controllers)**  
   Controllers expose resources (`/activo`, `/categoria-activo`) and translate requests/responses into DTOs.

2. **Business layer (Services)**  
   Services centralize domain logic (validation, ownership/access checks, orchestration between entities).

3. **Persistence layer (Repositories + Entities)**  
   Repositories abstract DB access, while entities map domain objects to relational tables.

4. **Security layer (JWT + Filters)**  
   Security components validate tokens, protect routes, and define unauthorized/forbidden behavior.

5. **Cross-cutting concerns (Exceptions + DTO mapping)**  
   Custom exceptions and mappers help keep the API contract clean and understandable.

---

## Project structure

```text
mini-pim-plytix-miniinfomates2003/
├── asset-management/                          # Main Spring Boot microservice
│   ├── docker-compose.yml                     # MySQL local service
│   ├── mvnw / mvnw.cmd                        # Maven wrapper
│   ├── pom.xml                                # Dependencies and build config
│   └── src/
│       ├── main/java/com/miniinfomates2003/asset_management/
│       │   ├── AssetManagementApplication.java
│       │   ├── controllers/                   # REST controllers
│       │   │   ├── ActivoController.java
│       │   │   ├── CategoriaController.java
│       │   │   └── Mapper.java
│       │   ├── services/                      # Business logic
│       │   ├── repositories/                  # JPA repositories
│       │   ├── entities/                      # Domain entities
│       │   ├── dtos/                          # DTOs for API requests/responses
│       │   ├── security/                      # JWT + Spring Security config
│       │   └── exceptions/                    # Custom exceptions
│       └── main/resources/
│           └── application.properties         # Runtime configuration
├── Configurar_mysql_docker.txt               # Detailed MySQL + Docker guide (ES)
└── instrucciones_trabajo.txt                 # Team workflow notes (ES)
```

---

## Tech stack

- Java 17
- Spring Boot 3
- Spring Web
- Spring Data JPA
- Spring Security
- JWT
- MySQL 8
- Maven

---

## Concept-to-code map

To connect theory with implementation, these are the key concepts and where they appear:

- **REST controllers**: `controllers/ActivoController.java`, `controllers/CategoriaController.java`
- **Business logic**: `services/ActivoService.java`, `services/CategoriaService.java`, `services/CuentaService.java`
- **Data model**: `entities/Activo.java`, `entities/Categoria.java`, `entities/Cuenta.java`, `entities/Usuario.java`
- **Database access**: `repositories/*`
- **Security and JWT**: `security/SecurityConfguration.java`, `security/JwtUtil.java`, `security/JwtRequestFilter.java`
- **Error model**: `exceptions/NotFoundException.java`, `exceptions/NoAccessException.java`, `exceptions/TokenMissingException.java`
- **API contract (DTOs)**: `dtos/ActivoDTO.java`, `dtos/CategoriaDTO.java`

---

## Request lifecycle (from client to database)

Typical flow for a protected endpoint:

1. Client sends HTTP request (optionally with JWT in `Authorization` header).
2. Security filter inspects/validates token.
3. Controller receives request parameters/body and delegates to service.
4. Service applies business rules and calls repository.
5. Repository executes persistence operations through JPA/Hibernate.
6. Service returns domain result.
7. Controller maps entity to DTO and returns HTTP response.
8. If an error appears (not found, no access, missing token), exception handling maps it to the proper status code.

This flow helped consolidate course topics around API design, security, and persistence in one end-to-end path.

---

## How to run locally

### 1) Start MySQL with Docker

```bash
cd asset-management
docker-compose up -d
```

### 2) Run the API

```bash
cd asset-management
# Linux / macOS
./mvnw spring-boot:run
# Windows
mvnw.cmd spring-boot:run
```

If you get `Permission denied` on Linux/macOS, run `sh ./mvnw ...` instead.

The API runs on:
- `http://localhost:8080`

---

## Build and test

From `asset-management/`:

```bash
# Run tests
./mvnw test
# Windows
mvnw.cmd test

# Build jar
./mvnw clean package
# Windows
mvnw.cmd clean package
```

---

## Main API routes

### Assets
- `POST /activo?idCuenta={idCuenta}`
- `GET /activo?idActivo={idActivo}`
- `GET /activo?idCategoria={idCategoria}`
- `GET /activo?idProducto={idProducto}`
- `GET /activo?idCuenta={idCuenta}`
- `PUT /activo/{idActivo}`
- `DELETE /activo/{idActivo}`

### Categories
- `POST /categoria-activo?idCuenta={idCuenta}`
- `GET /categoria-activo?idCuenta={idCuenta}`
- `GET /categoria-activo?idCategoria={idCategoria}`
- `PUT /categoria-activo/{idCategoria}`
- `DELETE /categoria-activo/{idCategoria}`

> Note: Endpoints are protected with Spring Security/JWT depending on role/access rules implemented in the service/security layers.

---

## Notes

- This is an academic project and an early Spring Boot API implementation.
- Existing setup and team instructions in Spanish are preserved in:
  - `Configurar_mysql_docker.txt`
  - `instrucciones_trabajo.txt`
- Credentials and secrets in configuration files are for local academic development only.
