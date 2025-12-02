🚀 Transaction Notification Microservice System

A lightweight microservices-based system where a user performs a transaction, and the system sends a notification using Kafka messaging.
This project demonstrates real-world backend concepts such as authentication, microservices communication, event-driven architecture, and multi-database integration.

🎯 Goal
Build a system where:
A client creates a transaction.
The Transaction Service stores it in SQL Server and publishes an event to Kafka.
The Notification Service listens to the event and writes notification logs into MongoDB.

🧩 Architecture Overview
1. Auth Service
Provides login API
Returns JWT token
Used by Transaction Service for authorization
2. Transaction Service
Validates incoming JWT
API to create a transaction
Saves transaction in SQL Server
Publishes "transaction_created" event to Kafka
3. Notification Service
Kafka consumer
Listens to "transaction_created" events
Stores notification logs into MongoDB

📦 Tech Stack

Spring Boot (multiple microservices)
Spring Security + JWT
Spring Data JPA (SQL Server)
Spring Data MongoDB
Apache Kafka (Producer + Consumer)
Docker (optional for running Kafka, SQL Server, MongoDB)
Postman for testing APIs

📑 Functional Flow
Step 1 — User Login
POST /auth/login
User receives a JWT token
Example: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9…
Step 2 — User Creates a Transaction
Endpoint: POST /transaction/create
Request Body:
{
  "amount": 500,
  "userId": 101
}
System Actions:
Transaction stored in SQL Server
Kafka event published:
{
  "transactionId": "tx_202501",
  "amount": 500,
  "userId": 101,
  "status": "CREATED"
}
Step 3 — Notification Service Reacts
Kafka consumer receives the event and writes to MongoDB:

{
  "transactionId": "tx_202501",
  "message": "Transaction created successfully",
  "timestamp": "2025-12-02T10:22:00Z"
}

🎯 Deliverables
**Microservices
auth-service
transaction-service
notification-service**

Additional Components-
Kafka topic: **transaction-events**
SQL Server table: **transactions**

MongoDB collection: notification_logs

Postman collection for API testing
