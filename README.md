# Employee Management System

A full-stack web application for managing employee records built with Spring Boot, Spring MVC, Thymeleaf, and Bootstrap.

## 📋 Overview

This is a CRUD (Create, Read, Update, Delete) application that allows users to manage employee information through an intuitive web interface. The application follows the MVC architecture pattern and uses JPA/Hibernate for database operations.

## ✨ Features

- **Employee List View**: Display all employees in a sortable table format
- **Add Employee**: Create new employee records with first name, last name, and email
- **Update Employee**: Edit existing employee information
- **Delete Employee**: Remove employee records with confirmation dialog
- **Auto-Sort**: Employees are automatically sorted by last name in ascending order
- **Responsive UI**: Bootstrap-powered interface that works on all devices
- **Auto-Redirect**: Root URL automatically redirects to employee list

## 🛠️ Technology Stack

- **Backend Framework**: Spring Boot 3.3.0
- **Java Version**: Java 17
- **Template Engine**: Thymeleaf
- **ORM**: Spring Data JPA with Hibernate
- **Database**: MySQL
- **Frontend**: HTML5, Bootstrap 5.3.8
- **Build Tool**: Maven
- **Development Tools**: Spring Boot DevTools

## 📦 Project Structure

```
demo-employees-mvc-project/
├── src/main/
│   ├── java/com/luv2code/springboot/thymeleafdemo/
│   │   ├── ThymeleafdemoApplication.java       # Main application class
│   │   ├── controller/
│   │   │   └── EmployeeController.java         # MVC Controller
│   │   ├── dao/
│   │   │   └── EmployeeRepository.java         # JPA Repository
│   │   ├── entity/
│   │   │   └── Employee.java                   # Employee entity
│   │   └── service/
│   │       ├── EmployeeService.java            # Service interface
│   │       └── EmployeeServiceImpl.java        # Service implementation
│   └── resources/
│       ├── application.properties               # Configuration file
│       ├── static/
│       │   └── index.html                      # Redirect page
│       └── templates/employees/
│           ├── list-employees.html             # Employee list view
│           └── employee-form.html              # Add/Edit form
└── pom.xml                                      # Maven dependencies
```

## 🗄️ Database Schema

The application uses a MySQL database with the following table structure:

```sql
CREATE TABLE employee (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    email VARCHAR(255)
);
```

## 🚀 Getting Started

### Prerequisites

- **JDK 17** or higher
- **Maven 3.6+**
- **MySQL Server** (running on localhost:3306)
- A MySQL database named `employee_directory`

### Database Setup

1. Create the MySQL database:
```sql
CREATE DATABASE employee_directory;
```

2. The application will automatically create the `employee` table on first run (DDL auto-update is enabled)

### Configuration

Update `src/main/resources/application.properties` with your database credentials:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/employee_directory
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```

### Installation & Running

1. **Clone the repository:**
```bash
git clone <repository-url>
cd demo-employees-mvc-project
```

2. **Build the project:**
```bash
mvn clean install
```

3. **Run the application:**
```bash
mvn spring-boot:run
```

4. **Access the application:**
- Open your browser and navigate to: `http://localhost:8080`
- You'll be automatically redirected to: `http://localhost:8080/employees/list`

## 🎯 Application Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Redirects to employee list |
| GET | `/employees/list` | Display all employees |
| GET | `/employees/showFormForAdd` | Show form to add new employee |
| GET | `/employees/showFormForUpdate?employeeId={id}` | Show form to update employee |
| POST | `/employees/save` | Save (create/update) employee |
| GET | `/employees/delete?employeeId={id}` | Delete employee by ID |

## 💻 Usage Examples

### Adding a New Employee
1. Click the "Add Employee" button
2. Fill in the employee details (First Name, Last Name, Email)
3. Click "Save"

### Updating an Employee
1. Click the "Update" button next to an employee
2. Modify the employee details
3. Click "Save"

### Deleting an Employee
1. Click the "Delete" button next to an employee
2. Confirm the deletion in the popup dialog

## 🎨 User Interface

The application uses **Bootstrap 5.3.8** for styling and provides:
- Clean, modern design
- Responsive tables
- Color-coded action buttons (Primary for Add, Info for Update, Danger for Delete)
- Confirmation dialogs for destructive actions
- Mobile-friendly layout

## 🏗️ Architecture

The application follows a **layered architecture**:

1. **Presentation Layer** (Controller + Thymeleaf Views)
   - Handles HTTP requests and responses
   - Renders HTML templates

2. **Service Layer** (Business Logic)
   - Contains business rules
   - Coordinates between controller and repository

3. **Data Access Layer** (Repository)
   - Manages database operations
   - Uses Spring Data JPA for automatic query generation

4. **Entity Layer**
   - Represents database tables as Java objects

## 🔑 Key Features Implementation

### Auto-Sorting
Employees are automatically sorted by last name using a custom repository method:
```java
List<Employee> findAllByOrderByLastNameAsc();
```

### Form Handling
The same form (`employee-form.html`) is used for both creating and updating employees:
- A hidden `id` field determines whether it's an insert or update operation
- Thymeleaf's `th:object` binding simplifies form data handling

### Delete Confirmation
JavaScript confirmation dialog prevents accidental deletions:
```javascript
onclick="return confirm('Are you sure you want to delete this employee?')"
```

## 🧪 Testing

Run the tests using:
```bash
mvn test
```

## 📝 Development Notes

- **Spring Boot DevTools** is enabled for automatic application restart during development
- **Hibernate DDL Auto** is set to `update` to automatically sync entity changes with the database
- The application uses **constructor-based dependency injection** for better testability
- **Optional** is used for null-safe database operations

## 🔧 Configuration Properties

| Property | Value | Description |
|----------|-------|-------------|
| `spring.datasource.url` | `jdbc:mysql://localhost:3306/employee_directory` | Database connection URL |
| `spring.jpa.hibernate.ddl-auto` | `update` | Hibernate schema generation |

## 🚦 Port Configuration

The application runs on the default port **8080**. To change it, add to `application.properties`:
```properties
server.port=9090
```

## 📚 Dependencies

Key dependencies (from `pom.xml`):
- `spring-boot-starter-web` - Spring MVC and REST
- `spring-boot-starter-thymeleaf` - Template engine
- `spring-boot-starter-data-jpa` - JPA and Hibernate
- `mysql-connector-j` - MySQL driver
- `spring-boot-devtools` - Development tools

## 🐛 Troubleshooting

**Database Connection Issues:**
- Ensure MySQL is running
- Verify database credentials in `application.properties`
- Check if the database `employee_directory` exists

**Port Already in Use:**
- Change the server port in `application.properties`
- Or stop the application using port 8080

**Thymeleaf Template Not Found:**
- Ensure templates are in `src/main/resources/templates/`
- Check template names match controller return values

## 🔮 Future Enhancements

- [ ] Add input validation (Bean Validation)
- [ ] Implement search/filter functionality
- [ ] Add pagination for large datasets
- [ ] Export employee list to CSV/Excel
- [ ] Add employee photos
- [ ] Implement user authentication
- [ ] Add department management
- [ ] REST API endpoints for mobile integration
- [ ] Unit and integration tests
- [ ] Custom exception handling

## 👨‍💻 Author

Omar Hamdi Ellafy

## 📄 License

This project is licensed under the MIT License.

---

**Built with ❤️ using Spring Boot and Thymeleaf**
