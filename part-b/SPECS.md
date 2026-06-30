# Part B — AI Feature Specification

## Feature Name
Smart Booking Copilot for IRCTC

## Objective
Reduce booking friction during high-load situations by giving users real-time guidance, detecting unstable flows, and protecting them from avoidable failures.

## Problem Context
IRCTC users often face three major issues during booking:
- Tatkal sessions fail under load with poor feedback.
- Search filters may reset or show stale data.
- Seat selection can be lost while moving between steps.

## Proposed Solution
A lightweight AI-assisted booking layer that monitors the current booking journey and provides proactive help such as:
- retry timing suggestions during peak Tatkal windows,
- filter consistency warnings when stale results are detected,
- seat-selection preservation prompts before navigation,
- payment status guidance for pending or delayed UPI transactions.

## Functional Requirements
1. Detect when the user is entering a high-traffic booking window.
2. Show a simple “booking health” indicator with status messages such as busy, stable, or delayed.
3. Recommend the best moment to retry when a booking request is likely to fail.
4. Flag inconsistent filter behavior and suggest reapplying filters.
5. Preserve the user’s selected berth/seat choice when the flow moves to the next step.
6. Provide clear transaction-state messages for payment and refund processes.

## Non-Functional Requirements
- Fast response time under 2 seconds for UI updates.
- Works on desktop and mobile web without layout breakage.
- Must not automate payments or bypass security controls.
- Should be accessible and easy to understand for first-time users.

## User Flow
1. User begins train search and booking.
2. The AI assistant analyzes the current page state and booking pressure.
3. The system shows a small guidance panel or toast message.
4. The user receives a suggested action such as “Wait 30 seconds” or “Reapply filters”.
5. The user continues with a higher-confidence booking journey.

## Success Metrics
- Reduced rate of failed booking attempts during Tatkal windows.
- Fewer repeated filter resets.
- Higher completion rate for seat selection and payment steps.
- Lower support queries related to unclear booking states.

## Scope
### In Scope
- Booking guidance, filter sanity checks, seat state preservation, payment status hints.

### Out of Scope
- Automatic booking or payment execution.
- Full replacement of the current IRCTC booking engine.
