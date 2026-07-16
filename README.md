# Full-Stack Application

A fully containerised full-stack application featuring a React-Vite frontend, a Spring Boot REST API, and a MySQL 8 database. The entire environment is managed and orchestrated using Docker Compose.

---

## 📂 Project Architecture
```text
fsd-project/
├── api/                        # Spring Boot (Java 25) Backend
│   ├── .mvn/
│   ├── src/
│   ├── Dockerfile
│   ├── mvnw
│   ├── mvnw.cmd
│   └── pom.xml 
├── frontend/                  # React (Vite / TypeScript) Frontend
│   ├── public/
│   ├── src/
│   ├── Dockerfile
│   ├── package.json
│   └── vite.config.ts
├── .env                       # Environment Variables (Ignored by Git)
└── docker-compose.yml         # Docker Compose Configuration
```
## Prerequisites
Before you begin, ensure you have the following installed on your machine:

- [Docker](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/)

## Getting Started
Follow these steps to set up and run the entire application stack locally.

### 1. Configure the Environment Variables
Duplicate the template `.env.example` file and rename it to `.env` in the root directory:

```bash
cp .env.example .env
```

Open the `.env` file and populate it with your preferred database credentials. Choose any name and password you like:

```bash
# Database Initialisation Settings
MYSQL_ROOT_PASSWORD=your_secure_root_password
MYSQL_DATABASE=a_database_name
MYSQL_USER=a_database_user
MYSQL_PASSWORD=your_user_password
```

### 2. Launch the Application Stack
Build the Docker images and start the services in the foreground to monitor their initialisation logs:

```bash
docker compose up --build
```

Docker will coordinate the startup sequence:

1. `jobbase-db` spins up and initializes the database schema with your custom credentials.
1. `jobbase-api` waits for the database to become healthy, establishes a connection pool, runs Hibernate migrations, and starts on port `8080`.
1. `jobbase-frontend` starts and serves your UI on port `8181`.

## Accessing the Services
Once the terminal shows that the applications are running, you can access them at:

| Service | URL | Description |
| -------- | ------- | ------- |
| Frontend UI | http://localhost:8181 | Main user interface (React/Vite) |
| Backend API | http://localhost:8080 | REST API endpoints (Spring Boot) |
| Database Port | http://localhost:3306 |Accessible via database clients |

## Stopping and Resetting

### Standard Shutdown
To stop the application while keeping your database records intact, press Ctrl + C in the running terminal, or run:

```bash
docker compose down
```

## Complete Reset (Clearing the Database)

If you modify your .env credentials, database schemas, or want to start with a completely blank database, you must delete the persistent volume. Run the following command to stop the containers and wipe the stored data volumes:

```bash
docker compose down -v
```

__⚠️ Note:__ The `-v` flag deletes the underlying Docker volume (`fsd-project_mysql_data`). The next time you run `docker compose up`, MySQL will freshly recreate the database using your current `.env` configurations.
