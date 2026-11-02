# Wallet System: Digital Wallet & Transaction Management

![Java](https://img.shields.io/badge/Java-17-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.9-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)
![Status](https://img.shields.io/badge/Status-Portfolio%20Ready-success)
[![CI](https://github.com/Mrinal-Jha-dev081/Wallet-System-Digital-Wallet-Transaction-Management/actions/workflows/ci.yml/badge.svg)](https://github.com/Mrinal-Jha-dev081/Wallet-System-Digital-Wallet-Transaction-Management/actions/workflows/ci.yml)

A secure digital wallet platform built with Java and Spring Boot for managing wallet balances, transactional activity, and order processing with consistency and traceability.

This project is designed to model realistic financial workflows where balance updates, transaction history, and order execution happen under strict integrity rules. It focuses on atomic operations, auditability, and reliable behavior in high-consequence financial scenarios.

## Overview

The application provides the core building blocks of a digital wallet system:

- Wallet creation and balance tracking
- Credit and debit operations with validation
- Client order creation that deducts from wallet balance
- Fulfillment integration with external API calls
- Append-only ledger records for audit and traceability
- Transaction safety around business-critical operations

## Key Features

- Secure wallet management for clients
- Admin-controlled credit and debit endpoints
- Atomic order processing with validation and rollback safety
- Transaction ledger to track every movement in the wallet
- External fulfillment simulation using WebClient
- Consistent JSON error responses via centralized exception handling
- H2 in-memory database for local development and testing

## Architecture

The project follows a clean layered architecture:

- Controller layer for API endpoints
- Service layer for business logic and transaction boundaries
- Repository layer for persistence
- Entity layer for domain models
- Ledger-based audit trail for reconciliation and accountability

## Tech Stack

- Java 17+
- Spring Boot 3.5.9
- Spring Web
- Spring Data JPA
- Spring Validation
- H2 Database
- WebClient for outbound HTTP calls
- Maven

## Project Structure

```text
wallet-system/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/WalletSystemApplication/
│   │   │       ├── config/
│   │   │       ├── controller/
│   │   │       ├── dto/
│   │   │       ├── entity/
│   │   │       ├── exception/
│   │   │       ├── handler/
│   │   │       ├── repository/
│   │   │       ├── service/
│   │   │       └── util/
│   │   └── resources/
│   └── test/
├── pom.xml
├── README.md
├── LICENSE
├── mvnw
├── mvnw.cmd
└── .gitignore
```

## Prerequisites

Before running the project locally, make sure you have:

- Java 21 or newer
- Maven 3.9+
- Git

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Mrinal-Jha-dev081/Wallet-System-Digital-Wallet-Transaction-Management.git
cd Wallet-System-Digital-Wallet-Transaction-Management
```

### 2. Build the project

```bash
./mvnw clean install
```

### 3. Run the application

```bash
./mvnw spring-boot:run
```

Once started, the application runs on:

- http://localhost:8080

### 4. H2 console

The project includes an H2 in-memory database for local development.

- URL: http://localhost:8080/h2-console
- JDBC URL: jdbc:h2:mem:walletdb

## Core API Flow

### Admin operations

- Credit wallet
- Debit wallet
- Validate balance before withdrawal

### Client operations

- View wallet balance
- Create order
- Retrieve order details

### Transaction model

The system processes financial actions in a transactional manner to ensure:

- no partial balance deduction
- no inconsistent ledger writes
- safe rollback when failures occur
- traceable audit history

## Example Requests

### Credit wallet

```http
POST /admin/wallet/credit
Content-Type: application/json

{
  "clientId": "client-1",
  "amount": 1000
}
```

### Create order

```http
POST /orders
client-id: client-1
Content-Type: application/json

{
  "amount": 300
}
```

## Business Goals

This project demonstrates how to design a wallet platform around:

- correctness
- transactional integrity
- ledger-based balance tracking
- external system integration safety
- maintainable financial workflows

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Portfolio Note

This repository is structured to present as a professional software project in a portfolio, showcasing backend engineering, transaction design, API-driven system thinking, and disciplined engineering practices.

## Ownership

This project is maintained and published under the GitHub account of Mrinal Kumar Jha and is intended to be presented as a personal portfolio project.

Identify edge cases

Improve API and error-handling clarity

Note- I had to use combination of manually creating getter,setter, noargsconstructor, builders and sometimes use lombok to create it, because the methods were not loading properly for some of the classes.
