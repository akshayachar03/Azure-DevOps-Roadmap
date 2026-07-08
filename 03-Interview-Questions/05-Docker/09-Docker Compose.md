# Docker Compose Interview Questions

## Most Frequently Asked Interview Questions

### Question 1

**Question**

What is Docker Compose, and why is it used?

**Answer**

Docker Compose is a tool used to define and manage multi-container Docker applications using a single YAML configuration file (`docker-compose.yml`).

Instead of running multiple `docker run` commands, Docker Compose allows you to start, stop, and manage all related containers with a single command.

**Explanation**

Docker Compose simplifies application deployment by defining services, networks, volumes, and environment variables in one file.

**Used in Production**

Docker Compose is commonly used for:

- Local development
- Testing environments
- Multi-container applications
- CI/CD testing
- Small to medium production deployments

**Common Mistake**

Many candidates think Docker Compose replaces Kubernetes. Docker Compose is primarily designed for managing multi-container Docker applications on a single host, whereas Kubernetes is designed for orchestrating containers across multiple hosts.

---

### Question 2

**Question**

What is the purpose of the `docker-compose.yml` file?

**Answer**

The `docker-compose.yml` file defines the entire application stack, including:

- Services
- Networks
- Volumes
- Environment variables
- Port mappings
- Build instructions
- Restart policies

Example:

```yaml
services:
  web:
    image: nginx
```

**Explanation**

Docker Compose reads this file and automatically creates the required infrastructure.

**Used in Production**

Infrastructure and application configuration are version-controlled alongside application code.

---

### Question 3

**Question**

What are Services in Docker Compose?

**Answer**

A Service represents a container within the application.

Example:

```yaml
services:
  web:
    image: nginx

  database:
    image: mysql
```

**Explanation**

Each service becomes one or more Docker containers.

**Used in Production**

Typical services include:

- Web server
- API
- Database
- Redis
- Message queue

**Common Mistake**

Confusing a service with a container. A service defines how containers are created.

---

### Question 4

**Question**

How are Networks defined in Docker Compose?

**Answer**

Networks allow services to communicate securely.

Example:

```yaml
networks:
  app-network:
```

Assign network:

```yaml
services:
  web:
    networks:
      - app-network
```

**Explanation**

Compose automatically creates the network and connects participating services.

**Used in Production**

Networks isolate applications and provide service discovery using container names.

---

### Question 5

**Question**

How are Volumes used in Docker Compose?

**Answer**

Volumes provide persistent storage.

Example:

```yaml
services:
  mysql:
    image: mysql
    volumes:
      - mysql-data:/var/lib/mysql

volumes:
  mysql-data:
```

**Explanation**

Docker manages the volume independently of the container lifecycle.

**Used in Production**

Used for:

- Databases
- Logs
- Uploaded files
- Shared application data

---

### Question 6

**Question**

How are Environment Variables configured in Docker Compose?

**Answer**

Inline example:

```yaml
environment:
  DB_HOST: mysql
  APP_ENV: production
```

Using an `.env` file:

```yaml
env_file:
  - .env
```

**Explanation**

Environment variables allow runtime configuration without modifying application code.

**Used in Production**

Commonly used for:

- Database connections
- API endpoints
- Feature flags
- Application settings

**Common Mistake**

Storing passwords directly in the Compose file instead of using secret management.

---

### Question 7

**Question**

What is the difference between `build` and `image` in Docker Compose?

**Answer**

`build`

Builds an image using a Dockerfile.

Example:

```yaml
build: .
```

`image`

Uses an existing image.

Example:

```yaml
image: nginx:latest
```

**Explanation**

- `build` creates a new image.
- `image` downloads or uses an existing image.

**Used in Production**

Development environments often use `build`, while production typically uses versioned images from a registry.

**Common Mistake**

Specifying both `build` and `image` without understanding how Compose handles image creation and tagging.

---

### Question 8

**Question**

How do Docker Compose services communicate with each other?

**Answer**

Services communicate using their service names.

Example:

```yaml
services:
  api:
  database:
```

The API connects using:

```
database
```

instead of an IP address.

**Explanation**

Docker Compose automatically creates an internal DNS server.

**Used in Production**

Microservices commonly use service names for communication.

---

### Question 9

**Question**

What are the most commonly used Docker Compose commands?

**Answer**

Start services:

```bash
docker compose up
```

Start in background:

```bash
docker compose up -d
```

Stop services:

```bash
docker compose down
```

View running services:

```bash
docker compose ps
```

View logs:

```bash
docker compose logs
```

Rebuild:

```bash
docker compose build
```

Restart:

```bash
docker compose restart
```

**Explanation**

These commands manage the complete application stack.

**Used in Production**

Frequently used in development, testing, and deployment automation.

---

### Question 10

**Question**

What is the difference between `docker run` and Docker Compose?

**Answer**

| docker run | Docker Compose |
|------------|----------------|
| Starts one container | Manages multiple containers |
| Command-line configuration | YAML configuration |
| Manual networking | Automatic networking |
| Manual volume creation | Automatic volume creation |
| Manual dependency management | Entire application defined in one file |

**Explanation**

Docker Compose is preferred for multi-container applications.

**Common Mistake**

Using multiple `docker run` commands for applications consisting of several services.

---

### Question 11

**Question**

What are the benefits of using Docker Compose?

**Answer**

Benefits include:

- Infrastructure as Code
- Easy multi-container deployment
- Automatic networking
- Automatic DNS
- Simplified configuration
- Faster onboarding
- Reproducible environments
- Easier CI/CD integration

**Explanation**

Compose makes application deployment consistent across development, testing, and staging environments.

**Used in Production**

Widely used for local development and pre-production environments.

---

## Scenario-Based Interview Questions

### Scenario 1

**Question**

A developer starts an application using five separate `docker run` commands. What would you recommend?

**Answer**

Replace the individual commands with a single `docker-compose.yml` file and manage the application using Docker Compose.

**Explanation**

Docker Compose centralizes configuration and simplifies deployment.

---

### Scenario 2

**Question**

Your application consists of a web server, API, Redis, and MySQL database. How would you deploy them together?

**Answer**

Define each component as a separate service in `docker-compose.yml`.

Example:

```yaml
services:
  web:
  api:
  redis:
  mysql:
```

**Explanation**

Docker Compose automatically creates the required containers and networking.

---

### Scenario 3

**Question**

Your API cannot connect to the MySQL container because the developer uses the database container's IP address. What would you recommend?

**Answer**

Use the service name instead.

Example:

```
DB_HOST=mysql
```

**Explanation**

Compose provides automatic DNS resolution for service names.

---

### Scenario 4

**Question**

A MySQL container loses all data every time the application stack is recreated. How would you solve this?

**Answer**

Attach a named volume to the database service.

Example:

```yaml
volumes:
  - mysql-data:/var/lib/mysql
```

**Explanation**

Named volumes preserve data across container recreation.

---

### Scenario 5

**Question**

Your development team wants source code changes to be reflected immediately without rebuilding the container. How would you configure Docker Compose?

**Answer**

Use a bind mount.

Example:

```yaml
volumes:
  - ./:/app
```

**Explanation**

The container directly uses files from the host system.

---

### Scenario 6

**Question**

Your application behaves differently in development and production because of different configuration values. How should you manage them?

**Answer**

Use environment variables or separate `.env` files.

Example:

```
.env.dev
.env.prod
```

**Explanation**

This avoids modifying the application image for different environments.

---

### Scenario 7

**Question**

Your CI/CD pipeline must rebuild application images before deployment. Which Compose directive should be used?

**Answer**

Use:

```yaml
build:
  context: .
```

**Explanation**

Docker Compose builds the image from the Dockerfile before starting the services.

---

### Scenario 8

**Question**

Your production deployment should use a prebuilt image stored in Docker Hub instead of rebuilding the application. Which Compose directive should you use?

**Answer**

Use:

```yaml
image: company/app:v2.0
```

**Explanation**

Production environments typically deploy immutable, versioned images built by the CI pipeline.

---

### Scenario 9

**Question**

Your manager asks you to stop the entire application stack, including all services and networks, with a single command. Which command would you use?

**Answer**

```bash
docker compose down
```

**Explanation**

This command stops and removes all containers, networks, and default resources created by Docker Compose. Volumes are preserved unless explicitly removed.

---

### Scenario 10

**Question**

You are deploying an e-commerce application consisting of an Nginx reverse proxy, a Node.js API, a Redis cache, and a MySQL database. The services must communicate internally, database data must persist, configuration should differ between development and production, and developers should be able to start the entire stack with one command. How would you design the solution?

**Answer**

- Define each component as a separate service in `docker-compose.yml`.
- Use a custom network for internal communication.
- Store MySQL data in a named volume.
- Configure environment-specific values using `.env` files.
- Use `build` during development and versioned `image` references in production.
- Start the complete application using:

```bash
docker compose up -d
```

**Explanation**

This design follows Docker Compose best practices by providing infrastructure as code, automatic networking, persistent storage, centralized configuration, and simplified deployment—an approach commonly used in development, testing, and CI/CD environments.
