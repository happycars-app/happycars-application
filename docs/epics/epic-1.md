# Epic 1: Project Foundation & User Authentication

Users can register, login, and access the platform across web and mobile.

**FRs covered:** FR50-FR59, FR63-FR69

---

### Story 1.1: Project Initialization & Backend Setup

As a developer,
I want the project infrastructure initialized,
So that I can build features on a solid foundation.

**Acceptance Criteria:**

**Given** the starter templates from architecture
**When** I run the initialization commands
**Then** Spring Boot backend compiles successfully
**And** Next.js web app runs locally
**And** Flutter mobile app builds for iOS/Android
**And** Vite admin portal starts locally

---

### Story 1.2: Database Schema & User Entity

As a system,
I want user data stored securely,
So that users can have persistent accounts.

**Acceptance Criteria:**

**Given** Flyway migrations configured
**When** the app starts
**Then** users table is created (id, phone, name, email, google_id, created_at)
**And** phone is unique and indexed
**And** email is unique if provided (nullable)

---

### Story 1.3: Phone + OTP Registration

As a user,
I want to register with my phone number,
So that I can access the platform.

**Acceptance Criteria:**

**Given** I am on the registration page
**When** I enter name, phone, and optional email
**Then** system sends OTP via SMS
**And** I can verify OTP within 5 minutes
**And** my account is created after verification
**And** I am logged in automatically

---

### Story 1.4: Google Sign-in + Phone Verification

As a user,
I want to register via Google,
So that I can use my existing Google account.

**Acceptance Criteria:**

**Given** I click "Sign in with Google"
**When** I select my Google account
**Then** my name and email are auto-filled (email locked)
**And** I must still enter and verify phone via OTP
**And** my account is created with Google ID linked

---

### Story 1.5: Phone + OTP Login

As a registered user,
I want to login with my phone,
So that I can access my account.

**Acceptance Criteria:**

**Given** I have an account
**When** I enter my phone and request OTP
**Then** I receive OTP via SMS
**And** I can login after verification
**And** I receive a JWT token (15min access, 7day refresh)

---

### Story 1.6: Google Login

As a user who registered via Google,
I want to login with Google,
So that I can access my account quickly.

**Acceptance Criteria:**

**Given** I registered via Google
**When** I click "Sign in with Google"
**Then** I am logged in directly
**And** I receive JWT tokens
**And** users who didn't register via Google cannot use Google login

---

### Story 1.7: Responsive Web Shell & Navigation

As a user,
I want a responsive web interface,
So that I can use the platform on any device.

**Acceptance Criteria:**

**Given** I access the web app
**When** I view on mobile (<768px)
**Then** I see hamburger menu navigation
**And** when I view on desktop, I see full header navigation
**And** the layout follows MUI + Teal theme

---

### Story 1.8: Mobile App Shell & Navigation

As a mobile user,
I want native iOS/Android apps,
So that I can use the platform on my phone.

**Acceptance Criteria:**

**Given** I install the app
**When** I open it
**Then** I see the home screen with navigation
**And** the design follows Flutter Material 3 + Teal theme
**And** I can navigate between main sections
