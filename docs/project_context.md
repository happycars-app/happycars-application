# Project Context for AI Agents

_Critical rules and patterns for implementing Happy Cars. Read before coding._

---

## Technology Stack

| Layer | Technology | Version |
|-------|------------|---------|
| Backend | Spring Boot + Java | 3.2.0 / 21 |
| Database | PostgreSQL | Latest |
| Cache | Redis | Latest |
| Search | ElasticSearch | 8.x |
| Web | Next.js + MUI | 14.2.x / 5.16.x |
| Mobile | Flutter + BLoC + Dio | 3.27+ / 8.1.x / 5.7.0 |
| Admin | Vite + React + MUI | Latest / 5.16.x |

---

## Critical Rules

### Backend (Spring Boot)

1. **Phone is primary ID** - All users identified by phone number, not email
2. **OTP required for all leads** - Never capture leads without OTP verification
3. **Use Flyway migrations** - `V{n}__description.sql` format
4. **Redis for OTP** - 5-min TTL, never store in database
5. **JWT + Redis** - Access: 15min, Refresh: 7 days in Redis, blacklist on logout
6. **snake_case in DB** - Tables: `car_listings`, Columns: `created_at`
7. **camelCase in API** - JSON responses use camelCase
8. **GlobalExceptionHandler** - All errors through `@ControllerAdvice`

### API Design

1. **Base path**: `/api/v1/`
2. **Plural resources**: `/cars`, `/submissions`, `/enquiries`
3. **Standard error format**:
```json
{
  "error": "VALIDATION_ERROR",
  "message": "Phone number is required",
  "details": { "field": "phone" }
}
```
4. **Public endpoints**: `/api/v1/auth/**`, `/api/v1/cars/**` (GET), `/api/v1/valuation`
5. **Protected**: `/api/v1/submissions/**`, `/api/v1/profile/**`
6. **Admin only**: `/api/v1/admin/**`

### Web (Next.js)

1. **App Router** - Use `src/app/` structure
2. **SSR for SEO** - Car listing pages must be server-rendered
3. **MUI theme** - Teal primary (#0D9488), follow `styles/theme.ts`
4. **Skeleton loaders** - Never spinners (per UX spec)
5. **Chatbot lazy-load** - Don't block initial page render

### Mobile (Flutter)

1. **Feature-first structure** - `lib/features/{feature}/bloc|data|ui`
2. **BLoC naming**: `AuthBloc`, `AuthLoginRequested`, `AuthAuthenticated`
3. **snake_case files** - `login_screen.dart`, `auth_bloc.dart`
4. **Pin Dio to 5.7.0** - 5.8.x has web issues

---

## Naming Conventions

| Context | Convention | Example |
|---------|------------|---------|
| DB tables | snake_case, plural | `car_listings` |
| DB columns | snake_case | `created_at` |
| Java classes | PascalCase | `CarListing` |
| Java services | `{Entity}Service` | `CarListingService` |
| React components | PascalCase | `ListingCard.tsx` |
| Flutter files | snake_case | `listing_card.dart` |
| API endpoints | lowercase, plural | `/api/v1/cars` |
| JSON fields | camelCase | `createdAt` |

---

## Business Logic

1. **Consignment model** - Sellers submit, Happy Cars verifies, approves, lists, sells
2. **Submission states**: `SUBMITTED` → `UNDER_REVIEW` → `APPROVED`/`REJECTED` → `LISTED` → `SOLD`
3. **Lead states**: `PENDING` → `CALLED` → `VISITED`
4. **All enquiries route to Happy Cars** - No direct buyer-seller contact
5. **Unified accounts** - Same account can buy and sell (no role classification)
6. **Google OAuth still needs phone** - Phone is always required

---

## Don't Do

- Don't expose stack traces to users
- Don't store OTP codes in database (use Redis)
- Don't use spinners (use skeletons)
- Don't auto-trigger chatbot (user-initiated only)
- Don't use Dio 5.8.x in Flutter
- Don't use Next.js 15 with MUI 6 and Turbopack
- Don't use ElasticSearch 7.x with Spring Boot 3.x

---

## Reference Documents

- **PRD**: `docs/prd.md` (69 functional requirements)
- **UX Spec**: `docs/ux-design-specification.md`
- **Architecture**: `docs/architecture.md`
