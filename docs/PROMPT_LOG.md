# Prompt log

This file records the build-prompt sequence and the purpose of each stage.

## Stage 0 — Product brief

IceCold Sprint helps students prepare for an exam with limited time. It converts subjects, topics, confidence, importance, and available hours into a prioritized study plan, then uses a quiz to update the next recommended action.

## Stage 1 — Core implementation

The first implementation prompt must create the complete workflow, not only the navigation shell:

> Build a responsive web app called IceCold Sprint. Create a complete workflow where a student chooses a sample subject or enters custom topics, generates a time-limited study plan, opens a topic quiz, submits answers, receives a score, and sees a next-best study recommendation. Include four usable areas: setup, schedule, quiz, and progress. Seed a Biology sample sprint so judges can test the workflow immediately. Use deterministic prioritization and scheduling. Persist the sprint locally. Do not add authentication, payments, social features, or empty placeholder pages.

## Stage 2 — Plan logic

Add validation, topic ranking, time-budget enforcement, breaks, prioritized explanations, and local persistence.

## Stage 3 — Quiz logic

Generate or load five questions, show feedback, calculate a score, and change the recommendation based on score bands.

## Stage 4 — Visual polish

Improve hierarchy, loading states, error states, mobile layout, topic badges, progress indicators, and the primary next action without adding scope.

## Stage 5 — QA

Test empty input, one topic, many topics, limited time, quiz submission, refresh persistence, mobile layout, public URL access, and provider failure fallback.

## Stage 6 — Publish

Confirm the public URL, sample workflow, no-login access, demo video, tool disclosure, and final submission text.
