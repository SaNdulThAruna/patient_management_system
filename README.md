# 🏥 Patient Management System – Microservices Architecture

A production-ready distributed healthcare backend system built using **Java 21** and **Spring Boot**, following modern microservices architecture principles.

This system demonstrates:

- Domain-driven microservices separation
- Secure JWT-based authentication
- Event-driven architecture using Kafka
- High-performance inter-service communication with gRPC
- Redis caching for performance optimization
- Docker-based containerization
- Infrastructure as Code using AWS CDK

---

## 🚀 Architecture Overview

The system follows a **microservices architecture** with clear domain
boundaries, asynchronous event-driven communication, and independent
data stores per service.

### 🏗 High-Level Architecture

                    ┌─────────────┐
                    │   Client    │
                    │ (Web/Mobile)│
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   API Layer │
                    │ (REST Entry)│
                    └──────┬──────┘
                           │
     ┌─────────────┬──────────────┬───────────────┬──────────────┐
     │ Patient MS  │  Auth MS     │  Billing MS   │ Analytics MS │
     └─────┬───────┴───────┬──────┴───────┬───────┴───────┬──────┘
           │               │              │               │
       PostgreSQL       PostgreSQL     PostgreSQL        Kafka
           │                               │               │
           └────────────── Kafka Event Streaming ───────────┘
                              │
                            Redis

------------------------------------------------------------------------

### 🔎 Architectural Characteristics

-   **Database Per Service Pattern**\
    Each microservice owns its own PostgreSQL database.

-   **Event-Driven Communication (Kafka)**\
    Services publish and consume domain events asynchronously.

-   **Synchronous Communication (gRPC)**\
    Used for high-performance inter-service calls.

-   **Stateless Authentication (JWT)**\
    Auth service issues secure tokens validated by other services.

-   **Distributed Caching (Redis)**\
    Reduces database load and improves response times.

------------------------------------------------------------------------

### 🔁 Example Request Flow

1.  Client sends request to API layer.\
2.  API forwards request to appropriate microservice.\
3.  Patient Service stores data in PostgreSQL.\
4.  Patient Service publishes event to Kafka.\
5.  Billing and Analytics services consume event.\
6.  Frequently accessed data is cached in Redis.

------------------------------------------------------------------------

### 🎯 Design Goals

-   High scalability\
-   Loose coupling between services\
-   Fault isolation\
-   Independent deployments\
-   Cloud-native readiness

---

## 🧩 Microservices

### 1️⃣ Patient Service
- Manages patient records  
- CRUD operations  
- Publishes events when patient data changes  
- Uses PostgreSQL  

---

### 2️⃣ Auth Service
- User registration & login  
- JWT-based authentication & authorization  
- Secure password hashing (BCrypt)  
- Role-based access control  

---

### 3️⃣ Billing Service
- Invoice generation  
- Payment tracking  
- Consumes patient-related Kafka events  

---

### 4️⃣ Analytics Service
- Event-driven analytics processing  
- Real-time data aggregation  
- Uses Kafka consumers for async processing  

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Java 21 |
| Framework | Spring Boot |
| Messaging | Apache Kafka |
| Caching | Redis |
| Inter-Service | gRPC |
| Database | PostgreSQL |
| Containerization | Docker |
| Infrastructure | AWS CDK |
| Security | JWT |

---

## 🔐 Security Implementation

- Stateless authentication using JWT  
- Spring Security integration  
- Role-based endpoint protection  
- Secure token validation across services  
- Password hashing using BCrypt  

---

## ⚡ Event-Driven Architecture

- Kafka producers publish domain events  
- Kafka consumers process async workflows  
- Decoupled services via event streams  
- Supports scalability and fault tolerance  

### Example Events
- `PatientCreatedEvent`
- `InvoiceGeneratedEvent`
- `PaymentCompletedEvent`

---

## 📦 gRPC Communication

Used for:

- Low-latency inter-service communication  
- Strongly-typed contract-based communication  
- High performance compared to REST for internal calls  

---

## 🧠 Caching Strategy

Redis is used for:

- Frequently accessed patient data  
- Authentication session validation  
- Reducing DB load  
- Improving response time  
