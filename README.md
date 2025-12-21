💳 Wallet Transaction System

A Spring Boot–based transaction system that manages client wallets, supports admin-controlled credits and debits, and enables clients to create orders with external fulfillment integration.

📌 Problem Summary

The system maintains a wallet per client.

Admins can credit or debit client wallets

Clients can create orders that deduct money from their wallet

Each order triggers a fulfillment API call, and the returned fulfillment ID is stored with the order

Design Focus

✅ Correctness

✅ Transactional safety

✅ Scalability

✅ Clear error handling

🏗️ Architecture Overview

The application follows a layered architecture:

Controller → Service → Repository → Database

Responsibilities

Controller
Handles HTTP requests and request validation

Service
Contains business logic and defines transaction boundaries

Repository
Handles database access using Spring Data JPA

Entity
Domain models (Wallet, Order, WalletLedger)

Global Exception Handler
Ensures consistent error responses

🧰 Tech Stack

Java 17

Spring Boot

Spring Web

Spring Data JPA

H2 In-Memory Database

WebClient (external API call)

Hibernate Transactions

🔌 APIs Implemented
1️⃣ Admin – Credit Wallet

POST /admin/wallet/credit

{
  "clientId": "client-1",
  "amount": 1000
}


Behavior

Adds amount to the wallet

Creates a ledger entry (CREDIT)

2️⃣ Admin – Debit Wallet

POST /admin/wallet/debit

{
  "clientId": "client-1",
  "amount": 200
}


Behavior

Checks for sufficient balance

Deducts amount from wallet

Creates ledger entry (DEBIT)

Fails if balance is insufficient

3️⃣ Client – Create Order

POST /orders

Header

client-id: client-1


Body

{
  "amount": 300
}


Workflow

Validate wallet balance

Deduct wallet amount atomically

Create order record

Create ledger entry (ORDER)

Call fulfillment API

Store fulfillment ID

Mark order as COMPLETED

Fulfillment API

POST https://jsonplaceholder.typicode.com/posts

4️⃣ Client – Get Order Details

GET /orders/{orderId}

Header

client-id: client-1


Returns

Order amount

Order status

Fulfillment ID

5️⃣ Client – Wallet Balance

GET /wallet/balance

Header

client-id: client-1


Returns

Current wallet balance

🔄 Transaction Workflow (Core Logic)
Order Creation (Atomic Operation)
BEGIN TRANSACTION
 → Fetch wallet
 → Validate balance
 → Deduct wallet
 → Create order
 → Insert ledger entry
 → Call fulfillment API
 → Update order with fulfillmentId
COMMIT


Failure Handling

Transaction rolls back

Wallet balance remains consistent

📒 Ledger Design

Append-only ledger table

Records every credit, debit, and order deduction

Ensures auditability and traceability

Wallet balance is derived from ledger actions

⚠️ Error Handling

Handled globally using @RestControllerAdvice.

Scenario	HTTP Status
Invalid input	400
Wallet / Order not found	404
Insufficient balance	409
Fulfillment API failure	503
Unexpected error	500

All errors return a consistent JSON structure.

🗄️ Database

H2 in-memory database

Auto schema creation via JPA

Tables

wallet

wallet_ledger

orders

H2 Console
http://localhost:8080/h2-console


JDBC URL

jdbc:h2:mem:walletdb

▶️ How to Run

Import project as a Maven project

Run WalletSystemApplication

Application starts at:

http://localhost:8080

🤖 AI Tool Usage

AI tools were used to:

Create and beautify the README

Validate system design


Reason about transactional boundaries

Identify edge cases

Improve API and error-handling clarity

Note- I had to use combination of manually creating getter,setter, noargsconstructor, builders and sometimes use lombok to create it, because the methods were not loading properly for some of the classes.
