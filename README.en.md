# railway-12306

railway-12306 is a railway ticket booking system designed to emulate the 12306 website, aiming to provide a reference implementation of a high-concurrency, distributed architecture-based ticketing system. Built on Spring Cloud and Alibaba's microservices architecture, this project integrates various distributed components such as RocketMQ, Redis, ShardingSphere, Feign, and Sentinel to implement core functionalities including ticket booking, payment, order management, and user management.

## Technology Stack

- **Spring Boot / Spring Cloud / Spring Cloud Alibaba**
- **MyBatis Plus / ShardingSphere** (Database sharding and partitioning)
- **Redis / Redisson** (Caching, distributed locks)
- **RocketMQ** (Asynchronous message queue)
- **Feign / OpenFeign** (Inter-service communication)
- **Sentinel / Nacos** (Service governance and configuration center)
- **XXL-JOB** (Scheduled tasks)
- **Hippo4j** (Dynamic thread pool)
- **Canal / RocketMQ** (Data synchronization)
- **Vue.js** (Frontend interface)

## Functional Modules

### User Service
- User registration, login, and logout
- User information management
- Passenger information management
- User deactivation and reuse mechanism
- BloomFilter-based cache penetration protection using Redis

### Ticket Service
- Train schedule management
- Station and route queries
- Ticket inventory management
- Seat selection and locking mechanism
- Ticket purchase, refund, and rescheduling
- Token Bucket-based ticket availability control

### Order Service
- Order creation, query, cancellation, and closure
- Order status management
- Delayed order closure mechanism based on RocketMQ
- Order status reversal mechanism

### Payment Service
- Payment interface integration (e.g., Alipay)
- Payment callback handling
- Refund mechanism
- Asynchronous payment result notifications

### Aggregation Service
- Unified service aggregation entry point
- Integration of user, ticket, order, and payment services
- Provides a unified interface invocation chain

### Gateway Service
- Unified API entry point
- Token validation
- Routing control and permission interception

## Featured Features

- **High-Concurrency Optimization**: Enhances system throughput via Redis caching, distributed locks, Token Bucket, and thread pools.
- **Distributed ID Generation**: Uses an improved Snowflake algorithm to generate globally unique order and payment IDs.
- **Idempotency Control**: Implements interface idempotency via custom annotations combined with Redis to prevent duplicate submissions.
- **Distributed Tracing**: Integrates logging and traceability for easier debugging and monitoring.
- **Data Synchronization**: Achieves database Binlog synchronization to cache via Canal + RocketMQ to ensure data consistency.
- **Task Scheduling**: Uses XXL-JOB to execute scheduled tasks such as cache warming and data synchronization.

## Project Structure

- **console-vue**: Frontend Vue project providing the user interface.
- **frameworks/**: Common component modules including caching, logging, thread pools, idempotency, and exception handling.
- **services/**: Microservice modules including user, ticket, order, payment, aggregation, and gateway services.
- **tests/**: Testing modules containing unit and integration tests.

## Quick Start

### Frontend Startup

```bash
# Enter frontend directory
cd console-vue

# Install dependencies
yarn install

# Start development environment
yarn serve

# Build production environment
yarn build
```

### Backend Startup

1. **Start Dependency Services**: Ensure MySQL, Redis, RocketMQ, Nacos, Sentinel, and XXL-JOB are running.
2. **Import Database**: Initialize the database using SQL files under `resources/db/`.
3. **Start Microservices**: Launch the services in order: `user-service`, `ticket-service`, `order-service`, `pay-service`, `aggregation-service`, and `gateway-service`.
4. **Access API Documentation**: View API documentation via Swagger or Knife4j.

## Developer Guide

- **Code Style**: Utilize modern development tools such as Lombok, Slf4j, and Spring Boot Starters.
- **Exception Handling**: Unified exception handling with customizable error codes and encapsulation.
- **Logging**: Implements interface logging via AOP for request chain tracing.
- **Configuration Center**: Manages service configurations via Nacos with dynamic refresh support.
- **Service Registration & Discovery**: Implements service registration and discovery based on Nacos.

## Open Source License

This project is licensed under the **MIT License**. Contributions and suggestions are welcome!

## Contact

- Author: Bushituo
- Gitee Repository: [railway-12306](https://gitee.com/bu-shituo/railway-12306)

---

railway-12306 is a complete reference implementation of a railway ticket booking system, ideal for learning microservices architecture, high-concurrency system design, and distributed transactions. Welcome to Star, Fork, and contribute code!