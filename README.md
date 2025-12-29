# 🌳 ZenGarden Backend API

## 📋 Project Overview

ZenGarden is a task management and focus tracking application with gamification features, helping users increase productivity through a tree system, XP points, challenges, and various interactive features. This project is a Backend API built with .NET 8.0, implementing Clean Architecture and software development best practices.

## 🛠️ Technology Stack

### Core Framework
- **.NET 8.0** - Main framework
- **ASP.NET Core Web API** - RESTful API
- **Entity Framework Core 8.0** - ORM
- **MySQL (Pomelo.EntityFrameworkCore.MySql)** - Database
- **Redis** - Caching & Session Management

### Authentication & Security
- **JWT (JSON Web Token)** - Authentication & Authorization
- **BCrypt.Net** - Password Hashing
- **ASP.NET Core Rate Limiting** - API Rate Limiting
- **Data Protection** - Sensitive data protection

### Real-time & Communication
- **SignalR** - Real-time notifications and updates
- **Email Service (MailKit)** - Email verification and notifications

### Third-party Services
- **AWS S3** - File Storage
- **Stripe** - Payment Gateway
- **OpenAI/DeepInfra** - AI Integration for Focus Methods
- **Firebase Admin** - Push Notifications

### Validation & Mapping
- **FluentValidation** - Input Validation
- **AutoMapper** - Object Mapping

### API Features
- **OData** - Query support (Filter, OrderBy, Select, Expand)
- **Swagger/OpenAPI** - API Documentation
- **Health Checks** - System monitoring

### Background Jobs
- **Hangfire** - Background job processing
- **Hosted Services** - Scheduled tasks

### DevOps & Deployment
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Render/Azure** - Cloud deployment

## 🏗️ System Architecture

The project is organized following **Clean Architecture** with the following layers:

```
ZenGarden/
├── ZenGarden.API/          # Presentation Layer
│   ├── Controllers/        # API Controllers
│   ├── Middleware/         # Custom Middleware
│   ├── Filters/            # Action Filters
│   └── Validations/        # FluentValidation Validators
│
├── ZenGarden.Core/         # Application Layer
│   ├── Services/           # Business Logic
│   ├── Interfaces/         # Contracts (IServices, IRepositories)
│   ├── Hubs/               # SignalR Hubs
│   └── Mappings/           # AutoMapper Profiles
│
├── ZenGarden.Domain/       # Domain Layer
│   ├── Entities/           # Domain Models
│   ├── DTOs/               # Data Transfer Objects
│   ├── Enums/              # Enumerations
│   └── Config/             # Configuration Classes
│
├── ZenGarden.Infrastructure/ # Infrastructure Layer
│   ├── Repositories/       # Data Access Implementation
│   ├── Persistence/        # DbContext
│   ├── BackgroundJobs/     # Background Services
│   └── Migrations/         # EF Core Migrations
│
└── ZenGarden.Shared/       # Shared Layer
    ├── Helpers/            # Utility Helpers
    └── Utils/              # Common Utilities
```

## ✨ Key Features

### 🔐 Authentication & Authorization
- User registration/Login with JWT
- Refresh Token mechanism
- Forgot password & Reset password
- Email verification
- Role-based access control

### 📝 Task Management
- CRUD operations for tasks
- Task status tracking (Pending, In Progress, Completed, Overdue)
- Task types & categorization
- Task reordering
- Task completion with XP rewards
- Real-time task updates via SignalR

### 🎯 Challenge System
- Create and manage challenges
- Challenge tasks
- User challenge participation
- Challenge status tracking
- Weekly task reset

### 🌲 Gamification System
- **Tree System**: Users own and care for trees
- **XP System**: Experience points system for users and trees
- **Level Progression**: Level up based on XP
- **Tree Trading**: Trade trees between users

### 💰 Wallet & Payment
- Wallet management
- Stripe payment integration
- Purchase history
- Transaction tracking
- Package purchases

### 🎒 Inventory System
- Bag & Bag Items management
- Item details & types
- Use items functionality
- Item status tracking

### 🎯 Focus Tracking
- Focus session tracking
- Focus activity logging
- AI-powered focus method suggestions (OpenAI/DeepInfra)
- Focus statistics

### 🔔 Notification System
- Real-time notifications via SignalR
- Email notifications
- Push notifications (Firebase)
- Notification history

### 📊 Additional Features
- User experience tracking
- User configurations
- Trade history
- OData query support
- Redis caching
- Background job processing
- Health checks
- Performance monitoring middleware
- Exception handling middleware
- Request logging middleware

## 🚀 Installation & Setup

### System Requirements
- .NET 8.0 SDK
- MySQL 8.0+
- Redis Server
- Docker & Docker Compose (optional)

### Installation with Docker Compose

1. **Clone repository**
```bash
git clone <repository-url>
cd ZenGarden-BE
```

2. **Create `.env` file**
```env
DATABASE_URL=Server=localhost;Port=3306;Database=ZenGardenDB;Uid=root;Pwd=12345678
REDIS_HOST=localhost
REDIS_PORT=6379
JWT_KEY=your-secret-key-here
DEEPINFRA_API_KEY=your-deepinfra-api-key
AWS_ACCESS_KEY=your-aws-access-key
AWS_SECRET_KEY=your-aws-secret-key
STRIPE_SECRET_KEY=your-stripe-secret-key
```

3. **Run with Docker Compose**
```bash
docker-compose up -d
```

API will be available at: `http://localhost:8080`

### Manual Installation

1. **Clone repository**
```bash
git clone <repository-url>
cd ZenGarden-BE
```

2. **Configure database**
- Create MySQL database
- Update connection string in `appsettings.json`

3. **Configure Redis**
- Install and run Redis server
- Update Redis connection in `appsettings.json`

4. **Run migrations**
```bash
cd ZenGarden/ZenGarden.API
dotnet ef database update --project ../ZenGarden.Infrastructure
```

5. **Run application**
```bash
dotnet run
```

API will be available at: `https://localhost:7262` or `http://localhost:5153`

## 📚 API Documentation

After running the application, access Swagger UI at:
- Development: `https://localhost:7262/swagger`
- Production: `https://your-domain.com/swagger`

### Main API Endpoints

#### Authentication
- `POST /api/Auth/register` - User registration
- `POST /api/Auth/login` - User login
- `POST /api/Auth/refresh-token` - Refresh JWT token
- `POST /api/Auth/forgot-password` - Forgot password
- `POST /api/Auth/reset-password` - Reset password

#### Tasks
- `GET /api/Task` - Get all tasks
- `POST /api/Task` - Create new task
- `PUT /api/Task/{id}` - Update task
- `DELETE /api/Task/{id}` - Delete task
- `POST /api/Task/complete` - Complete task

#### Challenges
- `GET /api/Challenges` - Get all challenges
- `POST /api/Challenges` - Create new challenge
- `PUT /api/Challenges/{id}` - Update challenge

#### Trees & Gamification
- `GET /api/Trees` - Get all trees
- `GET /api/UserTrees` - Get user's trees
- `POST /api/TradeTree` - Trade tree

#### Payment
- `POST /api/Payment/create-checkout` - Create Stripe checkout session
- `GET /api/Payment/success` - Payment success callback

#### SignalR Hubs
- `/hubs/notification` - Notification hub
- `/hubs/task` - Task real-time updates hub

## 🔧 Configuration

### Environment Variables
- `DATABASE_URL` - MySQL connection string
- `DEEPINFRA_API_KEY` - DeepInfra API key for AI features
- `JWT_KEY` - Secret key for JWT
- `AWS_ACCESS_KEY`, `AWS_SECRET_KEY` - AWS credentials
- `STRIPE_SECRET_KEY` - Stripe secret key

### AppSettings
Important configurations in `appsettings.json`:
- JWT settings (Issuer, Audience, Expiry)
- Redis configuration
- Email SMTP settings
- Rate limiting rules
- Performance thresholds

## 🧪 Testing

### Health Checks
Check system health:
```bash
GET /health
```

### Rate Limiting
API is protected by rate limiting:
- Default: 10,000 requests/minute per IP

## 📦 Background Jobs

Automated background jobs:
- **OverdueTaskJob**: Mark overdue tasks
- **HandleExpiredChallengesJob**: Handle expired challenges
- **WeeklyTaskResetJob**: Reset weekly tasks
- **TaskNotifierService**: Send task notifications

## 🔒 Security Features

- JWT Authentication & Authorization
- Password hashing with BCrypt
- Rate limiting for DDoS protection
- CORS configuration
- Input validation with FluentValidation
- Exception handling middleware
- Data protection

## 📈 Performance Optimizations

- Redis caching for frequently accessed data
- Database connection pooling
- Async/await patterns
- OData query optimization
- Background job processing
- Performance monitoring middleware

## 🚢 Deployment

### Render.com
The project is configured to deploy on Render.com with `render.yaml` file.

### Azure
Can be deployed to Azure App Service with similar configurations.

### Docker
```bash
docker build -t zengarden-api .
docker run -p 8080:8080 zengarden-api
```

## 👨‍💻 Developer Notes

### Code Structure
- **Clean Architecture**: Clear separation of layers
- **Repository Pattern**: Data access abstraction
- **Unit of Work**: Transaction management
- **Dependency Injection**: Loose coupling
- **Middleware Pipeline**: Request/Response processing

### Best Practices
- Async/await for I/O operations
- FluentValidation for input validation
- AutoMapper for object mapping
- Custom middleware for cross-cutting concerns
- Health checks for monitoring
- Structured logging

## 📝 License

[Add your license here]

## 👥 Contributors

[Add contributor information]

---

**Note**: This is the backend project for ZenGarden application. For a complete experience, it needs to be combined with the frontend application.
