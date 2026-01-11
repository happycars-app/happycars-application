# Epic 5: Buyer Enquiry & Lead Management

Buyers can enquire about cars and Happy Cars captures leads.

**FRs covered:** FR25-FR31

---

### Story 5.1: Enquiry Entity & API

As a system,
I want enquiries stored and tracked,
So that Happy Cars can follow up with buyers.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** the app starts
**Then** enquiries table exists (id, user_id, lead_id, listing_id, name, phone, email, message, status, created_at)
**And** status enum: PENDING, CALLED, VISITED
**And** POST /api/v1/enquiries creates enquiry
**And** enquiries link to leads table for unified tracking

---

### Story 5.2: Registered User Enquiry

As a registered buyer,
I want to enquire with one tap,
So that I don't re-enter my details.

**Acceptance Criteria:**

**Given** I am logged in and viewing a car
**When** I click "Enquire Now"
**Then** my name and phone are pre-filled
**And** I can add an optional message
**And** enquiry is submitted immediately
**And** I see confirmation with WhatsApp option

---

### Story 5.3: Guest Enquiry with Lead Capture

As a guest buyer,
I want to enquire about a car,
So that Happy Cars can contact me.

**Acceptance Criteria:**

**Given** I am not logged in and viewing a car
**When** I click "Enquire Now"
**Then** I must enter Name (mandatory) + Phone (mandatory) + Email (optional)
**And** phone must be verified via OTP
**And** enquiry is only captured after OTP verification
**And** I see confirmation with WhatsApp option

---

### Story 5.4: Enquiry Routing to Happy Cars

As a system,
I want all enquiries routed to Happy Cars team,
So that the team can follow up professionally.

**Acceptance Criteria:**

**Given** an enquiry is submitted
**When** it's stored
**Then** it appears in admin portal for team
**And** no direct contact between buyer and seller
**And** enquiry includes: car details, buyer info, timestamp

---

### Story 5.5: Lead Auto-Linking

As a system,
I want leads linked to accounts,
So that user history is unified.

**Acceptance Criteria:**

**Given** a guest submitted enquiry with phone X
**When** they later register with same phone X
**Then** previous enquiries are auto-linked to their account
**And** they can see their enquiry history in profile

---

### Story 5.6: Favorites / Save Cars

As a buyer,
I want to save cars I like,
So that I can compare them later.

**Acceptance Criteria:**

**Given** I am viewing a car listing
**When** I click the heart/save icon
**Then** car is added to my saved list
**And** I can view saved cars in my profile
**And** I can remove cars from saved list
**And** guests must login to save cars

---

### Story 5.7: Share Listing

As a buyer,
I want to share a car listing,
So that I can get opinions from family/friends.

**Acceptance Criteria:**

**Given** I am viewing a car detail page
**When** I click "Share"
**Then** I see options: WhatsApp, Copy Link
**And** WhatsApp opens with pre-filled message and link
**And** Copy Link copies URL to clipboard with confirmation
