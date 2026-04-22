# AI Feature Specification: Smart Tatkal Assistant

## Problem It Solves

Addresses Problem 1 (Tatkal crash) and Problem 2 (search confusion).

## Proposed Feature — User Perspective

When user searches Tatkal trains, AI shows:

- Best chance booking options
- Less crowded alternatives
- Recommended joining time
- Backup trains

## Model or API Choice

OpenAI GPT-4 + historical booking probability model.

## Training or Input Data

- Historical Tatkal booking success rates
- Route demand
- Time-of-day traffic
- Class availability

## How Output Is Shown to the User

Card above train results:

Recommended Option:
12628 Karnataka Express
Success Chance: High
Try joining at 9:57 AM

## Confidence Threshold and Fallback

Only show if confidence >75%.
Else show normal search results only.

## Success Metrics

- Higher successful bookings
- More users selecting alternatives
- Lower rage refresh behavior

## Limitations and Risks

- Prediction may fail on holidays
- Sudden demand spikes
- Must not mislead users
