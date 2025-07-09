# Spring Boot REST Security Employee Management API

This project is a Spring Boot application demonstrating a RESTful API for employee management with robust security features. It utilizes Spring Data JPA for data persistence and Spring Security for authentication and authorization.

### Key Components:

* **`CruddemoApplication.java`**: The main Spring Boot application entry point.
* **`dao`**: Contains the `EmployeeRepository` interface, extending `JpaRepository` for database operations on `Employee` entities.
* **`entity`**: Defines the `Employee` JPA entity, representing the employee data model.
* **`rest`**: Houses `EmployeeRestController`, which exposes the RESTful endpoints for employee management.
* **`security`**: Contains `DemoSecurityConfig`, where Spring Security configurations, including authorization rules, are defined.
* **`service`**: (Presumed) This package would typically contain interfaces and implementations for business logic related to employee operations, acting as an intermediary between the controller and the DAO.

## Available APIs and Security Configuration

The application's security configuration (defined in `DemoSecurityConfig`) enforces role-based access control for various API endpoints. Below is a breakdown of the available API endpoints and their required roles:

| HTTP Method | API Endpoint        | Required Role(s) | Description                                       |
| :---------- | :------------------ | :--------------- | :------------------------------------------------ |
| `GET`       | `/api/employees`    | `EMPLOYEE`       | Retrieve a list of all employees.                 |
| `GET`       | `/api/employees/**` | `EMPLOYEE`       | Retrieve a specific employee by ID or other criteria. |
| `POST`      | `/api/employees`    | `MANAGER`        | Create a new employee.                            |
| `PUT`       | `/api/employees`    | `MANAGER`        | Update an existing employee.                      |
| `PATCH`     | `/api/employees/**` | `MANAGER`        | Partially update an existing employee.            |
| `DELETE`    | `/api/employees/**` | `ADMIN`          | Delete an employee.                               |

**Note:** The `**` in the API endpoints indicates a wildcard, meaning any path segment after `/api/employees/` will match. For example, `/api/employees/123` or `/api/employees/search` would be covered.

## Getting Started

### Prerequisites

* JDK 17 or higher
* Maven 3.6+
* A MySQL database server.

### Database Setup

Before running the application, you need to set up the database and populate it with initial data and user credentials for Spring Security.

1.  **Create the `employee_directory` database and `employee` table:**
    Run the SQL script located at `sql-scripts/employee-directory.sql` against your MySQL database. This script creates the necessary database schema for employee data.

2.  **Set up Spring Security users and roles:**
    Run the SQL script located at `sql-scripts/06-setup-spring-security-demo-database.sql` against your MySQL database. This script creates the `users` and `authorities` tables and inserts sample user data with predefined roles (`EMPLOYEE`, `MANAGER`, `ADMIN`).

### Build the Project

1.  Clone the repository:
    ```bash
    git clone <repository_url>
    cd spring-boot-rest-security-employee
    ```
2.  Build the project using Maven:
    ```bash
    mvn clean install
    ```

### Run the Application

You can run the Spring Boot application using Maven:

```bash
mvn spring-boot:run
```

Alternatively, you can run the `CruddemoApplication.java` file directly from your IDE.

The application will typically start on port `8080` (unless configured otherwise in `application.properties`).

## Usage

Once the application is running, you can interact with the API endpoints using tools like Postman, Insomnia.
Remember to include appropriate authentication headers (e.g., Basic Auth or Bearer Token) with the correct 
user credentials for the required roles (created by `06-setup-spring-security-demo-database.sql`).