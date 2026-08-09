# IceCold Sprint execution TODO

Last reviewed: **2026-08-09**
Current release state: **functional local source and Builder preview; published URL still serves the old shell; not submission-ready**

This is the execution checklist for completing IceCold Sprint in the native.builder project. The application source is generated and deployed through native.builder; this repository records the plan, decisions, verification results, and submission evidence.

## Local source checkpoint - 2026-08-09

- [x] Implementation branch `codex/icecold-sprint-core-workflow` is pushed at commit `a23b4fa`.
- [x] `npm.cmd run check` passes in the application source repository.
- [x] Core setup, plan generation, quiz, score/recommendation, progress, persistence, and reset code exists locally.
- [x] Stale quiz state is cleared when starting or regenerating a sprint.
- [x] Authenticated native.builder workspace and preview were inspected.
- [x] Authenticated Builder preview reaches the five-question quiz without reload and advanced through all five questions.
- [x] Builder publish control reported a successful publish.
- [ ] The named public URL still serves the old shell after Builder reported publish success.
- [x] A repeatable `npm.cmd run smoke` P0 check exists in the source repo.
- [ ] Run the smoke check after the Chromium dependency is available and the public URL serves the functional workflow.
- [ ] Native.builder has not been confirmed to contain commit `a23b4fa`; its internal one-file repair is not GitHub-synced.
- [ ] Builder GitHub sync remains unconfirmed; Builder publish was triggered successfully without it.
- [x] Sign in to GitHub in the browser session.
- [ ] Complete Builder Integrations → GitHub → Connect after the OAuth callback returns.
- [ ] The public URL has not received this checkpoint and remains a placeholder shell.
- [ ] A fresh-browser local workflow could not be run because the in-app browser could not reach the local Vite server.

## How to use this list

- Work from top to bottom unless a task is explicitly marked independent.
- Do not mark an item complete because code was generated. Mark it complete only after the behavior is visible in the published app and the verification evidence is recorded.
- Every completed build slice must add a dated entry to `docs/BUILD_LOG.md` and update `docs/PROJECT_STATUS.md` with the exact environment and result.
- Keep planned, locally tested, publicly verified, and submission-ready states separate.
- Use `[P0]` for eligibility blockers, `[P1]` for the required MVP, `[P2]` for reliability and presentation, and `[P3]` for optional improvements.

## Definition of done

IceCold Sprint is ready to submit only when a fresh, unauthenticated user can complete this flow in approximately three minutes:

1. Choose a Biology sample sprint or enter custom topics.
2. Set confidence, importance, and available study time.
3. Generate a prioritized plan that fits the available time.
4. Open the first recommended topic.
5. Complete five quiz questions.
6. Submit the quiz and receive a score with useful feedback.
7. See a different next recommendation based on the result.
8. Refresh the page and see the sprint progress retained locally.
9. Reset the sprint and start again without stale state.

The flow must work without a login, without a database, and without depending on an external model response.

## Current blockers

- [P0] The public deployment has navigation but no demonstrated end-to-end study workflow.
- [P0] The generated native.builder source and workspace history are not documented in this repository.
- [P0] The public app has not passed a fresh-browser workflow test.
- [P0] No complete demo video or final submission package exists.
- [P1] Fireworks usage, secret configuration, and deterministic fallback are unverified.
- [P1] Public branding still says `Study Sprint` while the project is named `IceCold Sprint`.

## Phase 0 — Freeze scope and establish evidence

### 0.1 Confirm the submission constraints [P0]

- [ ] Recheck the official event page for the current submission deadline and any changed requirements.
- [ ] Confirm that the project is being created primarily in native.builder.
- [ ] Confirm the public app URL and native.builder project URL are the URLs intended for judges.
- [ ] Confirm the team page and submission form are accessible to the team leader.
- [ ] Record the hackathon window and the exact verification date in the build log.
- [ ] Confirm whether the final form requires a pitch deck or public repository in addition to the event-page requirements.
- [ ] Confirm that all assets, copy, datasets, and external services are permitted and can be submitted under the event's originality/MIT-compliance rules.

### 0.2 Capture the baseline [P0]

- [ ] Capture a screenshot of the current public Dashboard.
- [ ] Capture a screenshot of the current Subjects, Schedule, Quiz, and Progress empty states.
- [ ] Capture the native.builder project workspace showing the project identity and generated application context.
- [ ] Record the current public title (`Study Sprint`) and route list.
- [ ] Record that no usable plan, quiz, score, recommendation, or persistence behavior was available at baseline.
- [ ] Add the baseline result to `docs/BUILD_LOG.md`; do not overwrite it with later success claims.

### 0.3 Confirm the build operating model [P0]

- [ ] Keep native.builder as the primary application-generation, workflow, and deployment surface.
- [ ] Use Codex/Luna for planning, prompt preparation, UX review, test design, documentation, and submission writing only where that preserves native.builder eligibility.
- [ ] Do not create a replacement application in this evidence repository.
- [ ] Keep API keys, session cookies, personal data, and private builder screenshots out of Git.

## Phase 1 — Build the usable sprint setup

### 1.1 Create the setup state [P1]

- [ ] Add a clear setup entry point from Dashboard to Subjects.
- [ ] Provide a one-click Biology sample sprint so a judge can start immediately.
- [ ] Provide sample sets for Physics, Math, Chemistry, Biology, and History if this does not delay the core gate.
- [ ] Allow a user to create a custom subject.
- [ ] Allow a user to add, edit, and remove topics.
- [ ] Require a topic name before saving a topic.
- [ ] Allow confidence to be selected on a clear scale, such as low, medium, or high.
- [ ] Allow importance to be selected on a clear scale, such as low, medium, or high.
- [ ] Ask for available study time in minutes or hours.
- [ ] Validate that available time is positive and within a reasonable demo range.
- [ ] Explain what confidence, importance, and available time affect.
- [ ] Make the primary action explicit: `Generate Sprint`.
- [ ] Keep the setup usable on a narrow mobile viewport.

### 1.2 Define the demo data contract [P1]

- [ ] Define a stable topic shape containing subject, topic name, confidence, importance, estimated minutes, completion state, and quiz state.
- [ ] Define a stable sprint shape containing available minutes, reserved break/review minutes, ordered study blocks, active topic, quiz result, recommendation, and version.
- [ ] Seed the Biology sample with enough topics to visibly demonstrate prioritization.
- [ ] Ensure seeded data is deterministic between fresh sessions.
- [ ] Ensure custom topics use the same shape as sample topics.
- [ ] Decide whether estimated minutes are user-entered, seeded, or derived; document the decision in `docs/DECISIONS.md`.

### 1.3 Setup acceptance gate [P0]

- [ ] A fresh user can load Biology without typing anything.
- [ ] A fresh user can add at least one custom topic.
- [ ] Missing topic names and invalid time values produce visible validation.
- [ ] The setup state survives navigation to Schedule.
- [ ] No authentication or database is required.
- [ ] Record the test path and result in the build log.

## Phase 2 — Implement deterministic planning

### 2.1 Define prioritization rules [P1]

- [ ] Rank low-confidence topics ahead of high-confidence topics.
- [ ] Rank high-importance topics ahead of low-importance topics.
- [ ] Ensure low confidence plus high importance receives the strongest priority.
- [ ] Use a deterministic tie-breaker, such as original topic order or topic name.
- [ ] Display a short reason for each topic's position.
- [ ] Document the scoring formula and tie-breaker in `docs/DECISIONS.md`.

### 2.2 Enforce the time budget [P1]

- [ ] Reserve a small, visible amount of time for review and breaks.
- [ ] Allocate study blocks without exceeding the user's available time.
- [ ] Handle one topic with very limited time.
- [ ] Handle more topics than can fit in the session.
- [ ] Make truncation or deferred topics understandable to the user.
- [ ] Display total planned minutes and compare them with available minutes.
- [ ] Show the first recommended topic as the primary next action.
- [ ] Make schedule generation repeatable for the same inputs.

### 2.3 Schedule acceptance gate [P0]

- [ ] A user can click `Generate Sprint` and see a non-empty schedule.
- [ ] The schedule visibly fits the selected time budget.
- [ ] At least one topic is marked as the next recommended action.
- [ ] Priority reasons are visible without opening developer tools.
- [ ] The Schedule page no longer displays the empty-state blocker after generation.
- [ ] Record one Biology sample result and one limited-time edge case.

## Phase 3 — Build the quiz and adaptive recommendation

### 3.1 Create the quiz contract [P1]

- [ ] Load exactly five questions for the active recommended topic.
- [ ] Provide answer controls that are keyboard accessible.
- [ ] Prevent submission before all required answers are selected, or clearly identify unanswered questions.
- [ ] Keep the question order deterministic for the fallback path.
- [ ] Store the correct answer and explanation separately from the displayed answer labels.
- [ ] Avoid exposing the answer before submission.

### 3.2 Add scoring and feedback [P1]

- [ ] Calculate the number correct and percentage score.
- [ ] Display the result immediately after submission.
- [ ] Show concise explanations for correct and incorrect answers.
- [ ] Use clear score bands, for example weak, developing, and strong.
- [ ] Mark the active topic as attempted and, when appropriate, completed.
- [ ] Update the progress summary after scoring.

### 3.3 Change the next recommendation [P0]

- [ ] Define the weak-score rule: recommend review or a simpler retry for the same topic.
- [ ] Define the developing-score rule: recommend targeted practice or a short revisit.
- [ ] Define the strong-score rule: advance to the next high-priority topic.
- [ ] Ensure the recommendation after submission is visibly different from the pre-quiz recommendation when the score warrants it.
- [ ] Explain why the next action changed.
- [ ] Add a clear button to continue the sprint.

### 3.4 Quiz acceptance gate [P0]

- [ ] A fresh user can reach the quiz from the generated schedule.
- [ ] Five questions can be answered and submitted.
- [ ] The score is visible and correct for a known answer set.
- [ ] The recommendation changes according to the score band.
- [ ] The Quiz page no longer displays the no-subjects blocker after setup.
- [ ] Record a weak-score and strong-score verification path.

## Phase 4 — Add reliability and persistence

### 4.1 Make the local workflow the source of truth [P1]

- [ ] Persist the sprint, schedule, active topic, answers/results, completed topics, and current recommendation in localStorage.
- [ ] Add a storage key prefix and schema version.
- [ ] Handle missing, malformed, or old localStorage data by starting cleanly.
- [ ] Restore the current sprint after a page refresh.
- [ ] Restore progress after closing and reopening the public app in the same browser profile.
- [ ] Add a visible `Reset Sprint` action.
- [ ] Confirm reset removes stale plan, quiz, score, and recommendation state.

### 4.2 Add quiz fallback before external integration [P0]

- [ ] Ship a deterministic fallback quiz first.
- [ ] Verify the complete flow with the external provider disabled.
- [ ] Add an explicit loading state for provider-backed generation.
- [ ] Add a visible, user-friendly provider error state.
- [ ] Fall back to the deterministic quiz when the provider is unavailable, slow, malformed, or missing credentials.
- [ ] Never expose an API key in client-visible code or browser storage.

### 4.3 Add Fireworks only if it remains low-risk [P2]

- [ ] Confirm the provider, model, endpoint, and credits are actually available.
- [ ] Keep the provider call server-side through native.builder's supported workflow.
- [ ] Validate the provider response against the five-question quiz contract.
- [ ] Sanitize generated question text and answer choices before display.
- [ ] Preserve the deterministic fallback as the demo-safe path.
- [ ] Record the actual provider and failure behavior in `docs/HACKATHON_SUBMISSION.md`.

### 4.4 Reliability acceptance gate [P0]

- [ ] The public demo remains usable with the external provider unavailable.
- [ ] Refresh restores the sprint and progress.
- [ ] Reset returns the app to a clean state.
- [ ] Malformed local state does not produce a blank or crashed page.
- [ ] No secret appears in the public app, repository, screenshots, or video.

## Phase 5 — UX, accessibility, and product polish

### 5.1 Remove prototype signals [P1]

- [ ] Rename visible `Study Sprint` branding to `IceCold Sprint`, or document and intentionally retain the alternate product label.
- [ ] Remove placeholder copy and unfinished controls.
- [ ] Replace generic empty states with useful next actions.
- [ ] Ensure every primary page has one obvious next action.
- [ ] Make the current sprint state visible from Dashboard.
- [ ] Show progress without requiring a judge to infer state from navigation.

### 5.2 Improve interaction quality [P2]

- [ ] Add loading, success, validation, and error states for every action.
- [ ] Disable duplicate submissions while work is in progress.
- [ ] Preserve user input when a non-fatal error occurs.
- [ ] Add a clear back/continue path between setup, schedule, quiz, result, and progress.
- [ ] Ensure long topic names and many topics do not break layout.
- [ ] Verify responsive behavior on mobile and desktop widths.
- [ ] Verify color contrast, focus visibility, labels, and keyboard navigation.
- [ ] Use plain language appropriate for a student under time pressure.

### 5.3 Presentation acceptance gate [P1]

- [ ] A judge can understand the product purpose within ten seconds.
- [ ] A judge can identify the current next action on every screen.
- [ ] The complete flow fits comfortably within the three-minute video limit.
- [ ] No screen shown in the demo contains placeholder or misleading text.

## Phase 6 — Native.builder and eligibility evidence

### 6.1 Document how the app was built [P0]

- [ ] Record the native.builder project URL.
- [ ] Record the major builder prompts or agent actions that created setup, planning, quiz, persistence, and polish.
- [ ] Record which workflows, backend functions, integrations, and deployment steps were performed in native.builder.
- [ ] Record which work was supporting work performed outside native.builder.
- [ ] Capture a redacted screenshot of the builder workspace showing meaningful application work.
- [ ] Confirm the final public deployment corresponds to the project being submitted.
- [ ] Keep the explanation factual; do not claim builder capabilities or integrations that were not used.

### 6.2 Confirm access and eligibility [P0]

- [ ] Test the public URL in an incognito/private window.
- [ ] Test the public URL while logged out of NativelyAI.
- [ ] Confirm the app does not require an invite, password, or private session.
- [ ] Confirm the native.builder project/application URL is valid for judges.
- [ ] Confirm the app was created during the August 3–10 hackathon window.
- [ ] Confirm originality and permission to use all submitted assets and data.
- [ ] Record any remaining access caveat before submission.

## Phase 7 — Verification matrix

### 7.1 Fresh-user happy path [P0]

- [ ] Open the public URL in a fresh browser context.
- [ ] Load Biology sample data.
- [ ] Generate the sprint.
- [ ] Verify planned minutes do not exceed available minutes.
- [ ] Open the first recommended topic.
- [ ] Complete all five questions.
- [ ] Verify the score against a known answer key.
- [ ] Verify the next recommendation changes.
- [ ] Verify progress updates.
- [ ] Refresh and verify state is retained.
- [ ] Reset and verify state is cleared.
- [ ] Time the full path and keep it below approximately three minutes.

### 7.2 Input and planning edge cases [P1]

- [ ] Empty subject name.
- [ ] Empty topic name.
- [ ] One topic.
- [ ] Many topics.
- [ ] Duplicate topic names.
- [ ] Very long topic name.
- [ ] Low available time.
- [ ] Large available time.
- [ ] Equal confidence and importance ties.
- [ ] All topics high confidence.
- [ ] All topics low confidence.
- [ ] Mixed sample and custom topics.
- [ ] Navigation away before generation.

### 7.3 Quiz and provider edge cases [P1]

- [ ] Unanswered question submission.
- [ ] All answers correct.
- [ ] All answers incorrect.
- [ ] Mixed score.
- [ ] Reopening an already attempted topic.
- [ ] Provider success.
- [ ] Provider timeout.
- [ ] Provider malformed response.
- [ ] Provider unavailable.
- [ ] Missing provider secret.
- [ ] Fallback quiz scoring and recommendation.

### 7.4 Persistence and browser checks [P1]

- [ ] Refresh during setup.
- [ ] Refresh after plan generation.
- [ ] Refresh during quiz.
- [ ] Refresh after score.
- [ ] Close and reopen the tab.
- [ ] Reset after completed quiz.
- [ ] Malformed storage data.
- [ ] Storage unavailable or quota failure, if the platform permits simulation.
- [ ] Verify no sensitive data is stored.

### 7.5 Device and accessibility checks [P2]

- [ ] Desktop viewport.
- [ ] Narrow mobile viewport.
- [ ] Keyboard-only navigation.
- [ ] Focus order and visible focus.
- [ ] Screen-reader-readable labels and headings.
- [ ] Slow network/loading state.
- [ ] Browser refresh and back-button behavior.

### 7.6 Verification record [P0]

- [ ] For every test group, record date, URL, browser context, result, and any limitation.
- [ ] Distinguish local/builder preview results from public deployment results.
- [ ] Keep failed or incomplete checks visible until retested.
- [ ] Add final screenshots and short recordings under `docs/evidence/`.
- [ ] Do not store secrets, cookies, private user data, or unredacted builder information.

## Phase 8 — Documentation and submission package

### 8.1 Keep the evidence repository current [P0]

- [ ] Update `docs/PROJECT_STATUS.md` after each completed phase.
- [ ] Add dated entries to `docs/BUILD_LOG.md` for implementation and public verification.
- [ ] Update `docs/DECISIONS.md` with the final scheduling, quiz, persistence, and provider decisions.
- [ ] Update `docs/PROMPT_LOG.md` with the prompts or agent actions actually used.
- [ ] Replace all `TODO` placeholders in `docs/HACKATHON_SUBMISSION.md`.
- [ ] Keep `docs/ROADMAP.md` aligned with this execution list.
- [ ] Update `docs/evidence/README.md` with the final artifact names.

### 8.2 Required evidence artifacts [P0]

- [ ] `01-native-builder-workspace.png` — builder project and meaningful workflow context.
- [ ] `02-setup.png` — sample/custom topic setup.
- [ ] `03-study-plan.png` — generated plan with time budget and priority reason.
- [ ] `04-quiz.png` — five-question quiz in progress.
- [ ] `05-adaptive-result.png` — score and changed recommendation.
- [ ] `06-public-url-check.png` — public app tested without authentication.
- [ ] Add a concise verification note for each artifact.

### 8.3 Demo video [P0]

- [ ] Write the final narration from `docs/DEMO_SCRIPT.md` only after the public flow is stable.
- [ ] Show the problem and target user briefly.
- [ ] Show setup with Biology sample data.
- [ ] Show plan generation and the time budget.
- [ ] Show the first recommended topic.
- [ ] Show five quiz questions and submission.
- [ ] Show score feedback and changed recommendation.
- [ ] Show progress or persistence briefly.
- [ ] Disclose native.builder and actual external tools used.
- [ ] Keep the final video at or below three minutes.
- [ ] Watch the exported video from beginning to end.
- [ ] Confirm the public URL shown in the video is the final URL.

### 8.4 Submission form [P0]

- [ ] Project name is consistent across app, repository, builder project, team page, and video.
- [ ] Problem statement is concise and specific.
- [ ] Target user is specific.
- [ ] Native.builder usage explanation is factual and complete.
- [ ] External APIs, models, datasets, and tools are listed accurately.
- [ ] Public app URL works without authentication.
- [ ] Native.builder project/application URL is correct.
- [ ] Demo video is attached and within the time limit.
- [ ] Pitch deck/repository fields are completed if required by the submission form.
- [ ] Final submission is reviewed from the judge's perspective before sending.

## Phase 9 — Final release gate

Do not claim readiness until every item below is checked:

- [ ] Functional public application.
- [ ] Meaningful native.builder workflow, not only navigation or a landing page.
- [ ] Fresh-user setup works.
- [ ] Deterministic plan works.
- [ ] Five-question quiz works.
- [ ] Score is correct.
- [ ] Recommendation changes after scoring.
- [ ] Progress updates.
- [ ] Refresh persistence works.
- [ ] Reset works.
- [ ] Provider failure fallback works.
- [ ] No authentication required.
- [ ] No placeholder copy remains in the demonstrated path.
- [ ] Public URL verified after final publish.
- [ ] Native.builder usage documented.
- [ ] External tools disclosed.
- [ ] Evidence archive complete.
- [ ] Demo video complete and under three minutes.
- [ ] Submission form complete.
- [ ] Final status and build log updated with exact evidence.

## Explicitly out of scope until the release gate passes

- [ ] Authentication and accounts.
- [ ] Payments or subscriptions.
- [ ] Social features or collaboration.
- [ ] Multi-user database persistence.
- [ ] Complex analytics dashboards.
- [ ] Broad curriculum ingestion.
- [ ] Multiple AI providers.
- [ ] Native mobile packaging.
- [ ] Decorative animation that does not improve the demo.

These may become follow-up work only after the complete public workflow is functional, reliable, and documented.
