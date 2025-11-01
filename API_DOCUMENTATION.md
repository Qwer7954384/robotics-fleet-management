# Robotics Fleet Management - API Documentation

This directory contains comprehensive API specifications for the Robotics Fleet Management System.

## 📋 Available Specifications

### 1. OpenAPI 3.1 Specification (`openapi.yaml`)
- **Size**: 50 KB
- **Endpoints**: 20+ REST API endpoints
- **Examples**: 40+ detailed request/response examples
- **Coverage**: Complete REST API documentation including robots, tasks, path planning, fleet health, and charging stations

### 2. AsyncAPI 3.0 Specification (`asyncapi.yaml`)
- **Size**: 37 KB
- **Channels**: 9 Kafka event topics
- **Events**: 11 domain events with detailed examples
- **Coverage**: Complete event-driven architecture documentation

---

## 🚀 Using the Specifications

### Viewing the OpenAPI Specification

#### Option 1: Swagger UI (Online)
1. Go to [Swagger Editor](https://editor.swagger.io/)
2. File → Import File → Select `openapi.yaml`
3. View interactive documentation and try out endpoints

#### Option 2: Swagger UI (Local with Docker)
```bash
docker run -p 8080:8080 \
  -e SWAGGER_JSON=/openapi.yaml \
  -v $(pwd)/openapi.yaml:/openapi.yaml \
  swaggerapi/swagger-ui
```
Then open: http://localhost:8080

#### Option 3: ReDoc (Better for reading)
```bash
docker run -p 8080:80 \
  -e SPEC_URL=openapi.yaml \
  -v $(pwd)/openapi.yaml:/usr/share/nginx/html/openapi.yaml \
  redocly/redoc
```
Then open: http://localhost:8080

#### Option 4: Stoplight Elements
```bash
npx @stoplight/elements-dev-portal openapi.yaml
```

#### Option 5: Validate the specification
```bash
# Using Docker
docker run --rm -v $(pwd):/spec redocly/cli lint /spec/openapi.yaml

# Or install the CLI
npm install -g @redocly/cli
redocly lint openapi.yaml
```

### Viewing the AsyncAPI Specification

#### Option 1: AsyncAPI Studio (Online)
1. Go to [AsyncAPI Studio](https://studio.asyncapi.com/)
2. Import `asyncapi.yaml`
3. View interactive event documentation

#### Option 2: AsyncAPI Generator (Generate HTML docs)
```bash
# Install AsyncAPI CLI
npm install -g @asyncapi/cli

# Generate HTML documentation
asyncapi generate fromTemplate asyncapi.yaml @asyncapi/html-template -o ./docs/asyncapi

# Open the generated docs
open ./docs/asyncapi/index.html
```

#### Option 3: Generate Markdown documentation
```bash
asyncapi generate fromTemplate asyncapi.yaml @asyncapi/markdown-template -o ./docs/asyncapi-md
```

#### Option 4: Validate the specification
```bash
asyncapi validate asyncapi.yaml
```

---

## 📦 Generating Code from Specifications

### Generate Java Spring Boot Server (from OpenAPI)
```bash
# Using OpenAPI Generator
docker run --rm -v $(pwd):/local openapitools/openapi-generator-cli generate \
  -i /local/openapi.yaml \
  -g spring \
  -o /local/generated/spring-server \
  --additional-properties=useSpringBoot3=true,java8=false,interfaceOnly=true
```

### Generate TypeScript Client (from OpenAPI)
```bash
docker run --rm -v $(pwd):/local openapitools/openapi-generator-cli generate \
  -i /local/openapi.yaml \
  -g typescript-axios \
  -o /local/generated/typescript-client
```

### Generate Python Client (from OpenAPI)
```bash
docker run --rm -v $(pwd):/local openapitools/openapi-generator-cli generate \
  -i /local/openapi.yaml \
  -g python \
  -o /local/generated/python-client
```

### Generate Kafka Java Code (from AsyncAPI)
```bash
# Generate Spring Cloud Stream bindings
asyncapi generate fromTemplate asyncapi.yaml @asyncapi/java-spring-cloud-stream-template \
  -o ./generated/kafka-bindings \
  -p javaPackage=com.paklog.robotics.events
```

---

## 🧪 Testing the API

### Using the OpenAPI Spec with Postman
1. Open Postman
2. Import → Link/File → Select `openapi.yaml`
3. Postman will create a collection with all endpoints and examples

### Using the OpenAPI Spec with Insomnia
1. Open Insomnia
2. Import/Export → Import Data → From File → Select `openapi.yaml`
3. All endpoints will be imported with examples

### Generate Mock Server
```bash
# Using Prism (Mock Server)
npm install -g @stoplight/prism-cli

# Start mock server on port 4010
prism mock openapi.yaml

# Test it
curl http://localhost:4010/api/v1/robots
```

---

## 📊 API Overview

### REST API Endpoints (OpenAPI)

#### Robots
- `POST /api/v1/robots` - Register a new robot
- `GET /api/v1/robots` - List all robots (with filtering)
- `GET /api/v1/robots/{robotId}` - Get robot details
- `DELETE /api/v1/robots/{robotId}` - Decommission a robot
- `PUT /api/v1/robots/{robotId}/assign-task` - Assign task to robot
- `PUT /api/v1/robots/{robotId}/battery` - Update battery level
- `PUT /api/v1/robots/{robotId}/position` - Update robot position

#### Tasks
- `POST /api/v1/tasks` - Create a new task
- `GET /api/v1/tasks` - List all tasks (with filtering)
- `GET /api/v1/tasks/{taskId}` - Get task details

#### Path Planning
- `POST /api/v1/paths/calculate` - Calculate optimal path
- `POST /api/v1/paths/validate` - Validate path safety

#### Fleet
- `GET /api/v1/fleet/health` - Get fleet health metrics

#### Charging Stations
- `POST /api/v1/charging-stations` - Register charging station
- `GET /api/v1/charging-stations/{stationId}` - Get station details

#### Monitoring
- `GET /actuator/health` - Health check
- `GET /actuator/metrics` - Prometheus metrics

### Event Topics (AsyncAPI)

#### Robot Events
- `robot.registered` - Robot registration events
- `robot.task.assigned` - Task assignment events
- `robot.task.started` - Task start events
- `robot.task.completed` - Task completion events
- `robot.task.failed` - Task failure events
- `robot.maintenance.required` - Maintenance requirement events

#### Battery & Charging Events
- `robot.battery.low` - Low battery alerts
- `robot.charging.started` - Charging session start
- `robot.charging.completed` - Charging completion

#### Fleet Events
- `fleet.rebalanced` - Fleet workload rebalancing

---

## 🔍 Key Features

### OpenAPI Specification Highlights
✅ **40+ Detailed Examples** - Every endpoint has multiple realistic examples
✅ **Complete Error Handling** - All error responses documented with examples
✅ **Business Rules Documentation** - Constraints and validation rules clearly defined
✅ **Pagination Support** - All list endpoints support pagination
✅ **Filtering & Sorting** - Query parameters for flexible data retrieval
✅ **Security Schemes** - JWT and API Key authentication (ready for implementation)
✅ **CloudEvents Integration** - Event headers follow CloudEvents standard

### AsyncAPI Specification Highlights
✅ **CloudEvents v1.0 Compliant** - All events follow CloudEvents standard
✅ **Correlation & Causation IDs** - Full distributed tracing support
✅ **Event Versioning** - Aggregate versioning for optimistic locking
✅ **Multiple Environments** - Local, dev, staging, production configurations
✅ **Consumer Group Documentation** - All consumer groups and their purposes
✅ **Event Examples** - Every event has realistic payload examples

---

## 🏗️ Architecture Patterns

### REST API (Synchronous)
```
Client → REST API → Domain Layer → Repository → MongoDB
                 ↓
                Events → Kafka
```

### Event-Driven (Asynchronous)
```
Domain Event → Kafka Topic → Multiple Consumers
                           ↓
                   - Analytics Service
                   - Monitoring Service
                   - Alert Service
                   - Audit Service
```

### Event Flow Example
```
1. POST /api/v1/robots (REST)
   ↓
2. Robot.register() (Domain)
   ↓
3. RobotRegisteredEvent (Event)
   ↓
4. Kafka Topic: robot.registered
   ↓
5. Multiple Consumers Process Event
```

---

## 📚 Data Models

### Robot
- **ID**: Unique identifier (e.g., ROBOT-001)
- **Status**: IDLE, BUSY, CHARGING, MAINTENANCE, OFFLINE
- **Capabilities**: PICKER, TRANSPORTER, SORTER, LIFTER, SCANNER, COLLABORATIVE
- **Battery**: 0-100% with health status
- **Position**: X, Y coordinates and heading (0-360°)

### Task
- **Type**: PICK, TRANSPORT, SORT, DELIVER, CHARGE, MAINTENANCE
- **Priority**: LOW, MEDIUM, HIGH, CRITICAL
- **Status**: PENDING, ASSIGNED, IN_PROGRESS, COMPLETED, FAILED, CANCELLED

### Fleet
- **Utilization Target**: 85%
- **Rebalancing Threshold**: >20% imbalance
- **Metrics**: Total robots, idle robots, active tasks, healthy robots

---

## 🔐 Security

### Authentication (To Be Implemented)
The OpenAPI specification includes security schemes for:
- **Bearer Token (JWT)**: For REST API authentication
- **API Key**: For service-to-service communication
- **SASL/SCRAM**: For Kafka authentication (AsyncAPI)

### Implementation Checklist
- [ ] Implement JWT token validation
- [ ] Configure API key authentication
- [ ] Set up Kafka SASL/SCRAM
- [ ] Add rate limiting
- [ ] Implement audit logging
- [ ] Enable CORS configuration

---

## 🧰 Development Tools

### Recommended Tools
- **API Testing**: Postman, Insomnia, HTTPie
- **Mock Server**: Prism, WireMock
- **Code Generation**: OpenAPI Generator, AsyncAPI Generator
- **Documentation**: Swagger UI, ReDoc, AsyncAPI Studio
- **Validation**: Redocly CLI, AsyncAPI CLI

### VS Code Extensions
- **OpenAPI (Swagger) Editor** - 42Crunch
- **AsyncAPI Preview** - AsyncAPI
- **REST Client** - For testing endpoints

---

## 📈 Monitoring & Observability

### Prometheus Metrics (Available via `/actuator/metrics`)
- Robot count by status
- Task count by status and priority
- Fleet utilization rate
- Battery levels distribution
- Task completion rates
- Task failure rates
- Average task duration
- Charging session metrics

### Health Checks (Available via `/actuator/health`)
- MongoDB connection
- Redis connection
- Kafka connection
- Fleet health status

---

## 🤝 Contributing

When making changes to the API:
1. Update the OpenAPI specification for REST endpoints
2. Update the AsyncAPI specification for events
3. Regenerate documentation
4. Validate specifications
5. Update this README if needed

### Validation Commands
```bash
# Validate OpenAPI
redocly lint openapi.yaml

# Validate AsyncAPI
asyncapi validate asyncapi.yaml

# Check for breaking changes
redocly diff openapi-old.yaml openapi.yaml
```

---

## 📞 Support

For questions or issues:
- Email: robotics@paklog.com
- Documentation: See inline specification documentation
- Examples: Check the `examples` section in each endpoint/event

---

## 📄 License

Apache 2.0 - See LICENSE file for details

---

**Generated**: 2025-11-01
**OpenAPI Version**: 3.1.0
**AsyncAPI Version**: 3.0.0
**API Version**: 1.0.0
