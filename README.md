# 🌳 ZenGarden Backend API

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet)](https://dotnet.microsoft.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Redis](https://img.shields.io/badge/Redis-Cache-DC382D?logo=redis&logoColor=white)](https://redis.io/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Swagger](https://img.shields.io/badge/API-Swagger-85EA2D?logo=swagger&logoColor=black)](https://zengarden-be.onrender.com/swagger/index.html)

> **ZenGarden** is a productivity-focused task management platform with gamification features. Built with **.NET 8.0** and **Clean Architecture**, it helps users increase productivity through an engaging tree-growing system, XP rewards, challenges, and real-time collaboration features.

**🔗 Live API:** [https://zengarden-be.onrender.com/swagger/index.html](https://zengarden-be.onrender.com/swagger/index.html)

---

## 💡 My Contributions

As the **Backend Developer** for this project, I was responsible for:

- **Architecture & Design**: Designed and implemented Clean Architecture with Repository & Unit of Work patterns, ensuring maintainable and scalable codebase
- **Database Design**: Created comprehensive ERD for 30+ entities including users, tasks, trees, XP system, wallet, challenges, and trading system
- **Authentication System**: Implemented JWT-based authentication with refresh tokens, password reset, and role-based authorization
- **RESTful APIs**: Developed 30+ API endpoints with OData support for flexible querying, filtering, and pagination
- **Real-time Features**: Integrated SignalR for real-time notifications and task updates across multiple hubs
- **Payment Integration**: Integrated Stripe payment gateway for secure transactions and purchase management
- **Performance Optimization**: Implemented Redis caching layer, database connection pooling, and async/await patterns throughout
- **Background Jobs**: Created scheduled background services for task automation, challenge expiration, and notification delivery
- **Third-party Integrations**: Integrated AWS S3 for file storage, OpenAI/DeepInfra for AI-powered focus suggestions, and Firebase for push notifications
- **Security & Validation**: Implemented rate limiting, input validation with FluentValidation, exception handling middleware, and data protection
- **DevOps**: Configured Docker containerization, deployment pipelines for Render.com and Azure, and health check endpoints

---

## 🛠️ Technology Stack

### Core
- **.NET 8.0** | **ASP.NET Core Web API** | **Entity Framework Core 8.0**
- **MySQL** (Pomelo) | **Redis** | **SignalR**

### Security & Auth
- **JWT** | **BCrypt** | **Rate Limiting** | **Data Protection**

### Services & Integrations
- **AWS S3** (File Storage) | **Stripe** (Payments) | **OpenAI/DeepInfra** (AI) | **Firebase** (Push Notifications)

### Tools & Libraries
- **FluentValidation** | **AutoMapper** | **OData** | **Swagger/OpenAPI** | **Hangfire** | **MailKit**

### DevOps
- **Docker** | **Docker Compose** | **Render.com** | **Azure**

---

## 🏗️ Architecture

Built with **Clean Architecture** principles:

```
ZenGarden/
├── ZenGarden.API/          # Presentation Layer (Controllers, Middleware, Validations)
├── ZenGarden.Core/         # Application Layer (Services, Interfaces, SignalR Hubs)
├── ZenGarden.Domain/       # Domain Layer (Entities, DTOs, Enums)
├── ZenGarden.Infrastructure/ # Infrastructure (Repositories, DbContext, Background Jobs)
└── ZenGarden.Shared/       # Shared Utilities
```

**Key Patterns:**
- Repository Pattern with Unit of Work
- Dependency Injection
- Middleware Pipeline
- Async/Await throughout

---

## ✨ Key Features

### 🔐 Authentication & Security
JWT authentication, refresh tokens, password reset, email verification, role-based access control

### 📝 Task Management
Full CRUD operations, status tracking, task types, reordering, XP rewards, real-time updates via SignalR

### 🎯 Challenge System
Create/manage challenges, user participation, status tracking, weekly task resets

### 🌲 Gamification
Tree ownership system, XP & level progression, tree trading between users

### 💰 Payment & Wallet
Stripe integration, wallet management, purchase history, transaction tracking

### 🎯 Focus Tracking
Session tracking, activity logging, AI-powered focus method suggestions

### 🔔 Real-time Notifications
SignalR hubs for notifications and task updates, email & push notifications

### 📊 Additional
OData query support, Redis caching, background jobs, health checks, performance monitoring

---

## 🚀 Quick Start

### Prerequisites
- .NET 8.0 SDK
- MySQL 8.0+
- Redis Server
- Docker (optional)

### Docker Compose (Recommended)

```bash
git clone <repository-url>
cd ZenGarden-BE

# Create .env file with your configurations
docker-compose up -d
```

API available at: `http://localhost:8080`

### Manual Setup

```bash
# Clone and navigate
git clone <repository-url>
cd ZenGarden-BE/ZenGarden/ZenGarden.API

# Configure appsettings.json with your database and Redis connections

# Run migrations
dotnet ef database update --project ../ZenGarden.Infrastructure

# Run application
dotnet run
```

---

## 📚 API Documentation

**🔗 Live Swagger UI:** [https://zengarden-be.onrender.com/swagger/index.html](https://zengarden-be.onrender.com/swagger/index.html)

### Main Endpoints

| Category | Endpoints |
|----------|-----------|
| **Auth** | `/api/Auth/register`, `/api/Auth/login`, `/api/Auth/refresh-token` |
| **Tasks** | `/api/Task` (CRUD), `/api/Task/complete` |
| **Challenges** | `/api/Challenges` (CRUD) |
| **Trees** | `/api/Trees`, `/api/UserTrees`, `/api/TradeTree` |
| **Payment** | `/api/Payment/create-checkout` |
| **SignalR** | `/hubs/notification`, `/hubs/task` |

Full API documentation available in Swagger UI.

---

## 🔧 Configuration

### Environment Variables
```env
DATABASE_URL=your-mysql-connection-string
DEEPINFRA_API_KEY=your-deepinfra-key
JWT_KEY=your-jwt-secret-key
AWS_ACCESS_KEY=your-aws-key
AWS_SECRET_KEY=your-aws-secret
STRIPE_SECRET_KEY=your-stripe-key
```

### Key Settings
- JWT settings (Issuer, Audience, Expiry)
- Redis configuration
- Email SMTP settings
- Rate limiting rules (10,000 req/min default)

---

## 📦 Background Jobs

Automated services running in the background:
- **OverdueTaskJob**: Marks overdue tasks
- **HandleExpiredChallengesJob**: Processes expired challenges
- **WeeklyTaskResetJob**: Resets weekly tasks
- **TaskNotifierService**: Sends task notifications

---

## 🔒 Security & Performance

### Security
- JWT Authentication & Authorization
- BCrypt password hashing
- Rate limiting (DDoS protection)
- CORS configuration
- FluentValidation input validation
- Exception handling middleware
- Data protection

### Performance
- Redis caching for frequently accessed data
- Database connection pooling
- Async/await patterns throughout
- OData query optimization
- Performance monitoring middleware

---

## 🚢 Deployment

- **Render.com**: Configured with `render.yaml`
- **Azure App Service**: Ready for deployment
- **Docker**: `docker build -t zengarden-api .`

---

## 📝 Project Structure

- **Clean Architecture**: Clear separation of concerns
- **Repository Pattern**: Data access abstraction
- **Unit of Work**: Transaction management
- **Dependency Injection**: Loose coupling
- **Middleware Pipeline**: Cross-cutting concerns

---

## 📄 License

[Add your license here]

---

**Note**: This is the backend API for ZenGarden. The frontend application is required for the complete user experience.
