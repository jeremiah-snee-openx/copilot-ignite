# Flame Framework for GitHub Spark

## Purpose

Flame is the **execution and governance framework** that controls how GitHub Spark performs complex, multi-step refactors and architectural changes.

It exists to safely convert *approved intent* into *verified code changes* without scope creep, silent drift, or runaway automation.

Flame is authoritative. When Flame is present, GitHub Spark must operate under its rules.

---

## What Flame Is (and Is Not)

**Flame is:**

* A phase-gated execution system
* A human–machine contract
* A safety and verification layer
* A permanent execution record

**Flame is not:**

* The source of intent
* A brainstorming space
* An autonomous decision-maker

If Spark is the engine, **Flame is the control system**.

---

## Lifecycle of Intent

Flame operates on a strict lifecycle that defines how ideas become execution. Each stage represents a different **energy state of intent**, with explicit ownership and permissions.

### 1. Oil — Raw Intent (Human-Owned)

Unrefined ideas and observations.

Examples:

* Architectural critiques
* Brainstorms
* Review feedback
* Exploratory refactor notes

Properties:

* High ambiguity
* High potential energy
* **Not safe to execute**

Rules:

* Oil must never be executed by GitHub Spark.
* Oil must be refined by a human before entering Flame.

---

### 2. Fuel — Refined Intent (Human-Approved Input)

Oil that has been refined into a structured, explicit, executable plan.

Artifacts:

* `REFACTORING_PLAN.md`
* `flame/MASTER_PLAN.md` (read-only copy)

Properties:

* Ordered
* Explicit
* Testable
* Safe to burn *only under control*

Rules:

* Fuel defines **what may be done**.
* Fuel is immutable during execution.
* Spark may consume fuel, but may not create or modify it.

---

### 3. Phases — Controlled Burn Units

Fuel is divided into discrete, ordered execution units.

Artifacts:

* `flame/phases/NN-*.md`

Properties:

* Sequential
* Isolated
* Verifiable
* Gate-controlled

Rules:

* Only one phase may be active at a time.
* A phase must be completed and verified before the next phase begins.
* Phases define **how much fuel may be burned at once**.

---

### 4. Spark — Ignition (Executor)

Spark is the execution engine.

Properties:

* Fast
* Powerful
* Non-authoritative

Rules:

* Spark does not decide intent.
* Spark does not advance phases.
* Spark executes only within the active phase and Flame rules.

---

### 5. Flame — Containment & Governance

Flame is the system that makes execution safe.

Artifacts:

* `flame/`
* `flame/burning.md`

Responsibilities:

* Enforce ordering
* Define completion
* Require verification
* Preserve auditability

Summary rule:

> Spark may ignite fuel **only** inside Flame, **only** within the current phase, and **only** until verification criteria are met.

---

## Directory Structure

```
flame/
├── MASTER_PLAN.md      # Read-only copy of approved fuel
├── burning.md          # Append-only execution log
└── phases/
    ├── 00-dependency-cleanup.md
    ├── 01-router-setup.md
    ├── 02-testing-infra.md
    └── ...
```

---

## Phase Files (`flame/phases/NN-*.md`)

Each phase file must contain:

* A link to `flame/MASTER_PLAN.md`
* A concise **Context** section with only the most relevant constraints and rationale
* The full, detailed steps for that phase (copied from the master plan)
* A checklist of actionable items using markdown task syntax

Phase files are the **only surface** where Spark may actively work.

---

## Completion & Gating Rules (Hard Requirements)

A phase is complete only when **both** conditions are met:

1. All checklist items are marked complete.
2. A structured entry is appended to `flame/burning.md`.

Until both are satisfied:

* The phase is considered active.
* No subsequent phase may begin.

---

## `burning.md` — Execution Log

Rules:

* Created if missing
* Append-only unless explicitly overridden by a human
* One entry per completed phase

Required structure:

```
## Phase <N> — <Phase Title>
Date: YYYY-MM-DD
Summary:
- What changed

Verification:
- How correctness was validated

Notes:
- Optional
```

Verification guidance:

* Use passing tests when feasible
* Use grep or tooling output when relevant
* If verification is uncertain, explicitly request human confirmation

---

## Behavioral Rules for GitHub Spark

When Flame is present, GitHub Spark must:

* Treat Flame artifacts as **binding control structures**
* Never modify `REFACTORING_PLAN.md` or `flame/MASTER_PLAN.md`
* Never skip phases
* Never infer completion
* Never rewrite execution history
* Prefer correctness and traceability over speed
* Stop and wait when human confirmation is required

---

## Intent Flow Diagram (Agent-Readable)

```
[ Oil ]
  |
  | (Human refinement)
  v
[ Fuel ]
(REFACTORING_PLAN.md)
  |
  | (Read-only copy)
  v
[ MASTER_PLAN.md ]
  |
  | (Phase decomposition)
  v
[ Phase 00 ] -> [ Phase 01 ] -> [ Phase 02 ] -> ...
     |
     | (Spark executes)
     v
  [ Code Changes ]
     |
     | (Verification)
     v
[ burning.md ]
```

Control boundary:

* Spark operates only between **Phase → Code Changes**.
* Spark cannot refine intent or advance phases.

---

## In Short

Flame exists to make powerful automation **safe, deliberate, and reviewable**.

Fire is useful.
Uncontrolled fire is dangerous.

**Flame is the containment.**
