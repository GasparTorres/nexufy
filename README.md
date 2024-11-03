README for Backend
## Nexufy Backend
### Introduction
Nexufy is a platform that connects producers and suppliers of inputs such as plastics, glass, and
other materials. This backend handles the business logic and API for interactions on the platform,
enabling the management of products, users, and roles, with security and authentication features.
### Technologies Used
- **Framework**: Spring Boot
- **Database**: MongoDB
- **Authentication**: JWT (Json Web Token)
- **Report Generation**: JasperReports
- **Security**: Spring Security
- **API Documentation**: Swagger
### Database Structure
The MongoDB database is organized into the following collections:
- **comments**: Stores comments.
- **customers**: Contains registered customer information, including roles and associated products.
- **products**: Stores published products.
- **roles**: Defines system roles (ROLE_USER, ROLE_ADMIN, ROLE_SUPERADMIN).
### Roles and Permissions
- **Unregistered User (Visitor)**: Browse and view product listings.
- **Registered User (ROLE_USER)**: View details of other users.
- **Administrator (ROLE_ADMIN)**: Publish and manage their own products.
- **Super Administrator (ROLE_SUPERADMIN)**: Manage all users, products, and view statistics.
### Installation and Configuration Guide
#### Prerequisites
- Java 17
- MongoDB
- Git
#### Clone the Repository
```bash
git clone https://github.com/GasparTorres/nexufy.git
cd nexufy
```
#### Configuration
Edit the `src/main/resources/application.properties` file with your MongoDB credentials and JWT
settings:
```properties
spring.application.name=nexufy
spring.data.mongodb.database=Nexufy
spring.data.mongodb.uri=mongodb+srv://<user>:<password>@nexufy.mongodb.net/
nexufy.app.jwtSecret=YourJWTSecretKey
nexufy.app.jwtExpirationMs=86400000
server.port=8081
spring.main.allow-circular-references=true
```
#### Run the Application
```bash
./mvnw install
./mvnw spring-boot:run
```
The application will be available at `http://localhost:8081`.
### Project Architecture
- **Controllers**: Manage HTTP requests.
- **Services**: Contains business logic.
- **Repositories**: Handle database interaction.
- **Security**: Configures CORS and JWT in `SecurityConfig`.
### API Endpoints
#### Authentication
- `POST /api/auth/login`: Log in.
- `POST /api/auth/register`: Register new users.
#### Customers
- `GET /api/customer/all`: Get all customers.
- `PUT /api/customer/{id}`: Update customer.
- `DELETE /api/customer/{id}`: Delete customer.
#### Products
- `GET /api/customer/{id}/products`: Get products of a customer.
- `POST /api/products/customer/{customerId}`: Create a product.
#### Users and Roles
- `PUT /api/user/promote/admin`: Promote user to administrator.
### Security (CORS and JWT)
The security configuration in `SecurityConfig` allows:
- **Public access**: login, registration, and access to products.
- **Protection**: Routes for super administrators and reports require specific permissions.
