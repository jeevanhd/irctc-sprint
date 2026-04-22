# IRCTC Problem Discovery — Part A

## Summary

- Total problems documented: 6
- 3 given + 3 self-discovered
- Platform explored: irctc.co.in
- Devices used: Desktop Chrome, Mobile Chrome
- Date explored: 21 April 2026

---

## Problem 1: Tatkal Booking Crashes at 10:00 AM [Given]

**What is broken:**
During Tatkal opening hours, IRCTC becomes slow or unresponsive under peak traffic. Users often cannot complete booking before quota sells out.

**Affected users:**
Daily Tatkal travellers, emergency travellers, agents, office commuters. Potentially thousands of concurrent users at 10:00 AM.

**Frequency:**
Daily recurring during Tatkal opening window (especially 10:00 AM AC, 11:00 AM Non-AC depending rules).

**Current flow — step by step:**

1. User opens IRCTC around 9:50 AM.
2. User logs in and prepares passenger details.
3. User refreshes train list before 10:00 AM.
4. Tatkal quota opens at 10:00 AM.
5. User clicks Book Now immediately.
6. Site becomes slow / spinner appears / request stalls.
7. User retries or refreshes page.
8. Session expires or captcha resets.
9. User re-enters flow.
10. Tatkal quota becomes unavailable.

**Where exactly it breaks:**
Step 6 — booking request submission layer under sudden traffic spike. No queue system or transparent load handling feedback.

---

## Problem 2: Search Filters Do Not Work Reliably [Given]

**What is broken:**
Applying filters does not always refresh results correctly. Some filters reset after navigation or show inconsistent train lists.

**Affected users:**
All train search users, especially first-time users comparing many trains.

**Frequency:**
Frequent during repeated searches and back-navigation.

**Current flow — step by step:**

1. User enters source and destination.
2. User searches trains.
3. Results page loads.
4. User selects Sleeper filter.
5. User selects Available seats only.
6. User sees little or delayed result change.
7. User opens train detail page.
8. User clicks back.
9. Previous filters disappear or partially reset.
10. User repeats filtering manually.

**Where exactly it breaks:**
Step 6 and Step 9 — filter state management between UI and search results is inconsistent.

---

## Problem 3: Seat Selection Resets [Given]

**What is broken:**
Selected berth or seat preference is not consistently preserved when moving to passenger details or next booking stage.

**Affected users:**
Senior citizens, women travellers, families, users needing lower berth.

**Frequency:**
Intermittent; higher on mobile browsers.

**Current flow — step by step:**

1. User searches train.
2. User selects available class.
3. User opens booking flow.
4. User chooses lower berth / preferred berth.
5. User clicks Proceed.
6. Passenger detail page loads.
7. Preference appears reset or defaulted.
8. User manually re-enters preference.
9. User loses confidence in final allotment.

**Where exactly it breaks:**
Step 6–7 during state transfer between seat preference UI and passenger form.

---

## Problem 4: Session Timeout Without Warning [Self-discovered]

**How I found it:**
While spending time in booking flow entering passenger details.

**Screenshot or description:**
Passenger details page returned to login/home after inactivity.

**What is broken:**
Session expires suddenly without countdown or warning, causing data loss.

**Affected users:**
Slow typers, elderly users, users filling many passengers.

**Frequency:**
Common during long booking flows.

**Current flow — step by step:**

1. User starts booking.
2. Passenger form opens.
3. User enters multiple names/ages.
4. User pauses for ID details.
5. Session silently expires.
6. User clicks continue.
7. Redirect occurs.
8. Entered data lost.

**Where exactly it breaks:**
Step 5 — no session expiry warning or auto-save.

---

## Problem 5: Mobile Website Layout Issues [Self-discovered]

**How I found it:**
Opened irctc.co.in in mobile Chrome.

**Screenshot or description:**
Buttons crowded, filters hard to tap, horizontal scroll appears.

**What is broken:**
Desktop-heavy layout creates poor mobile usability.

**Affected users:**
Users booking from phone browser.

**Frequency:**
Persistent on smaller screens.

**Current flow — step by step:**

1. User opens mobile site.
2. Homepage loads.
3. User searches route.
4. Results page opens.
5. Filter controls appear cramped.
6. User mis-taps controls.
7. Needs zoom/scroll repeatedly.
8. Search becomes slower.

**Where exactly it breaks:**
Step 5–6 responsive layout and touch target sizing.

---

## Problem 6: Cancellation Refund Clarity Poor [Self-discovered]

**How I found it:**
Visited cancellation / ticket management area.

**Screenshot or description:**
Refund rules shown in fragmented text with little immediate clarity.

**What is broken:**
Users cannot quickly understand refund amount, deduction, and timeline.

**Affected users:**
Users cancelling urgent or waitlisted tickets.

**Frequency:**
Any cancellation attempt.

**Current flow — step by step:**

1. User opens booked tickets.
2. Selects cancel option.
3. Looks for refund estimate.
4. Finds policy-heavy text.
5. No clear instant refund summary.
6. User hesitates to cancel.
7. Searches elsewhere for rules.

**Where exactly it breaks:**
Step 3–5 information architecture fails to present clear refund summary.

---
