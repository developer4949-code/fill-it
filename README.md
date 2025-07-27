# Fill-It Backend - Spring Boot API Service

A robust, scalable REST API service built with Spring Boot that powers the Fill-It ride-sharing platform. Provides authentication, trip management, user management, and real-time communication services for both customers and drivers.

## 🚀 Features

### Authentication & Authorization
- **Firebase Authentication**: Secure user registration and login
- **Role-based Access Control**: Customer and driver role management
- **JWT Token Management**: Secure session handling
- **User Profile Management**: Complete user information handling

### Trip Management
- **Trip Creation**: Create new ride requests with location data
- **Trip Acceptance**: Driver trip acceptance workflow
- **Trip Completion**: Complete trip lifecycle management
- **Real-time Updates**: Live trip status synchronization
- **Location Services**: GPS coordinates and distance calculation

### User Management
- **Customer Management**: Customer profile and data operations
- **Driver Management**: Driver profile and vehicle information
- **Profile Updates**: Phone number and information updates
- **Data Validation**: Comprehensive input validation

### Real-time Communication
- **Firebase Realtime Database**: Live data synchronization
- **Push Notifications**: Real-time alerts and updates
- **Location Tracking**: GPS-based location services
- **Status Updates**: Trip status real-time updates

## 🛠 Tech Stack

### Core Framework
- **Spring Boot 3.5.0** - Main application framework
- **Java 17** - Programming language with latest LTS features
- **Spring Web** - RESTful web services
- **Spring Dependency Management** - Dependency injection

### Database & Storage
- **Firebase Realtime Database** - Primary database for trip data
- **Firebase Firestore** - Document database for user data
- **Firebase Authentication** - User authentication and authorization

### Google Services Integration
- **Firebase Admin SDK 9.1.1** - Server-side Firebase operations
- **Google API Client 1.35.2** - Google services integration
- **Google OAuth Client 1.34.1** - OAuth authentication
- **Google Drive API v3** - File storage and management

### Development Tools
- **Lombok 1.18.30** - Reduces boilerplate code
- **JavaCV Platform 1.5.9** - Computer vision and media processing
- **Spring Boot Mail** - Email services
- **Spring Boot Test** - Testing framework

### Build & Deployment
- **Gradle** - Build automation tool
- **Spring Boot Testcontainers** - Integration testing
- **JUnit Jupiter** - Unit testing framework

## 🏗 Project Structure

```
fill-it-master/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/fill_it/
│   │   │       ├── config/
│   │   │       │   ├── FirebaseConfig.java
│   │   │       │   └── WebConfig.java
│   │   │       ├── controller/
│   │   │       │   ├── AuthController.java
│   │   │       │   ├── TripController.java
│   │   │       │   └── UserController.java
│   │   │       ├── dto/
│   │   │       │   ├── CustomerSignupRequest.java
│   │   │       │   ├── DriverSignupRequest.java
│   │   │       │   ├── LoginRequest.java
│   │   │       │   └── LoginResponse.java
│   │   │       ├── model/
│   │   │       │   ├── Customer.java
│   │   │       │   ├── Driver.java
│   │   │       │   └── Trip.java
│   │   │       ├── service/
│   │   │       │   ├── AuthService.java
│   │   │       │   ├── TripService.java
│   │   │       │   └── UserService.java
│   │   │       └── FillItApplication.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── serviceAccountKey.json
│   └── test/
│       └── java/
│           └── com/example/fill_it/
│               └── FillItApplicationTests.java
├── build.gradle
├── settings.gradle
├── gradlew
└── gradlew.bat
```

## 🚀 Getting Started

### Prerequisites

- **Java 17+** - [Download here](https://adoptium.net/)
- **Gradle 7.0+** - Build tool (included with project)
- **Firebase Project** - Set up Firebase for authentication and database
- **Google Cloud Project** - For additional Google services

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/fill-it-backend.git
   cd fill-it-backend
   ```

2. **Set up Firebase**
   - Create a Firebase project at [Firebase Console](https://console.firebase.google.com/)
   - Enable Authentication with Email/Password
   - Set up Firestore Database
   - Set up Firebase Realtime Database
   - Download `serviceAccountKey.json` from Project Settings

3. **Configure Firebase**
   - Place `serviceAccountKey.json` in `src/main/resources/`
   - Update Firebase configuration in `FirebaseConfig.java`

4. **Environment Configuration**
   - Create `application.properties` or use environment variables:
   ```properties
   spring.application.name=Fill_It
   server.address=0.0.0.0
   server.port=8080
   ```

5. **Build the project**
   ```bash
   ./gradlew build
   ```

6. **Run the application**
   ```bash
   ./gradlew bootRun
   ```

## 📡 API Endpoints

### Authentication Endpoints (`/api/auth`)

#### Driver Registration
```http
POST /api/auth/signup/driver
Content-Type: application/json

{
  "name": "John Driver",
  "email": "driver@example.com",
  "password": "securepassword",
  "vehicleNumber": "ABC123",
  "phoneNumber": "+1234567890"
}
```

#### Customer Registration
```http
POST /api/auth/signup/customer
Content-Type: application/json

{
  "name": "Jane Customer",
  "email": "customer@example.com",
  "password": "securepassword",
  "phoneNumber": "+1234567890"
}
```

#### User Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password"
}
```

#### Get User Details
```http
GET /api/auth/user-details?email=user@example.com
```

#### User Logout
```http
POST /api/auth/logout?email=user@example.com
```

### Trip Management Endpoints (`/api/trips`)

#### Create Trip
```http
POST /api/trips/create
Content-Type: application/json

{
  "customerEmail": "customer@example.com",
  "from": "123 Main St, City",
  "to": "456 Oak Ave, City",
  "date": "2024-01-15",
  "fromLat": "40.7128",
  "fromLon": "-74.0060",
  "toLat": "40.7589",
  "toLon": "-73.9851"
}
```

#### Accept Trip
```http
POST /api/trips/accept
Content-Type: application/json

{
  "tripId": "trip123",
  "driverEmail": "driver@example.com"
}
```

#### Complete Trip
```http
POST /api/trips/complete
Content-Type: application/json

{
  "tripId": "trip123"
}
```

#### Get Customer Trips
```http
GET /api/trips/by-customer?email=customer@example.com
```

#### Get Driver Trips
```http
GET /api/trips/by-driver?email=driver@example.com
```

#### Get Nearby Trips
```http
GET /api/trips/nearby?lat=40.7128&lon=-74.0060
```

### User Management Endpoints (`/api/user`)

#### Update Customer Phone
```http
PUT /api/user/customer/phone?email=customer@example.com&newPhone=+1234567890
```

#### Update Driver Phone
```http
PUT /api/user/driver/phone?email=driver@example.com&newPhone=+1234567890
```

#### Get Customer Details
```http
GET /api/user/customer/details?email=customer@example.com
```

#### Get Driver Details
```http
GET /api/user/driver/details?email=driver@example.com
```

## 🔧 Configuration

### Application Properties

```properties
# Server Configuration
spring.application.name=Fill_It
server.address=0.0.0.0
server.port=8080

# Firebase Configuration
firebase.database.url=https://your-project.firebaseio.com
firebase.project.id=your-project-id

# Logging Configuration
logging.level.com.example.fill_it=DEBUG
logging.level.org.springframework.web=INFO

# CORS Configuration
spring.web.cors.allowed-origins=*
spring.web.cors.allowed-methods=GET,POST,PUT,DELETE,OPTIONS
spring.web.cors.allowed-headers=*
```

### Firebase Setup

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Create a new project
   - Enable Authentication with Email/Password
   - Set up Firestore Database
   - Set up Firebase Realtime Database

2. **Download Service Account Key**
   - Go to Project Settings → Service Accounts
   - Generate new private key
   - Download JSON file
   - Place in `src/main/resources/serviceAccountKey.json`

3. **Update Firebase Configuration**
   ```java
   // In FirebaseConfig.java
   .setDatabaseUrl("https://your-project-id.firebaseio.com/")
   ```

### Environment Variables

```bash
# Server Configuration
SERVER_PORT=8080
SERVER_ADDRESS=0.0.0.0

# Firebase Configuration
FIREBASE_DATABASE_URL=https://your-project.firebaseio.com
FIREBASE_PROJECT_ID=your-project-id

# Logging
LOGGING_LEVEL=INFO
```

## 🧪 Testing

### Running Tests

```bash
# Run all tests
./gradlew test

# Run tests with coverage
./gradlew test jacocoTestReport

# Run specific test class
./gradlew test --tests AuthServiceTest

# Run integration tests
./gradlew integrationTest
```

### Test Structure

```
src/test/java/com/example/fill_it/
├── controller/
│   ├── AuthControllerTest.java
│   ├── TripControllerTest.java
│   └── UserControllerTest.java
├── service/
│   ├── AuthServiceTest.java
│   ├── TripServiceTest.java
│   └── UserServiceTest.java
└── integration/
    └── ApiIntegrationTest.java
```

### Test Configuration

```properties
# Test properties
spring.profiles.active=test
firebase.database.url=https://test-project.firebaseio.com
```

## 🚀 Deployment

### Local Development

```bash
# Run with Gradle
./gradlew bootRun

# Run with Java
java -jar build/libs/fill-it-0.0.1-SNAPSHOT.jar
```

### Docker Deployment

1. **Create Dockerfile**
   ```dockerfile
   FROM openjdk:17-jdk-slim
   VOLUME /tmp
   COPY build/libs/*.jar app.jar
   ENTRYPOINT ["java","-jar","/app.jar"]
   ```

2. **Build and Run**
   ```bash
   # Build Docker image
   docker build -t fill-it-backend .

   # Run container
   docker run -p 8080:8080 fill-it-backend
   ```

### Cloud Deployment

#### Google Cloud Platform
```bash
# Deploy to Google Cloud Run
gcloud run deploy fill-it-backend \
  --source . \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated
```

#### AWS
```bash
# Deploy to AWS Elastic Beanstalk
eb init fill-it-backend
eb create fill-it-backend-env
eb deploy
```

#### Heroku
```bash
# Deploy to Heroku
heroku create fill-it-backend
git push heroku main
```

## 🔒 Security

### Authentication & Authorization
- **Firebase Authentication**: Secure user management
- **Role-based Access Control**: Customer and driver roles
- **Input Validation**: Comprehensive request validation
- **CORS Configuration**: Cross-origin resource sharing

### Data Protection
- **HTTPS Communication**: Encrypted data transmission
- **Firebase Security Rules**: Database access control
- **Input Sanitization**: Prevent injection attacks
- **Error Handling**: Secure error responses

### Best Practices
- **Environment Variables**: Secure configuration management
- **Logging**: Audit trail and monitoring
- **Rate Limiting**: Prevent abuse
- **Regular Updates**: Security patches and updates

## 📊 Monitoring & Logging

### Application Monitoring
- **Spring Boot Actuator**: Health checks and metrics
- **Custom Metrics**: Business-specific monitoring
- **Performance Tracking**: Response time monitoring
- **Error Tracking**: Exception monitoring

### Logging Configuration
```properties
# Logging levels
logging.level.root=INFO
logging.level.com.example.fill_it=DEBUG
logging.level.org.springframework.web=INFO

# Log file configuration
logging.file.name=logs/fill-it.log
logging.pattern.file=%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
```

### Health Checks
```http
GET /actuator/health
GET /actuator/info
GET /actuator/metrics
```

## 🔧 Development

### Code Style
- Follow Java coding conventions
- Use meaningful variable and method names
- Add comprehensive comments
- Follow SOLID principles

### Git Workflow
1. Create feature branch
2. Make changes with meaningful commits
3. Write tests for new features
4. Create pull request
5. Code review and merge

### IDE Setup
- **IntelliJ IDEA**: Recommended IDE
- **Eclipse**: Alternative option
- **VS Code**: Lightweight option

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow existing code style
- Write meaningful commit messages
- Add tests for new features
- Update documentation
- Ensure all tests pass

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

### Common Issues

1. **Firebase Connection Issues**
   - Verify service account key
   - Check Firebase project configuration
   - Ensure proper permissions

2. **Build Issues**
   ```bash
   ./gradlew clean build
   ```

3. **Port Conflicts**
   - Change server port in `application.properties`
   - Check if port is already in use

### Getting Help

- **Documentation**: Check Spring Boot docs
- **Issues**: Create an issue in this repository
- **Discussions**: Use GitHub Discussions
- **Email**: support@fill-it.com

## 🙏 Acknowledgments

- Spring Boot team for the excellent framework
- Firebase team for the comprehensive backend services
- All contributors who helped build this application
- Open source community for valuable tools and libraries

## 📞 Contact

- **Website**: [fill-it.com](https://fill-it.com)
- **Email**: info@fill-it.com
- **Twitter**: [@fillitapp](https://twitter.com/fillitapp)
- **LinkedIn**: [Fill-It](https://linkedin.com/company/fill-it)

---

**Made with ❤️ by the Fill-It Team**
