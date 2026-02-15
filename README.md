# Fitness Recommendation Microservices Application

A comprehensive full-stack microservices-based fitness tracking application with AI-powered recommendations, built with Spring Boot, React, and integrated with Google Gemini API.

## 🏗️ Architecture Overview

This project implements a **microservices architecture** with the following components:

### Backend Services (Java Spring Boot 3.4.3)
1. **Eureka Server** - Service Registry & Discovery
2. **Config Server** - Centralized Configuration Management
3. **API Gateway** - Request routing and authentication
4. **User Service** - User management and authentication
5. **Activity Service** - Activity tracking and logging
6. **AI Service** - AI-powered fitness recommendations using Google Gemini

### Frontend
- **React 19** with Vite for modern, fast development
- Material-UI (MUI) for component design
- Redux Toolkit for state management
- OAuth2 authentication with PKCE flow

---

## 📋 Detailed Functionality

### 1. **Eureka Service Discovery**
- **Purpose**: Service registration and discovery for microservices
- **Features**: Automatic service registration, health checks, dynamic routing, load balancing

### 2. **Config Server** (Java 17 LTS)
- **Purpose**: Centralized configuration management
- **Key Files**: activity-service.yml, ai-service.yml, api-gateway.yml, user-service.yml

### 3. **User Service** (Port 8082, PostgreSQL, Java 23)
- **Endpoints**: Registration, profile fetch, user validation
- **Features**: User authentication, RBAC, password hashing, profile management

### 4. **Activity Service** (Port 8081, MongoDB, Java 23)
- **Endpoints**: Track activities, retrieve user activities, get activity details
- **Features**: Real-time tracking, RabbitMQ integration, WebFlux for reactive processing

### 5. **AI Service** (Port 8083, MongoDB, Java 23)
- **External API**: Google Gemini API
- **Features**: AI recommendations, async message processing, WebClient for HTTP calls

### 6. **API Gateway** (Port 8080, Java 23)
- **Features**: Request routing, OAuth2 authentication, user validation, CORS

### 7. **Frontend** (React 19 + Vite)
- **Components**: ActivityForm, ActivityList, ActivityDetail
- **State Management**: Redux Toolkit with authSlice
- **Authentication**: OAuth2 with PKCE flow

---

## 🛠️ Tech Stack

**Backend**: Java 23, Spring Boot 3.4.3, Spring Cloud 2024.0.0, PostgreSQL, MongoDB, RabbitMQ, Netflix Eureka

**Frontend**: React 19, Vite, Redux Toolkit, Material-UI, Axios, OAuth2

**Infrastructure**: Maven, Java 21 LTS (recommended), Git

---

## 📊 Inter-Service Communication

**Synchronous**: Frontend → API Gateway → (User/Activity/AI Services)

**Asynchronous**: Activity Service → RabbitMQ → AI Service → MongoDB

**Discovery**: All services → Eureka Server

**Configuration**: All services → Config Server

---

## 🚀 Key Features

- **Microservices Architecture** with independent scaling
- **Service Discovery** via Netflix Eureka
- **Centralized Configuration** with Spring Cloud Config
- **AI Integration** with Google Gemini for recommendations
- **OAuth2 Security** with PKCE flow
- **Message Queue** for async processing (RabbitMQ)
- **Reactive Programming** with WebFlux
- **Polyglot Persistence** (PostgreSQL + MongoDB)

---

## 🔄 API Endpoints

| Service | Method | Endpoint | Purpose |
|---------|--------|----------|---------|
| User | POST | `/api/users/register` | Register user |
| User | GET | `/api/users/{userId}` | Get profile |
| User | GET | `/api/users/{userId}/validate` | Validate user |
| Activity | POST | `/api/activities` | Track activity |
| Activity | GET | `/api/activities` | Get user activities |
| Activity | GET | `/api/activities/{activityId}` | Get activity |
| AI | GET | `/api/recommendations/{userId}` | Get recommendations |
| AI | POST | `/api/recommendations` | Generate recommendations |

---

## 🎓 Design Patterns

Microservices Pattern, Service Registry Pattern, API Gateway Pattern, Message Queue Pattern, Repository Pattern, Dependency Injection, DTO Pattern, Factory Pattern, Observer Pattern, Strategy Pattern

---

## 💼 Resume Bullet Points

### Senior-Level
- **Designed and implemented a production-grade microservices architecture** with Netflix Eureka service discovery, Spring Cloud Config server, and API Gateway
- **Engineered inter-service communication** using REST APIs and RabbitMQ for eventual consistency
- **Integrated Google Gemini AI API** for intelligent, context-aware fitness recommendations
- **Implemented OAuth2 security** with PKCE flow across full-stack application
- **Optimized performance** using Spring WebFlux for non-blocking I/O
- **Managed polyglot persistence** with MongoDB and PostgreSQL for different access patterns
- **Built scalable infrastructure** supporting independent scaling through Eureka

### Mid-Level
- **Developed 6 microservices** using Spring Boot 3.4.3 and Java 23 with clean layered architecture
- **Created RESTful APIs** with proper HTTP methods, validation, and error handling
- **Implemented asynchronous event processing** using RabbitMQ for service decoupling
- **Built React 19 frontend** with Redux Toolkit and Material-UI components
- **Configured centralized configuration management** for zero-downtime config updates
- **Integrated service discovery** for dynamic routing and automatic failover
- **Applied design patterns** (Repository, DTO, Dependency Injection, Async Message)

### Junior-Level
- **Contributed to microservices development** with REST endpoint implementations
- **Developed React components** for activity tracking and management
- **Implemented database operations** using Spring Data JPA and MongoDB
- **Worked with Spring Cloud infrastructure** (Eureka, Config Server, Gateway)
- **Participated in API design** following REST conventions
- **Integrated external APIs** with WebClient for async HTTP calls
- **Collaborated on OAuth2 implementation** across frontend and backend

---

## 👨‍💻 Interview Q&A

### Architecture Questions

**Q: Why microservices instead of monolith?**
A: Independent scalability, technology flexibility per service, easier maintenance, fault isolation. Activity Service scales separately during peak hours without affecting User Service.

**Q: How does service discovery work?**
A: Netflix Eureka acts as registry. Each microservice registers on startup. API Gateway queries Eureka for service instances and routes requests accordingly. Enables dynamic scaling without hardcoded URLs.

**Q: What happens if a microservice fails?**
A: Eureka detects failures via health checks. Gateway stops routing to unhealthy instances. RabbitMQ persists messages if AI Service is down. Fallback mechanisms handle critical operations.

**Q: How is data consistency maintained?**
A: Eventual consistency model with async messaging. Activities tracked immediately, then published to RabbitMQ. AI Service processes asynchronously. User validation is synchronous via gateway.

**Q: Activity tracking flow?**
A: 1. Frontend → API Gateway, 2. Gateway validates user with User Service, 3. Routes to Activity Service, 4. Activity Service saves to MongoDB and publishes to RabbitMQ, 5. AI Service consumes and calls Gemini API, 6. Recommendations stored in MongoDB.

### Technical Implementation

**Q: How did you implement OAuth2?**
A: React frontend uses react-oauth2-code-pkce for PKCE flow. Tokens stored in Redux. API Gateway validates with Spring Security OAuth2 Resource Server. User info extracted from token claims.

**Q: Config Server importance?**
A: Centralized configuration management. Services don't need redeploy when URLs, API keys change. Environment-based profiles (dev, prod). Services poll Config Server on startup.

**Q: RabbitMQ benefits?**
A: Service decoupling, reliability (persistent messages), scalability (concurrent processing), async processing (non-blocking), load leveling (absorbs spikes).

**Q: X-User-ID header usage?**
A: Client includes in every request. Gateway extracts and passes to services. Activity Service uses it to associate activities. Prevents cross-user access (security).

**Q: WebFlux/Reactive Programming?**
A: Non-blocking I/O with Mono/Flux. WebClient for async HTTP. Handles thousands of concurrent requests with fewer threads. GeminiService uses WebClient instead of RestTemplate.

### Frontend Questions

**Q: State management approach?**
A: Redux Toolkit with authSlice. Stores tokens and user data. useDispatch updates state. useSelector accesses in components. Persists auth across refreshes. Axios interceptor adds tokens to requests.

**Q: Authentication flow in React?**
A: User clicks LOGIN → OAuth redirect → grant permissions → code exchange for tokens → stored in Redux/localStorage → Axios interceptor adds to requests → protected routes check token.

**Q: Component interaction?**
A: ActivityForm creates activities (POST). ActivityList fetches all (GET). ActivityDetail shows selected activity. Form submission reloads page. Each calls API service layer.

### Database Questions

**Q: MongoDB vs PostgreSQL?**
A: MongoDB for activities (flexible schema, easy scaling). PostgreSQL for users (relational, ACID, strong consistency needed). Optimizes each for access patterns.

**Q: Data partitioning?**
A: Activity Service owns activity data. User Service owns user data. AI Service owns recommendations. No direct DB access between services. Services evolve independently.

### Performance & Scalability

**Q: Scale to millions of users?**
A: Horizontal scaling with load balancer. DB scaling (PostgreSQL replicas, MongoDB sharding). Caching with Redis. RabbitMQ decoupling. CDN for frontend. Database indexing (userId, timestamps).

**Q: Monitoring strategy?**
A: Spring Boot Actuator (/health). ELK Stack for logging. Prometheus/Grafana metrics. Distributed tracing (Sleuth/Zipkin). Alert thresholds for latency, errors. RabbitMQ queue depth.

### Testing & Security

**Q: Test activity tracking?**
A: Unit tests (service logic). Integration tests (Controller→Service→DB). Mock external services. Mock WebClient. End-to-end tests (REST→DB).

**Q: Security considerations?**
A: OAuth2 PKCE (mobile security). User validation on gateway. Password hashing (bcrypt). Rate limiting. Input validation (@Valid). CORS config. Sensitive data in Config Server, not code.

**Q: Inter-service authentication?**
A: Currently internal trust model. For production: OAuth2 client credentials. mTLS for encryption. Gateway validates tokens. API keys from Config Server.

### Problem-Solving

**Q: Debug missing recommendations?**
A: Check if activity saved (query MongoDB). Verify RabbitMQ message. Check AI Service running. Check Gemini API errors in logs. Query recommendation collection. Test network connectivity. Verify Config Server has API key.

**Q: Migrate Java 23 to 21?**
A: Update java.version in pom.xml. Test with Java 21. Check deprecated features. Update Docker images. Run integration tests. Gradual rollout. Monitor performance.

### System Design

**Q: Real-time notifications?**
A: Replace HTTP polling with WebSocket. Spring WebSocket + SockJS fallback. AI Service publishes to WebSocket channel on recommendation. Frontend subscribes. Instant notifications.

**Q: Add social features?**
A: Create Social Service for following. Activity Service publishes "activity shared" events. Social Service listens and broadcasts via WebSocket. Add feed service for aggregation. Cache with Redis.

---

## 🎖️ Project Complexity

✅ 7 independent microservices  
✅ Multiple tech stack (Java, React, SQL, NoSQL, Message Queue)  
✅ Third-party API integration (Google Gemini)  
✅ Distributed system patterns  
✅ OAuth2 security implementation  
✅ Full-stack implementation  
✅ Production-ready patterns  

---

## 📝 Build & Deployment

**Maven Build**: `mvn clean package`

**Startup Order**:
1. Eureka Server
2. Config Server
3. User Service (PostgreSQL)
4. Activity Service (MongoDB)
5. AI Service (MongoDB, RabbitMQ)
6. API Gateway
7. Frontend (React)

---

## License

Part of comprehensive Java and Spring Boot course from EmbarkX.

