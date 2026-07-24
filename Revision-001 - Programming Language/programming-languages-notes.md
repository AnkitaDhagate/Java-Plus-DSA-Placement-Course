# Programming Languages — Concepts & Interview Notes

Personal notes made while revising core CS fundamentals for interview prep.
Covers: types of programming languages, paradigms, typing systems, and Java memory management (Stack, Heap, Garbage Collection).

---

## Table of Contents
- [1. What is a Programming Language](#1-what-is-a-programming-language)
- [2. Levels Based on Translation](#2-levels-based-on-translation)
- [3. Paradigms](#3-paradigms)
- [4. Static vs Dynamic Typing](#4-static-vs-dynamic-typing)
- [5. Memory Management in Java](#5-memory-management-in-java)
- [6. Stack vs Heap](#6-stack-vs-heap)
- [7. How Garbage Collection Works](#7-how-garbage-collection-works)
- [8. Quick Interview Answers (Cheat Sheet)](#8-quick-interview-answers-cheat-sheet)

---

## 1. What is a Programming Language

To communicate with a person, we need a shared language. To communicate with a computer, we need a **programming language** — a set of instructions written in a specific, well-defined syntax that a machine can eventually execute.

At its core, it's a translation layer: humans think in logic and words, computers only understand binary signals (on/off). Programming languages exist to bridge that gap.

---

## 2. Levels Based on Translation

### A. Machine Language
- Lowest-level language — a series of `0`s and `1`s.
- This *is* what the CPU executes directly.
- Requires **no translation**, but is practically unreadable/unwritable by humans.

### B. Assembly Language
- Also low-level, but designed for a **specific processor architecture** (x86, ARM, etc.) — not portable across CPUs.
- Represents instructions in a symbolic, human-understandable form (e.g. `MOV`, `ADD`, `JMP`).
- Converted to machine code by an **Assembler**.

### C. High-Level Language
- Developer-friendly (Python, Java, C++, JavaScript...).
- Needs a **Compiler** (translates the whole program ahead of time — C, C++) or an **Interpreter** (executes line by line at runtime — Python) to convert it into machine-executable form.
- Java is a hybrid: source code compiles to **bytecode**, and the JVM interprets/JIT-compiles that bytecode at runtime.

| Level | Readability | Speed | Portability | Example |
|---|---|---|---|---|
| Machine | Very low | Fastest | None | Binary |
| Assembly | Low | Very fast | Processor-specific | x86 ASM |
| High-level | High | Depends on compiler/interpreter | High | Python, Java |

---

## 3. Paradigms

Paradigms describe *how you structure the solution*, not the language itself. Many languages support more than one paradigm.

### A. Procedural
- List of instructions telling the computer what to do, step by step.
- Program is divided into small procedures called **routines/functions**.
- Also called *structured programming*.
- Examples: **FORTRAN, C**

### B. Functional
- An approach to problem solving where every computation is treated as a **mathematical function**.
- A function takes `n` arguments and returns a value; it's evaluated logically as needed during execution.
- Emphasizes pure functions (no side effects) and function composition.
- Examples: **Python (supports it), Haskell**

### C. Object-Oriented (OOP)
- Programs are divided into small parts called **objects**, each bundling related data and functions together.
- Encourages reuse of these objects within the same program and across other programs.
- Built around four pillars: **Encapsulation, Inheritance, Polymorphism, Abstraction.**
- Example: **Java**

### D. Scripting
- Uses a high-level construct to interpret and execute **one command at a time**.
- Generally easier to learn and faster to write than structured/compiled languages like C or C++.
- Commonly used for automation, gluing systems together, and web behavior.

---

## 4. Static vs Dynamic Typing

### E. Statically Typed Language
- Type checking happens **at compile time**.
- Declaring the data type is compulsory (`int age = 25;`).
- Catches type errors early; enables better tooling/autocomplete; generally faster execution.
- Examples: **Java, C, C++**

### F. Dynamically Typed Language
- Type checking happens **at run time**.
- No need to declare data types upfront (`age = 25`).
- More flexible/faster to write, but type errors only surface when that line actually executes.
- Examples: **Python, JavaScript**

> **Interview soundbite:** "Static typing catches errors at compile time; dynamic typing catches them at runtime — it's a trade-off between safety and flexibility."

---

## 5. Memory Management in Java

In Java, **memory management** is the process of allocating and de-allocating memory for objects during a program's execution.

Java handles this **automatically** through a background process called the **Garbage Collector (GC)** — unlike C/C++, where developers manually allocate (`malloc`) and free (`free`) memory.

---

## 6. Stack vs Heap

| | Stack Memory | Heap Memory |
|---|---|---|
| Stores | Variables, method call frames | Objects |
| Scope | Per-thread | Shared across the application |
| Speed | Very fast | Slower than stack |
| Management | Automatic — LIFO order, freed when method returns | Managed by the Garbage Collector |
| Failure mode | `StackOverflowError` (e.g. infinite recursion) | `OutOfMemoryError` (heap fills up) |

**Rule of thumb:** primitive local variables and references live on the **Stack**; the actual objects those references point to live on the **Heap**.

```java
void example() {
    int x = 10;                 // x -> stored on the Stack
    Person p = new Person();    // 'p' reference -> Stack
                                 // the actual Person object -> Heap
}
```

---

## 7. How Garbage Collection Works

A simplified version of the **Mark-and-Sweep** algorithm most JVM garbage collectors are built on:

1. GC starts from **"root" references** — local variables currently on the Stack, static variables, etc.
2. It walks the Heap, **marking** every object still reachable from a root as *live*.
3. Any object with **no path back to a root** is considered *unreachable* — nothing in the running program can access it anymore.
4. Unreachable objects are **swept away**, and their memory is freed for reuse.

Modern JVM collectors add more sophistication on top of this basic idea — e.g. **generational garbage collection**, which separates "young" (recently created, likely short-lived) objects from "old" (long-lived) objects and collects them with different strategies for efficiency. Worth mentioning if the interview goes deeper into JVM internals.

---

## 8. Quick Interview Answers (Cheat Sheet)

**Q: What's the difference between compiled and interpreted languages?**
> A compiler translates the entire program into machine code before execution (faster runtime, e.g. C++). An interpreter translates and executes line by line at runtime (more flexible, easier to debug, e.g. Python).

**Q: What's the difference between procedural and OOP?**
> Procedural organizes code around functions operating on data; OOP bundles data and the functions that operate on it into objects, enabling encapsulation and reuse.

**Q: Static vs dynamic typing — which is "better"?**
> Neither is strictly better — static typing trades flexibility for early error detection and performance; dynamic typing trades safety for speed of development. The right choice depends on the project.

**Q: How does Java manage memory?**
> Automatically, via the Garbage Collector. Local variables live on the Stack and are cleared when a method returns; objects live on the Heap and are cleared by the GC once they become unreachable — i.e., nothing references them anymore.

**Q: What causes a memory leak in Java if GC is automatic?**
> If an object is still referenced somewhere (e.g. held in a static collection, or a listener that's never removed) even though it's logically "done," GC can't reclaim it — the reference itself is the leak, not a GC failure.

---

*Notes based on personal lecture material — compiled while prepping for software development interviews.*
