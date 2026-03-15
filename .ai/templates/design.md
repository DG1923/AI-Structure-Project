# Design: [Feature Name]

> Fill this BEFORE writing spec or any code.
> When done: [ ] reviewed → proceed to spec

---

## 1. Data model
What does the data look like? Fields, types, relations.

```
{
  id: string
  userId: string
  ...
}
```

Relations:
- [ ] ...

---

## 2. Function contracts
Signatures only — no implementation yet.

```typescript
function doSomething(input: InputType): Promise<Result<Output, ErrorType>>
```

---

## 3. Happy path
Step by step when everything works:

1. 
2. 
3. 

---

## 4. Error path

| Condition        | Behavior                  |
|------------------|---------------------------|
| Input invalid    | throw ValidationError     |
| Not found        | return NOT_FOUND          |
| DB constraint    | return CONFLICT           |

---

## 5. What if it fails?

| Scenario              | Strategy                          |
|-----------------------|-----------------------------------|
| DB unavailable        | fail open / fail closed? why?     |
| External API null     | fallback value / propagate?       |
| Concurrent writes     | transaction / optimistic lock?    |
| Timeout               | how long? what fallback?          |
| Queue full            | drop / retry / block?             |

---

## 6. Scale considerations

- Expected volume: 
- N+1 risk: 
- Index needed on: 
- Cache: what data / TTL / invalidation trigger?
- Pagination: cursor or offset? why?

---

## 7. Security boundaries

- Auth required: yes / no
- User A access User B data: prevented by?
- Input sanitized before DB/shell/eval: 
- Secrets or tokens logged anywhere: