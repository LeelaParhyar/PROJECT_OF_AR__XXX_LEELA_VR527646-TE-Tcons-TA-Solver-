# Implementation of a Solver for the Union of the Theories of Equality, Lists, and Arrays

## Course

Planning and Automated Reasoning – Automated Reasoning  
Academic Year 2025–2026  
University of Verona

## Project Description

This project implements a prototype solver for determining the satisfiability of conjunctions of literals in the quantifier-free union of the following theories:

- **TE** : Theory of equality with free (uninterpreted) symbols
- **Tcons** : Theory of non-empty, possibly cyclic lists
- **TA** : Theory of arrays without extensionality

The solver is designed to handle mixed inputs, where literals from different theories appear together in the same problem. Rather than using a general-purpose theory combination framework (e.g., Nelson–Oppen), the solver follows the theory-specific reduction procedures presented in class:

- Array constraints are simplified by eliminating store and select through case splitting
- List constraints are handled by generating structural axioms for cons, car, and cdr
- The resulting problem is solved using congruence closure for equality reasoning

The implementation is written in Java (JDK 17) and serves as a pedagogical prototype, emphasizing correctness and adherence to theoretical foundations rather than full industrial optimization.

## Project Structure

```
project-root/
│
├── Main.java                 # Main solver implementation
│
├── inputs/                   # Input test files
│   ├── Test_TE_01.txt
│   ├── Test_TE_02.txt
│   ├── Test_TE_03.txt
│   ├── Test_TE_04.txt
│   ├── Test_Tcons_01.txt
│   ├── Test_Tcons_02.txt
│   ├── Test_Tcons_03.txt
│   ├── Test_Tcons_04.txt
│   ├── Test_TA_01.txt
│   ├── Test_TA_02.txt
│   ├── Test_TA_03.txt
│   └── Test_TA_04.txt
│
├── outputs/                  # Corresponding output files (SAT / UNSAT)
│   ├── Test_TE_01.out
│   ├── Test_TE_02.out
│   ├── Test_TE_03.out
│   ├── Test_TE_04.out
│   ├── Test_Tcons_01.out
│   ├── Test_Tcons_02.out
│   ├── Test_Tcons_03.out
│   ├── Test_Tcons_04.out
│   ├── Test_TA_01.out
│   ├── Test_TA_02.out
│   ├── Test_TA_03.out
│   └── Test_TA_04.out
│
└── README                    # This file
```

## Compilation Instructions

### Requirements

- Java Development Kit (JDK) 17 or newer
- Linux, Windows, or macOS

### Compile

From the project root directory:

```bash
javac Main.java
```

This command generates the corresponding .class files.

## Execution Instructions

Run the solver by providing an input file as argument:

```bash
java Main inputs/Test_TE_01.txt
```

## Output

The solver prints one of the following to standard output:

- **SAT**  : The input set of literals is satisfiable
- **UNSAT** : The input set of literals is unsatisfiable

## Input Format

- Each non-empty line represents a single literal
- Comments start with `#` and are ignored

**Supported literals:**

- Equality: `eq(expr1, expr2)`
- Disequality: `neq(expr1, expr2)`

**Expressions:**

- Variables: lowercase identifiers (e.g., `x`, `y`)
- Constants: uppercase identifiers (e.g., `A`, `B`)
- Function applications:
  - `f(a,b)`
  - `cons(a,b)`
  - `store(A,i,v)`
  - `select(A,i)`

Each input file contains a comment stating the source of the problem, as required by the assignment.

## Solver Features and Notes

- Handles mixed theories (TE, Tcons, TA) in a single input
- Eliminates array store / select via case splitting
- Automatically adds list structural axioms
- Uses congruence closure with:
  - Path compression
  - Largest-class representative heuristic
- Maximum term nesting depth is limited to 10
- Array extensionality is not supported, as required

## Input Sources

- Course lecture examples (Planning and Automated Reasoning)
- Bradley & Manna, *The Calculus of Computation*
- Nelson–Oppen congruence closure examples
- Kroening & Strichman, *Decision Procedures*
- Adapted academic examples for lists and arrays

Each source is explicitly documented in the corresponding input file.
