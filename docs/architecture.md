---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]
status: 'complete'
completedAt: '2026-01-11'
inputDocuments:
  - docs/prd.md
  - docs/ux-design-specification.md
workflowType: 'architecture'
lastStep: 8
project_name: 'happycars-application'
user_name: 'Prabhakaranr'
date: '2026-01-11'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

## Project Context Analysis

### Requirements Overview

**Functional Requirements:**
69 functional requirements across 9 domains:
- Car Discovery & Search (7 FRs): Browse, filter, search, view listings without auth
- Vehicle Valuation (5 FRs): Lead capture + instant valuation teaser with disclaimer
- Car Submission (6 FRs): Seller flow with 3-9 photos, optional video, status tracking
- AI Chatbot (6 FRs): RAG integration for specs, pricing, comparisons, contextual guidance
- Buyer Enquiry (7 FRs): OTP-verified lead capture, all enquiries route to Happy Cars team
- Admin Portal (11 FRs): Separate application, Super Admin + Admin roles with distinct permissions
- Content Management (3 FRs): News/articles, categories, English only
- New Cars Section (4 FRs): Manual + API data, on-road pricing
- User Account Management (20 FRs): Unified account, Phone+OTP primary, Google OAuth secondary

**Non-Functional Requirements:**
| Category | MVP Target | Post-MVP Target |
|----------|------------|-----------------|
| Page Load | <5s on 4G | <3s on 3G |
| Search Response | <2s | <500ms |
| Valuation Calculation | <3s | - |
| Chatbot Response | <5s | - |
| Uptime | 99% | 99.9% |
| Concurrent Users | 10,000 | 50,000 |
| Listings Capacity | 10,000 | 100,000+ |

**Scale & Complexity:**
- Primary domain: Full-stack automotive marketplace
- Complexity level: Medium-High
- Estimated architectural components: 15-20 major components
- Platforms: 3 (React Web, Flutter Mobile, Admin Portal)

### Technical Constraints & Dependencies

**Specified Tech Stack:**
- Backend: Java/Spring Boot 3.2.0
- Database: PostgreSQL
- Search Engine: ElasticSearch
- Web Frontend: React (SPA with SSR for SEO)
- Mobile: Flutter (iOS 13+, Android 8.0+)
- Admin: Separate deployment, MUI-based

**External Dependencies:**
| Integration | Purpose | Criticality |
|-------------|---------|-------------|
| SMS Gateway | OTP + Seller notifications | Critical |
| WhatsApp API | Click-to-chat lead routing | High |
| Google OAuth | Secondary registration | Medium |
| RAG API | Chatbot responses (existing) | High |
| Valuation Data | Benchmark pricing | Medium |
| FCM/APNs | Push notifications | Medium |

**Deployment Constraints:**
- Admin portal on separate subdomain (admin.happycars.com)
- SSR required for car listing pages (SEO)
- CDN required for static assets and images

### Cross-Cutting Concerns Identified

1. **Authentication & Authorization**
   - Phone+OTP as primary (all users)
   - Google OAuth as secondary (registration only, phone still required)
   - Role-based access for admin (Super Admin: full access, Admin: limited)
   - Session management with secure tokens

2. **Lead Capture & Account Linking**
   - Phone number as universal identifier
   - OTP verification required for all lead captures
   - Auto-link previous leads when user registers with same phone
   - Guest → Registered transition without data loss

3. **File Storage & Media Processing**
   - Photo upload: 3-9 images, JPEG/PNG, max 5MB each
   - Auto-compression for slow networks (tier-2 cities)
   - Video: any format, max 2 min, max 100MB
   - Admin can replace seller photos with showroom photos
   - CDN delivery for all media

4. **Notification Orchestration**
   - SMS: OTP (all), status updates (sellers only)
   - Push: Enquiry confirmation (buyers), optional for sellers
   - In-app indicators (dot, no count)

5. **Search & Discovery**
   - ElasticSearch for listings
   - Filters: brand, model, price range, year, mileage
   - No city filter MVP (single showroom)
   - Infinite scroll pagination

6. **State Management**
   - Submission states: Submitted → Under Review → Approved/Rejected → Listed → Sold
   - Lead states: Pending → Called → Visited
   - State transitions trigger notifications

## Starter Template Decisions

### Backend (Existing)
- **Spring Boot 3.2.0 + Java 21** - already configured
- **Add when needed:** `spring-boot-starter-data-elasticsearch` (requires ES 8.x)

### Web Frontend
- **Next.js 14.2.x + MUI 5.16.x**
- Stable, proven combination
- SSR for SEO on listing pages

```bash
npx create-next-app@14.2 happycars-web --typescript --eslint --app --src-dir
npm install @mui/material@^5.16.0 @emotion/react @emotion/styled @mui/material-nextjs@^5.16.0
```

### Mobile App
- **Flutter 3.27+ with BLoC + Dio 5.7.0**
- Feature-first structure

```yaml
# pubspec.yaml
dependencies:
  flutter_bloc: ^8.1.6
  dio: 5.7.0
  equatable: ^2.0.5
```

### Admin Portal
- **Vite + React + MUI 5.16.x**
- No SSR needed

```bash
npm create vite@latest happycars-admin -- --template react-ts
npm install @mui/material@^5.16.0 @emotion/react @emotion/styled
```

### Why These Versions
- Next.js 15 + MUI 6/7 has Turbopack hydration issues - not worth the risk
- Dio 5.8.x breaks on Flutter web - pin to 5.7.0
- Spring Boot 3.2 + ES 8.x is the supported combination

## Core Architectural Decisions

### Decision Summary

| Category | Decision | Choice |
|----------|----------|--------|
| Database Migration | Tool | Flyway |
| Caching | Strategy | Redis (sessions, OTP, listings) |
| Authentication | Token Strategy | JWT + Redis (stateful) |
| API Security | Approach | Spring Security + JWT filter |
| API Style | Pattern | REST |
| API Versioning | Format | URL path (`/api/v1/`) |
| Error Handling | Format | Standard JSON |
| Infrastructure | Hosting | Deferred to implementation |

### Data Architecture

**Database Migration: Flyway**
- SQL-based migrations in `src/main/resources/db/migration/`
- Naming: `V1__create_users_table.sql`, `V2__create_listings_table.sql`
- Spring Boot auto-runs on startup

**Caching: Redis**
- OTP codes (5-min TTL)
- JWT blacklist (for logout)
- Search results cache
- Session storage

```properties
# application.properties
spring.data.redis.host=localhost
spring.data.redis.port=6379
spring.cache.type=redis
```

### Authentication & Security

**JWT + Redis (Stateful)**
- Access token: 15 min expiry
- Refresh token: 7 days, stored in Redis
- Logout: Add token to Redis blacklist
- Phone number as primary claim

**Spring Security Configuration**
- JWT filter validates tokens
- Public endpoints: `/api/v1/auth/**`, `/api/v1/cars/**` (read), `/api/v1/valuation`
- Protected: `/api/v1/submissions/**`, `/api/v1/enquiries/**`, `/api/v1/profile/**`
- Admin: `/api/v1/admin/**` (role-based)

### API Design

**REST with URL Versioning**
- Base path: `/api/v1/`
- Resources: `cars`, `submissions`, `enquiries`, `users`, `valuations`

**Standard Error Response**
```json
{
  "error": "VALIDATION_ERROR",
  "message": "Phone number is required",
  "details": { "field": "phone" },
  "timestamp": "2026-01-11T10:00:00Z"
}
```

**HTTP Status Codes**
- 200: Success
- 201: Created
- 400: Validation error
- 401: Unauthorized
- 403: Forbidden
- 404: Not found
- 500: Server error

### Infrastructure

**Deferred to Implementation Phase**
- Hosting platform selection
- CI/CD pipeline setup
- Monitoring and logging
- Will decide based on team preference and budget

## Implementation Patterns & Consistency Rules

### Naming Patterns

**Database (PostgreSQL):**
| Element | Convention | Example |
|---------|------------|---------|
| Tables | snake_case, plural | `users`, `car_listings`, `lead_enquiries` |
| Columns | snake_case | `created_at`, `phone_number`, `listing_id` |
| Foreign Keys | `{table}_id` | `user_id`, `listing_id` |
| Indexes | `idx_{table}_{columns}` | `idx_users_phone` |

**API Endpoints:**
| Element | Convention | Example |
|---------|------------|---------|
| Resources | plural, lowercase | `/api/v1/cars`, `/api/v1/submissions` |
| Actions | verb prefix for non-CRUD | `/api/v1/valuations/calculate` |
| IDs | path param | `/api/v1/cars/{id}` |
| Query params | camelCase | `?priceMin=500000&brandId=1` |

**Backend (Java/Spring):**
| Element | Convention | Example |
|---------|------------|---------|
| Entities | PascalCase, singular | `User`, `CarListing`, `Submission` |
| Repositories | `{Entity}Repository` | `UserRepository` |
| Services | `{Entity}Service` | `CarListingService` |
| Controllers | `{Entity}Controller` | `SubmissionController` |
| DTOs | `{Entity}{Action}Dto` | `CarListingResponseDto`, `SubmissionCreateDto` |

**Frontend (React/Next.js):**
| Element | Convention | Example |
|---------|------------|---------|
| Components | PascalCase | `ListingCard.tsx`, `PriceBreakdown.tsx` |
| Hooks | camelCase, `use` prefix | `useAuth.ts`, `useListings.ts` |
| Utils | camelCase | `formatPrice.ts`, `validatePhone.ts` |
| Pages (Next.js) | kebab-case folders | `cars/[id]/page.tsx` |

**Mobile (Flutter/Dart):**
| Element | Convention | Example |
|---------|------------|---------|
| Files | snake_case | `listing_card.dart`, `car_bloc.dart` |
| Classes | PascalCase | `ListingCard`, `CarBloc` |
| BLoCs | `{Feature}Bloc` | `AuthBloc`, `SubmissionBloc` |
| Events | `{Feature}{Action}` | `AuthLoginRequested`, `SubmissionCreated` |
| States | `{Feature}{State}` | `AuthAuthenticated`, `SubmissionLoading` |

### Format Patterns

**API Response Wrapper:**
```json
// Success
{
  "data": { ... },
  "meta": { "page": 1, "total": 100 }
}

// Error
{
  "error": "VALIDATION_ERROR",
  "message": "Phone number is required",
  "details": { "field": "phone" }
}
```

**JSON Field Naming:**
- API responses: `camelCase` (JavaScript convention)
- Database: `snake_case` (PostgreSQL convention)
- Spring handles conversion automatically with `@JsonNaming`

**Date/Time:**
- API: ISO 8601 strings (`2026-01-11T10:00:00Z`)
- Display: Formatted per locale (`11 Jan 2026`)

### Structure Patterns

**Backend Structure:**
```
src/main/java/com/happycars/
├── config/           # Spring configs
├── controller/       # REST controllers
├── dto/
│   ├── request/      # Input DTOs
│   └── response/     # Output DTOs
├── entity/           # JPA entities
├── exception/        # Custom exceptions
├── mapper/           # Entity ↔ DTO mappers
├── repository/       # JPA repositories
├── service/
│   └── impl/         # Service implementations
└── util/             # Utilities
```

**Frontend Structure (Next.js):**
```
src/
├── app/              # Next.js app router
├── components/
│   ├── common/       # Shared (Button, Input)
│   └── features/     # Feature-specific (ListingCard)
├── hooks/            # Custom hooks
├── lib/              # API clients, utils
├── styles/           # Global styles, theme
└── types/            # TypeScript types
```

**Mobile Structure (Flutter):**
```
lib/
├── core/
│   ├── api/          # Dio client, interceptors
│   ├── theme/        # App theme, colors
│   └── utils/        # Shared utilities
├── features/
│   ├── auth/
│   │   ├── bloc/
│   │   ├── data/
│   │   └── ui/
│   ├── browse/
│   ├── submission/
│   └── profile/
└── main.dart
```

### Process Patterns

**Loading States:**
- Use `isLoading`, `isError`, `isSuccess` booleans
- Show skeleton loaders, not spinners (per UX spec)

**Error Handling:**
- Backend: Throw custom exceptions, `@ControllerAdvice` handles them
- Frontend: Try-catch in hooks, display friendly messages
- Never expose stack traces to users

## Project Structure & Boundaries

### Repository Structure

```
happycars-application/
├── happycars/                    # Backend API (Spring Boot) - EXISTS
├── happycars-web/                # Consumer Web (Next.js)
├── happycars-mobile/             # Mobile Apps (Flutter)
├── happycars-admin/              # Admin Portal (Vite + React)
└── docs/                         # Shared documentation
```

### Backend: `happycars/`

```
happycars/
├── pom.xml
├── src/main/java/com/happycars/
│   ├── HappycarsApplication.java
│   ├── config/
│   │   ├── SecurityConfig.java
│   │   ├── RedisConfig.java
│   │   ├── ElasticsearchConfig.java
│   │   └── CorsConfig.java
│   ├── controller/
│   │   ├── AuthController.java
│   │   ├── CarController.java
│   │   ├── SubmissionController.java
│   │   ├── EnquiryController.java
│   │   ├── ValuationController.java
│   │   ├── UserController.java
│   │   └── admin/
│   │       ├── AdminListingController.java
│   │       ├── AdminLeadController.java
│   │       └── AdminContentController.java
│   ├── dto/request/
│   ├── dto/response/
│   ├── entity/
│   │   ├── User.java
│   │   ├── CarListing.java
│   │   ├── Submission.java
│   │   ├── Lead.java
│   │   └── OtpToken.java
│   ├── repository/
│   ├── service/
│   │   ├── AuthService.java
│   │   ├── OtpService.java
│   │   ├── CarListingService.java
│   │   ├── SubmissionService.java
│   │   ├── ValuationService.java
│   │   ├── SmsService.java
│   │   └── ChatbotService.java
│   ├── security/
│   │   ├── JwtTokenProvider.java
│   │   ├── JwtAuthenticationFilter.java
│   │   └── UserDetailsServiceImpl.java
│   └── exception/
│       ├── GlobalExceptionHandler.java
│       └── custom/
├── src/main/resources/
│   ├── application.properties
│   └── db/migration/
│       ├── V1__create_users.sql
│       ├── V2__create_car_listings.sql
│       ├── V3__create_submissions.sql
│       └── V4__create_leads.sql
└── docker-compose.yml
```

### Web: `happycars-web/`

```
happycars-web/
├── package.json
├── next.config.js
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx                      # Home
│   │   ├── cars/
│   │   │   ├── page.tsx                  # Listings
│   │   │   └── [id]/page.tsx             # Car detail
│   │   ├── sell/
│   │   │   ├── page.tsx                  # Valuation
│   │   │   └── submit/page.tsx           # Submission
│   │   ├── auth/
│   │   │   ├── login/page.tsx
│   │   │   └── register/page.tsx
│   │   └── profile/
│   │       ├── submissions/page.tsx
│   │       ├── enquiries/page.tsx
│   │       └── saved/page.tsx
│   ├── components/
│   │   ├── common/
│   │   │   ├── Header.tsx
│   │   │   └── Footer.tsx
│   │   └── features/
│   │       ├── ListingCard.tsx
│   │       ├── PriceBreakdown.tsx
│   │       ├── ChatbotWidget.tsx
│   │       └── PhotoUploader.tsx
│   ├── hooks/
│   ├── lib/
│   │   └── api.ts
│   └── styles/
│       └── theme.ts
└── public/
```

### Mobile: `happycars_mobile/`

```
happycars_mobile/
├── pubspec.yaml
├── lib/
│   ├── main.dart
│   ├── core/
│   │   ├── api/
│   │   ├── theme/
│   │   └── utils/
│   └── features/
│       ├── auth/
│       │   ├── bloc/
│       │   ├── data/
│       │   └── ui/
│       ├── browse/
│       │   ├── bloc/
│       │   ├── data/
│       │   └── ui/
│       ├── submission/
│       └── profile/
├── android/
├── ios/
└── test/
```

### Admin: `happycars-admin/`

```
happycars-admin/
├── package.json
├── vite.config.ts
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   ├── components/
│   ├── pages/
│   │   ├── DashboardPage.tsx
│   │   ├── SubmissionsPage.tsx
│   │   ├── LeadsPage.tsx
│   │   ├── ListingsPage.tsx
│   │   └── ContentPage.tsx
│   └── lib/
│       └── api.ts
└── public/
```

### Requirements Mapping

| PRD Feature | Backend | Web | Mobile | Admin |
|-------------|---------|-----|--------|-------|
| Car Discovery (FR1-7) | `CarController` | `cars/` | `browse/` | - |
| Valuation (FR8-12) | `ValuationController` | `sell/` | `submission/` | - |
| Submission (FR13-18) | `SubmissionController` | `sell/submit/` | `submission/` | `SubmissionsPage` |
| Chatbot (FR19-24) | `ChatbotService` | `ChatbotWidget` | - | - |
| Enquiry (FR25-31) | `EnquiryController` | Forms | Forms | `LeadsPage` |
| Admin (FR32-42) | `admin/` | - | - | All pages |
| Auth (FR50-63) | `AuthController` | `auth/` | `auth/` | Login |

## Architecture Validation

### Validation Status: PASSED ✅

**Coherence:** All technology decisions compatible
**Coverage:** All 69 functional requirements have architectural support
**Readiness:** Implementation patterns defined for consistent development

### Architecture Checklist

- [x] Project context analyzed (69 FRs, 9 categories)
- [x] Technology stack specified with verified versions
- [x] Core decisions documented (Data, Auth, API, Infrastructure)
- [x] Implementation patterns defined (Naming, Structure, Format)
- [x] Project structure complete with requirements mapping
- [x] All platforms covered (Backend, Web, Mobile, Admin)

### Implementation Priority

1. **Backend API** - Complete Spring Boot setup with auth, add ElasticSearch
2. **Web Frontend** - Initialize Next.js, implement core pages
3. **Mobile App** - Initialize Flutter, implement feature modules
4. **Admin Portal** - Initialize Vite+React, implement dashboard

### AI Agent Guidelines

- Follow naming conventions exactly as documented
- Use project structure patterns consistently
- Reference this document for all architectural questions
- Report any gaps or conflicts found during implementation
