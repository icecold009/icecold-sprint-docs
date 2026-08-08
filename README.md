# IceCold Sprint

IceCold Sprint is an AI-assisted study sprint planner for students preparing for an exam with limited time. It is being built for the [AI Factory — Native.builder Hackathon](https://lablab.ai/ai-hackathons/nativebuilder-build-without-limits).

## Current status

**Early public prototype — incomplete as of 2026-08-08.** The public deployment loads without authentication and has working navigation, but the core study workflow is not implemented yet.

- Public app: <https://icecold-sprint.nativelyai.app>
- Native.builder project: <https://builder.nativelyai.com/projects/644dc3a8-4c81-41ab-a4ae-d2f89ed22d10>
- Hackathon team page: <https://lablab.ai/ai-hackathons/nativebuilder-build-without-limits/icecold-org>

## Intended MVP

1. Select a sample subject or enter custom topics.
2. Generate a time-limited, prioritized study plan.
3. Take a five-question topic quiz.
4. Receive a score and next-best study recommendation.
5. View progress persisted locally in the browser.

The core scheduling and prioritization logic is planned to be deterministic for reliability. Fireworks-hosted open-source AI is planned for quiz generation, with a deterministic fallback quiz for outages or missing credentials.

## Repository purpose

This repository documents the product decisions, prompt history, evidence, incomplete work, demo plan, and final submission materials. It is intentionally separate from the generated application source.

## Documentation map

- [Project status](docs/PROJECT_STATUS.md)
- [Build log](docs/BUILD_LOG.md)
- [Architecture and product decisions](docs/DECISIONS.md)
- [Prompt log](docs/PROMPT_LOG.md)
- [Roadmap and completion gates](docs/ROADMAP.md)
- [Hackathon submission draft](docs/HACKATHON_SUBMISSION.md)
- [Demo script](docs/DEMO_SCRIPT.md)
- [Evidence guide](docs/evidence/README.md)

## Documentation rule

Record verified behavior separately from plans. Every new build checkpoint should add a dated entry to `docs/BUILD_LOG.md` and update `docs/PROJECT_STATUS.md` with what was actually tested.
