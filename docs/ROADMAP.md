# Roadmap and completion gates

## Local source checkpoint - 2026-08-09

- [x] Core setup, planning, quiz, score, recommendation, progress, and reset flow exists in the implementation repository.
- [x] Local TypeScript validation and production build pass through `npm.cmd run check`.
- [x] Stale quiz results are cleared when starting or regenerating a sprint.

The following gates remain public-deployment gates. Do not treat local source completion as submission readiness until the same behavior is visible at the published URL.

For the detailed execution checklist, dependencies, QA matrix, and submission evidence requirements, see [TODO.md](TODO.md).

## Now — Core workflow

- [ ] Replace empty Subjects page with sample and custom topic setup.
- [ ] Add Generate Sprint action.
- [ ] Generate a schedule that respects available time.
- [ ] Display the first recommended topic.

**Gate:** a user can enter or select topics and receive a visible study plan.

## Next — Quiz and progress

- [ ] Add five-question quiz flow.
- [ ] Add score calculation.
- [ ] Add recommendation rules for weak, developing, and strong results.
- [ ] Update progress after quiz completion.

**Gate:** a user can complete a quiz and see a different next action.

## Then — Reliability and persistence

- [ ] Save the plan and results in localStorage.
- [ ] Restore after refresh.
- [ ] Add clear/reset action.
- [ ] Add deterministic fallback quiz.
- [ ] Add Fireworks integration only after the local workflow works.

**Gate:** the demo remains usable when the external model is unavailable.

## Final — Presentation and submission

- [ ] Rename public branding consistently to IceCold Sprint.
- [ ] Remove placeholder copy and unfinished controls.
- [ ] Test the public URL without login.
- [ ] Record a three-minute workflow demo.
- [ ] Complete the submission draft.
- [ ] Archive final screenshots and evidence.
