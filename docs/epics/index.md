---
stepsCompleted: [1, 2, 3, 4]
status: 'complete'
completedAt: '2026-01-11'
inputDocuments:
  - docs/prd.md
  - docs/architecture.md
  - docs/ux-design-specification.md
workflowType: 'epics'
lastStep: 4
project_name: 'happycars-application'
user_name: 'Prabhakaranr'
date: '2026-01-11'
---

# Happy Cars - Epic Breakdown

## Overview

This document provides the complete epic and story breakdown for Happy Cars, decomposing the requirements from the PRD, UX Design, and Architecture into implementable stories.

## Requirements Inventory

### Functional Requirements

**Car Discovery & Search (FR1-FR7)**
- FR1: Buyers can browse all used car listings without authentication
- FR2: Buyers can filter listings by brand, model, city, price range, year, mileage, and ownership history
- FR3: Buyers can sort listings by price, year, or popularity
- FR4: Buyers can search for cars using keywords (brand, model)
- FR5: Buyers can view car thumbnail previews with key metrics (price, year, mileage, showroom location)
- FR6: Buyers can view detailed car information including photos, specs, condition, and showroom location
- FR7: Buyers can browse new car models with specifications and on-road pricing

**Vehicle Valuation (FR8-FR12)**
- FR8: Users can enter vehicle registration number to initiate valuation
- FR9: System requires phone (mandatory) + email (optional) capture before showing valuation
- FR10: System generates instant valuation teaser (price range) using basic formula
- FR11: Users can view valuation range with factors affecting price
- FR12: Full valuation details available after user registration

**Car Submission (FR13-FR18)**
- FR13: Sellers can submit car details via submission form
- FR14: Sellers must upload minimum 3 photos, maximum 9 photos
- FR15: Sellers can optionally upload video
- FR16: Sellers can upload vehicle documentation
- FR17: Sellers can preview submission before sending
- FR18: Sellers can check submission status (pending/approved/rejected/listed/sold)

**AI Chatbot (FR19-FR24)**
- FR19: Users can interact with RAG chatbot from any page
- FR20: Chatbot can answer questions about car specifications
- FR21: Chatbot can explain pricing and valuation factors
- FR22: Chatbot can compare multiple car models
- FR23: Chatbot can provide contextual guidance based on browsing history
- FR24: Chatbot displays WhatsApp/contact link for further enquiries

**Buyer Enquiry & Lead Capture (FR25-FR31)**
- FR25: Registered buyers can enquire about cars directly
- FR26: Guest buyers must provide Name + Phone (mandatory) + Email (optional)
- FR27: Guest phone number must be verified via OTP
- FR28: All enquiries route to Happy Cars team
- FR29: System captures lead details (car, name, phone, email, timestamp)
- FR30: Buyers can submit contact request for new cars (OTP verified)
- FR31: Leads auto-link to account if user registers with same phone

**Admin Portal (FR32-FR42)**
- FR32: Admins can log in with role-based access (Super Admin, Admin)
- FR33: Super Admins can view dashboard with key metrics
- FR34: Super Admins can review car submissions (approve/reject/request more info)
- FR35: Super Admins can create listings from approved submissions
- FR36: Super Admins can replace seller photos with showroom photos
- FR37: Super Admins can edit listing details and pricing
- FR38: Admins can view all buyer enquiries/leads
- FR39: Super Admins can assign leads to sales team
- FR40: Admins can track callback status and update lead progress
- FR41: Super Admins can manage dealer partner information
- FR42: Admins can view valuation enquiry queries

**Content Management (FR43-FR45)**
- FR43: Admins can create and edit news/articles in English
- FR44: Admins can tag articles with categories
- FR45: Users can browse news articles by category

**New Cars Section (FR46-FR49)**
- FR46: Admins can add new car models with specs and pricing
- FR47: System can fetch new car data from external API
- FR48: Buyers can view new car specs and on-road pricing
- FR49: Buyers can enquire about new cars (OTP verified)

**User Account Management (FR50-FR63)**
- FR50: Unified account (no buyer/seller classification)
- FR51: Users can register via Phone + OTP
- FR52: Users can register via Google Sign-in + Phone verification
- FR53: Phone number is primary identifier (mandatory, unique)
- FR54: Email is optional (case-insensitive, unique if provided)
- FR55: Name is mandatory and editable
- FR56: Google-provided email is locked, name is editable
- FR57: Users can login via Phone + OTP
- FR58: Users can login via Google (if registered via Google)
- FR59: No password required for MVP
- FR60: Registered users can view submission history and status
- FR61: Users receive SMS notifications for submission status changes
- FR62: Users receive push notifications if app installed
- FR63: Previous leads auto-link to account by phone number

**Platform Experience (FR64-FR69)**
- FR64: Users can access all features via responsive web application
- FR65: Users can access all features via iOS mobile application
- FR66: Users can access all features via Android mobile application
- FR67: Users can use camera to upload car photos (mobile)
- FR68: System can detect user location for nearby showroom listings
- FR69: All UI displayed in English (MVP)

### Non-Functional Requirements

**Performance**
- NFR1: Page load <5 seconds on 4G connection (MVP)
- NFR2: Search results <2 seconds response
- NFR3: Valuation calculation <3 seconds response
- NFR4: Chatbot response <5 seconds for simple queries
- NFR5: Image upload support files up to 10MB

**Security**
- NFR6: All data transmission over HTTPS
- NFR7: Sensitive data encrypted at rest
- NFR8: Input validation and sanitization on all forms
- NFR9: OWASP Top 10 vulnerability protection
- NFR10: Role-based access control for admin functions
- NFR11: Session management with secure token handling
- NFR12: Audit logging for admin actions

**Scalability**
- NFR13: Support 10,000 concurrent users (MVP)
- NFR14: Handle 10,000 listings in database
- NFR15: Process 500 lead captures per day

**Accessibility**
- NFR16: WCAG 2.1 Level AA compliance
- NFR17: Screen reader support for primary user flows
- NFR18: Sufficient color contrast (4.5:1)
- NFR19: Keyboard navigation for web application

**Reliability**
- NFR20: 99% uptime (MVP)
- NFR21: Listing submission must never lose user data
- NFR22: User-friendly error messages in English

### Additional Requirements

**From Architecture:**
- AR1: Spring Boot 3.2 + Java 21 backend (existing)
- AR2: Next.js 14.2 + MUI 5.16 for web frontend
- AR3: Flutter 3.27+ + BLoC + Dio 5.7.0 for mobile
- AR4: Vite + React + MUI 5.16 for admin portal
- AR5: PostgreSQL database with Flyway migrations
- AR6: Redis for OTP (5-min TTL), JWT blacklist, session storage
- AR7: ElasticSearch 8.x for search/filters
- AR8: JWT + Redis authentication (access: 15min, refresh: 7 days)
- AR9: REST API with /api/v1/ versioning
- AR10: Standard error response format (JSON)

**From UX:**
- UX1: Teal primary color (#0D9488)
- UX2: MUI design system (web) + Flutter Material 3 (mobile)
- UX3: Skeleton loaders (not spinners)
- UX4: Chatbot: always visible, collapsed, user-initiated only
- UX5: Mobile navigation: hamburger menu
- UX6: Infinite scroll pagination
- UX7: Bottom sheet for mobile filters

### FR Coverage Map

| FR | Epic | Description |
|----|------|-------------|
| FR1-FR6 | Epic 2 | Car Browsing & Discovery |
| FR7 | Epic 8 | New Cars browsing |
| FR8-FR12 | Epic 3 | Seller Valuation |
| FR13-FR18 | Epic 4 | Car Submission |
| FR19-FR24 | Epic 6 | AI Chatbot |
| FR25-FR31 | Epic 5 | Buyer Enquiry |
| FR32-FR42 | Epic 7 | Admin Portal |
| FR43-FR49 | Epic 8 | Content & New Cars |
| FR50-FR59 | Epic 1 | User Authentication |
| FR60-FR62 | Epic 4 | Status Tracking & Notifications |
| FR63 | Epic 1 | Lead auto-linking |
| FR64-FR69 | Epic 1 | Platform Experience |

## Epic List

### [Epic 1: Project Foundation & User Authentication](./epic-1.md)
Users can register, login, and access the platform across web and mobile.
**FRs covered:** FR50-FR59, FR63-FR69
**Stories:** 8

### [Epic 2: Car Browsing & Discovery](./epic-2.md)
Buyers can browse, search, filter, and view used car listings.
**FRs covered:** FR1-FR6
**Stories:** 5

### [Epic 3: Seller Valuation & Lead Capture](./epic-3.md)
Sellers get instant valuation and Happy Cars captures leads.
**FRs covered:** FR8-FR12, FR27
**Stories:** 5

### [Epic 4: Car Submission & Status Tracking](./epic-4.md)
Sellers can submit cars with photos and track submission status.
**FRs covered:** FR13-FR18, FR60-FR62
**Stories:** 8

### [Epic 5: Buyer Enquiry & Lead Management](./epic-5.md)
Buyers can enquire about cars and Happy Cars captures leads.
**FRs covered:** FR25-FR31
**Stories:** 7

### [Epic 6: AI Chatbot Integration](./epic-6.md)
Users get AI-powered help for specs, pricing, and comparisons.
**FRs covered:** FR19-FR24
**Stories:** 7

### [Epic 7: Admin Portal - Core Operations](./epic-7.md)
Admins can manage submissions, listings, and leads.
**FRs covered:** FR32-FR42
**Stories:** 10

### [Epic 8: Content & New Cars](./epic-8.md)
Users can browse news articles and new car catalog.
**FRs covered:** FR7, FR43-FR49
**Stories:** 8

---

**Total: 8 Epics, 58 Stories covering all 69 FRs**
