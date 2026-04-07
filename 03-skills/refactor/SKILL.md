---
name: code-refactor
description: Systematic code refactoring based on Martin Fowler's methodology. Use when users ask to refactor code, improve code structure, reduce technical debt, clean up legacy code, eliminate code smells, or improve code maintainability. This skill guides through a phased approach with research, planning, and safe incremental implementation.
---

# Code Refactoring Skill

A systematic approach to refactoring code based on Martin Fowler's *Refactoring: Improving the Design of Existing Code* (2nd Edition).

> "Refactoring is the process of changing a software system in such a way that it does not alter the external behavior of the code yet improves its internal structure." — Martin Fowler

## Core Principles

1. **Behavior Preservation**: External behavior must remain unchanged
2. **Small Steps**: Make tiny, testable changes
3. **Test-Driven**: Tests are the safety net
4. **Continuous**: Refactoring is ongoing, not a one-time event
5. **Collaborative**: User approval required at each phase

## Workflow Overview

```
Phase 1: Research & Analysis
    ↓
Phase 2: Test Coverage Assessment
    ↓
Phase 3: Code Smell Identification
    ↓
Phase 4: Refactoring Plan Creation
    ↓
Phase 5: Incremental Implementation
    ↓
Phase 6: Review & Iteration
```

## Phase 1: Research & Analysis

### Objectives
- Understand the codebase structure and purpose
- Identify the scope of refactoring
- Gather context about business requirements

### Questions to Ask User
1. **Scope**: Which files/modules/functions need refactoring?
2. **Goals**: What problems are you trying to solve?
3. **Constraints**: Areas that should NOT be changed?
4. **Test status**: Do tests exist? Are they passing?

## Phase 2: Test Coverage Assessment

> "Refactoring without tests is like driving without a seatbelt." — Martin Fowler

**If tests exist and pass:** Proceed to Phase 3

**If tests are missing:** Write tests first (recommended)

**If tests are failing:** STOP. Fix failing tests before refactoring.

## Phase 3: Code Smell Identification

### Common Code Smells

| Smell | Signs | Impact |
|-------|-------|--------|
| **Long Method** | Methods > 30-50 lines | Hard to understand, test, maintain |
| **Duplicated Code** | Same logic in multiple places | Bug fixes needed in multiple places |
| **Large Class** | Class with too many responsibilities | Violates Single Responsibility |
| **Feature Envy** | Method uses another class's data more | Poor encapsulation |
| **Primitive Obsession** | Overuse of primitives instead of objects | Missing domain concepts |
| **Long Parameter List** | Methods with 4+ parameters | Hard to call correctly |
| **Dead Code** | Unused code | Confusion, maintenance burden |

See [references/code-smells.md](references/code-smells.md) for complete catalog.

## Phase 4: Refactoring Plan Creation

### Smell-to-Refactoring Mapping

| Code Smell | Recommended Refactoring(s) |
|------------|---------------------------|
| Long Method | Extract Method, Replace Temp with Query |
| Duplicated Code | Extract Method, Pull Up Method |
| Large Class | Extract Class, Extract Subclass |
| Feature Envy | Move Method, Move Field |
| Long Parameter List | Introduce Parameter Object |

### Phased Approach

**Phase A: Quick Wins** (Low risk, high value)
- Rename variables for clarity
- Extract obvious duplicate code
- Remove dead code

**Phase B: Structural Improvements** (Medium risk)
- Extract methods from long functions
- Introduce parameter objects

**Phase C: Architectural Changes** (Higher risk)
- Replace conditionals with polymorphism
- Extract classes

## Phase 5: Incremental Implementation

### The Golden Rule
> "Change → Test → Green? → Commit → Next step"

For each refactoring step:
1. **Pre-check**: Tests passing, code compiles
2. **Make ONE small change**
3. **Verify**: Run tests immediately
4. **If tests pass**: Commit with descriptive message
5. **If tests fail**: STOP, undo, analyze

## Phase 6: Review & Iteration

### Post-Refactoring Checklist
- [ ] All tests passing
- [ ] No new warnings/errors
- [ ] Code compiles successfully
- [ ] Behavior unchanged
- [ ] Documentation updated if needed

## Important Guidelines

### When to STOP and Ask
- Unsure about business logic
- Change might affect external APIs
- Test coverage is inadequate
- Significant architectural decision needed

### Safety Rules
1. **Never refactor without tests** (unless user acknowledges risk)
2. **Never make big changes** - break into tiny steps
3. **Never skip the test run** after each change
4. **Never continue if tests fail** - fix or rollback first

## References

- [Code Smells Catalog](references/code-smells.md)
- [Refactoring Catalog](references/refactoring-catalog.md)
- [Refactoring Plan Template](templates/refactoring-plan.md)
