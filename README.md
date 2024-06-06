# NOVA
Spring boot microservices application. Java + Kotlin + Vue + Keycloak

The application is a CRM tool for Telecom Providers. It allows to manage customers, plans, subscriptions, services, offers, and sales.

## Design
The application consists of 5 microservices. CRM and Sales services are resources. API Gateway helps to connect resource servers under one endpoint. The authentication service contains the docker container for Keycloak. To let all of these services talk to each other, the Eureka server was used.

## Links to repos
1. [Eureka server](https://github.com/Asatillo/eureka-server)
2. [API Gateway service](https://github.com/Asatillo/api-gateway-service)
3. [Authentication service(Keycloak in Docker container)](https://github.com/Asatillo/authentication-service)
4. [CRM service](https://github.com/Asatillo/crm-service)
5. [Sales service](https://github.com/Asatillo/sales-service)
6. [Frontend service](https://github.com/Asatillo/frontend-service)

## Software requirements
- Docker: Latest version
- Git: Latest version
- Kotlin 1.8 or later
- Java 17 or later
- Gradle and Maven: Latest versions
- npm

## Install Guide
The steps outlined below are specifically designed for the Windows Operating
System. Different configurations may be necessary when building this application
on MacOS or other operating systems. Therefore, please refer to the documentation
for guidance on issuing commands in the corresponding operating system.
Due to the application’s implementation using a Microservices architecture, each
service requires individual cloning. The order in which these services are started is
crucial for proper initialization. The recommended startup sequence is as follows:

1. Eureka server
2. API Gateway service
3. Authentication service(Keycloak in Docker container)
4. CRM service
5. Sales service
6. Frontend service
To keep the project organized, create a folder to save all cloned repositories.
After creating, move into the folder.

### Eureka server
1. Run this command in the terminal to clone the repository for the service registry:
```
git clone https://github.com/Asatillo/eureka-server.git
```
2. Move to the eureka-server folder
3. Run the command:
```
mvn spring-boot:run
```

### API Gateway service
1. Run this command in the terminal to clone the repository for the API Gateway
service:
```
git clone https://github.com/Asatillo/api-gateway-service.git
```
2. Move to the `api-gateway-service` folder
3. Run the command:
```
mvn spring-boot:run
```

### Authentication service
1. Run this command in the terminal to clone the repository for the authentication service:
```
git clone https://github.com/Asatillo/authentication-service.git
```
2. Move to the `authentication-service` folder
3. Create `.env` file with the content:
```
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin
POSTGRES_DB=keycloak_db
POSTGRES_LOCAL_PORT=5431
POSTGRES_CONTAINER_PORT=5431

KEYCLOAK_ADMIN_USER=kc_admin
KEYCLOAK_ADMIN_PASSWORD=kc_admin
# Port 8080 has to be free
KEYCLOAK_LOCAL_PORT=8080
KEYCLOAK_CONTAINER_PORT=8080
```
4. Run the Docker container:
```
1 docker-compose up --build
```
5. In your browser go to `the http://localhost:8080`. This should show you the main page of the Keycloak server.
6. Click on the Administration console and log in with `KEYCLOAK_ADMIN` credentials written in the .env file.
7. Click on Master and choose ‘Create realm‘. Click on browse and choose `realm_export.json`

### CRM service
1. Run this command in the terminal to clone the repository for the CRM service:
```
git clone https://github.com/Asatillo/crm-service.git
```
2. Move to the `crm-service` folder
3. Create `.env` file with the content:
```
MYSQLDB_USER=root
MYSQLDB_ROOT_PASSWORD=root
MYSQLDB_DATABASE=crm
MYSQLDB_LOCAL_PORT=3307
MYSQLDB_DOCKER_PORT=3306
```
4. Run the docker container to access the MySQL database
```
docker-compose up --build
```
5. Run the application:
```
mvn spring-boot:run
```

### Sales service
1. Run this command in the terminal to clone the repository for the sales service:
```
git clone https://github.com/Asatillo/sales-service.git
```
2. Move to the `sales-service` folder
3. Create `.env` file with the content:
```
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_SALES_DB=sales_db
POSTGRES_LOCAL_PORT=5432
POSTGRES_CONTAINER_PORT=5432
```
4. Run the docker container to access the PostgreSQL database
```
docker-compose up --build
```
5. Run the application:
```
./gradlew bootRun
```

### Frontend service
1. Run this command in the terminal to clone the repository for the frontend service:
```
git clone https://github.com/Asatillo/frontend-service.git
```
3. Move to the `frontend-service` folder
4. Install all of the packages:
```
npm install
```
6. Run the application
```
npm run serve
```
To ensure that all services are up and running, visit the following page: `http://localhost:8761/`

🪄 You can now access the application’s frontend page by navigating to `http://localhost:8083` in your web browser.


## Roadmap
- Improving Navigation Performance with Caching
- Use granular access control
- Set up token lifecycle in the frontend
- Enhance Scalability and Manageability with Docker and Kubernetes
