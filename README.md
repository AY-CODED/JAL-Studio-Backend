# JAL Studio Backend (formerly EKŌ)

The core backend infrastructure for **JAL Studio**, a premium, high-fashion mobile marketplace connecting elite local fashion ateliers with modern buyers in Nigeria. 

This API is built to power a highly scalable, minimalist, luxury editorial mobile application (Flutter) with rigorous financial accuracy and robust vendor management.

## 🚀 The 12-Week MVP Vision
This project is currently in a "hardcore" 12-week rapid development sprint. Scope is strictly constrained to ensure a flawless, reliable launch:
*   **Currency:** Naira (₦ NGN) only.
*   **Payments:** No custom escrow. Direct split-settlement via Paystack and Flutterwave webhooks.
*   **Ledger Accuracy:** All financial transactions utilize MongoDB Multi-Document ACID Transactions and strict `Decimal128` types.

## 🛠️ Tech Stack & Infrastructure
*   **Framework:** Node.js with [NestJS](https://nestjs.com/)
*   **Database:** MongoDB Atlas (Mongoose)
*   **Cloud Infrastructure:** AWS (ECS Fargate for compute, S3 for secure document/image storage, SQS for durable webhook processing, Secrets Manager for API keys).
*   **Architecture:** Domain-Driven Modular Monolith (Designed for future microservice extraction to Go/Java).

## 📂 Domain-Driven Folder Structure
To ensure scalability and prevent tangled dependencies, this backend strictly follows a feature-module architecture:

```text
eko-backend/
├── src/
│   ├── config/                # Environment, AWS, and MongoDB configurations
│   ├── core/                  # Global guards, interceptors (idempotency for payments)
│   ├── modules/               # 📦 THE DOMAINS
│   │   ├── catalog/           # Products, variants, categories, and search
│   │   ├── orders/            # Order state machine and tracking
│   │   ├── payments/          # Paystack/Flutterwave Webhooks & verification
│   │   ├── ledger/            # ⚠️ ACID double-entry financial transactions
│   │   ├── sellers/           # Vendor management, KYC, and payouts
│   │   └── users/             # Buyer authentication and profiles
│   ├── app.module.ts          # Root module
│   └── main.ts                # App entry point
