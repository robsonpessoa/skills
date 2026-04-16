---
name: Python Progressive Architecure Enforcer
description: Guide the generation and refactoring of Python projects to follow a clean, scalable, and idiomatic structure that evolves with complexity.
---

# Python Progressive Architecture Enforcer (Pythonic & Scalable)

## Purpose

Guide the generation and refactoring of Python projects to follow a clean, scalable, and idiomatic structure that evolves with complexity.

The assistant MUST prioritize simplicity first, and only introduce structure when justified by real complexity.

The architecture should be inspired by modern modular Python practices (similar in organization to FastAPI-style projects), but MUST remain fully idiomatic to Python.

---

## Core Principle

Start simple.
Only introduce structure when complexity demands it.
Prefer clarity over abstraction.

---

## Decision Process (MANDATORY)

The assistant MUST follow this process before generating or refactoring code:

1. Assess code size and responsibility:

   * If the code is small (<150 lines, single responsibility) → Level 1
   * If multiple responsibilities exist → Level 2
   * If business logic, I/O, and data access are mixed → Level 3
   * If multiple domains or modules exist → Level 4

2. ONLY escalate structure if strictly necessary

3. NEVER skip levels without explicit justification

4. ALWAYS prefer the lowest level that satisfies the problem

---

## Complexity Signals (MANDATORY TRIGGERS)

The assistant MUST refactor when ANY of the following are true:

* A file exceeds ~150–200 lines
* A module mixes business logic, I/O, and validation
* Code duplication appears
* Functions become long (>30–50 lines)
* Logic becomes difficult to test
* Multiple domains (e.g., user, order) emerge

---

## Structural Evolution Levels

### Level 1 — Minimal (Default)

Use a flat structure:

* main.py
* utils.py (optional)

Constraints:

* No artificial separation
* No services/, repositories/, or schemas/

---

### Level 2 — Basic Modularization

Introduce light separation:

* core/ → business logic
* infra/ → external concerns (file system, APIs)

Constraints:

* Keep structure shallow
* Avoid over-segmentation

---

### Level 3 — Structured Architecture (Pythonic)

ONLY use this level if:

* Business logic is non-trivial
* External systems (DB, APIs, files) are involved
* Responsibilities are clearly separable

Structure:

* domain/ → core entities and pure logic
* services/ → orchestration (FUNCTIONS, not classes)
* repositories/ → data access (FUNCTIONS, not classes)
* schemas/ → validation / data shapes
* infra/ → external integrations

---

### Level 4 — Scalable Project Layout

ONLY use this level if:

* Multiple domains exist
* The project spans multiple modules or features

Structure:

* src/app/

  * domain/
  * services/
  * repositories/
  * schemas/
  * core/
  * infra/
* tests/
* scripts/

---

## Pythonic Style (MANDATORY)

The assistant MUST prioritize idiomatic Python over class-based or Java-style design.

---

### Prefer Functions Over Classes

The assistant MUST:

* Use plain functions for business logic
* Treat modules as the primary unit of organization

The assistant MUST ONLY use classes when:

* There is shared state that must persist
* Behavior is tightly coupled to that state
* A real object abstraction simplifies the problem

The assistant MUST NOT:

* Create classes that only group functions
* Use classes as static namespaces
* Use one-class-per-file patterns without justification

---

### Module-Oriented Design

* Each module should encapsulate a clear responsibility
* Functions inside a module must be cohesive
* Prefer modules over class hierarchies

---

### Keep Code Simple and Explicit

* Prefer readability over abstraction
* Avoid unnecessary indirection
* Use built-in data structures (dict, list, tuple)

---

### Avoid Java-Style Patterns

The assistant MUST NOT introduce:

* Service classes without state
* Repository classes without real complexity
* Interfaces or abstract base classes without multiple implementations
* Factory patterns unless truly necessary

---

### Embrace Python Features

The assistant SHOULD use:

* First-class functions
* List/dict comprehensions
* Context managers
* Standard library utilities

---

### Functional Core, Imperative Shell

* Business logic should be pure functions whenever possible
* Side effects (I/O, DB, APIs) must be isolated

---

## Separation of Concerns (MANDATORY)

When structure is introduced:

* domain/ → pure logic only
* services/ → orchestration only
* repositories/ → data access only
* infra/ → external systems only

No mixing responsibilities.

---

## Hard Constraints (NON-NEGOTIABLE)

The assistant MUST NOT:

* Introduce services/, repositories/, or schemas/ in simple scripts
* Create abstractions without a real use case
* Mimic Java-style layered architecture unnecessarily
* Split files without clear responsibility boundaries
* Over-engineer small codebases

---

## Anti-Patterns (STRICTLY FORBIDDEN)

* Empty layers (pass-through functions)
* Artificial abstractions
* Deeply nested folder structures
* One-class-per-file without justification
* Premature modularization
* Overuse of classes

---

## Refactoring Scope Control

The assistant MUST:

* Refactor only what is necessary
* Preserve working code whenever possible
* Avoid large rewrites unless explicitly requested

---

## Refactoring Transparency (MANDATORY)

When refactoring or restructuring, the assistant MUST:

1. Explain WHY the change is necessary
2. Identify which complexity signal triggered it
3. Describe the benefit (e.g., testability, separation of concerns)
4. State which structural level is being applied

---

## Output Expectations

* Produce idiomatic Python code
* Prefer clarity over cleverness
* Keep structure aligned with real complexity
* Avoid unnecessary verbosity
* Ensure consistency across modules

---

## Examples (Few-Shot)

---

### Example 1 — Keep It Simple (Level 1)

**User request:**
"Create a script to read a CSV file and calculate the average value of a column."

**Expected approach:**

* Do NOT introduce layers
* Keep everything simple

**Output:**

```python
import csv

def calcular_media(caminho_arquivo, coluna):
    with open(caminho_arquivo, newline="") as f:
        reader = csv.DictReader(f)
        valores = [float(row[coluna]) for row in reader]
    return sum(valores) / len(valores)


def main():
    media = calcular_media("dados.csv", "idade")
    print(media)


if __name__ == "__main__":
    main()
```

**Explanation:**
Level 1 applied. The problem is simple and does not justify additional structure.

---

### Example 2 — Introduce Modules (Level 2)

**User request:**
"Refactor this script because it's mixing file reading and business logic."

**Expected approach:**

* Separate concerns lightly
* Do NOT over-engineer

**Output structure:**

```
project/
├── main.py
├── core/
│   └── calculo.py
└── infra/
    └── csv_reader.py
```

**Code:**

```python
# core/calculo.py

def calcular_media(valores):
    return sum(valores) / len(valores)
```

```python
# infra/csv_reader.py

import csv

def ler_coluna_csv(caminho_arquivo, coluna):
    with open(caminho_arquivo, newline="") as f:
        reader = csv.DictReader(f)
        return [float(row[coluna]) for row in reader]
```

```python
# main.py

from core.calculo import calcular_media
from infra.csv_reader import ler_coluna_csv


def main():
    valores = ler_coluna_csv("dados.csv", "idade")
    media = calcular_media(valores)
    print(media)


if __name__ == "__main__":
    main()
```

**Explanation:**
Level 2 applied due to separation of concerns (I/O vs business logic).

---

### Example 3 — Structured Architecture (Level 3, Pythonic)

**User request:**
"We now need to persist users and apply validation rules. The code is getting hard to maintain."

**Expected approach:**

* Introduce structure
* Keep it Pythonic (functions, not classes)

**Output structure:**

```
project/
├── main.py
├── domain/
│   └── usuario.py
├── services/
│   └── usuario.py
├── repositories/
│   └── usuario.py
├── schemas/
│   └── usuario.py
└── infra/
    └── db.py
```

**Code:**

```python
# domain/usuario.py

def validar_usuario(dados):
    if "email" not in dados:
        raise ValueError("Email é obrigatório")
    return dados
```

```python
# repositories/usuario.py

def salvar_usuario(db, usuario):
    db.append(usuario)
    return usuario
```

```python
# services/usuario.py

from domain.usuario import validar_usuario
from repositories.usuario import salvar_usuario


def criar_usuario(db, dados):
    usuario = validar_usuario(dados)
    return salvar_usuario(db, usuario)
```

```python
# infra/db.py

def get_db():
    return []
```

```python
# main.py

from infra.db import get_db
from services.usuario import criar_usuario


def main():
    db = get_db()
    usuario = criar_usuario(db, {"email": "teste@email.com"})
    print(usuario)


if __name__ == "__main__":
    main()
```

**Explanation:**
Level 3 applied due to:

* Growing complexity
* Presence of business rules and persistence
* Need for separation of concerns

Functions were used instead of classes to maintain idiomatic Python style.
