# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Happy Cars is an automotive marketplace platform operating on a **consignment model** in Tamil Nadu, India. The platform:
- Connects car buyers with quality-verified used vehicles at Happy Cars showrooms
- Enables sellers to submit cars (Happy Cars handles the entire sales process)
- Provides AI-powered instant valuation and RAG chatbot
- Routes all enquiries through Happy Cars team (commission model)

**Current PRD:** `docs/prd.md` (source of truth for all requirements)

The backend is a Java Spring Boot application.

## Build & Development Commands

All commands should be run from the `happycars/` directory:

```bash
# Build the project
./mvnw clean compile

# Run tests
./mvnw test

# Run a single test class
./mvnw test -Dtest=HappycarsApplicationTests

# Run a specific test method
./mvnw test -Dtest=HappycarsApplicationTests#contextLoads

# Package the application
./mvnw package

# Run the application
./mvnw spring-boot:run

# Skip tests during build
./mvnw package -DskipTests
```

## Technology Stack

- **Java 21** with Spring Boot 3.2.0
- **Database**: PostgreSQL
- **Security**: Spring Security with OAuth2
- **Build**: Maven (wrapper included)
- **Lombok**: Used for boilerplate reduction

## Architecture

The backend follows a standard layered Spring Boot architecture:

```
happycars/src/main/java/com/happycars/
├── config/          # Spring configuration classes
├── constants/       # Application constants
├── controller/      # REST controllers
├── dto/
│   ├── request/     # Request DTOs
│   └── response/    # Response DTOs
├── entity/          # JPA entities
├── exception/       # Custom exceptions
├── mapper/          # Entity-DTO mappers
├── repository/      # JPA repositories
└── service/
    └── impl/        # Service implementations
```

## Feature Development Workflow

This project uses SpecKit for feature specification and planning. Available commands:

- `/speckit.specify` - Create feature specification from description
- `/speckit.plan` - Generate technical implementation plan
- `/speckit.tasks` - Generate actionable tasks from design artifacts
- `/speckit.clarify` - Clarify underspecified areas in specs
- `/speckit.implement` - Execute implementation plan
- `/speckit.analyze` - Cross-artifact consistency analysis
- `/speckit.checklist` - Generate custom checklist for features

Feature specs are stored in `specs/<number>-<feature-name>/` directories.

## Key Directories

- `happycars/` - Main Spring Boot application
- `docs/prd.md` - **Current PRD** (source of truth)
- `docs/analysis/` - Analysis documents (product brief - superseded)
- `documents/prd.md` - Original PRD (superseded, kept for reference)
- `.specify/` - SpecKit templates and configuration
- `.specify/memory/constitution.md` - Project principles (template, needs customization)
- `.bmad/` - BMAD workflow configurations

## Key Business Rules (from PRD)

- **Consignment Model**: Sellers submit cars → Happy Cars verifies (contacts seller) → Approves → Cars go to showroom → Happy Cars handles sales
- **Unified Account**: No buyer/seller classification - same account can buy or sell
- **Lead Capture**: Phone (OTP verified) + Name required, Email optional for guests
- **Registration**: Phone + OTP primary, Google + Phone secondary (phone is primary ID)
- **Valuation**: Estimated only (disclaimer shown), users can enquire for clarification
- **Notifications**: SMS as primary for sellers, push notifications secondary
- **Payments**: Offline/cash only at showroom (no online payments for MVP)
- **Language**: English only for MVP
- **Admin Portal**: Separate application (admin.happycars.com)
- **Admin Roles**: Super Admin (full access) + Admin (limited: view submissions read-only, view/update leads, content management, callback tracking - no dashboard, no approvals, no listing creation)

## UX Design Reference

**UX Specification:** `docs/ux-design-specification.md` (source of truth for all UX decisions)

Key UX decisions:
- **Design System**: MUI (React Web) + Flutter Material 3 (Mobile)
- **Primary Color**: Teal (#0D9488)
- **Typography**: Inter or Work Sans
- **Mobile Navigation**: Hamburger menu
- **Chatbot**: Always visible, collapsed by default, user-initiated only
- **Favorites/Share**: MVP features
- **City Filter**: Not in MVP (single showroom)

## Architecture Reference

**Architecture:** `docs/architecture.md` (source of truth for all technical decisions)

Key architecture decisions:
- **Backend**: Spring Boot 3.2 + Java 21 + PostgreSQL + Redis + ElasticSearch 8.x
- **Web**: Next.js 14.2 + MUI 5.16 (stable, avoids Turbopack issues)
- **Mobile**: Flutter 3.27+ + BLoC 8.1 + Dio 5.7.0 (pinned)
- **Admin**: Vite + React + MUI 5.16
- **Auth**: JWT + Redis (stateful), Phone+OTP primary
- **API**: REST with `/api/v1/` versioning
- **Caching**: Redis for OTP, sessions, search results
- **Migrations**: Flyway

**Project Context:** `docs/project_context.md` (critical rules for AI agents)

## Epics & Stories Reference

**Epics Document:** `docs/epics/index.md` (implementation breakdown)

| Epic | Title | Stories |
|------|-------|---------|
| 1 | Project Foundation & User Authentication | 8 |
| 2 | Car Browsing & Discovery | 5 |
| 3 | Seller Valuation & Lead Capture | 5 |
| 4 | Car Submission & Status Tracking | 8 |
| 5 | Buyer Enquiry & Lead Management | 7 |
| 6 | AI Chatbot Integration | 7 |
| 7 | Admin Portal - Core Operations | 10 |
| 8 | Content & New Cars | 8 |

**Total: 8 Epics, 58 Stories covering all 69 FRs**
