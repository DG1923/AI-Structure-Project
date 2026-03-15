# Test Plan: [Feature Name]

---

## Unit Tests

### [function / module name]

| Case             | Input          | Expected output       | Type    |
|------------------|----------------|-----------------------|---------|
| Happy path       | valid input    | correct result        | happy   |
| Null input       | null           | throws NullError      | error   |
| Empty collection | []             | returns []            | edge    |
| Boundary value   | max int        | handled correctly     | edge    |
| Concurrent call  | race condition | consistent result     | failure |

---

## Integration Tests

| Scenario     | Setup       | Steps               | Expected            |
|--------------|-------------|---------------------|---------------------|
| Full flow    | seed DB     | call endpoint       | response matches    |
| Auth required| no token    | call endpoint       | returns 401         |

---

## Failure Tests

These must be written. No exceptions.

| Scenario                  | How to simulate              | Expected behavior               |
|---------------------------|------------------------------|---------------------------------|
| DB unavailable            | mock db.query to throw       | returns 503, logs error         |
| External API returns null | mock to return null          | uses fallback / returns error   |
| External API timeout      | mock with 10s delay          | returns 408, does not hang      |
| Concurrent writes         | fire 2 requests in parallel  | one succeeds, one gets conflict |
| Queue full                | mock queue.push to reject    | retries or returns gracefully   |

---

## Test commands

```bash
# Unit
npm test -- <feature>.test.ts

# Integration
npm test -- <feature>.integration.test.ts

# All
npm test
```