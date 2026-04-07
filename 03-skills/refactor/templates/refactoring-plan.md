# Refactoring Plan Template

Use this template to document and track your refactoring effort.

---

## Project Information

| Field | Value |
|-------|-------|
| **Project/Module** | [Project name] |
| **Target Files** | [List of files to refactor] |
| **Date Created** | [Date] |
| **Author** | [Name] |
| **Status** | Draft / In Review / Approved / In Progress / Completed |

---

## Executive Summary

### Goals
- [ ] [Primary goal: e.g., Improve readability of payment processing]
- [ ] [Secondary goal: e.g., Reduce code duplication]
- [ ] [Tertiary goal: e.g., Improve testability]

### Constraints
- [ ] [Constraint 1: e.g., Cannot change public API]
- [ ] [Constraint 2: e.g., Must maintain backward compatibility]

### Risk Level
- [ ] Low - Minor changes, well-tested code
- [ ] Medium - Moderate changes, some risk
- [ ] High - Significant changes, careful attention needed

---

## Pre-Refactoring Checklist

### Test Coverage Assessment

| Metric | Current | Target | Status |
|--------|---------|--------|--------|
| Unit Test Coverage | __%  | >=80% | |
| Integration Tests | Yes/No | Yes | |
| All Tests Passing | Yes/No | Yes | |

### Required Before Starting
- [ ] All tests passing
- [ ] Code reviewed and understood
- [ ] Backup/version control in place
- [ ] User approval obtained

---

## Identified Code Smells

### Summary

| # | Smell | Location | Severity | Priority |
|---|-------|----------|----------|----------|
| 1 | [e.g., Long Method] | [file:line] | High | P1 |
| 2 | [e.g., Duplicate Code] | [file:line] | Medium | P2 |
| 3 | [e.g., Feature Envy] | [file:line] | Low | P3 |

---

## Refactoring Phases

### Phase A: Quick Wins (Low Risk)

**Objective**: Simple improvements with immediate value

| # | Task | File | Refactoring | Status |
|---|------|------|-------------|--------|
| A1 | Rename variable to clear name | utils.js:15 | Rename Variable | [ ] |
| A2 | Remove unused function | api.js:89 | Remove Dead Code | [ ] |
| A3 | Extract duplicate validation | form.js:23,67 | Extract Method | [ ] |

**Rollback Plan**: Revert commits A1-A3

---

### Phase B: Structural Improvements (Medium Risk)

**Objective**: Improve code organization and clarity

**Dependencies**: Phase A must be complete

| # | Task | File | Refactoring | Status |
|---|------|------|-------------|--------|
| B1 | Extract calculatePrice() | order.js:45 | Extract Method | [ ] |
| B2 | Introduce OrderDetails object | order.js:12 | Introduce Parameter Object | [ ] |

---

## Detailed Refactoring Steps

### Task [ID]: [Task Name]

**Smell Addressed**: [Smell name]
**Refactoring Technique**: [Technique name]
**Risk Level**: Low / Medium / High

#### Context

**Before**:
```javascript
// Paste current code here
```

**After**:
```javascript
// Paste expected code here
```

#### Step-by-Step Mechanics

1. [ ] **Step 1**: [Description]
   - Test: Run tests after this step

2. [ ] **Step 2**: [Description]
   - Test: Run tests after this step

#### Verification

- [ ] All tests passing
- [ ] Behavior unchanged
- [ ] Code compiles

#### Commit Message
```
refactor: [Describe the refactoring]
```

---

## Progress Tracking

### Phase Status

| Phase | Status | Started | Completed | Tests Passing |
|-------|--------|---------|-----------|---------------|
| A | Not Started / In Progress / Done | | | |
| B | Not Started / In Progress / Done | | | |
| C | Not Started / In Progress / Done | | | |

---

## Post-Refactoring Checklist

- [ ] All tests passing
- [ ] No new warnings or errors
- [ ] Code compiles successfully
- [ ] Manual verification completed
- [ ] Documentation updated
- [ ] User sign-off obtained
