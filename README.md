# Mini PIM - Asset Management API

This repository contains my **first Spring Boot API**, developed for a **university Web Development subject**.

The project implements a small Product Information Management (PIM) style backend to manage:
- **Assets** (`Activo`)
- **Asset Categories** (`Categoria`)
- **Accounts and users** (`Cuenta`, `Usuario`)
- **JWT-based authentication and authorization**

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
