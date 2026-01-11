# Epic 7: Admin Portal - Core Operations

Admins can manage submissions, listings, and leads.

**FRs covered:** FR32-FR42

---

### Story 7.1: Admin Portal Setup & Authentication

As an admin,
I want to login to a separate admin portal,
So that I can manage platform operations.

**Acceptance Criteria:**

**Given** admin portal at admin.happycars.com
**When** I access the login page
**Then** I can login with admin credentials
**And** system validates role (Super Admin or Admin)
**And** JWT tokens are issued
**And** unauthorized users cannot access admin routes

---

### Story 7.2: Admin Entity & Role-Based Access

As a system,
I want admin roles enforced,
So that permissions are properly controlled.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** app starts
**Then** admins table exists (id, email, password_hash, name, role, created_at)
**And** role enum: SUPER_ADMIN, ADMIN
**And** API endpoints check role before allowing action
**And** audit_logs table tracks admin actions

---

### Story 7.3: Super Admin Dashboard

As a Super Admin,
I want to see key metrics,
So that I can monitor platform health.

**Acceptance Criteria:**

**Given** I am logged in as Super Admin
**When** I view dashboard
**Then** I see: total submissions, pending reviews, active listings, today's enquiries
**And** I see callback completion rate
**And** Admin role does NOT see dashboard

---

### Story 7.4: Submission Review Queue

As an admin,
I want to review car submissions,
So that I can approve quality listings.

**Acceptance Criteria:**

**Given** submissions exist
**When** I view submissions list
**Then** I see all pending submissions
**And** Super Admin can approve/reject/request more info
**And** Admin can view only (read-only)
**And** I can filter by status

---

### Story 7.5: Submission Approval Workflow

As a Super Admin,
I want to approve or reject submissions,
So that only quality cars are listed.

**Acceptance Criteria:**

**Given** I am reviewing a submission
**When** I click Approve
**Then** status changes to APPROVED and seller receives SMS
**When** I click Reject
**Then** status changes to REJECTED with reason and seller receives SMS
**When** I click "Request More Info"
**Then** status stays UNDER_REVIEW and seller is notified

---

### Story 7.6: Create Listing from Submission

As a Super Admin,
I want to create listings from approved submissions,
So that cars go live on the platform.

**Acceptance Criteria:**

**Given** submission is APPROVED
**When** I click "Create Listing"
**Then** listing form opens with submission data pre-filled
**And** I can edit details and pricing
**And** I can replace seller photos with showroom photos
**And** on save, listing is created with status LISTED
**And** seller receives SMS notification

---

### Story 7.7: Lead Management & Assignment

As an admin,
I want to manage buyer leads,
So that team can follow up promptly.

**Acceptance Criteria:**

**Given** enquiries/leads exist
**When** I view leads list
**Then** I see all buyer enquiries with car details
**And** Super Admin can assign leads to team members
**And** both roles can update lead status (PENDING → CALLED → VISITED)
**And** I can filter by status, date, assigned team member

---

### Story 7.8: Callback Tracking

As an admin,
I want to track callbacks,
So that no lead is missed.

**Acceptance Criteria:**

**Given** leads are assigned
**When** team member makes callback
**Then** they update status with notes
**And** timestamp is recorded
**And** overdue callbacks (>2 hours) are highlighted
**And** both roles can track callbacks

---

### Story 7.9: Valuation Enquiry Management

As an admin,
I want to view valuation enquiries,
So that team can follow up with sellers.

**Acceptance Criteria:**

**Given** users clicked "Have questions about valuation?"
**When** I view valuation enquiries
**Then** I see all valuation-related queries
**And** I see user's valuation result and contact info
**And** I can mark as contacted

---

### Story 7.10: Dealer Partner Management

As a Super Admin,
I want to manage dealer partners,
So that we track our network.

**Acceptance Criteria:**

**Given** dealer partnership exists
**When** I access dealer management
**Then** I can add/edit dealer info (name, location, contact)
**And** Admin role cannot access this section
**And** dealers are stored for reference (manual entry)
