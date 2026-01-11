# Epic 2: Car Browsing & Discovery

Buyers can browse, search, filter, and view used car listings.

**FRs covered:** FR1-FR6

---

### Story 2.1: Car Listing Entity & API

As a system,
I want car listings stored and retrievable,
So that buyers can browse available cars.

**Acceptance Criteria:**

**Given** Flyway migration runs
**When** the app starts
**Then** car_listings table exists (id, brand, model, year, price, mileage, condition, status, photos, showroom_location, created_at)
**And** GET /api/v1/cars returns paginated listings
**And** listings are filterable by status (listed only shown to public)

---

### Story 2.2: Car Listings Page with Infinite Scroll

As a buyer,
I want to browse car listings,
So that I can find cars I'm interested in.

**Acceptance Criteria:**

**Given** I visit the cars page
**When** listings load
**Then** I see ListingCard components with photo, brand/model, price, year, mileage
**And** as I scroll down, more listings load (infinite scroll)
**And** I can browse without logging in

---

### Story 2.3: Search & Filter Functionality

As a buyer,
I want to search and filter cars,
So that I can find cars matching my criteria.

**Acceptance Criteria:**

**Given** I am on the listings page
**When** I enter search keywords
**Then** results filter by brand/model match
**And** I can filter by brand, price range, year, mileage
**And** filters work together (AND logic)
**And** mobile shows filters in bottom sheet

---

### Story 2.4: Car Detail Page

As a buyer,
I want to view full car details,
So that I can evaluate if this car suits my needs.

**Acceptance Criteria:**

**Given** I click on a listing card
**When** the detail page loads
**Then** I see all photos in a gallery
**And** I see full specs (brand, model, year, mileage, condition)
**And** I see showroom location
**And** I see price with breakdown
**And** the page is SSR for SEO

---

### Story 2.5: ElasticSearch Integration

As a system,
I want fast search performance,
So that buyers get results quickly.

**Acceptance Criteria:**

**Given** ElasticSearch 8.x is configured
**When** listings are created/updated
**Then** they are indexed in ElasticSearch
**And** search queries use ElasticSearch
**And** search returns results in <2 seconds
