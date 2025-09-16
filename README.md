# NETCONF Protocol Simulator

A comprehensive Java-based implementation that provides both REST API and Web UI interfaces for simulating NETCONF protocol operations, enabling seamless network configuration management without direct device access.

## Project Overview

This project simulates NETCONF protocol operations through:
- **REST API** for programmatic access
- **Web UI** for interactive usage
- **Mock implementation** for testing without real devices

It provides a realistic environment for testing network configuration workflows without requiring physical network devices. It's particularly valuable for development, testing, and training scenarios where access to actual network infrastructure is limited or impractical.

## Key Features

- Full NETCONF operation simulation (get-config, edit-config, copy-config, lock, unlock, etc.)
- Dual interface (REST API and Web UI)
- XML configuration handling
- Session management with automatic cleanup of inactive sessions
- Operation history tracking
- Comprehensive error handling

## Technology Stack

- **Java 17**: Core programming language
- **Spring Boot 3.1.0**: Application framework
- **Maven**: Build and dependency management
- **Thymeleaf**: Server-side templating for the Web UI
- **Bootstrap**: Frontend styling
- **jQuery**: Frontend interactivity

## Getting Started

### Prerequisites

- Java 17 or later
- Maven 3.6 or later
- Git

### Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/netconf-simulator.git
    cd netconf-simulator
    ```

2.  **Build the project:**
    This command compiles the code, runs tests, and packages the application into a JAR file.
    ```bash
    mvn clean install
    ```

### Running the Application

You can run the application in several ways:

**Option 1: Using the Maven Spring Boot Plugin (Recommended for development)**
```bash
mvn spring-boot:run
```

**Option 2: Running the executable JAR**
```bash
java -jar target/netconf-simulator-1.0.0.jar
```

The application will start on `http://localhost:8081` by default.

## Using the Application

### Web UI Interface

The web interface provides an interactive way to use the application:

1.  **Home Page**: `http://localhost:8081/`
    - Provides an overview and quick links to other pages.

2.  **Operations Page**: `http://localhost:8081/web/netconf/operations`
    - Connect to devices.
    - Select and perform NETCONF operations.
    - View results in formatted XML.
    - Manage active sessions.

3.  **History Page**: `http://localhost:8081/web/netconf/history`
    - View a chronological history of all operations performed.
    - Filter and search for specific operations.
    - Examine detailed request and response data.

### REST API Interface

The application provides a RESTful API for programmatic access.

**Base URL**: `http://localhost:8081/api/netconf`

**Endpoints:**

- **`POST /connect`**: Establish a new NETCONF session.
  **Request Body:**
  ```json
  {
    "host": "192.168.1.1",
    "port": 830,
    "username": "admin",
    "password": "password"
  }
  ```

- **`POST /get-config`**: Retrieve configuration from a device.
  **Request Body:**
  ```json
  {
    "sessionId": "YOUR_SESSION_ID",
    "datastore": "running",
    "filter": "<system/>"
  }
  ```

- **`POST /edit-config`**: Modify the device configuration.
  **Request Body:**
  ```json
  {
    "sessionId": "YOUR_SESSION_ID",
    "datastore": "candidate",
    "config": "<config><system><hostname>new-name</hostname></system></config>",
    "defaultOperation": "merge"
  }
  ```

- **Other operations** (`/copy-config`, `/lock`, `/unlock`, etc.) follow a similar pattern.

## Project Structure

The project follows a standard Spring Boot layout:

```
src/
├── main/
│   ├── java/com/netconf/
│   │   ├── config/      # Spring configuration
│   │   ├── controller/  # REST and Web controllers
│   │   ├── dto/         # Data Transfer Objects
│   │   ├── exception/   # Custom exceptions and handlers
│   │   ├── model/       # Core domain models
│   │   ├── service/     # Business logic and services
│   │   └── utils/       # Utility classes
│   └── resources/
│       ├── static/      # CSS, JS, images
│       ├── templates/   # Thymeleaf templates
│       └── application.properties
└── test/
    └── java/com/netconf/ # Unit and integration tests
pom.xml                  # Maven project configuration
```
#
