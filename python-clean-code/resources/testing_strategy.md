# TESTING STRATEGY

## 1. Transformation Logic

Characteristics:
- Deterministic input → output
- Mathematical or structural invariants

Examples:
- string manipulation
- numeric transformations
- data normalization

→ Use: Property-Based Testing (Hypothesis)

---

## 2. Multiple Input/Output Cases

Characteristics:
- Same logic applied to many inputs
- Clear expected outputs

Examples:
- validators (CPF, email, etc.)
- parsing
- business rules

→ Use: Table-Driven Tests (pytest.mark.parametrize)

---

## 3. Simple Logic

Characteristics:
- Minimal branching
- Straightforward behavior

→ Use: Direct unit tests

---

## Decision Rules

- Prefer the SIMPLEST effective strategy
- Do NOT use property-based testing unnecessarily
- Do NOT overuse parametrization for trivial cases