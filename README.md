# ZIPP - DEVELOPMENT README

## Overview

Zipp is a **cashless ride-hailing and delivery platform** built for African cities (starting with Buea, Limbe, and Kumba).

The system includes:

* Mobile App (Rider + Driver)
* Admin Dashboard
* Backend API
* Wallet & Payment System (MoMo-first)

Goal:
Build a **scalable, production-ready platform** with strong architecture, clean code, and reliable money flow.

---

# PROJECT STRUCTURE

This project uses a **monorepo architecture**:

```
/zipp
  /apps
    /mobile        - React Native (Expo)
    /admin         - React (Web dashboard)
    /api           - Node.js backend
  /packages
    /ui            - Shared UI components
    /types         - Shared TypeScript types
    /utils         - Helpers
  /infra           - Deployment configs
```

---

# TEAM RULES (VERY IMPORTANT)

### Git Workflow

* ALWAYS create a new branch:

  ```
  feature/ride-booking
  feature/wallet-topup
  fix/driver-dispatch
  ```

* ALWAYS:

  * Commit small changes
  * Push frequently
  * Open PR for review

---

# MOBILE APP STRUCTURE (React Native)

```
/apps/mobile
  /src
    /screens
    /components
    /features
      /auth
      /wallet
      /trips
      /delivery
      /driver
    /navigation
    /store
    /services
```

---

# FEATURE-BASED STRUCTURE (IMPORTANT)

Each feature must be isolated:

```
/features/wallet
  WalletScreen.tsx
  wallet.service.ts
  wallet.store.ts
  wallet.types.ts
```

---

# BACKEND STRUCTURE (Node.js + Prisma)

```
/apps/api
  /src
    /modules
      /auth
      /user
      /wallet
      /trip
      /delivery
      /driver
      /admin
      /support
    /common
    /config
    /middlewares
```

---

# DATABASE (POSTGRESQL + PRISMA)

### Core Models

```
User
UserRole
DriverProfile
Vehicle
Wallet
WalletLedger
Trip
TripLog
Delivery
DeliveryLog
DriverLocation
Rating
SupportTicket
SupportMessage
WithdrawalRequest
OTPCode
TwoFactorAuth
AdminActionLog
```

---

# WALLET SYSTEM (CRITICAL RULES)

* NEVER update balance directly
* ALWAYS use `wallet_ledger`

### States:

* Available
* Frozen

### Flow:

1. Top-up - Pending
2. Confirm - Available
3. Book trip - Frozen
4. Complete - Split
5. Cancel - Refund

---

# API STRUCTURE

### Auth

```
POST /auth/register
POST /auth/login
POST /auth/verify
POST /auth/2fa
```

### Wallet

```
POST /wallet/top-up
POST /wallet/withdraw
GET /wallet/transactions
```

### Trips

```
POST /trips/request
POST /trips/accept
POST /trips/start
POST /trips/complete
```

### Delivery

```
POST /deliveries/request
POST /deliveries/complete
```

---

# DELIVERY RULE (IMPORTANT)

* ONLY one feature: **Delivery**
* NO Logistics duplication

### Modes:

* Standard (1.0x)
* Express (1.5x)

---

# DESIGN RULES

* Follow Figma strictly
* Use green theme: `#00C853`
* No random UI changes
* No unused screens

---

# COMPONENT RULES

### Shared Components

```
/packages/ui
```

### Feature Components

```
/features/trips/components
```

---

# REALTIME SYSTEM

Using:

* Socket.IO

For:

* Driver tracking
* Trip updates
* Delivery tracking

---

# SECURITY RULES

* Use JWT (access + refresh)
* Hash passwords (bcrypt)
* Enable 2FA for all users
* Protect admin routes

---

# PAYMENTS

### Providers:

* MTN MoMo
* Orange Money

### Rules:

* Backend only handles API keys
* Webhooks REQUIRED
* Always verify payment

---

# ADMIN DASHBOARD

Located in:

```
/apps/admin
```

### Features:

* Users
* Drivers
* Trips
* Deliveries
* Wallet
* Fraud
* Support

---

# TESTING RULES

Must test:

* Auth
* Wallet flow
* Trip flow
* Delivery flow
* Payment flow
* Admin actions

---

# GETTING STARTED

### 1. Clone repo

```
git clone <repo>
```

### 2. Install

```
pnpm install
```

### 3. Run backend

```
pnpm dev:api
```

### 4. Run mobile

```
pnpm dev:mobile
```

### 5. Run admin

```
pnpm dev:admin
```

---

# ENV VARIABLES

Example:

```
DATABASE_URL=
JWT_SECRET=
MTN_MOMO_API_KEY=
ORANGE_MONEY_CLIENT_ID=
REDIS_URL=
```

---

# IMPORTANT TEAM RULES

* No dead buttons
* No fake data in production
* No direct DB balance edits
* No skipping wallet logic
* No exposing admin endpoints

---

# DEVELOPMENT PRIORITY ORDER

1. Auth
2. Wallet
3. Trips
4. Driver
5. Delivery
6. Admin
7. Payments

---

# FINAL NOTE

This is not just an app.

It is a **financial system + transport system**

If wallet logic breaks:
You lose money

If dispatch breaks:
You lose users

---
