# Epic 8: Content & New Cars

Users can browse news articles and new car catalog.

**FRs covered:** FR7, FR43-FR49

---

### Story 8.1: Content Entity & API

As a system,
I want articles stored and retrievable,
So that users can browse news content.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** app starts
**Then** articles table exists (id, title, slug, content, category, author_id, status, published_at, created_at)
**And** category enum: REVIEWS, TIPS, INDUSTRY_NEWS
**And** status enum: DRAFT, PUBLISHED
**And** GET /api/v1/articles returns published articles

---

### Story 8.2: Admin Content Editor

As an admin,
I want to create and edit articles,
So that we can publish news content.

**Acceptance Criteria:**

**Given** I am logged in as admin
**When** I access content editor
**Then** I can create new article with title, content, category
**And** I can save as draft or publish immediately
**And** I can edit existing articles
**And** both Super Admin and Admin can manage content

---

### Story 8.3: Article Categories & Tagging

As an admin,
I want to categorize articles,
So that users can browse by topic.

**Acceptance Criteria:**

**Given** I am creating/editing an article
**When** I select category
**Then** I can choose: Reviews, Tips, Industry News
**And** category is saved with article
**And** articles can be filtered by category

---

### Story 8.4: News Browsing Page

As a user,
I want to browse news articles,
So that I can stay informed about cars.

**Acceptance Criteria:**

**Given** I visit the news section
**When** page loads
**Then** I see list of published articles
**And** I can filter by category
**And** I see article thumbnail, title, date, category
**And** clicking opens full article
**And** articles are in English only

---

### Story 8.5: New Car Entity & API

As a system,
I want new car data stored,
So that users can browse new car catalog.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** app starts
**Then** new_cars table exists (id, brand, model, variant, specs, ex_showroom_price, on_road_price, images, created_at)
**And** GET /api/v1/new-cars returns catalog
**And** data can be manual or from external API

---

### Story 8.6: Admin New Car Management

As a Super Admin,
I want to manage new car catalog,
So that buyers see accurate information.

**Acceptance Criteria:**

**Given** I am logged in as Super Admin
**When** I access new car management
**Then** I can add new car with specs and pricing
**And** I can edit existing entries
**And** I can upload images
**And** pricing includes ex-showroom and on-road

---

### Story 8.7: New Car Browsing Page

As a buyer,
I want to browse new cars,
So that I can explore options.

**Acceptance Criteria:**

**Given** I visit new cars section
**When** page loads
**Then** I see new car catalog with images
**And** I can view specs and on-road pricing
**And** I can filter by brand
**And** clicking opens detail page with full specs

---

### Story 8.8: New Car Enquiry

As a buyer,
I want to enquire about a new car,
So that Happy Cars can connect me with dealers.

**Acceptance Criteria:**

**Given** I am viewing a new car
**When** I click "Enquire"
**Then** same lead capture form as used cars
**And** phone must be verified via OTP
**And** enquiry routes to Happy Cars team
**And** team connects buyer with dealer partner
