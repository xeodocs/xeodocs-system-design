---
title: Infrastructure and Security
description: Production/dev infrastructure and security measures.
---

## Infrastructure

### Production Environment
- **Hosting:** Docker Swarm on Virtual Private Server (VPS).
- **Database:** PostgreSQL (managed by Supabase).
- **Backend:** Go (Modular Monolith architecture) running in Docker containers.
- **Frontend (Web):** Next.js (SSG/SSR) running in Docker containers.
- **Frontend (Admin):** Tauri (Desktop App) or Next.js Web App interacting with the API.
- **Email Service:** Resend.

### Development Environment
- **Containerization:** Docker Compose on Docker Desktop.
- **Repositories:**
  - Uses the same GitHub account as production.
  - Fork names are prefixed with `staging-` or `dev-` to distinguish them from production forks.

## Security

### Authentication
- **Admin Panel:**
  - Authentication using JWT stored in HTTPOnly Secure Cookies.
  - Standard Username/Password login.
- **CLI (Command Line Interface):**
  - Authenticates via a long-lived API Key assigned to an administrator.
  - The API Key is passed in headers (e.g., `X-API-Key` or Bearer Token) for all CLI requests.

### Access Control
- **Role-Based Access:** Currently single role (Administrator), but designed to support granular permissions in the future.
- **API Security:**
  - Endpoints are protected and require valid authentication (JWT/Cookie or API Key).
  - Input validation on all endpoints to prevent injection attacks.

### Data Protection
- **Credentials:** Passwords hashed using standard algorithms (e.g., bcrypt/argon2) before storage.
- **API Keys:** Generated securely and stored in the database.
- **Connection:** All communication between CLI, Frontend, and Backend should be over HTTPS.
