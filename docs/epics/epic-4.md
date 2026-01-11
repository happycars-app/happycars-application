# Epic 4: Car Submission & Status Tracking

Sellers can submit cars with photos and track submission status.

**FRs covered:** FR13-FR18, FR60-FR62

---

### Story 4.1: Submission Entity & API

As a system,
I want submissions stored and managed,
So that sellers can submit cars and track status.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** the app starts
**Then** submissions table exists (id, user_id, brand, model, year, reg_number, mileage, condition, description, photos, video_url, status, created_at, updated_at)
**And** status enum: SUBMITTED, UNDER_REVIEW, APPROVED, REJECTED, LISTED, SOLD
**And** POST /api/v1/submissions creates submission
**And** GET /api/v1/submissions returns user's submissions

---

### Story 4.2: Car Submission Form

As a seller,
I want to submit my car details,
So that Happy Cars can review and list it.

**Acceptance Criteria:**

**Given** I am logged in
**When** I access the submission form
**Then** I can enter: registration, year, mileage, condition checklist, description
**And** condition checklist includes: scratches, dents, mechanical issues, interior wear
**And** all required fields are validated before submission

---

### Story 4.3: Photo Upload

As a seller,
I want to upload photos of my car,
So that buyers can see its condition.

**Acceptance Criteria:**

**Given** I am filling the submission form
**When** I upload photos
**Then** I must upload minimum 3 photos
**And** I can upload maximum 9 photos
**And** each photo max 5MB, JPEG/PNG only
**And** photos are auto-compressed if needed
**And** I see upload progress per photo
**And** mobile uses camera directly

---

### Story 4.4: Video Upload (Optional)

As a seller,
I want to optionally upload a video,
So that buyers get a better view.

**Acceptance Criteria:**

**Given** I am filling the submission form
**When** I choose to upload video
**Then** video is optional
**And** max 2 minutes, max 100MB
**And** any common format accepted
**And** I see upload progress

---

### Story 4.5: Submission Preview & Submit

As a seller,
I want to preview before submitting,
So that I can verify everything is correct.

**Acceptance Criteria:**

**Given** I filled all details and uploaded photos
**When** I click "Preview"
**Then** I see all entered details and photos
**And** I can go back to edit
**And** when I click "Submit", submission is created with status SUBMITTED
**And** I see confirmation message

---

### Story 4.6: Submission Status Tracking

As a seller,
I want to track my submission status,
So that I know where it stands.

**Acceptance Criteria:**

**Given** I submitted a car
**When** I visit "My Submissions"
**Then** I see all my submissions
**And** each shows current status with 4-step tracker
**And** steps: Under Review → Approved → Listed → Sold
**And** I see when status was last updated

---

### Story 4.7: SMS Notifications for Status Changes

As a seller,
I want SMS updates on my submission,
So that I stay informed without checking the app.

**Acceptance Criteria:**

**Given** my submission status changes
**When** status moves to APPROVED, REJECTED, LISTED, or SOLD
**Then** I receive SMS notification
**And** SMS includes submission summary and new status
**And** rejected SMS mentions callback will be scheduled

---

### Story 4.8: Push Notifications (Optional)

As a seller with the app installed,
I want push notifications,
So that I get instant updates.

**Acceptance Criteria:**

**Given** I have the mobile app installed
**When** my submission status changes
**Then** I receive push notification
**And** tapping notification opens submission details
**And** push is secondary to SMS (always send SMS)
