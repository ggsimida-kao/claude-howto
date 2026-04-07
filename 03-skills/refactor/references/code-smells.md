# Code Smells Catalog

A comprehensive reference of code smells based on Martin Fowler's *Refactoring* (2nd Edition).

> "A code smell is a surface indication that usually corresponds to a deeper problem in the system." — Martin Fowler

---

## Bloaters

Code smells representing something that has grown too large.

### Long Method

**Signs:**
- Method exceeds 30-50 lines
- Multiple levels of nesting
- Comments explaining what sections do

**Why it's bad:**
- Hard to understand
- Difficult to test in isolation
- Changes have unintended consequences

**Refactorings:**
- Extract Method
- Replace Temp with Query
- Introduce Parameter Object

---

### Large Class

**Signs:**
- Class has many instance variables (>7-10)
- Class has many methods (>15-20)
- Class name is vague (Manager, Handler, Processor)

**Why it's bad:**
- Violates Single Responsibility Principle
- Hard to test
- Changes ripple through unrelated features

**Refactorings:**
- Extract Class
- Extract Subclass
- Extract Interface

---

### Primitive Obsession

**Signs:**
- Using primitives for domain concepts (string for email, int for money)
- Arrays of primitives instead of objects
- Magic numbers/strings

**Why it's bad:**
- No validation at type level
- Logic scattered across codebase
- Missing domain concepts

**Refactorings:**
- Replace Primitive with Object
- Replace Type Code with Class

---

### Long Parameter List

**Signs:**
- Methods with 4+ parameters
- Parameters that always appear together
- Boolean flags changing method behavior

**Why it's bad:**
- Hard to call correctly
- Parameter order confusion
- Hard to add new parameters

**Refactorings:**
- Introduce Parameter Object
- Preserve Whole Object
- Remove Flag Argument

---

## Object-Orientation Abusers

### Switch Statements

**Signs:**
- Long switch/case or if/else chains
- Same switch in multiple places
- Switch on type codes

**Why it's bad:**
- Violates Open/Closed Principle
- Hard to extend
- Often indicates missing polymorphism

**Refactorings:**
- Replace Conditional with Polymorphism
- Replace Type Code with State/Strategy

---

## Change Preventers

### Divergent Change

**Signs:**
- One class changed for multiple different reasons
- Changes in different areas trigger same class edits

**Why it's bad:**
- Violates Single Responsibility
- High change frequency

**Refactorings:**
- Extract Class
- Extract Superclass

---

### Shotgun Surgery

**Signs:**
- One change requires edits in many classes
- Small feature needs touching 10+ files

**Why it's bad:**
- Easy to miss a spot
- High coupling

**Refactorings:**
- Move Method
- Inline Class

---

## Dispensables

### Dead Code

**Signs:**
- Unreachable code
- Unused variables/methods/classes
- Commented-out code

**Why it's bad:**
- Confusion
- Maintenance burden

**Refactorings:**
- Remove Dead Code

---

### Duplicate Code

**Signs:**
- Same code in multiple places
- Similar code with small variations

**Why it's bad:**
- Bug fixes needed in multiple places
- Inconsistency risk

**Refactorings:**
- Extract Method
- Extract Class
- Pull Up Method

---

## Couplers

### Feature Envy

**Signs:**
- Method uses more data from another class than its own
- Many getter calls to another object

**Why it's bad:**
- Wrong location for behavior
- Poor encapsulation

**Refactorings:**
- Move Method
- Extract Method (then move)

---

### Message Chains

**Signs:**
- Long chains of method calls: `a.getB().getC().getD()`
- Client depends on navigation structure

**Why it's bad:**
- Fragile—any change breaks chain
- Violates Law of Demeter

**Refactorings:**
- Hide Delegate
- Extract Method

---

## Smell Severity Guide

| Severity | Description | Action |
|----------|-------------|--------|
| **Critical** | Blocks development, causes bugs | Fix immediately |
| **High** | Significant maintenance burden | Fix in current sprint |
| **Medium** | Noticeable but manageable | Plan for near future |
| **Low** | Minor inconvenience | Fix opportunistically |

---

## Quick Detection Checklist

- [ ] Any method > 30 lines?
- [ ] Any class > 300 lines?
- [ ] Any method with > 4 parameters?
- [ ] Any duplicated code blocks?
- [ ] Any switch/case on type codes?
- [ ] Any unused code?
- [ ] Any methods using another class's data heavily?
- [ ] Any primitives that should be objects?
