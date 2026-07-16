# Full-Stack Application


## System Setup

### Project Folder Structure
```
fsd-project/
├── api/
│   ├── .mvn/
│   ├── src/
│   ├── Dockerfile
│   ├── mvnw
│   ├── mvnw.cmd
│   └── pom.xml 
├── frontend/
│   ├── public/
│   ├── src/
│   ├── Dockerfile
│   ├── package.json
│   └── vite.config.ts
└── docker-compose.yml
```

## Configure `.env` File
Rename the `.env.example` file to `.env`. Enter MySQL passwords, a database name and a MySQL user name.

```bash
MYSQL_ROOT_PASSWORD=
MYSQL_DATABASE=
MYSQL_USER=
MYSQL_PASSWORD=
```

## Run the Solution

Run the following command to build and run the solution.

```bash
docker compose up --build
```

## Tear Down the Solution
Run the following command to tear down the containers.

```bash
docker compose down -v
```