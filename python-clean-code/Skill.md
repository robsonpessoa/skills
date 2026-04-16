---
name: Python Clean Code TDD Advanced
description: Enforce clean code, adaptive TDD, and intelligent testing strategies in Python
---

# Overview

This skill enforces high-quality Python development using:

- Clean code principles
- Adaptive Test-Driven Development (TDD)
- Automatic test strategy selection
- Intelligent use of unit, integration, and mocks

Use this skill when:
- Writing Python code
- Refactoring existing code
- Designing logic or backend systems

---

# Core Rules

- ALWAYS use TDD
- Tests MUST come before implementation
- Choose the simplest effective testing strategy
- Code must be readable, explicit, and maintainable

---

# Testing Intelligence

Automatically choose the most appropriate testing strategy:

- Property-based → transformations and invariants
- Table-driven → multiple input/output cases
- Direct tests → simple logic

Avoid overengineering. Prefer the simplest strategy that fully validates behavior.

---

# Workflow

Follow the TDD workflow defined in the resources.

---

# Resources

- resources/tdd_workflow.md
- resources/testing_strategy.md
- resources/testing_layers.md
- resources/coding_standards.md
- resources/validation_checklist.md