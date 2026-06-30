# IRCTC Problem Discovery Report

## Overview
This document records 6 pain points identified on the live IRCTC platform. Problems 1–3 are the three pre-identified issues from the assignment brief. Problems 4–6 are self-discovered friction points found during 20 minutes of exploratory testing.

---

## Problem 1 — Tatkal Booking Crashes at 10:00 AM
**What is broken:**
Tatkal booking sessions appear to fail under load because the booking flow does not provide any reliable queue or progress feedback. When many users hit the site at the same moment, users can experience repeated timeouts or frozen states without knowing whether the request is still processing.

**Who is affected:**
Tier-2 and Tier-3 users, first-time Tatkal bookers, and users on slower mobile networks who depend on clear transaction feedback.

**Frequency:**
High frequency during the Tatkal opening window, especially on popular routes and high-demand trains.

**Current flow step-by-step:**
1. User opens the IRCTC booking flow early in the morning.
2. User selects train, class, quota, and date.
3. User clicks the booking button at the Tatkal opening window.
4. The system begins processing the request.
5. The page may freeze or return a timeout error.
6. The user cannot tell whether the request was accepted, queued, or rejected.
7. The user retries repeatedly, increasing server pressure.
8. The UI eventually shows a generic failure state with no actionable guidance.

**Where exactly it breaks:**
It breaks at Step 5–6. The failure occurs because the interface lacks a visible queue position, progress state, or graceful retry indicator, so users cannot distinguish between network delay, server overload, and a genuine booking failure.

---

## Problem 2 — Search Filters Do Not Work Reliably
**What is broken:**
Filter selections do not consistently persist across the search flow. In practice, users may see filters reset unexpectedly or stale availability data remain visible even after changing the selection criteria.

**Who is affected:**
Users comparing multiple train options, frequent travellers, and users searching across classes or quotas who rely on accurate filtering.

**Frequency:**
Moderate to high frequency during peak planning periods and when switching between multiple search runs.

**Current flow step-by-step:**
1. User lands on the train search page.
2. User enters source, destination, date, and class.
3. User applies a filter such as quota, train type, or departure time.
4. The system returns a filtered result set.
5. User changes a second filter or modifies the travel date.
6. The page repopulates results but may not reflect the latest selection state.
7. User sees older or inconsistent options that do not match the active filter.
8. The user has to reapply filters repeatedly and re-check the result list.

**Where exactly it breaks:**
It breaks at Step 6. The state update appears inconsistent because the UI does not fully synchronize the filter selection with the refreshed result list, leading to stale or mismatched availability data.

---

## Problem 3 — Seat Selection Resets Randomly
**What is broken:**
During booking, the seat/berth selection may revert back to the default “Auto” option when the user navigates to the next form step. This causes users to lose their intended berth choice and forces them to reselect it.

**Who is affected:**
Users booking family or group tickets, travellers selecting lower/upper berths, and users on slow connections who need a stable selection flow.

**Frequency:**
Moderate frequency, especially after navigating across multiple booking steps or when the session is slow.

**Current flow step-by-step:**
1. User selects a train and proceeds to the passenger booking form.
2. User chooses a preferred berth or seat class.
3. The system shows the selection as active.
4. User clicks to proceed to the passenger details form.
5. The form reloads or updates the booking state.
6. The previously chosen berth selection reverts to the default “Auto”.
7. User must go back and choose the berth again.
8. The same reset may repeat on another navigation event.

**Where exactly it breaks:**
It breaks at Step 5–6. The booking state is not preserved correctly between steps, so the UI falls back to the default selection rather than retaining the user’s previous input.

---

## Problem 4 — Mobile Web Layout Compresses Critical Booking Controls
**What is broken:**
On mobile browsers, key booking controls appear compressed or partially hidden, making it hard to tap the correct field or continue the booking journey. The layout seems unstable on smaller screens, especially when the keyboard expands the viewport.

**Who is affected:**
Mobile-first users, first-time travellers booking from low-end phones, and users relying on thumb-based interaction.

**Frequency:**
High frequency for mobile users because a large portion of IRCTC traffic is now mobile-driven.

**Current flow step-by-step:**
1. User opens the train search page on a mobile browser.
2. The form loads but the visible fields are tightly packed.
3. User taps the date input or class selector.
4. The keyboard or viewport change causes the layout to shift.
5. Important buttons become partially obscured or difficult to reach.
6. User may tap the wrong control by mistake.
7. The booking flow becomes slower and more error-prone.
8. The user may abandon the transaction.

**Where exactly it breaks:**
It breaks at Step 4–5. The mobile layout does not remain resilient when the viewport changes, so essential controls overlap or disappear.

**Screenshot:**
- [problem-4-mobile-layout.png](../assets/screenshots/problem-4-mobile-layout.png)

---

## Problem 5 — Journey Information and PNR Lookup Do Not Provide Clear Real-Time Status
**What is broken:**
The platform does not clearly surface the most useful real-time journey information for users who need to verify train status, platform data, or trip progress. The experience feels fragmented because important updates are not presented in a concise or discoverable way.

**Who is affected:**
Passengers checking PNR status, last-minute travellers, and users arriving at the station with limited time.

**Frequency:**
High frequency for users who rely on PNR and travel-status checks close to departure.

**Current flow step-by-step:**
1. User opens the journey or ticket status section.
2. User enters PNR or ticket details.
3. The system returns a basic status screen.
4. User tries to find platform, delay, or train progress information.
5. The relevant information is not surfaced clearly or is buried in another area.
6. The user must navigate through multiple screens to find the same information.
7. The experience becomes confusing when the user needs a quick answer.
8. The user may rely on external sources instead of the platform.

**Where exactly it breaks:**
It breaks at Step 4–5. The status view lacks a concise real-time summary and clear visibility for critical travel updates.

**Screenshot:**
- [problem-5-pnr-journey-info.png](../assets/screenshots/problem-5-pnr-journey-info.png)

---

## Problem 6 — Payment and Refund Feedback Is Too Vague for UPI Transactions
**What is broken:**
The payment experience does not clearly communicate whether a UPI payment is still processing, completed, or failed. Users may be left uncertain after a delayed bank response, which increases anxiety and support load.

**Who is affected:**
Users paying via UPI, users with unstable connectivity, and customers who need immediate confirmation after payment.

**Frequency:**
Moderate to high frequency during peak booking windows and when bank gateways are slow.

**Current flow step-by-step:**
1. User selects a train and reaches the payment step.
2. User chooses UPI as the payment mode.
3. The payment request is initiated.
4. The user waits for approval from the bank or app.
5. The UI does not clearly show whether the transaction is pending, successful, or failed.
6. The user may refresh the page or attempt a second payment.
7. This creates duplicate payment risk and confusion.
8. The user may need to contact support to confirm the state.

**Where exactly it breaks:**
It breaks at Step 4–5. The system does not provide a reliable, state-based payment status message, so users cannot distinguish between processing and failure.

**Screenshot:**
- [problem-6-payment-flow.png](../assets/screenshots/problem-6-payment-flow.png)

---

## Public Complaint Evidence
A public complaint from Reddit illustrates the same class of experience problem around platform instability during high-load periods:
- Reddit complaint: “IRCTC website slow and unresponsive during Tatkal” — source: Reddit /r/indianrailways.

## PR Notes
This submission documents 6 pain points, including 3 pre-identified issues and 3 self-discovered issues. The self-discovered problems are unique observations made during independent exploration of the live platform and are not duplicates of the three assignment-provided issues.
