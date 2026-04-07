# Refactoring Catalog

A curated catalog of refactoring techniques from Martin Fowler's *Refactoring* (2nd Edition).

> "A refactoring is defined by its mechanics—the precise sequence of steps that you follow to carry out the change." — Martin Fowler

---

## Most Common Refactorings

### Extract Method

**When to use**: Long method, duplicate code, need to name a concept

**Motivation**: Turn a code fragment into a method whose name explains the purpose.

**Mechanics**:
1. Create a new method named for what it does
2. Copy the code fragment into the new method
3. Pass local variables as parameters
4. Replace the original fragment with a call to the new method
5. Test

---

### Inline Method

**When to use**: Method body is as clear as its name, excessive delegation

**Motivation**: Remove needless indirection.

**Mechanics**:
1. Check that the method isn't polymorphic
2. Replace each call with the method body
3. Remove the method definition

---

### Rename Variable

**When to use**: Name doesn't clearly communicate purpose

**Motivation**: Good names are crucial for clean code.

**Tips**:
- Use intention-revealing names
- Avoid abbreviations
- Use domain terminology

---

### Change Function Declaration

**When to use**: Function name doesn't explain purpose, parameters need change

**Motivation**: Good function names make code self-documenting.

**Mechanics**:
1. Remove parameters not needed
2. Change the name
3. Add parameters needed
4. Test

---

### Introduce Parameter Object

**When to use**: Several parameters that frequently go together

**Motivation**: Group data that naturally belongs together.

**Mechanics**:
1. Create a new class/structure for the grouped parameters
2. Use Change Function Declaration to add the new object
3. For each parameter in the group, remove it from the function

---

## Moving Features

### Move Method

**When to use**: Method uses more features of another class than its own

**Motivation**: Put functions with the data they use most.

**Mechanics**:
1. Copy method to target class
2. Adjust for new context
3. Make original method delegate to target
4. Test

---

### Move Field

**When to use**: Field is used more by another class

**Motivation**: Keep data with the functions that use it.

---

## Organizing Data

### Replace Primitive with Object

**When to use**: Data item needs more behavior than simple value

**Motivation**: Encapsulate data with its behavior.

---

### Replace Temp with Query

**When to use**: Temporary variable holds result of an expression

**Motivation**: Make the code clearer by extracting the expression into a function.

---

## Simplifying Conditional Logic

### Decompose Conditional

**When to use**: Complex conditional (if-then-else) statement

**Motivation**: Make the intention clear by extracting conditions and actions.

---

### Replace Nested Conditional with Guard Clauses

**When to use**: Deeply nested conditionals making flow hard to follow

**Motivation**: Use guard clauses for special cases, keeping normal flow clear.

---

### Replace Conditional with Polymorphism

**When to use**: Switch/case based on type, conditional logic varying by type

**Motivation**: Let objects handle their own behavior.

---

## Refactoring APIs

### Separate Query from Modifier

**When to use**: Function both returns a value and has side effects

**Motivation**: Make it clear which operations have side effects.

---

### Parameterize Function

**When to use**: Several functions doing similar things with different values

**Motivation**: Remove duplication by adding a parameter.

---

### Remove Flag Argument

**When to use**: Boolean parameter that changes function behavior

**Motivation**: Make the behavior explicit through separate functions.

---

## Dealing with Inheritance

### Pull Up Method

**When to use**: Same method in multiple subclasses

**Motivation**: Remove duplication in class hierarchy.

---

### Push Down Method

**When to use**: Behavior relevant only to a subset of subclasses

**Motivation**: Put method where it's used.

---

### Replace Subclass with Delegate

**When to use**: Inheritance is being used incorrectly, need more flexibility

**Motivation**: Prefer composition over inheritance when appropriate.

---

## Extract Class

**When to use**: Large class with multiple responsibilities

**Motivation**: Split class to maintain single responsibility.

**Mechanics**:
1. Decide how to split responsibilities
2. Create new class
3. Move field from original to new class
4. Move methods from original to new class
5. Review and rename both classes

---

## Quick Reference: Smell to Refactoring

| Code Smell | Primary Refactoring | Alternative |
|------------|-------------------|-------------|
| Long Method | Extract Method | Replace Temp with Query |
| Duplicate Code | Extract Method | Pull Up Method |
| Large Class | Extract Class | Extract Subclass |
| Long Parameter List | Introduce Parameter Object | Preserve Whole Object |
| Feature Envy | Move Method | Extract Method + Move |
| Switch Statements | Replace Conditional with Polymorphism | Replace Type Code |
| Dead Code | Remove Dead Code | - |

---

## Further Reading

- Fowler, M. (2018). *Refactoring: Improving the Design of Existing Code* (2nd ed.)
- Online catalog: https://refactoring.com/catalog/
