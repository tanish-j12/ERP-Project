# 🎓 University ERP System

A comprehensive desktop application for managing university academic operations with role-based access control, secure authentication, and modern UI.

**Course:** Advanced Programming (CSE201) | **Instructor:** Dr. Raghava Muthuraju  
**Tech Stack:** Java 21, Swing, MySQL, bcrypt  
**Team:** Nalin Gupta, Tanish Jindal

---

## 🚀 Key Features

### Role-Based Access Control
- **Student:** Course registration, timetable view, grade tracking, transcript export
- **Instructor:** Grade management, section oversight, class statistics
- **Admin:** User management, course/section creation, system settings

### Security & Authentication
- **Password Hashing:** bcrypt with salt for secure storage
- **Dual Database:** Separate auth and ERP databases
- **Session Management:** Single active session per user
- **Maintenance Mode:** System-wide read-only mode for safety

### Modern UI
- **Dark Theme:** FlatLaf with contemporary design
- **Sidebar Navigation:** Intuitive panel switching
- **Responsive Layout:** MigLayout for clean forms
- **Real-time Updates:** Auto-refresh on tab switch

---

## 🛠️ Technology Stack

| Category | Technology |
|----------|-----------|
| Language | Java JDK 21 |
| UI Framework | Java Swing + FlatLaf (Dark) |
| Layout | MigLayout |
| Database | MySQL 8.0 (dual DB architecture) |
| Security | jBCrypt password hashing |
| Testing | JUnit 5 + Mockito |
| Logging | SLF4J with Logback |
| Build Tool | Maven |

---

## 📦 Quick Start

### Prerequisites
```bash
# Required installations
- Java JDK 21+
- MySQL Server 8.0+
- Maven 3.6+
```

### Database Setup
```bash
# 1. Configure credentials in src/resources/application.conf
# 2. Start MySQL server
# 3. Load seed data
mysql -u root -p < small_seed.sql
```

### Run Application
```bash
# Using Maven
mvn clean compile
mvn exec:java -Dexec.mainClass="edu.univ.erp.ui.Main"

# Or using JAR
java -jar target/university-erp-1.0.jar
```

### Default Credentials
| Username | Password | Role |
|----------|----------|------|
| admin1 | pass123 | Admin |
| inst1 | pass123 | Instructor |
| stu1 | pass123 | Student |

---

## 📊 System Architecture

### Dual Database Design

**Auth DB (auth_db):**
- User authentication data
- Password hashes (bcrypt)
- Login tracking
- No business data

**ERP DB (erp_db):**
- Student/instructor profiles
- Courses and sections
- Enrollments and grades
- System settings
- No authentication data

**Link:** Both databases connected via `user_id` foreign key

---

## 🎯 Core Functionality

### Student Features
✅ Browse course catalog with availability  
✅ Register/drop courses (capacity-aware)  
✅ View weekly timetable  
✅ Track component scores (Quiz, Midterm, Endterm)  
✅ Export transcript to CSV  

### Instructor Features
✅ View assigned sections  
✅ Enter/edit assessment scores (0-100)  
✅ Define custom grading thresholds (A+, A, B, C, D, F)  
✅ Compute final letter grades  
✅ View class statistics  

### Admin Features
✅ Create/manage users (students, instructors, admins)  
✅ Create/edit courses and sections  
✅ Assign instructors to sections  
✅ Set registration and drop deadlines  
✅ Toggle maintenance mode  

---

## 🔐 Security Implementation

### Password Security
```java
// bcrypt hashing with work factor 10
String hash = BCrypt.hashpw(password, BCrypt.gensalt(10));
boolean valid = BCrypt.checkpw(plaintext, stored_hash);
```

### Access Control
- Role-based permissions enforced at service layer
- Instructors can only modify their own sections
- Students can only access their own data
- Admins have full system access

### Maintenance Mode
- System-wide read-only enforcement
- Yellow warning banner on all dashboards
- Write operations blocked for students/instructors
- Admin retains full control

---

## 📈 Grading System

### Assessment Components
Each course uses three components (each 0-100):
- **Quiz:** Continuous assessment
- **Midterm:** Mid-semester exam
- **Endterm:** Final exam

### Final Score Calculation
```
Final Score = Quiz + Midterm + Endterm  (max 100)
```

### Instructor-Defined Thresholds
Instructors set custom grade boundaries:
- **Example:** A+ ≥ 70, A ≥ 60, B ≥ 50, C ≥ 40, D ≥ 30, F < 30

### Letter Grade Assignment
System assigns highest grade where score meets minimum threshold with automatic validation:
- Sum of components = 100
- Thresholds strictly decreasing
- All values non-negative

---

## 🧪 Testing

### Test Coverage
✅ **Login & Authentication:** All roles, error handling  
✅ **Student Module:** Registration, timetable, grades, transcript  
✅ **Instructor Module:** Grade entry, statistics, final grade computation  
✅ **Admin Module:** User/course management, system settings  
✅ **Security:** Password hashing, access control, SQL injection prevention  
✅ **Maintenance Mode:** Write blocking, banner display  

### Test Results
- **Framework:** JUnit 5 with Mockito
- **Status:** All acceptance tests passed
- **Coverage:** Service and repository layers

---

## 📸 Screenshots

### Login Interface
Modern dark-themed login with secure authentication.

### Student Dashboard
- Course catalog with real-time availability
- Timetable view with registered sections
- Grades with component breakdown

### Instructor Dashboard
- Gradebook with score entry
- Custom grading threshold configuration
- Class statistics panel

### Admin Dashboard
- User management interface
- Course and section creation
- System settings and maintenance toggle

---

## 💡 What I Learned

- **Desktop Application Development:** Java Swing with modern UI libraries
- **Database Design:** Multi-database architecture with proper separation
- **Security Best Practices:** Password hashing, access control, session management
- **Role-Based Systems:** Implementing granular permissions
- **Testing:** Unit testing with mocking and dependency injection
- **Maven Build System:** Dependency management and project structure

---

## 🔧 Project Structure

```
university-erp/
├── src/main/java/edu/univ/erp/
│   ├── ui/                    # Swing UI components
│   ├── api/                   # API layer (auth, student, instructor, admin)
│   ├── service/               # Business logic layer
│   ├── data/                  # Database repositories
│   ├── domain/                # Data models
│   ├── access/                # Access control
│   └── auth/                  # Authentication & session
├── src/main/resources/
│   ├── application.conf       # Database configuration
│   └── logback.xml           # Logging configuration
├── src/test/java/             # JUnit tests
├── small_seed.sql            # Test database
├── large_seed.sql            # Extended dataset
└── pom.xml                   # Maven dependencies
```

---

## 📄 License

This project is for **educational purposes only**.

---

## 📧 Contact

**Nalin Gupta & Tanish Jindal**  
B.Tech Computer Science | IIIT Delhi

- 📧 Email: tanish24579@iiitd.ac.in
- 💼 LinkedIn: [linkedin.com/in/tanishjindal](https://linkedin.com/in/tanishjindal)
- 🐙 GitHub: [github.com/tanish-j12](https://github.com/tanish-j12)

---

⭐ **Star this repository if you find it useful for learning Java desktop application development!**
