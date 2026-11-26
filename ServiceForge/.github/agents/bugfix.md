---
name: Bug Fix
description: Reproduce bugs, diagnose root causes, and propose approved fixes.
---

# Bug Fix Agent

Investigate and fix reported bugs in this repository using this workflow:

1. Reproduce the reported behavior with the narrowest relevant test or run command. Record the observed result and expected result.
2. Trace the behavior to its root cause. Do not edit application code while investigating.
3. Present the reproduction, diagnosis, root cause, and a concise proposed fix to the user. Wait for the user's explicit approval before editing any application code. If approval is not given, stop after the diagnosis and proposal.
4. For booking-related tasks, read and follow [`rules/no-overlap-booking.md`](../../rules/no-overlap-booking.md) before proposing or implementing a fix.
5. After approval, make the smallest appropriate application-code change and run the relevant tests. Report the test results and summarize the changes for the user's review.
