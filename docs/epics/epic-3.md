# Epic 3: Seller Valuation & Lead Capture

Sellers get instant valuation and Happy Cars captures leads.

**FRs covered:** FR8-FR12, FR27

---

### Story 3.1: Lead Entity & Valuation API

As a system,
I want to capture and store leads,
So that Happy Cars can follow up with potential sellers.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** the app starts
**Then** leads table exists (id, phone, email, name, type, vehicle_reg, valuation_result, created_at)
**And** valuations table exists (id, lead_id, brand, model, year, mileage, condition, min_price, max_price)
**And** POST /api/v1/valuations/calculate returns price range

---

### Story 3.2: Valuation Entry Page

As a seller,
I want to start the valuation process,
So that I can know my car's worth.

**Acceptance Criteria:**

**Given** I visit the "Sell Your Car" page
**When** I enter my vehicle registration number
**Then** I am prompted for phone (mandatory) + email (optional)
**And** I see trust message explaining why phone is needed
**And** I cannot proceed without phone entry

---

### Story 3.3: OTP Verification for Lead Capture

As a system,
I want verified phone numbers,
So that leads are genuine and contactable.

**Acceptance Criteria:**

**Given** I enter my phone number
**When** I click "Get Valuation"
**Then** OTP is sent via SMS
**And** I must verify OTP within 5 minutes
**And** OTP is stored in Redis with 5-min TTL
**And** lead is only captured after OTP verification

---

### Story 3.4: Instant Valuation Result

As a seller,
I want to see my car's estimated value,
So that I can decide whether to sell.

**Acceptance Criteria:**

**Given** I verified my phone
**When** valuation is calculated
**Then** I see price range (e.g., "₹5.2 - 5.6 lakhs")
**And** I see factors affecting price (year, mileage, condition)
**And** I see disclaimer: "Estimated valuation. Final price may vary."
**And** I see "Have questions?" link to enquire

---

### Story 3.5: Full Valuation After Registration

As a seller,
I want detailed valuation info,
So that I can make informed decisions.

**Acceptance Criteria:**

**Given** I am a guest with valuation teaser
**When** I click "Get Full Details"
**Then** I am prompted to register
**And** after registration, I see detailed breakdown
**And** my lead is auto-linked to my new account
