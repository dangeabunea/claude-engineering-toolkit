---
name: interviewing-human
description: Interview the human one question at a time about the work under discussion in the current conversation, to surface edge cases, corner cases, regression risks, maintainability concerns, and decisions that are hard to revert. Use when a requirement is vague or underspecified, the domain is unfamiliar, the change touches legacy code that other systems depend on, or it affects API contracts, event schemas, data models, failure handling, or shared infrastructure, and generally whenever a wrong guess would be expensive to undo. Works on its own or as a step in a planning workflow, after the task has been described and the relevant code explored. Skip it when tests, examples, or a precise spec already settle the requirement, or when the change is small and every question would have an obvious answer.
allowed-tools: Read, AskUserQuestion
---

# Interviewing the human

Interview the human about the task already under discussion in this
conversation. Use what has been said so far, and what exploring the code has
found, to decide what to ask. If the task isn't clear from the conversation,
ask what it is as your first question.

Do not write or change any files. Your job is to turn open questions into
decisions the human has made.

## Interview

Use the AskUserQuestion tool. Ask one question at a time.

- Offer 2–4 likely answers, mark one as (Recommended), and give a one-line reason.
- Always let the human answer in their own words. AskUserQuestion adds an
  "Other" option for free text automatically, so don't add a separate one.
- Ground each question in the conversation and the code where you can.
- Skip questions the conversation or the code already answers. State the
  answer you found instead.

Cover these areas, most expensive to reverse first:

1. Hard-to-revert decisions: anything other code, teams, or stored data will depend on.
2. Failure behavior: what should happen when something the change relies on goes wrong.
3. Edge cases: inputs at the limits of what the change expects.
4. Corner cases: conditions that are harmless alone but break things together.
5. Regression risk: existing behavior that must keep working.
6. Maintainability: how the change fits the codebase and who will own it.
7. Unstated assumptions: anything the request takes for granted.

If the answer is "not sure" or "need to check," treat it as an open question
with a likely owner. Do not guess on the human's behalf.

Stop when the remaining questions would have obvious answers.

## Wrap up

Summarize the outcome in the conversation:

- The decisions made
- The edge and corner cases, each phrased as a testable case.
- The open questions, and who should answer them.

Example output:

```text
Decisions
- Callers get an error when the provider is down, never a guessed value: stale data would mislead downstream reports.
- Retry only on connection errors and 503s, up to 3 times with backoff.
- Follow the existing client pattern in the orders module rather than introducing a new HTTP library.

Cases to test
- Provider returns an empty list → return an empty result, not an error.
- Provider returns 429 while a retry is pending → stop retrying and honor Retry-After.
- Existing nightly export still receives the same field order.

Assumptions confirmed
- Peak load is about 50 requests per second.

Open questions
- Does the provider enforce a rate limit per client or per account? → owning team
```

Do not record the decisions anywhere or start implementing. The human decides
what happens next.