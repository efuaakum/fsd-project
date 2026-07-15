# Full-Stack Application

## Folder structure
```
my-project/
├── api/
│   ├── src/
│   ├── pom.xml 
│   └── Dockerfile
├── frontend/
│   ├── src/
│   ├── package.json
│   ├── vite.config.ts
│   └── Dockerfile
└── docker-compose.yml
```

### API: Spring Boot (Java 25) Dockerfile
This build uses Eclipse Temurin JDK 25 to compile a Maven-based project, then copies the compiled JAR into a lightweight JRE 25 runtime image.

### Frontend: React Vite TS Dockerfile
It uses Node to compile the static assets, then serves them using a highly performant __Nginx__ server configured for single-page applications (SPA routing).

To make sure routing works properly (preventing 404s when hard-refreshing nested routes in React) added an `nginx.conf` file.

### Orchestration: docker-compose.yml
This orchestrates all three services, setting up local networking, persistent database volumes, and startup dependency orders.