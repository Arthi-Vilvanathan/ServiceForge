# Feature 2 — Parts Stock Check and Reservation

**Status:** Draft

## Intent

Check stock and reserve the required parts for a scheduled job.

## User Stories

- As a dispatcher, I want to see whether a scheduled job's required parts are available so I can identify shortages before the job.
- As a dispatcher, I want available required parts reserved for a scheduled job so they are not allocated to another job.
- As a dispatcher, I want to see which parts cannot be reserved so I can resolve shortages.

## Acceptance Criteria

1. Given a scheduled job with required parts, when stock is checked, the result identifies each required part and its availability.
2. When all required quantities are available, a reservation can be created for the job and the reserved quantities are reflected in subsequent stock checks.
3. When any required quantity is unavailable, the result identifies the affected parts and the quantity short; no partial reservation is made unless the business rule for partial reservations is confirmed.
4. A reservation is associated with the scheduled job and records the part and quantity reserved.
5. A request to reserve more than the available quantity does not make stock available go below zero.
6. Repeating a reservation request for the same job does not reserve the same requirement twice; the expected behavior for changed requirements is an open question.
7. A request for a nonexistent job or part returns a clear not-found result and does not change stock or reservations.
8. Invalid quantities, including zero and negative values, are rejected without changing stock or reservations.

## Edge Cases

- A job has no required parts.
- A required part is not present in the stock records.
- Two jobs attempt to reserve the remaining quantity of the same part.
- A job's required quantities change after a reservation is made.
- A reservation is cancelled, or the job is rescheduled or completed.
- The same reservation request is submitted more than once.
- A requested quantity is partially available.

## Dependencies

- Candidate dependency: Feature 1's technician availability calendar and its scheduled-job context. Confirm whether Feature 2 should depend on a specific decision in [pipeline/decisions/feature-1-decisions.md](pipeline/decisions/feature-1-decisions.md).
- Review [pipeline/features/feature-1-technician-availability.md](pipeline/features/feature-1-technician-availability.md) to confirm the job identifier and scheduling lifecycle this feature should use.

## Success Metrics

- Percentage of reservation attempts that return an availability result for every requested part.
- Percentage of reservation attempts that complete without overselling stock.
- Count of reservations that cannot be associated with a scheduled job.
- Track these measures during testing; target thresholds are open questions.

## Open Questions

- Is stock represented as on-hand quantity, available quantity, or both?
- Should a reservation be all-or-nothing or allow partial reservation?
- When should a reservation expire or be released: cancellation, rescheduling, job completion, or another event?
- Can stock be reserved for a job before its schedule is confirmed?
- How should concurrent reservation attempts be handled by the in-memory data store?
- What should happen when required quantities change after reservation?
- What response format and status codes should availability and reservation outcomes use?
- What target thresholds should apply to the success metrics?
- Which named Feature 1 decision, if any, is a required dependency?