# IRCTC Feature Specifications — Part B

---

## Feature Spec 1: Tatkal Smart Queue System

### Problem Statement

Part A showed that Tatkal users face crashes and failed booking attempts exactly at peak opening time. Thousands of users hit the platform simultaneously, causing load spikes and zero transparency.

### Current State (from Part A)

Users log in before 10 AM, click Book Now when quota opens, then face freezing, retries, session resets, and sold-out quota.

### Proposed Solution

Introduce a virtual queue. At Tatkal opening, users are placed into a queue with live wait time, queue position, and readiness checks.

### Proposed User Flow — Step by Step

1. User logs in before 10 AM.
2. User joins Tatkal queue.
3. Queue number shown.
4. Progress updates every few seconds.
5. When turn arrives, booking page unlocks.
6. User completes booking in reserved 3-minute slot.

### Technical Implementation Plan

**System components affected:**

- Booking gateway
- Queue manager
- Session service
- Notification system

**New data requirements:**

- Queue token
- Queue timestamp
- Reserved booking slot

**API changes:**

- POST /tatkal/join
- GET /tatkal/status

**Frontend changes:**

- Queue screen
- Progress bar
- Slot timer

**Third-party services:**

- Redis for queue state

### Success Metrics

- 70% fewer failed requests
- 50% lower refresh traffic
- Higher successful bookings

### Edge Cases and Constraints

- User refreshes page
- User misses slot
- Queue server outage fallback = normal booking flow

---

## Feature Spec 2: Persistent Smart Filters

### Problem Statement

Users repeatedly lose filters or see inconsistent search results.

### Current State

Filters like Sleeper / Morning / Available only often reset after back navigation.

### Proposed Solution

Sticky filters saved per session with instant result refresh.

### Proposed User Flow

1. Search trains
2. Apply filters
3. Results refresh instantly
4. Open train detail
5. Return back
6. Filters remain active

### Technical Implementation Plan

**System components affected:**

- Search API
- Frontend state layer

**New data requirements:**

- Session filter preferences

**API changes:**

- GET /trains?filters=

**Frontend changes:**

- Filter chips
- Saved state

### Success Metrics

- 40% faster repeat searches
- Lower bounce rate
- Higher booking continuation

### Edge Cases

- No matching results
- Expired session resets defaults

---

## Feature Spec 3: Confirmed Seat Preference Sync

### Problem Statement

Users choose lower berth or preference but settings reset.

### Current State

Preference chosen earlier disappears on passenger form.

### Proposed Solution

Seat preference lock shown across all steps with confirmation badge.

### Proposed User Flow

1. Choose berth
2. Continue
3. Preference summary visible
4. Edit if needed
5. Submit booking

### Technical Implementation Plan

**System components affected:**

- Booking state service
- Passenger form

**New data requirements:**

- Seat preference field

**API changes:**

- PATCH /booking/preferences

**Frontend changes:**

- Summary card
- Edit button

### Success Metrics

- 80% reduction preference resets

### Edge Cases

- Preference unavailable after allocation

---

## Feature Spec 4: Auto Save + Session Warning

### Problem Statement

Users lose entered data due to silent timeout.

### Current State

Long forms expire without warning.

### Proposed Solution

Autosave form every 15 sec + timeout warning modal.

### Proposed User Flow

1. Fill passenger details
2. Draft autosaves
3. Warning at 2 mins left
4. Extend session or continue

### Technical Plan

Session service, draft storage, modal UI.

### Success Metrics

- Lower drop-offs
- Fewer re-entry attempts

---

## Feature Spec 5: Mobile First Responsive Booking UI

### Problem Statement

IRCTC mobile browser experience is cramped and hard to use.

### Current State

Small tap targets, horizontal scrolling, cluttered filters.

### Proposed Solution

Responsive redesign for mobile browsers.

### Proposed User Flow

Large buttons, bottom sticky CTA, collapsible filters.

### Technical Plan

Frontend CSS rebuild + responsive components.

### Success Metrics

- Lower mobile abandonment
- Faster booking completion

---

## Feature Spec 6: Refund Clarity Calculator

### Problem Statement

Users do not know refund amount before cancellation.

### Current State

Dense policy text instead of clear numbers.

### Proposed Solution

Instant refund estimate before cancellation.

### Proposed User Flow

1. Open booking
2. Click cancel
3. See refund amount + deduction + ETA
4. Confirm cancellation

### Technical Plan

Rules engine + fare calculator UI.

### Success Metrics

- More confident cancellations
- Fewer support queries

---
