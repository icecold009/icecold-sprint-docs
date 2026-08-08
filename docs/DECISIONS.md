# Architecture and product decisions

## D1 — Native.builder is the primary platform

The hackathon requires a functional application created primarily with native.builder. Supporting tools may help with planning, copy, testing, or integrations, but the main application workflow must remain in native.builder.

## D2 — Narrow MVP over broad platform

The product will focus on one complete workflow rather than authentication, payments, social features, multi-user collaboration, or complex analytics.

## D3 — Deterministic scheduling

Topic prioritization and time allocation will use predictable rules:

- Low confidence increases priority.
- High importance increases priority.
- Low confidence plus high importance comes first.
- The schedule must fit within available study time.
- A small portion of the session is reserved for review and breaks.

This avoids making the core demo depend on an external model call.

## D4 — Fireworks for quiz generation

Fireworks is planned for generating five quiz questions and answer explanations through a server-side function. The API key must remain a server-side secret. If the provider is unavailable, the app must use a deterministic fallback quiz.

## D5 — localStorage for the sprint demo

The app will persist the current plan, quiz scores, completed topics, and recommendation locally. This avoids adding authentication, database schema, and row-level security during the two-day build. Supabase database persistence can be a future improvement.

## D6 — Sample data plus customization

The demo will provide sample sets for Physics, Math, Chemistry, Biology, and History, while allowing users to edit or add topics.
