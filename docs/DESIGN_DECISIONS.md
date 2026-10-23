# Key Design Decisions

## 1. Stable identity, variable context

A logical AI resident is not defined by a single model session.

```text
actor != session != room != channel != runtime != model
```

This allows execution context to change without inventing a new identity every time the model, process or surface changes.

---

## 2. The Ledger is the message source of truth

The UI can be refreshed.

A model can lose its current session.

Neither event should destroy the durable Home conversation.

The Message Ledger therefore owns message history; the UI renders it.

---

## 3. Durable history and per-turn context are separated

Replaying an entire lifetime of conversation on every turn is expensive and noisy.

Home retains durable history while compiling a smaller Context Pack for current inference.

This enables:

**long-lived thread + bounded runtime context**

---

## 4. Authorization occurs before semantic recall

Semantic similarity cannot grant access.

The retrieval pipeline applies actor scope and other hard constraints before returning memory candidates.

Unauthorized, unavailable and non-existent resources should not leak distinguishable details through search behaviour.

---

## 5. Derived summaries do not replace evidence

A summary is an interpretation.

The raw source remains available as evidence and provenance.

Derived context artifacts are versioned and rebuildable.

---

## 6. Memory Service is a routing layer, not just a database

The runtime should not independently decide which storage system to query.

The Memory Service provides one controlled boundary for:

- recall intent
- source planning
- filtering
- retrieval
- ranking
- provenance
- bounded output

---

## 7. New AI behaviour is introduced progressively

Potentially influential memory behaviour follows a staged rollout:

```text
Foundation
→ Retrieval Service
→ Shadow Compiler
→ Observation / Quality Gate
→ Controlled Production Activation
```

This is intentionally slower than simply switching on automatic retrieval.

---

## 8. Provider inference is not resident identity

The resident runtime owns continuity and orchestration.

A model/provider may change without requiring the resident, Ledger or durable memory to be recreated.

---

## 9. AI-assisted implementation is represented transparently

My contribution is not framed as “I manually coded every line”.

My role is best described as:

> I drove the problem framing, architecture decisions, constraints, testing and acceptance, while using AI extensively as an implementation partner.

This distinction is important to the way I want to work in applied AI teams.
