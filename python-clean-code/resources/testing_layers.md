# TESTING LAYERS

## Unit Tests (Default)

Use when:
- Testing pure logic
- No external dependencies

Characteristics:
- Fast
- Deterministic
- Isolated

---

## Use Mocks When

- Calling APIs
- Accessing databases
- Reading/writing files
- External services

Rules:
- Mock only what is necessary
- Do not mock internal logic
- Avoid over-mocking

---

## Integration Tests

Suggest when:
- Multiple components interact
- Real systems need validation

Examples:
- API + service + database
- file processing pipelines

Rules:
- Use sparingly
- Focus on critical paths

---

## General Rule

Prefer unit tests first  
Use integration tests only when needed