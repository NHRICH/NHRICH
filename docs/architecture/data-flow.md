# System Architecture — Data Flow

This document illustrates the data flow between the Django backend and the Next.js / Flutter frontends used across AV SaaS projects.

---

## High-Level Request Flow

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        NextJS["Next.js (Web)"]
        Flutter["Flutter (Mobile)"]
    end

    subgraph API["API Layer"]
        DRF["Django REST Framework"]
        Auth["JWT / Session Auth"]
        Celery["Celery (Async Tasks)"]
    end

    subgraph Data["Data Layer"]
        Postgres["PostgreSQL"]
        Redis["Redis (Cache & Broker)"]
        S3["AWS S3 / DigitalOcean Spaces"]
    end

    subgraph Infra["Infrastructure"]
        DO["DigitalOcean / AWS"]
        CDN["CDN"]
    end

    NextJS -->|HTTPS REST / GraphQL| DRF
    Flutter -->|HTTPS REST| DRF
    DRF --> Auth
    DRF --> Postgres
    DRF --> Redis
    DRF --> S3
    DRF --> Celery
    Celery --> Redis
    Celery --> Postgres
    S3 --> CDN
    CDN --> NextJS
    CDN --> Flutter
    DO --> DRF
    DO --> Postgres
    DO --> Redis
```

---

## Authentication Flow

```mermaid
sequenceDiagram
    participant User
    participant Frontend as Next.js / Flutter
    participant Django as Django (DRF)
    participant DB as PostgreSQL
    participant Redis

    User->>Frontend: Enter credentials
    Frontend->>Django: POST /api/auth/login
    Django->>DB: Validate user
    DB-->>Django: User record
    Django->>Django: Generate JWT (access + refresh)
    Django-->>Frontend: 200 OK — tokens
    Frontend->>Frontend: Store tokens (httpOnly cookie / secure storage)

    Note over Frontend,Django: Subsequent authenticated requests

    Frontend->>Django: GET /api/resource (Authorization: Bearer <access_token>)
    Django->>Redis: Check token blacklist
    Redis-->>Django: Not blacklisted
    Django-->>Frontend: 200 OK — resource data
```

---

## Payment Flow (Chapa / Stripe)

```mermaid
sequenceDiagram
    participant User
    participant Frontend as Next.js
    participant Django as Django (DRF)
    participant Gateway as Chapa / Stripe
    participant DB as PostgreSQL
    participant Celery

    User->>Frontend: Initiate payment
    Frontend->>Django: POST /api/payments/initiate
    Django->>Gateway: Create checkout session
    Gateway-->>Django: Checkout URL
    Django-->>Frontend: Redirect URL
    Frontend->>User: Redirect to payment page
    User->>Gateway: Complete payment
    Gateway->>Django: Webhook — payment.success
    Django->>Celery: Enqueue fulfilment task
    Celery->>DB: Update order status
    Celery->>Django: Trigger notification
    Django->>Frontend: WebSocket / polling update
    Frontend->>User: Confirmation screen
```

---

## Component Responsibilities

| Layer | Technology | Role |
|-------|-----------|------|
| Web Frontend | Next.js 14 (App Router) | SSR/SSG, user interface, API consumption |
| Mobile Frontend | Flutter | Cross-platform mobile app |
| API Backend | Django + DRF | Business logic, auth, REST endpoints |
| Task Queue | Celery + Redis | Async jobs: emails, payments, reports |
| Primary Database | PostgreSQL | Relational data storage |
| Cache / Broker | Redis | Session cache, Celery message broker |
| Object Storage | AWS S3 / DO Spaces | Media, documents, exports |
| Infrastructure | AWS / DigitalOcean | Hosting, networking, CDN |
