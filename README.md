# Project-Platform

Platform infrastructure services for the ECA microservices ecosystem. This repository serves as the parent module containing the core platform services that enable service discovery, configuration management, and API routing for the entire system.

## About

Project-Platform is a multi-module repository that aggregates the foundational Spring Cloud infrastructure services required to run the ECA (Enterprise Cloud Application) microservices architecture. It uses Git submodules to manage the individual service repositories, allowing each service to be versioned independently while maintaining a unified project structure.

This platform layer includes:
- **Config-Server**: Centralized configuration management
- **Service-Registry**: Netflix Eureka-based service discovery
- **API-Gateway**: Spring Cloud Gateway for request routing and load balancing

## Student Information

| Detail | Value |
|---|---|
| **Name** | Shashi Madushan |
| **Student Number** | 2301691002 |
| **Course** | Enterprise Computing Architecture |
| **Institution** | Institute of Software Engineering (IJSE) |

## Repository Structure

```
Project-Platform/
├── .gitmodules              # Submodule configuration
├── pom.xml                  # Parent Maven POM
├── ecosystem.config.js      # PM2 process orchestration config
├── config-server/           # Git submodule - Config-Server
├── service-registry/        # Git submodule - Service-Registry
└── api-gateway/             # Git submodule - API-Gateway
```

## Git Submodules

This repository uses Git submodules to include the platform service repositories:

| Submodule | Path | Repository URL |
|-----------|------|----------------|
| config-server | `config-server/` | https://github.com/Shashi-Madushan/config-server.git |
| service-registry | `service-registry/` | https://github.com/Shashi-Madushan/service-registry.git |
| api-gateway | `api-gateway/` | https://github.com/Shashi-Madushan/api-gateway.git |

### Cloning This Repository

**Clone with all submodules:**
```bash
git clone --recurse-submodules https://github.com/Shashi-Madushan/Project-Platform.git
```

**Clone without submodules (then initialize separately):**
```bash
git clone https://github.com/Shashi-Madushan/Project-Platform.git
cd Project-Platform
git submodule update --init --recursive
```

### Submodule Commands

**Initialize submodules after cloning:**
```bash
git submodule update --init --recursive
```

**Update all submodules to latest commits:**
```bash
git submodule update --remote
```

**Pull changes for all submodules:**
```bash
git pull --recurse-submodules
```

**Add new submodule:**
```bash
git submodule add <repository-url> <path>
```

## Tech Stack

| Technology | Details |
|---|---|
| Java | 25 |
| Spring Boot | 4.0.3 |
| Spring Cloud | 2025.1.0 |
| Netflix Eureka | Service discovery |
| Spring Cloud Config | Centralized configuration |
| Spring Cloud Gateway | API Gateway (WebFlux) |
| PM2 | Process orchestration |

## Getting Started

### Prerequisites

- Java 25 or higher
- Maven 3.8+
- PM2 (optional, for process management)

### Startup Order

Platform services must be started in this order:

1. **Config-Server** (`9000`) - Must start first
2. **Service-Registry** (`9001`) - Depends on Config-Server
3. **API-Gateway** (`7000`) - Depends on Config-Server and Service-Registry

### Running with Maven

```bash
# Start Config-Server
cd config-server
./mvnw spring-boot:run

# Start Service-Registry (in new terminal)
cd service-registry
./mvnw spring-boot:run

# Start API-Gateway (in new terminal)
cd api-gateway
./mvnw spring-boot:run
```

### Running with PM2

```bash
# Start all platform services
pm2 start ecosystem.config.js

# View logs
pm2 logs

# Stop all
pm2 stop all
```

## Service URLs

| Service | URL | Description |
|---|---|---|
| Config-Server | http://localhost:9000 | Configuration management |
| Eureka Dashboard | http://localhost:9001 | Service registry UI |
| API Gateway | http://localhost:7000 | Entry point for all requests |

## Troubleshoot

| Issue | Solution |
|---|---|
| Submodule shows as empty | Run `git submodule update --init --recursive` |
| Config-Server won't start | Check port 9000 is available |
| Services not registering | Ensure Service-Registry is running before domain services |
| Submodule commit not appearing | Run `git submodule update --remote` in parent repo |
| Cannot pull submodule updates | Check you have access to the submodule repositories |
| Maven build fails in submodule | Ensure you run Maven commands from within the submodule directory |

## Related Projects

- [Project-Services](https://github.com/Shashi-Madushan/Project-Services) - Domain microservices (IAM, Product, Order)

## License

This project is part of an academic assignment for the Enterprise Computing Architecture course at IJSE.
