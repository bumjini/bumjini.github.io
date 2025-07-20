---
layout: distill
title: 'ILP Methods: FOIL and FOCL'
description: Preprint Papers
gradient: linear-gradient(135deg, #0064e1 0%, #5bd3ff 100%)
hover-gradient: linear-gradient(135deg, #00c6fb 0%, #005bea 100%)
date: 2025-07-20
background_color: rgb(255, 255, 255)
---

# Learning Logical Rules from Examples

## 1. Overview

**First-Order Inductive Learner (FOIL)** and **First-Order Combined Learner (FOCL)** are algorithms that learn logical rules from relational data.  
They take as input:
- **Facts** (also called atoms), e.g., `father(john, bob)`
- **Background knowledge**, e.g., known rules or domain theories

### Objectives
- Construct rules (clauses) that **cover all positive examples**
- Avoid covering **any negative examples**

### Key Differences

| Feature                    | FOIL               | FOCL                                   |
|---------------------------|--------------------|----------------------------------------|
| Search Space Constraints  | ❌ Not applied      | ✅ Applied                              |
| Use of Domain Theory      | ❌ Not used         | ✅ Utilized for guiding rule search     |
| Use of Example Patterns   | ❌ Not used         | ✅ Extracted from known examples        |


## 2. Concrete Example: Learning `grandfather`

### Family Tree
        john
       /    \
    mary     tom
     |         |
   alice     lucy

### Input Facts

    parent(john, mary).
    parent(mary, alice).
    parent(john, tom).
    parent(tom, lucy).

### Examples

    % Positive Examples
    grandfather(john, alice).   % John → Mary → Alice
    grandfather(john, lucy).    % John → Tom → Lucy

    % Negative Examples
    grandfather(mary, lucy).    % Mary is not Lucy’s grandfather
    grandfather(john, tom).     % John is Tom’s father, not grandfather

### Rule Construction Process (FOIL/FOCL)

1. Start with an empty clause:

        grandfather(X, Y) :- 

2. Add a literal (predicate):

        grandfather(X, Y) :- parent(X, Z)

3. Add another to eliminate negatives:

        grandfather(X, Y) :- parent(X, Z), parent(Z, Y)

4. Additional clauses may be added to cover all positives:

        grandfather(X, Y) :- man(X)

## 3. FOCL: Search Space Constraints

To improve efficiency, FOCL introduces constraints to reduce the size of the hypothesis space.

### Types of Constraints

1. **Variable Binding Constraints**  
   Ensure that variables are meaningfully shared between literals.

2. **Type Constraints**  
   Restrict variables to expected types (e.g., `X` is a male human).

3. **Semantic Constraints**  
   Disallow semantically invalid patterns.  
   Example:

        between(X, X, Y)  % Invalid: X cannot be between itself and Y

## 4. Key Concepts

### Variabilization
The process of generalizing concrete atoms by replacing constants with variables.  
Example:

    % From example:
    father(john, bob)
    % To general rule:
    father(X, Y)

### Operationalization
Turning abstract predicates into concrete, executable rules.  
Example:

    % Abstract
    illegal(X) :- unethical(X), harmful(X).

    % Operational
    illegal(X) :- breaks_law(X), causes_injury(X).

## References

- Quinlan, J.R. *Learning Logical Definitions from Relations*, Machine Learning, Vol. 5, No. 3, 1990.  
- Pazzani, M.J. *The Utility of Knowledge in Inductive Learning*, 1992.