# Epic 6: AI Chatbot Integration

Users get AI-powered help for specs, pricing, and comparisons.

**FRs covered:** FR19-FR24

---

### Story 6.1: Chatbot Widget Component

As a user,
I want to see the chatbot on every page,
So that I can get help anytime.

**Acceptance Criteria:**

**Given** I am on any page
**When** the page loads
**Then** I see chatbot icon (collapsed by default)
**And** chatbot does NOT auto-expand (user-initiated only)
**And** clicking icon opens chat interface
**And** chatbot is lazy-loaded (doesn't block page render)

---

### Story 6.2: RAG API Integration

As a system,
I want to connect to the RAG API,
So that chatbot can answer questions intelligently.

**Acceptance Criteria:**

**Given** RAG API is configured
**When** user sends a message
**Then** message is sent to RAG API with context
**And** response is received within 5 seconds
**And** if API fails, show fallback message with WhatsApp link

---

### Story 6.3: Car Specification Questions

As a buyer,
I want to ask about car specs,
So that I understand the vehicle better.

**Acceptance Criteria:**

**Given** I am chatting with the bot
**When** I ask about specs (e.g., "What's the mileage of this Swift?")
**Then** bot provides accurate spec information
**And** bot uses current car context if on detail page
**And** response includes relevant details from listing

---

### Story 6.4: Pricing & Valuation Explanations

As a user,
I want to understand pricing,
So that I know if a car is fairly priced.

**Acceptance Criteria:**

**Given** I am viewing a car or valuation
**When** I ask about pricing (e.g., "Is this price fair?")
**Then** bot explains factors affecting price
**And** mentions mileage, year, condition, ownership
**And** provides comparison context if available

---

### Story 6.5: Car Comparison Queries

As a buyer,
I want to compare cars via chat,
So that I can make informed decisions.

**Acceptance Criteria:**

**Given** I ask to compare (e.g., "Compare Swift vs i20")
**When** bot processes the request
**Then** bot provides comparison on key specs
**And** includes price range differences
**And** suggests which might suit my needs

---

### Story 6.6: Contextual Guidance

As a user,
I want relevant suggestions,
So that I discover options I might have missed.

**Acceptance Criteria:**

**Given** I am browsing the platform
**When** I open chatbot
**Then** bot can reference my browsing context
**And** suggest similar cars in my price range
**And** offer help based on current page

---

### Story 6.7: Fallback to Human Support

As a user,
I want human help when bot can't answer,
So that I'm never stuck.

**Acceptance Criteria:**

**Given** bot cannot answer my query
**When** response is uncertain or fails
**Then** bot shows "Talk to our team" option
**And** clicking opens WhatsApp with pre-filled context
**And** includes car details if applicable
