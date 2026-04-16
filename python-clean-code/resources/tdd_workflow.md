# ADAPTIVE TDD WORKFLOW

## Step 0 — Classify Complexity

- TRIVIAL → 1–5 lines, no branching
- SIMPLE → some branching, limited cases
- COMPLEX → multiple paths, business logic

---

## Step 1 — Identify Problem Type

- Transformation (input → output)
- Multiple input/output cases
- Simple linear logic

---

## Step 2 — Select Testing Strategy

- Property-based
- Table-driven
- Direct unit tests

---

## Step 3 — Select Test Layer

- Unit (default)
- Integration (if multiple components interact)

---

## Step 4 — Write tests FIRST

- Tests must define expected behavior
- Include edge cases when relevant

---

## Step 5 — Ensure tests would fail

- Tests must not pass without implementation

---

## Step 6 — Implement minimal code

- Only enough to pass tests

---

## Step 7 — Refactor

- Improve naming
- Remove duplication
- Simplify logic

---

## Rule

TDD is ALWAYS required  
Testing depth MUST match complexity