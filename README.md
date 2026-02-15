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








