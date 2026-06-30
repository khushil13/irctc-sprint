# Part B — AI Feature Proposal

## Feature Idea
AI Booking Assistant for IRCTC

## What It Does
The assistant helps users during booking by detecting common failure patterns and giving simple guidance before they abandon the flow.

## Core Benefits
- Reduces frustration during high-demand Tatkal periods.
- Prevents loss of seat choices and repeated filter errors.
- Improves confidence during payment and refund steps.
- Makes the experience more understandable for new users.

## Example Interactions
- “Booking demand is high. Waiting 30 seconds may improve success.”
- “Your selected berth was preserved automatically.”
- “Filters changed. Results may be stale; reapply the latest filters.”
- “Payment is still processing. Please wait before retrying.”

## Why It Matters
Many users do not understand whether a problem is a network issue, a temporary server issue, or a genuine booking failure. An AI layer can translate system state into understandable guidance.

## Suggested Implementation Approach
1. Add a lightweight status panel to the booking UI.
2. Track booking events and detect anomalies.
3. Use rule-based assistance first, then expand to machine-learning predictions.
4. Keep suggestions short, actionable, and non-intrusive.

## Expected Outcome
A more supportive booking experience that helps users complete transactions with less confusion and fewer retries.
