---
stepsCompleted: [1, 2, 3, 4, 7, 8, 9, 10, 11]
inputDocuments:
  - docs/analysis/product-brief-happycars-application-2025-12-18.md
  - documents/prd.md
documentCounts:
  briefs: 1
  research: 0
  brainstorming: 0
  projectDocs: 0
workflowType: 'prd'
lastStep: 11
project_name: 'happycars-application'
user_name: 'Prabhakaranr'
date: '2025-12-18'
---

# Product Requirements Document - happycars-application

**Author:** Prabhakaranr
**Date:** 2025-12-18

## Executive Summary

Happy Cars is an automotive marketplace platform operating on a **consignment model** - connecting car buyers with quality-verified used vehicles while enabling individuals and dealers to sell through the Happy Cars network. Targeting all of Tamil Nadu as its initial market, the platform combines an intuitive multi-channel experience (React web + Flutter mobile) with AI-powered features including instant vehicle valuation and a RAG-based chatbot for contextual car guidance.

**Business Model:** Happy Cars acts as the trusted intermediary. Sellers submit their vehicles, Happy Cars reviews and takes approved cars to their showroom network (owned + partner locations). Buyers browse online, enquire through Happy Cars, and visit showrooms to inspect vehicles. Happy Cars earns commission by connecting buyers with the right vehicles and facilitating transactions.

The platform addresses the fragmented automotive marketplace where buyers lack reliable listings with verified vehicles, and sellers have no access to transparent valuation tools or trusted sales channels. Happy Cars bridges this gap through free vehicle submissions, instant valuation insights, quality-verified inventory at physical showrooms, and professional sales support.

### What Makes This Special

- **Consignment Model** - Happy Cars handles the entire sales process, sellers just submit and wait
- **Free Vehicle Submission** - Zero-cost for sellers to list their vehicles through Happy Cars
- **Instant AI Valuation** - Empowers sellers with market intelligence before submission (lead capture + teaser approach)
- **Physical Showrooms** - Quality-verified cars at Happy Cars owned + partner showroom locations across Tamil Nadu
- **RAG Chatbot** - Contextual AI guidance for specs, comparisons, and valuation explanations
- **Professional Sales Team** - Happy Cars team handles all buyer enquiries and dealer connections (commission model)
- **WhatsApp Integration** - Lead capture with all enquiries routed through Happy Cars team

## Project Classification

**Technical Type:** Web App + Mobile App (React + Flutter) + Separate Admin Portal
**Domain:** Automotive Marketplace (Consignment Model)
**Complexity:** High (multi-platform, AI integration, physical showroom operations)
**Project Context:** Greenfield - new project
**Geography:** All Tamil Nadu (MVP)

**Tech Stack:** Java/Spring Boot backend, PostgreSQL database, ElasticSearch for search/filters, RAG API integration for chatbot

## Success Criteria

### User Success

**Buyer (Ravi) Success Moments:**
- Finds suitable car with confidence within budget
- Gets prompt callback from Happy Cars team after enquiry
- Uses chatbot for valuation/comparison queries and gets clarity on pricing
- Visits showroom and sees the exact car from the listing
- Says: "I understand why this car is priced this way and the Happy Cars team helped me find the right one"

**Seller (Lakshmi) Success Moments:**
- Receives instant valuation teaser within 10% accuracy of market benchmarks
- Submission approved and car picked up by Happy Cars within reasonable time
- Gets notified when car is sold
- Says: "I just submitted my car details, Happy Cars handled everything else, and I got a fair price"

### Business Success

| Timeframe | Metric | Target |
|-----------|--------|--------|
| 6 months | User registrations | 50,000 |
| 6 months | Listings per month | 10,000 |
| 6 months | WhatsApp enquiries | 40,000 total |
| 12 months | Lead-to-dealer conversion | ≥20% |
| 12 months | Chatbot adoption | 30% of active users |

### Technical Success

**MVP Priority:** Core functionality working end-to-end
- All user flows functional (browse, search, submit car, enquire, chatbot)
- Lead capture working reliably (valuation teaser, enquiry forms)
- WhatsApp/contact integration routing to Happy Cars team
- Valuation engine returning results
- Admin portal operational for listing management

**Post-MVP:** Performance optimization
- Search response time <300ms
- Platform uptime 99.9%
- Mobile app rating ≥4.2 stars

### Measurable Outcomes

| Metric | 3-Month Target | 6-Month Target |
|--------|----------------|----------------|
| Registered users | 10,000 | 50,000 |
| Listings/month | 2,500 | 10,000 |
| WhatsApp enquiries | 5,000 | 40,000 |
| Valuation tool usage | 30% of sellers | 30% of sellers |
| Chatbot interaction | 20% of users | 30% of users |
| Listing approval rate | 70% | 80% |

## Product Scope

### MVP - Minimum Viable Product

**Must have for launch:**
- Home page with search, quick access buttons, featured cars
- Used Cars browse/filter (brand, price, year, mileage) - Note: City filter not needed for MVP (single showroom)
- New Cars catalog with specs and pricing (manual + API data)
- Sell Your Car submission form with instant valuation (lead capture + teaser)
- RAG Chatbot integration for car info and guidance
- Enquiry flow with lead capture (Name + Phone mandatory, Email optional for guests)
- Contact routing to Happy Cars team (not direct to dealers)
- Separate Admin portal (listings, leads, content management)
- Seller status tracking (approved/pending/rejected)
- SMS notifications for sellers (submission status, sale updates)
- Favorites/Save cars for buyers
- Share listing (WhatsApp + Copy Link)
- English UI only
- React web + Flutter mobile apps
- Photo requirements: Min 3, Max 9 + optional video (3D view deferred to post-MVP)

### Phase 2 (Post-MVP)

- Side-by-side comparison tool (compare cars on specs, price, features)
- Search sorting (by price, year, mileage)
- Search autocomplete suggestions
- 3D view for car listings
- Performance optimization (<300ms search, faster page loads)

### Phase 3 (Future)

- Financing integration (EMI calculators, loan pre-approval with partners)

### Backlog (Not Planned)

*Features explicitly deprioritized:*
- Multi-language UI (Tamil, Hindi)
- Dealer self-service portal
- Enhanced seller dashboard
- Car inspection reports
- Return & warranty programs
- Geographic expansion
- B2B marketplace
- Predictive pricing (ML)
- Advanced analytics

## User Journeys

### Journey 1: Ravi - Finding His Family's Next Car

Ravi is a 32-year-old IT professional in Chennai, married with one child, earning ₹12-15 LPA. He needs a reliable used car for his daily commute and weekend family trips. He's spent the last three weekends scrolling through CarWale and OLX, but feels overwhelmed by inconsistent listings and uncertain pricing. His colleagues have shared horror stories about unreliable private sellers and sketchy dealers.

One evening, Ravi searches "used cars Chennai" and clicks on a Happy Cars ad. He browses without logging in, filtering by his ₹5-8 lakh budget, and finds a 2019 Maruti Swift that looks promising. The listing shows professional photos and mentions the car is available at the Happy Cars showroom in Chennai. But he's unsure if ₹6.2 lakhs is a fair price.

He taps the chatbot icon and asks: "Is this Swift priced fairly?" The RAG chatbot explains that this particular car has lower mileage (28,000 km) and single ownership, which justifies the premium over similar models. It even shows him a comparison with another Swift listed at ₹5.8 lakhs that has higher mileage.

Convinced, Ravi clicks "Enquire Now." Since he's not registered, a form pops up asking for his name, mobile number (mandatory), and email (optional). He enters his details and submits. Within 30 minutes, a Happy Cars sales executive calls him, confirms his interest, and schedules a showroom visit for Saturday.

That weekend, Ravi visits the Happy Cars showroom. The Swift is exactly as shown in the photos - clean, well-maintained, with all documentation ready. The sales executive explains the car's history and offers a test drive. Ravi negotiates confidently (armed with chatbot insights) and drives home in the Swift.

**Success Moment:** "The chatbot explained pricing, the Happy Cars team called me back quickly, and when I visited the showroom, the car was exactly as advertised. No surprises, no hassle."

---

### Journey 2: Lakshmi - Selling Her First Car with Confidence

Lakshmi is a 45-year-old school teacher in Coimbatore. She's selling her 2017 Honda City to upgrade to a larger vehicle - her aging parents now need more space. She's never sold a car before and has heard that dealers lowball individual sellers. She doesn't want the hassle of meeting strangers or negotiating with buyers.

Last week, she called two local dealers. One quoted ₹4.5 lakhs, the other ₹5.8 lakhs. The ₹1.3 lakh difference left her confused and anxious. A colleague mentions Happy Cars - they handle everything, and it's free to submit your car.

That evening, Lakshmi opens the Happy Cars website and clicks "Sell Your Car." She enters her vehicle registration number. A form asks for her phone number and email first (lead capture). After entering her details, she sees a valuation teaser: **"Your 2017 Honda City is worth approximately ₹5.2 - 5.6 lakhs"** based on model year, typical mileage, and market trends.

To get a detailed valuation and proceed, she registers with her phone and email. She then fills out the submission form: car details, condition notes, uploads 5 photos (exterior, interior, dashboard, engine, documents). She submits and sees: "Submission received! Our team will review and contact you within 24 hours."

The next day, a Happy Cars representative calls her. They confirm the car details, explain the process, and schedule a pickup. Two days later, a Happy Cars team member arrives, inspects the car, and takes it to their partner showroom in Coimbatore.

Lakshmi can check her submission status anytime: "Approved - Listed for sale." Two weeks later, she gets a call: "Your car has been sold for ₹5.4 lakhs. Payment will be processed within 3 business days."

**Success Moment:** "I just filled a form and uploaded photos. Happy Cars handled the showroom, the buyers, the negotiations - everything. I got ₹5.4 lakhs without any stress."

---

### Journey 3: Priya - Keeping Happy Cars Running Smoothly

Priya is a 28-year-old operations associate at Happy Cars, managing listings, leads, and content from the separate admin portal (admin.happycars.com). Her morning starts with coffee and the metrics dashboard - 12 new car submissions overnight, 8 pending review, and 23 new buyer enquiries.

She starts with submission review. A seller submitted a Honda Civic with only 2 photos (minimum is 3). She marks it as "Photos Required" - the system sends an automated email asking for more photos. Another submission for a 2015 Swift looks good - clear photos, complete details, reasonable valuation expectation. She approves it and assigns it to the Coimbatore showroom for pickup.

Next, lead management. She sees 15 new buyer enquiries from overnight. For each lead, she reviews the car they're interested in and schedules callbacks. She assigns 8 Chennai leads to Raj (sales executive) and 7 Coimbatore leads to Meena. High-intent leads (those who provided detailed requirements) get priority callbacks.

She then creates a new listing. A car that arrived at the Chennai showroom yesterday needs to go live. She uploads the professional photos taken at the showroom, enters the verified details, sets the price based on the valuation tool, and publishes the listing.

Before lunch, she reviews the content queue. A new article on "Monsoon Car Care Tips" needs to be published. She reviews it in English, makes minor edits, and publishes it.

By end of day, submission approval rate is 78%, average lead callback time is under 2 hours, and 3 new cars are listed on the platform.

**Success Moment:** "Smooth operations from submission to listing to lead callback. Every car on the platform is verified, and every buyer gets a prompt response."

---

### Journey Requirements Summary

| Journey | Capabilities Revealed |
|---------|----------------------|
| **Ravi (Buyer)** | Search/filter, car details page, chatbot Q&A, lead capture form, enquiry to Happy Cars team, showroom visit |
| **Lakshmi (Seller)** | Lead capture, valuation teaser, registration, submission form, photo upload (min 3, max 9 + video + 3D), status tracking |
| **Priya (Admin)** | Separate admin portal, submission review, listing creation, lead assignment, callback scheduling, content management |

### Edge Cases & Recovery Paths

| Scenario | Recovery |
|----------|----------|
| Buyer can't find cars in budget | Chatbot suggests adjusting filters or nearby cities |
| Seller submits with insufficient photos | Mark as "Photos Required", automated email with instructions |
| Submission rejected for quality | Clear feedback via email + option to resubmit |
| Lead not called back in time | Escalation to supervisor, priority flag |
| Chatbot can't answer query | Show WhatsApp link to Happy Cars team |
| Car not picked up as scheduled | Reschedule notification, seller status update |
| Valuation expectation mismatch | Happy Cars team calls to discuss, may adjust or decline |

## Registration & Authentication

### Account Model
**Unified Account** - No buyer/seller classification
- Single account type for all users
- Same account can browse cars (buyer action) AND submit cars (seller action)
- User actions determine role, not account type
- No "Are you buyer or seller?" during registration

### Primary Identifier
**Phone Number** - unique, mandatory for all users

### Registration Options

**Option 1: Phone + OTP (Primary)**
```
Enter Name + Email (optional) + Phone → Send OTP → Verify → Account Created
```

**Option 2: Google Sign-in + Phone (Secondary)**
```
Click Google → Select Account → Auto-fill Name (editable) + Email (locked) → Enter Phone → Send OTP → Verify → Account Created
```

### Login Options

| Method | Flow | Available To |
|--------|------|--------------|
| Phone + OTP | Enter Phone → OTP → Logged in | All users |
| Google | Click Google → Select account → Logged in | Only users who registered via Google |

### Key Rules

| Rule | Detail |
|------|--------|
| Phone | Mandatory, unique, primary identifier |
| Email | Optional, case-insensitive, unique if provided |
| Name | Mandatory, editable |
| Password | Not for MVP (may add in future) |
| Phone Verification | Required for ALL registration paths |
| Account Linking | Previous leads auto-linked by phone number |
| One Account | Same phone = same account |

### Lead Capture Fields

| Field | Buyer Enquiry | Seller Valuation |
|-------|---------------|------------------|
| Name | Mandatory | Not required (captured at registration) |
| Phone | Mandatory (OTP verified) | Mandatory (OTP verified) |
| Email | Optional | Optional |

### Lead Capture OTP Verification
- **All lead captures require OTP verification** on phone number
- Prevents fake/typo phone numbers
- Ensures reliable lead-to-account linking
- Flow: Enter details → Send OTP → Verify → Lead captured

## Operational Details

### Valuation Algorithm
- **Approach:** Basic formula
- **Factors:** Model + Year + Mileage + Condition (self-reported)
- **Output:** Price range (e.g., ₹5.2 - 5.6 lakhs)
- **Disclaimer:** "This is an estimated valuation based on market data. Final price may vary after physical inspection."
- **Enquiry Button:** Users can click "Have questions about valuation?" → Routes query to admin platform

### Photo Flow
- **Seller submits:** Min 3, Max 9 photos + optional video + 3D view
- **Admin option:** Can replace seller photos with professional showroom photos
- **Listing display:** Shows whichever photos admin chooses (seller's or showroom's)
- **Storage:** Both sets retained for reference

### Payment Flow
- **Model:** Offline/Cash only
- All payments happen at showroom (not through platform)
- No online payment integration for MVP

### Showroom Management
- **MVP:** Single showroom location (hardcoded)
- Showroom address displayed on all listings
- Future: Multiple showroom locations

### Callback & Lead Handling
- **SLA:** Best effort (no strict SLA for MVP)
- Happy Cars team manually calls back buyers
- Leads assigned to sales team via admin portal

### Submission Verification & Approval
- **Before Approval:** Happy Cars contacts seller to verify car details
- **Verification:** Phone call or showroom visit to inspect car
- **After Verification:** Submission approved/rejected based on actual condition
- Seller can resubmit with corrections if rejected
- No auto-rejection without human review

### Submission Rejection
- If submission has issues, Happy Cars calls seller to discuss
- Seller can resubmit with corrections
- No auto-rejection without human review

## Platform-Specific Requirements

### Web Application (React)

**Architecture:**
- Single Page Application (SPA) with React
- Server-side rendering (SSR) for car listing pages to support SEO
- Modern browser support only (Chrome, Firefox, Safari, Edge - latest 2 versions)

**SEO Strategy:**
- Car listing pages must be crawlable and indexable
- Meta tags for car details (make, model, price, location)
- News/articles optimized for search traffic
- Clean URL structure for listings and content

**Responsive Design:**
- Mobile-first responsive design
- Breakpoints: Mobile (<768px), Tablet (768-1024px), Desktop (>1024px)
- Touch-friendly interactions on all screen sizes

**Performance Targets:**
- Initial page load: <3 seconds on 3G
- Search results: <500ms (ElasticSearch)
- Image optimization with lazy loading

### Mobile Application (Flutter)

**Platform Support:**
- Cross-platform: iOS and Android via Flutter
- Minimum versions: iOS 13+, Android 8.0+ (API 26)
- Feature parity with web application

**Device Features:**

| Feature | Usage |
|---------|-------|
| Camera | Photo upload for car listings |
| GPS/Location | Auto-detect city, nearby listings |
| Phone | Direct WhatsApp integration |
| Storage | Cache recently viewed listings |

**Seller Notifications (SMS as Primary):**

| Notification Type | Channel | Trigger |
|-------------------|---------|---------|
| Submission Received | SMS | Car submission received |
| Submission Approved | SMS | Car approved after verification |
| Submission Rejected | SMS | Car rejected (with callback scheduled) |
| Car Listed | SMS | Car is now live on platform |
| Car Sold | SMS | Car has been sold |

**Push Notifications (Secondary - if app installed):**

| Notification Type | Trigger |
|-------------------|---------|
| Submission Update | Status change (pending/approved/rejected/listed/sold) |
| Car Sold | Seller notified when their car is sold |

**Offline Mode:** Not supported in MVP (reduces complexity)

**App Store Compliance:**
- Apple App Store guidelines compliance
- Google Play Store policies compliance
- Privacy policy and data handling disclosures

### Shared Technical Requirements

**Language Support (MVP):**
- English only for MVP
- UI strings, content, and articles in English
- Multi-language (Tamil, Hindi) in backlog (not planned for near-term)

**Accessibility:**
- Standard WCAG 2.1 Level AA compliance
- Screen reader support for core flows
- Sufficient color contrast ratios
- Keyboard navigation (web)

**Security:**
- HTTPS everywhere
- Input validation and sanitization
- OWASP top 10 protection
- Secure API communication
- Lead data protection (phone, email)

### Implementation Considerations

**Shared Codebase Strategy:**
- API-first design enabling web and mobile to share backend
- Common design system/component library where possible
- Unified analytics tracking across platforms

**Build & Deployment:**
- CI/CD pipeline for automated testing and deployment
- Staging environment for QA
- Feature flags for gradual rollout

## Project Scoping & Phased Development

### MVP Strategy & Philosophy

**MVP Approach:** Problem-Solving + Experience MVP
- Solve the buyer/seller trust gap in automotive marketplace
- Deliver differentiated AI-powered valuation and chatbot experience
- Build foundation for dealer network expansion

**Project Complexity:** Medium scope
**Target Launch:** 3 months to MVP validation

### MVP Feature Set (Phase 1)

**Core User Journeys Supported:**
- Ravi (Buyer): Browse → Filter → Chatbot guidance → Enquiry → Callback → Showroom visit
- Lakshmi (Seller): Valuation teaser → Registration → Submit car → Status tracking
- Priya (Admin): Submission review → Listing creation → Lead assignment → Content management

**Must-Have Capabilities:**

| Category | MVP Features |
|----------|--------------|
| **Buyer** | Home page, search/filter, car details, chatbot Q&A, lead capture, enquiry to Happy Cars |
| **Seller** | Valuation teaser (lead capture), registration, car submission form, status tracking |
| **AI** | RAG chatbot for specs, comparisons, valuation explanations |
| **Admin** | Dashboard, submission review, listing creation, lead management, content editor |
| **Platform** | English UI, responsive web, mobile apps, separate admin portal |

### Post-MVP Features

**Phase 2:**
- Side-by-side comparison tool
- SMS notifications for sellers
- Performance optimization (<300ms search)

**Phase 3:**
- Financing integration (EMI calculators, loan pre-approval)

### Risk Mitigation Strategy

| Risk Type | Risk | Mitigation |
|-----------|------|------------|
| **Technical** | Valuation accuracy | Basic formula (Model + Year + Mileage + Condition), continuous calibration |
| **Technical** | RAG chatbot quality | RAG API already exists - integrate and expand knowledge base iteratively |
| **Market** | User adoption | Free submission model removes friction, consignment model builds trust |
| **Market** | Dealer engagement | Manual lead routing initially, prove value before dealer portal |
| **Resource** | Team capacity | API-first design enables parallel web/mobile development |

### MVP Success Gate

**Go/No-Go at Month 3:**
- 4 of 6 criteria met → Proceed to Phase 2
- Criteria: 10K users, 2.5K listings/month, 5K enquiries, 30% valuation usage, 20% chatbot usage, 70% approval rate

## Functional Requirements

### Car Discovery & Search

- FR1: Buyers can browse all used car listings without authentication
- FR2: Buyers can filter listings by brand, model, city, price range, year, mileage, and ownership history
- FR3: Buyers can sort listings by price, year, or popularity
- FR4: Buyers can search for cars using keywords (brand, model)
- FR5: Buyers can view car thumbnail previews with key metrics (price, year, mileage, showroom location)
- FR6: Buyers can view detailed car information including photos, specs, condition, and showroom location
- FR7: Buyers can browse new car models with specifications and on-road pricing

### Vehicle Valuation (Lead Capture Flow)

- FR8: Users can enter vehicle registration number to initiate valuation
- FR9: System requires phone (mandatory) + email (optional) capture before showing valuation
- FR10: System generates instant valuation teaser (price range) using basic formula (Model + Year + Mileage + Condition)
- FR11: Users can view valuation range with factors affecting price
- FR12: Full valuation details available after user registration

### Car Submission (Seller Flow)

- FR13: Sellers can submit car details via submission form (not create listings directly)
- FR14: Sellers must upload minimum 3 photos, maximum 9 photos of their vehicle
- FR15: Sellers can optionally upload video and 3D view of their vehicle
- FR16: Sellers can upload vehicle documentation
- FR17: Sellers can preview submission before sending
- FR18: Sellers can check submission status (pending/approved/rejected/listed/sold)

### AI Chatbot (RAG Integration)

- FR19: Users can interact with RAG chatbot from any page
- FR20: Chatbot can answer questions about car specifications
- FR21: Chatbot can explain pricing and valuation factors
- FR22: Chatbot can compare multiple car models
- FR23: Chatbot can provide contextual guidance based on user's browsing history
- FR24: Chatbot can display WhatsApp/contact link to Happy Cars team for further enquiries

### Buyer Enquiry & Lead Capture

- FR25: Registered buyers can enquire about cars directly (no re-entry of details)
- FR26: Guest buyers must provide Name + Phone (mandatory) + Email (optional) before enquiry
- FR27: Guest phone number must be verified via OTP before lead is captured
- FR28: All enquiries route to Happy Cars team (not directly to dealers/sellers)
- FR29: System captures lead details (car interested in, name, phone, email, timestamp)
- FR30: Buyers can submit contact request for new cars (same lead capture form with OTP)
- FR31: Leads are auto-linked to account if user later registers with same phone

### Admin Portal (Separate Application)

- FR32: Admins can log in to separate admin portal with role-based access control (Super Admin, Admin)

**Admin Role Access Matrix:**

| Function | Super Admin | Admin |
|----------|-------------|-------|
| Dashboard (metrics, KPIs) | ✅ Full | ❌ No |
| View Submissions | ✅ Yes | ✅ Read only |
| Approve/Reject Submissions | ✅ Yes | ❌ No |
| Create Listings | ✅ Yes | ❌ No |
| Edit Listings | ✅ Yes | ❌ No |
| View Leads/Enquiries | ✅ Yes | ✅ Yes |
| Mark Lead Status | ✅ Yes | ✅ Yes |
| Assign Leads | ✅ Yes | ❌ No |
| Search/Filter | ✅ Yes | ✅ Yes |
| Content Management | ✅ Yes | ✅ Yes |
| Callback Tracking | ✅ Yes | ✅ Yes |
| Manage Dealer Partners | ✅ Yes | ❌ No |
| User Account Management | ✅ Yes | ❌ No |
| System Settings | ✅ Yes | ❌ No |

- FR33: Super Admins can view dashboard with key metrics (submissions, listings, enquiries, callbacks)
- FR34: Super Admins can review car submissions (approve/reject/request more info)
- FR35: Super Admins can create listings from approved submissions
- FR36: Super Admins can replace seller photos with professional showroom photos (optional)
- FR37: Super Admins can edit listing details and pricing
- FR38: Admins can view all buyer enquiries/leads
- FR39: Super Admins can assign leads to sales team members for callback
- FR40: Admins can track callback status and update lead progress
- FR41: Super Admins can manage dealer partner information (manual entry)
- FR42: Admins can view valuation enquiry queries from users

### Content Management (Admin Portal)

- FR43: Admins can create and edit news/articles in English
- FR44: Admins can tag articles with categories (Reviews, Tips, Industry News)
- FR45: Users can browse news articles by category on main site

### New Cars Section

- FR46: Admins can add new car models with specs and pricing (manual entry)
- FR47: System can fetch new car data from external API (supplementary)
- FR48: Buyers can view new car specs and on-road pricing
- FR49: Buyers can enquire about new cars (routes to Happy Cars for dealer connection, OTP verified)

### User Account Management

**Account Model:**
- FR50: Unified account (no buyer/seller classification) - same account can buy or sell

**Registration Options:**
- FR51: Users can register via Phone + OTP (Name + Email optional + Phone → OTP → Verify)
- FR52: Users can register via Google Sign-in + Phone verification (Google → Auto-fill Name/Email → Enter Phone → OTP → Verify)
- FR53: Phone number is the primary identifier (mandatory, unique)
- FR54: Email is optional (case-insensitive, unique if provided)
- FR55: Name is mandatory and editable
- FR56: Google-provided email is locked (not editable), name is editable

**Login Options:**
- FR57: Users can login via Phone + OTP
- FR58: Users can login via Google (only if registered via Google)
- FR59: No password required for MVP

**Account Features:**
- FR60: Registered users can view their submission history and status
- FR61: Users receive SMS notifications for submission status changes (primary)
- FR62: Users receive push notifications if app installed (secondary)
- FR63: Previous leads (enquiries/valuations) auto-link to account by phone number

### Platform Experience

- FR64: Users can access all features via responsive web application
- FR65: Users can access all features via iOS mobile application
- FR66: Users can access all features via Android mobile application
- FR67: Users can use camera to upload car photos (mobile)
- FR68: System can detect user location for nearby showroom listings (mobile)
- FR69: All UI displayed in English (MVP)

## Non-Functional Requirements

### Performance

**MVP Baseline (Functional):**
- Page load: <5 seconds on 4G connection
- Search results: <2 seconds response
- Valuation calculation: <3 seconds response
- Chatbot response: <5 seconds for simple queries
- Image upload: Support files up to 10MB

**Optimization Targets (Post-MVP):**
- Page load: <3 seconds on 3G
- Search results: <500ms (ElasticSearch optimized)
- Platform response: <300ms for API calls

### Security

**Data Protection:**
- All data transmission over HTTPS
- Sensitive data encrypted at rest (contact details, listing data)
- Input validation and sanitization on all forms
- OWASP Top 10 vulnerability protection

**Access Control:**
- Admin authentication with secure password requirements
- Role-based access control for admin functions
- Session management with secure token handling
- Audit logging for admin actions (listing approvals, lead assignments)

**Privacy:**
- Seller authentication required to submit cars
- Contact details only shared via Happy Cars team (not exposed directly)
- Data retention policy for leads and submissions

### Scalability

**MVP Capacity:**
- Support 10,000 concurrent users
- Handle 10,000 listings in database
- Process 500 WhatsApp lead captures per day

**Growth Capacity (6 months):**
- Support 50,000 registered users
- Handle 100,000+ listings
- Process 2,000+ lead captures per day

**Architecture Approach:**
- Stateless API design for horizontal scaling
- Database indexing for search performance
- CDN for static assets and images

### Accessibility

**Compliance Level:** WCAG 2.1 Level AA

**Core Requirements:**
- Screen reader support for primary user flows
- Sufficient color contrast (4.5:1 for normal text)
- Keyboard navigation for web application
- Alt text for car images
- Form labels and error messages accessible

### Integration

**External Systems:**

| Integration | Purpose | Reliability |
|-------------|---------|-------------|
| WhatsApp API | Click-to-chat to Happy Cars team | Must work reliably |
| Valuation Data | Benchmark pricing for basic formula | Graceful fallback if unavailable |
| RAG API | Chatbot responses (existing API - just integrate) | Fallback to static FAQ if unavailable |
| SMS Gateway | OTP verification (registration + lead capture) + seller notifications | Must work reliably |
| Google OAuth | Google Sign-in for registration | Graceful fallback to Phone+OTP |
| Push Notification Services | FCM (Android), APNs (iOS) | Best effort delivery |

**Integration Resilience:**
- Retry logic for failed API calls
- Graceful degradation when external services unavailable
- Logging and monitoring for integration failures

### Reliability

**Availability Target:**
- MVP: 99% uptime (allows ~7 hours downtime/month)
- Post-MVP: 99.9% uptime

**Critical Path Protection:**
- Listing submission must never lose user data
- WhatsApp lead capture must be reliable
- Admin dashboard always accessible

**Error Handling:**
- User-friendly error messages in English
- Automatic retry for transient failures
- Clear recovery paths for user errors

### Admin Portal Requirements

**Separate Deployment:**
- Admin portal deployed separately from main application
- Dedicated subdomain (e.g., admin.happycars.com)
- Independent scaling from customer-facing apps

**Admin Portal Performance:**
- Dashboard load: <3 seconds
- Submission review: <2 seconds per record
- Lead list: Support 1000+ records with pagination

