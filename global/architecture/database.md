---
title: Database Schema Design
description: Global overview of the database schema and links to domain-specific schemas.
---

# Database Schema Design

The system uses PostgreSQL (via Supabase) to manage state, projects, and configurations.

Following Domain-Driven Design principles, the schema definitions are distributed across their respective domains.

## Domain Schemas

*   **[Identity Schema](../../domains/identity/database)**
    *   `users`: Administrator accounts.
    *   `user_preferences`: UI/Admin preferences.

*   **[Projects Schema](../../domains/projects/database)**
    *   `projects`: Documentation repositories.
    *   `languages`: Translation targets.
    *   `files`: State tracking and checksums.
    *   `ignored_paths`: Translation exclusion patterns.
    *   `special_paths`: Special rule patterns.

*   **[Configuration Schema](../../domains/configuration/database)**
    *   `configurations`: System-wide dynamic settings.

## Global Relationships Overview

While each domain owns its tables, there are relationships that cross domain boundaries:

*   **Identity -> Projects**: Loosely coupled. Access is governed by `users.api_key` for CLI and session-based auth for the Admin Panel. No direct database foreign keys exist between these domains.
*   **Configuration -> Projects**: Logical coupling. Orchestration logic (Background Worker) and AI Services in the Projects domain consume settings and prompt templates defined in the Configuration domain.
*   **Domain Internal**: Within the **Projects Domain**, there is strict coupling between `Projects`, `Languages`, and `Files` to ensure data integrity.

For detailed field definitions, please refer to the specific domain documentation linked above.
