#High-throughput Ledger 

> High-throughput, event-driven financial ledger microservice built with **Java, Spring Boot, PostgreSQL, Redis, Kafka, and Docker**.

A learning and portfolio project focused on **financial correctness, idempotency, concurrency, resilience, and scalable transaction processing**.

## Architecture

```text
Client
  │
  ▼
API Gateway ───► Redis
  │              │
  │              └─ Idempotency
  ▼
Kafka
  │
  ▼
Ledger Service
  │
  ▼
PostgreSQL
  ├─ Account Balances
  └─ Immutable Ledger Entries
```

## Key Features

* **Event-driven processing** with Kafka
* **Redis-based idempotency** using `SETNX`
* **Pessimistic locking** with `SELECT ... FOR UPDATE`
* Atomic financial transactions using **PostgreSQL ACID transactions**
* Immutable ledger entries for an **auditable transaction history**
* `BigDecimal` for accurate monetary calculations
* **Docker Compose** for local infrastructure
* Designed for **high-throughput and reliable transaction processing**

## Tech Stack

**Java 17+ · Spring Boot · PostgreSQL · Redis · Kafka · Docker · Maven**

## Transaction Flow

```text
POST /transfers
      │
      ▼
Redis Idempotency Check
      │
      ▼
Kafka Event
      │
      ▼
Ledger Service
      │
      ├── Lock Accounts
      ├── Validate Balance
      ├── Update Balances
      └── Create Ledger Entries
               │
               ▼
            Commit
```

## Project Structure

```text
├── api-gateway/       # Request handling & idempotency
├── ledger-service/    # Core ledger processing
├── db-init/           # Database initialization
├── k8s/               # Kubernetes manifests
├── Documentations/    # Design documentation
├── docker-compose.yml
└── pom.xml
```

## Getting Started

### Prerequisites

* Java 17+
* Docker & Docker Compose
* Git

### Build

```bash
./mvnw clean package -DskipTests
```

### Start Infrastructure

```bash
docker-compose up --build
```

### Run Tests

```bash
./mvnw -pl ledger-service test
```

## Reliability Focus

The project explores production-oriented patterns including **idempotency, concurrency control, Kafka retries, failure handling, database consistency, Redis optimization, and scalable event-driven processing**.

## Future Improvements

* Transactional Outbox
* Optimistic Concurrency Control
* Kafka Dead Letter Queue
* Observability and distributed tracing
* Transaction status API
* Kubernetes deployment
