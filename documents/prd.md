# **Product Requirements Document (PRD) – Happy Cars**

> ⚠️ **SUPERSEDED DOCUMENT**
>
> **This document is outdated and no longer the source of truth.**
>
> **Current PRD Location:** `docs/prd.md`
>
> **Key Changes in New PRD:**
> - Business model: **Consignment model** (Happy Cars handles entire sales process)
> - Sellers **submit cars** (not create listings directly)
> - All buyer enquiries route to **Happy Cars team** (not directly to dealers)
> - **Unified account** (no buyer/seller classification)
> - **OTP verification** required for lead capture (phone verification before enquiry)
> - **SMS as primary** notification channel for sellers
> - **Valuation disclaimer** (estimated only, may vary after inspection)
> - **English only** for MVP
> - **Separate admin portal** with Super Admin + Admin roles
> - **Phone + OTP** as primary registration (phone is primary identifier)
> - **Single showroom** location for MVP
> - **Offline/cash payments** only
>
> **Please refer to `docs/prd.md` for current requirements.**

---

**Product Name:** Happy Cars

**Project Owner:** Happy Cars Product Team

**Document Version:** 1.0 (SUPERSEDED)

**Date:** December 12, 2025

**Prepared By:** Product Management Team

---

## 1. 🧭 Executive Summary

Happy Cars is an automotive marketplace platform aimed at **connecting car buyers with partner dealers** and enabling **end users to sell their own used vehicles for free** via easy listings and an **instant vehicle valuation tool**. Supporting both **mobile (Flutter)** and **web (React)**, with a **Java backend**, Happy Cars provides core users an engaging experience to **browse, evaluate, list, and enquire about cars** — without direct payment processing at launch.

The product will initially focus on **Tamil Nadu**, with multi-language support in **Tamil, Hindi, and English**. A generative AI **RAG chatbot** will deliver contextual car information. Admins will have centralized control through a secure dashboard.

---

## 2. 🎯 Goals & Objectives

**Primary Objectives:**

- Enable users to **browse, evaluate, and enquire** about new and used cars
- Allow end users to **sell cars free of cost** with valuation insights
- Provide an accurate, user-friendly **used car valuation tool** similar to market leaders like CarWale and CARS24 using model, vehicle number, year, etc. [Google Play+1](https://play.google.com/store/apps/details?hl=en_IN&id=com.carwale&utm_source=chatgpt.com)
- Build awareness and engagement via **news/settler content**
- Support seamless admin workflows for inventory & lead management

**Key Performance Indicators (KPIs):**

| Metric | Target |
| --- | --- |
| User registrations | 50,000 in 6 months |
| Listings created per month | 10,000 |
| Used car submissions | 5,000 |
| Contact enquiries (WhatsApp redirects) | 40,000 |
| Conversion (lead → dealer engagement) | ≥ 20% |
| Chatbot usage rate | 30% of active users |

---

## 3. 🧨 Problem Statement

Car buyers and sellers today face fragmented experiences with disparate platforms. Sellers lack transparent valuation tools, while buyers struggle to find reliable listed cars with local dealer connection and contextual guidance.

Happy Cars solves this by providing:

- **Free car sell listing for individuals**
- **Instant valuation insights**
- **Connected dealer engagement**
- **Clear, localized content & guidance**

This PRD outlines the features required to support these goals. [AltexSoft](https://www.altexsoft.com/blog/product-requirements-document/?utm_source=chatgpt.com)

---

## 4. 🎯 Target Users & Personas

### 4.1 Primary Users

1. **Car Buyers**
    - Looking to purchase new or used cars
    - Seek reliable listings, dealer information, and valuation context
2. **Car Sellers**
    - Individuals who want to list their used car for free
    - Want accurate valuation and visibility to buyers/dealers
3. **Admin Users**
    - Internal Happy Cars staff who manage inventory, listings, and enquiries

---

## 5. 📌 Features & Functional Requirements

This section details all core features by user type.

---

### 5.1 Public/End-User Facing Features

### **5.1.1 Home Page**

**Purpose:** First user interaction: highlight featured cars, search bar, categories.

**Requirements:**

- Search by model, brand, type, or registration
- Quick access buttons: Used Cars, New Cars, Sell Your Car, Chatbot
- Personalized recommendations
- Latest News/Articles carousel

**Success Metric:** Click-through rate to listing pages

---

### **5.1.2 Used Cars Section**

**Purpose:** Users browse through multiple used listings.

**Features:**

- Search & filter by brand, city, price, model year, ownership, mileage
- Sort by price, year, popularity
- Thumbnail previews with key metrics

**User Story:**

> “As a buyer, I want to filter used cars by budget so I find options in my range.”
> 

**Dependencies:** Backend search API, filters cache indexing

---

### **5.1.3 New Cars Section**

**Purpose:** Showcase new car models & dealer contacts.

**Features:**

- List of new car models, pricing, specs
- On-road price presentations
- Dealer contact request form

**Note:** New cars are informational / lead generation — not purchase. [CarWale](https://www.carwale.com/?utm_source=chatgpt.com)

---

### **5.1.4 Sell Your Car (Free Listing + Valuation)**

**Purpose:** Enable users to list their cars for free with instant valuation estimations.

**Features:**

- Input fields: vehicle number, car make, model, year, kilometers, condition
- **Instant valuation tool** based on public market data & internal algorithms (similar to CarWale & CARS24) [Google Play+1](https://play.google.com/store/apps/details?hl=en_IN&id=com.carwale&utm_source=chatgpt.com)
- Upload photos & documentation
- Preview listing before submission
- Free publish & edit listing page

**User Story:**

> “As an individual seller, I want to list my car for free and see an estimated market price so I can set a competitive price.”
> 

**Validation:** Price output must align with real-world benchmarks

---

### **5.1.5 Chatbot (RAG + AI)**

**Purpose:** Provide car info and guidance.

**Features:**

- Integrated RAG-based chatbot UI
- Connects to internal data (listings, specs, valuation logic) and external car info APIs
- Contextual help: car specs, comparisons, explain valuation

**Constraints:** Text-only; redirects to WhatsApp for human follow-ups

---

### **5.1.6 News / Settler Page**

**Purpose:** Content to engage users and boost SEO.

**Features:**

- Articles on car trends, new models, ownership tips
- Tag categories: Reviews, Tips, Industry News
- Tags link to related used/new cars

---

### **5.1.7 About Page**

**Purpose:** Brand purpose, team, mission, and privacy policy

**Features:**

- Mission statement
- FAQs
- Contact form

---

### **5.1.8 Enquiry / Contact Handling**

**Purpose:** Capture user interest and drive lead to dealers via Happy Cars team.

**Flow:**

- Contact button on listings → opens **WhatsApp** with prefilled message
- Capture lead details in backend
- Admin can assign lead to dealer

---

### 5.2 **Admin Dashboard Requirements**

**Purpose:** Empower internal users to manage listings and leads.

**Features:**

- Login / role-based access
- Dashboard metrics: total listings, active enquiries, valuation stats
- Listing admin: approve/edit/delete listings
- Lead management: view lead details, assign to dealers
- News/Articles management
- Multi-language content editor

**Supported Languages:** Tamil, Hindi, English

---

## 6. 🏗️ UX & Navigation Flows

### Home → Used Car → View Details → Contact

### Home → Sell Car → Valuation → List → Admin Approval

### Home → Chatbot → Ask Query → Redirect to Contact

Ensure UX flows are consistent across **web & mobile platforms**.

---

## 7. 🧠 Technical Architecture

**Frontend:**

- Web: **React**
- Mobile: **Flutter**
- UI: Responsive & accessible

**Backend:**

- **Java** (Spring Boot or similar)
- Database: PostgreSQL
- Search & Filters: ElasticSearch
- Chatbot: RAG layer + OpenAI + internal data

**APIs:**

- Car listing/search APIs
- Valuation engine
- Chatbot endpoints

**Analytics:** Google Analytics + in-house metrics

---

## 8. 🧪 Non-Functional Requirements

| Category | Requirement |
| --- | --- |
| Performance | <300 ms search response |
| Security | Secure login, OWASP protections |
| Scalability | Handle peak traffic spikes |
| Availability | 99.9% uptime |
| Localization | Multi-language support |

---

## 9. 📊 KPIs & Success Criteria

1. **Listings Growth**
2. **Sell-Car Conversion**
3. **Lead Engagement**
4. **Chatbot Adoption**
5. **User Retention**

---

## 10. 🛠️ Future Enhancements (Phase 2+)

- Dealer dashboard
- Authentication for sellers & buyers
- Car inspection reports
- Financing APIs integration
- Return & warranty modules similar to industry platforms