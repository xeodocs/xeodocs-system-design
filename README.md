# XeoDocs System Design

Welcome to the System Design repository for **XeoDocs**, a platform designed for the orchestration and lifecycle management of open-source documentation translation.

## Architecture Overview

The repository is organized following a **Domain-Driven Structure**, separating cross-cutting concerns from specific business logic.

### [Global Architecture](/global)
The `/global` directory defines the "laws of the system" and cross-cutting architectural concerns:
- **[Gateway](/global/gateway)**: Unified System API (Master Roots) that aggregates all domain specs.
- **Architecture & Standards**: Centralized decisions, infrastructure, and coding conventions.

### [Domain Modules](/domains)
Each folder under `/domains` represents a specific business capability (Bounded Context). This system is split into the following domains:

-   **[Common](/domains/common)**: Shared components, schemas, and standards (error handling, pagination).
-   **[Configuration](/domains/configuration)**: System-wide dynamic settings and operational parameters.
-   **[Identity](/domains/identity)**: User management and authentication.
-   **[Projects](/domains/projects)**: Lifecycle of documentation projects, languages, and synchronization logic.

## API Specifications

This repository contains the authoritative API definitions:

-   **Rest API (OpenAPI)**: Aggregated at [Global Gateway](/global/gateway/openapi.yaml).
