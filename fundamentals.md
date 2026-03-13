
# Electronics Fundamentals: From Physics to Interview Mastery

> **Who this is for:** Engineering students and embedded/VLSI job seekers who know the formulas but keep losing marks on "simple" questions. This guide focuses on the *physics-first thinking* that separates a textbook student from a working engineer.
>
> **How to use this:** Read each concept. Study the trap. Solve the problems at the end *before* checking answers.

---

## Table of Contents

1. [The Language of Scale — SI Prefixes & Notation](#1-the-language-of-scale--si-prefixes--notation)
2. [What is Electricity? — Physical Intuition](#2-what-is-electricity--physical-intuition)
3. [Ohm's Law, Power Law & the Square Laws](#3-ohms-law-power-law--the-square-laws)
4. [Series & Parallel Circuits — Divider Network Mastery](#4-series--parallel-circuits--divider-network-mastery)
5. [Ground, Earth, Neutral & Circuit Traps](#5-ground-earth-neutral--circuit-traps)
6. [Quick-Reference Cheat Sheet](#6-quick-reference-cheat-sheet)
7. [Practice Problems (60 Questions)](#7-practice-problems-60-questions)
8. [Answer Key](#8-answer-key)

---

## 1. The Language of Scale — SI Prefixes & Notation

### Why This Matters for Embedded & VLSI

In a datasheet you will read: *"Supply current: 2.3 mA, Input capacitance: 15 pF, Clock: 1.8 GHz, ESD rating: 2 kV."* If you cannot instantly convert these, you will make calculation errors and design mistakes even before the circuit is drawn.

### The Complete Prefix Table

| Prefix | Symbol | Power of 10 | Value | Embedded / VLSI Context |
|--------|--------|-------------|-------|--------------------------|
| Tera   | T      | 10¹²        | 1,000,000,000,000 | Storage (TB SSD) |
| Giga   | G      | 10⁹         | 1,000,000,000 | CPU clock (3.2 GHz) |
| Mega   | M      | 10⁶         | 1,000,000 | Baud rates (1 Mbps UART) |
| Kilo   | k      | 10³         | 1,000 | Resistor values (4.7 kΩ) |
| —      | —      | 10⁰         | 1 | Base unit |
| milli  | m      | 10⁻³        | 0.001 | Current consumption (3.3 mA) |
| micro  | μ      | 10⁻⁶        | 0.000001 | Capacitor values (100 μF) |
| nano   | n      | 10⁻⁹        | 0.000000001 | Propagation delay (5 ns) |
| pico   | p      | 10⁻¹²       | 0.000000000001 | Parasitic capacitance (15 pF) |
| femto  | f      | 10⁻¹⁵       | 10⁻¹⁵ | VLSI gate leakage delay |

### Conversion Rules (No Calculator Needed)

**Moving from a larger prefix to a smaller one → multiply (number gets bigger)**
- 3.3 kΩ = 3,300 Ω
- 100 μF = 100,000 nF = 100,000,000 pF

**Moving from a smaller prefix to a larger one → divide (number gets smaller)**
- 4,700 Ω = 4.7 kΩ
- 0.033 A = 33 mA

**The 3-step jump rule:** Each prefix step is 10³ (1000×).
- G → M → k → base → m → μ → n → p
- Jump one step = ×1000 or ÷1000
- Jump two steps = ×1,000,000 or ÷1,000,000

### ⚠️ Trap: Capital M vs lowercase m

| Symbol | Meaning | Example |
|--------|---------|---------|
| M (capital) | Mega = 10⁶ | 1 MΩ = 1,000,000 Ω |
| m (lowercase) | milli = 10⁻³ | 1 mA = 0.001 A |

**These are a factor of 10⁹ apart.** Writing "1 mΩ" when you mean "1 MΩ" is a 1-billion-times error. In VLSI, this distinction appears in MHz vs mHz (millihertz) — know which one your spec means.

### ⚠️ Trap: Unit Mismatch in Ohm's Law

A resistor is labelled **4k7**. What is its value?

> This is European notation. 4k7 = **4.7 kΩ = 4700 Ω**. The letter replaces the decimal point. Similarly: 2R2 = 2.2 Ω, 3M3 = 3.3 MΩ.

---

## 2. What is Electricity? — Physical Intuition

### The Core Physical Model

All electrical behaviour comes from **electrons** — negatively charged particles orbiting the nucleus of atoms. In some materials (conductors), the outermost electrons are loosely bound and can drift freely between atoms. In others (insulators), they are tightly bound and cannot move.

**Three fundamental quantities:**

| Quantity | Symbol | Unit | Physical Meaning |
|----------|--------|------|-----------------|
| Charge   | Q      | Coulomb (C) | Amount of electrons. 1C = 6.25 × 10¹⁸ electrons |
| Voltage  | V      | Volt (V) | Electrical "pressure" — difference in electron concentration between two points |
| Current  | I      | Ampere (A) | Rate of charge flow. 1A = 1 Coulomb passing a point per second |

### Voltage: The "Pressure" Analogy

Imagine two water tanks connected by a pipe. If both tanks have the same water level (same number of free electrons), **no water flows** — potential difference = 0 V.

If one tank is higher (more electrons on one side), water flows from high to low until levels equalize.

**Potential difference (voltage)** is the measure of this imbalance. A 9V battery maintains a 9V difference between its terminals by chemical action.

> **Key insight:** Voltage does not flow. Voltage is a *difference between two points*. You cannot have "voltage at a point" without specifying a reference. This is why ground (reference) matters.

### Current: Electron Flow vs Conventional Flow

Here is one of the most confusing topics for beginners:

**Electron current** flows from the **negative terminal to the positive terminal** (–ve → +ve). This is the actual physical movement of electrons.

**Conventional current** flows from the **positive terminal to the negative terminal** (+ve → –ve). This is a historical convention (Benjamin Franklin's era) that was defined *before* electrons were discovered.

```
Battery:    [–] ————————————————————— [+]
                ← ← ← electrons flow ← ←
                → → → conventional current → →
```

> **Interview Trap:** Almost all circuit analysis (KVL, KCL, Ohm's Law diagrams) uses **conventional current**. When a question asks "which direction does current flow?" — they almost always mean conventional current unless they say "electron flow." Getting this backwards will give you wrong polarity answers.

### Resistance: Friction for Electrons

Resistance is the property of a material that **opposes the flow of current** and converts electrical energy into heat.

- **Low resistance materials** (copper, gold, silver) → good conductors → electrons flow freely
- **High resistance materials** (rubber, glass, ceramic) → insulators → electrons cannot flow
- **Medium resistance materials** (silicon, germanium) → semiconductors → resistance is controllable

**Why resistance produces heat:**

Electrons collide with atoms as they move through a material. Each collision transfers kinetic energy to the atom, which vibrates more → temperature rises. This is **Joule heating**, and it is the operating principle of bulbs, heaters, and fuses.

### ⚠️ Trap: Static vs Dynamic Electricity

**Static electricity:** Charge is present but *not flowing* (example: a charged balloon, an unconnected battery). Voltage exists; current = 0.

**Dynamic electricity:** Charge is actively flowing through a closed path (example: a battery connected to a bulb). Both voltage and current exist.

> A battery sitting on a shelf has voltage (potential difference between terminals) but zero current. The moment you connect a wire, dynamic electricity begins. This is why the *closed loop* is essential — current cannot flow in an open circuit.

---

## 3. Ohm's Law, Power Law & the Square Laws

> **This is the most important section.** More than 60% of basic electronics interview traps come from misapplying the formulas in this section. Master every subsection before moving on.

### 3.1 Ohm's Law

```
V = I × R
```

Three forms — memorize all three:

| Find | Formula | Use when you know |
|------|---------|-------------------|
| Voltage | V = I × R | Current and resistance |
| Current | I = V / R | Voltage and resistance |
| Resistance | R = V / I | Voltage and current |

**The VIR Triangle (memory aid):**

```
        [ V ]
       /     \
     [I]  ×  [R]
```
Cover the unknown — the remaining two show the operation.

### 3.2 Power Law

Power is the **rate of energy conversion** — how many joules per second are being converted from electrical energy to heat, light, or motion.

```
P = V × I          (primary form)
P = I² × R         (when V is unknown — series circuits)
P = V² / R         (when I is unknown — parallel circuits)
```

**Energy vs Power:**
- Power (P) = rate, measured in **Watts (W)** = Joules per second
- Energy (E) = total amount consumed, measured in **Watt-hours (Wh)** or **Joules (J)**
- E = P × t

> **Why does current provide energy, not voltage?**
> Voltage is just potential — a difference in pressure. It takes actual movement of charge (current) to do work. Power = V × I. If I = 0 (open circuit), P = 0 even with 1000 V present. The voltage alone does nothing without current.

### 3.3 Component Ratings — The W@V Notation

When a component is rated **"230W @ 230V"**, it means:
- At 230V supply, it will consume 230W
- From this, you can extract its **resistance** (the only constant when voltage changes)

```
R = V²_rated / P_rated
```

| Rating | Resistance calculation | Result |
|--------|----------------------|--------|
| 230W @ 230V | R = 230² / 230 | **230 Ω** |
| 230W @ 115V | R = 115² / 230 | **57.5 Ω** |
| 100W @ 200V | R = 200² / 100 | **400 Ω** |
| 60W  @ 230V | R = 230² / 60  | **881.7 Ω** |

> **Critical rule:** The resistance of a component is determined by its rating. When the *actual supply voltage* changes, R stays the same (approximately — ignoring temperature effects). Recalculate current and power using the new voltage and the fixed R.

### 3.4 The Square Laws — The #1 Interview Trap

Because P = V²/R and P = I²R, power changes with the **square** of voltage or current changes.

**Voltage–Power Square Law (R constant):**

| Voltage change | Power change | Example |
|---------------|-------------|---------|
| ×2 (doubles) | ×4 | 100W bulb at double voltage → 400W |
| ×3 (triples) | ×9 | — |
| ×½ (halved) | ×¼ | 100W bulb at half voltage → 25W |
| ×⅓ | ×⅑ | — |

**Current–Power Square Law (R constant):**

| Current change | Power change | Example |
|---------------|-------------|---------|
| ×2 (doubles) | ×4 | Current doubles → heat quadruples |
| ×3 (triples) | ×9 | — |
| ×½ (halved) | ×¼ | — |

**Resistance–Power (depends on what is constant):**

| R changes | V constant | I constant |
|-----------|-----------|-----------|
| R doubles | P halves (P = V²/R) | P doubles (P = I²R) |
| R halves  | P doubles | P halves |

> **The Trap:** Students assume power is proportional to voltage. "Voltage halved → power halved." **Wrong.** Power drops to one-quarter. This fails people in TI, Bosch, Intel interviews every year. Whenever you see voltage or current change, immediately think: **square the ratio**.

### 3.5 Maximum Current Rating of a Resistor

A resistor has two ratings: **resistance value (Ω)** and **power rating (W)**. The power rating is its **destruction limit**.

```
I_max = √(P_rated / R)
V_max = √(P_rated × R)
```

**Example: 100 Ω, 1W resistor**
```
I_max = √(1 / 100) = √0.01 = 0.1 A = 100 mA
V_max = √(1 × 100) = √100 = 10 V
```

> If you push 150 mA through a 100 Ω 1W resistor: P = (0.15)² × 100 = 2.25 W. That is **2.25× its rating**. It will overheat and fail within seconds.

### 3.6 Why Wires Burn — Fuse Design Logic

Every wire has resistance. Thin wire = higher resistance per unit length. Current through resistance → P = I²R heat.

A fuse is simply a **calibrated thin wire** designed to melt at exactly the current that would overheat the circuit it protects.

```
A 1A fuse wire is designed so that:
P = (1)² × R_fuse = just enough heat to melt the metal above 1A
```

> **Interview question:** "A 0.5mm copper wire carries 10A. What happens?" → Calculate P = I²R per meter. Compare to the wire's thermal limit. It burns. This is why wire gauge (AWG) specifications exist — each gauge has a maximum current rating.

---

## 4. Series & Parallel Circuits — Divider Network Mastery

### 4.1 Series Circuits — The Golden Rules

In a series circuit (components in a single loop):

```
┌────[R1]────[R2]────[R3]────┐
│                            │
└────────── V_supply ────────┘
```

| Quantity | Behaviour | Formula |
|----------|-----------|---------|
| Current (I) | **Same** everywhere | I = V_supply / R_total |
| Voltage | **Divides** across each R | V_Rn = I × Rn |
| Resistance | **Adds** | R_total = R1 + R2 + R3 |
| Power | **Divides** | P_Rn = I² × Rn |

### 4.2 Parallel Circuits — The Golden Rules

In a parallel circuit (components share the same two nodes):

```
┌────┬────[R1]────┬────┐
│    │            │    │
│    └────[R2]────┘    │
│    └────[R3]────┘    │
│                      │
└────── V_supply ──────┘
```

| Quantity | Behaviour | Formula |
|----------|-----------|---------|
| Voltage (V) | **Same** across all | V = V_supply |
| Current | **Divides** into each branch | I_Rn = V / Rn |
| Resistance | **Reduces** (reciprocal sum) | 1/R_total = 1/R1 + 1/R2 |
| Power | **Divides** | P_Rn = V² / Rn |

> **Quick parallel R for two resistors:** R_total = (R1 × R2) / (R1 + R2). This "product over sum" formula only works for exactly **two** resistors.

### 4.3 Voltage Divider — Inspection Shortcuts

In a series chain with two resistors and a supply voltage V:

```
V_R1 = V × R1 / (R1 + R2)
V_R2 = V × R2 / (R1 + R2)
```

**The Ratio Mental Hacks (solve in seconds):**

| Ratio | Larger R gets | Smaller R gets |
|-------|--------------|----------------|
| Equal (1:1) | 50% | 50% |
| 2:1 (R1 = 2×R2) | 2/3 = 66.7% | 1/3 = 33.3% |
| 3:1 | 3/4 = 75% | 1/4 = 25% |
| 4:1 | 4/5 = 80% | 1/5 = 20% |
| N:1 | N/(N+1) | 1/(N+1) |

**Example (no calculator):** 12V supply, R1 = 30 kΩ, R2 = 10 kΩ. What is V across R2?

> Ratio = 3:1. R2 is smaller, so it gets 1/(3+1) = 1/4 of total. V_R2 = 12 × ¼ = **3 V**.

### 4.4 Current Divider — The Inverse Rule

In parallel, current splits **inversely** proportional to resistance. The smaller resistor gets more current.

```
I_R1 = I_total × R2 / (R1 + R2)   ← Note: R2 in numerator for R1's current
I_R2 = I_total × R1 / (R1 + R2)
```

**The Swap Mental Hack:**

| Ratio | Larger R gets | Smaller R gets |
|-------|--------------|----------------|
| Equal (1:1) | 50% | 50% |
| 2:1 (R1 = 2×R2) | 1/3 | 2/3 ← **opposite of voltage divider** |
| 3:1 | 1/4 | 3/4 |
| N:1 | 1/(N+1) | N/(N+1) |

> ⚠️ **Trap:** This is the **opposite** of the voltage divider rule. Students who memorize the voltage divider rule and apply it to current dividers get exactly the wrong answer. Voltage: big R gets big share. Current: big R gets *small* share.

**Sanity check always:** After splitting current, verify: V = I_R1 × R1 = I_R2 × R2. If voltages don't match, you flipped the ratio.

### 4.5 Which Resistor Gets Hotter?

This is one of the most common TI/Intel interview trick questions.

| Circuit type | What is constant | Which gets hotter | Formula to use |
|-------------|-----------------|-------------------|----------------|
| **Series** | Current (I) | **Higher R** | P = I²R (I same, bigger R → bigger P) |
| **Parallel** | Voltage (V) | **Lower R** | P = V²/R (V same, smaller R → bigger P) |

> These rules are **opposite to each other.** In series, higher resistance = more heat. In parallel, lower resistance = more heat. This trips up nearly everyone in a high-pressure interview.

**Proof for parallel (10Ω vs 20Ω, 20V supply):**
- P_10Ω = 20² / 10 = 40 W
- P_20Ω = 20² / 20 = 20 W
- The 10Ω dissipates **double** the power despite having half the resistance.

### 4.6 Open Circuit and Short Circuit

**Open Circuit:**
- Resistance = ∞
- Current = 0 A
- The *full supply voltage appears across the open gap* (nothing to drop it elsewhere)
- Nothing works; no current flows anywhere in a series open circuit

**Short Circuit:**
- Resistance = 0 Ω
- Voltage across the short = 0 V
- Current → theoretically infinite (limited only by source impedance and wire resistance)
- Components in parallel with a short are bypassed — they see 0 V and draw 0 current

> ⚠️ **Trap — Short circuit in parallel:** If a plain wire is connected across a 100 kΩ resistor, the resistor does nothing. All current flows through the wire. The output voltage at that node = 0 V regardless of what came before.

### 4.7 Power-to-Resistance Workflow (Solving Bulb Problems)

When a problem gives you power ratings (e.g., 40W and 60W bulbs):

**Step 1:** Convert all power ratings to resistance.
```
R = V_rated² / P_rated
```

**Step 2:** Build the equivalent circuit with resistors.

**Step 3:** Apply series/parallel rules to find total current.

**Step 4:** Use divider rules to find voltage/current/power at each element.

**Classic Wheatstone Bridge problem:**

40W @ 230V bulb: R₄₀ = 230²/40 = **1322.5 Ω**
60W @ 230V bulb: R₆₀ = 230²/60 = **881.7 Ω**

In a bridge with (R₄₀ top-left, R₆₀ bottom-left) and (R₆₀ top-right, R₄₀ bottom-right):

```
Left midpoint voltage  = 230 × R₆₀/(R₄₀+R₆₀) = 230 × 881.7/2204.2 = 92 V
Right midpoint voltage = 230 × R₄₀/(R₆₀+R₄₀) = 230 × 1322.5/2204.2 = 138 V
V_bridge = |138 - 92| = 46 V
```

---

## 5. Ground, Earth, Neutral & Circuit Traps

### 5.1 The Three "Zeros" — They Are Not the Same

| Term | Physical meaning | Voltage | In a circuit |
|------|-----------------|---------|-------------|
| **Earth (Safety ground)** | Wire bolted to earth/soil | ≈ 0V (safety reference) | Protects against insulation failure — fault current flows to earth instead of through you |
| **Neutral** | Return path of AC supply | ≈ 0V at substation, may drift | Carries return current from load back to generator |
| **Negative (–ve rail)** | Circuit reference point | Defined as 0V by convention | All other voltages in the circuit measured relative to this |
| **Floating node** | Wire connected to nothing | **Undefined** — could be anything | Acts as an antenna, picks up noise. Dangerous in digital circuits. |

> **Zero voltage ≠ no voltage:** A node tied to ground is intentionally at 0V. A floating node has *no defined* voltage. Connecting 5V to ground = short circuit (0Ω path between 5V and 0V = unlimited current). Connecting 5V to a floating node just assigns the floating node to 5V.

### 5.2 Illegal Circuit Configurations

**Configuration 1: Two different ideal voltage sources in parallel**

```
┌────[9V battery]────┐
│                    │  ← ILLEGAL
└────[6V battery]────┘
```

This forces 9V = 6V, which is mathematically impossible. In reality, the 9V source drives current through the internal resistance of both batteries: I = (9-6) / (r₁ + r₂). Massive current flows, one battery charges the other, heat is generated, something eventually fails.

> **Interview answer:** "This is an undefined circuit. Ideal voltage sources in parallel must be equal in voltage. In practice, the 3V difference divided by the small internal resistances causes a destructive current loop."

**Configuration 2: Current source in series with anything**

A current source in a series loop **defines the current for the entire branch**. Resistors, capacitors, and voltage sources in the same series path cannot change that current — they only adjust the voltage that appears across the current source.

```
[5V] ──── [2A current source] ──── [10Ω] ────
```
Current through 10Ω = **2A** (not 5V/10Ω = 0.5A). The voltage source adjusts what the current source "sees."

**Configuration 3: Short circuit across a node**

If a 0Ω wire exists from a node to ground, that node is at **0V**. Every component in parallel with that wire also has 0V across it and draws zero current. The wire takes all the current.

### 5.3 KVL and KCL — The Foundation of All Circuit Analysis

**Kirchhoff's Voltage Law (KVL):**
> The sum of all voltages around any closed loop = 0.

Practical use: In a loop, rises (voltage sources) = falls (resistor drops).

```
+V_supply - V_R1 - V_R2 = 0
V_supply = I×R1 + I×R2
```

**Kirchhoff's Current Law (KCL):**
> The sum of all currents entering a node = sum of all currents leaving a node.

Practical use: Current that enters a junction must split into the branches without loss.

```
I_in = I_R1 + I_R2 + I_R3
```

> ⚠️ **Trap — Applying KVL with a current source:** The current source defines I; you cannot use Ohm's Law to find it. Use KCL to find I first, then use KVL to find the voltage that appears across the current source.

### 5.4 The Diode Parallel Trap

When diodes are connected in parallel with different anode voltages:

```
    3V ──[D1]──┐
    6V ──[D2]──┼── Output
    9V ──[D3]──┘
                └── GND
```

**Wrong answer:** 3 + 6 + 9 = 18V. (Diodes are not batteries in series!)

**Right answer:** 9V

**Why:** The 9V source forward-biases D3 first, pulling the output node to 9V (ideal diodes). Now D1 has 3V on the anode and 9V on the cathode → **reverse-biased** (off). D2 has 6V on anode and 9V on cathode → **reverse-biased** (off). Only D3 conducts.

> **Mental rule for parallel diodes pointing toward output:** The **highest anode voltage wins**. All others are reverse-biased. If diodes point away from the output (cathodes at different voltages), the **lowest cathode voltage wins**.

---

## 6. Quick-Reference Cheat Sheet

### All Core Formulas

```
OHM'S LAW:          V = IR          I = V/R         R = V/I

POWER:              P = VI          P = I²R         P = V²/R

ENERGY:             E = Pt          (Watt-hours = Watts × hours)

SERIES R:           R_total = R1 + R2 + R3 + ...

PARALLEL R (2):     R_total = (R1 × R2) / (R1 + R2)

PARALLEL R (n):     1/R_total = 1/R1 + 1/R2 + 1/R3 + ...

VOLTAGE DIVIDER:    V_Rx = V_supply × Rx / R_total

CURRENT DIVIDER:    I_R1 = I_total × R2 / (R1 + R2)    ← R2 for R1's current

MAX CURRENT:        I_max = √(P_rated / R)

COMPONENT R:        R = V_rated² / P_rated
```

### The Square Law Quick-Reference

| Change | What is constant | Power result |
|--------|-----------------|-------------|
| V × 2 | R | P × 4 |
| V × 3 | R | P × 9 |
| V ÷ 2 | R | P ÷ 4 |
| V ÷ 3 | R | P ÷ 9 |
| I × 2 | R | P × 4 |
| I × 3 | R | P × 9 |
| I ÷ 2 | R | P ÷ 4 |
| R × 2 | V constant | P ÷ 2 |
| R × 2 | I constant | P × 2 |

### Series vs Parallel Summary

| Property | Series | Parallel |
|----------|--------|---------|
| Current | Same everywhere | Splits (more through smaller R) |
| Voltage | Splits (more across larger R) | Same everywhere |
| Resistance | Increases (sum) | Decreases (less than smallest) |
| Which R is hotter | **Larger** R | **Smaller** R |

### Open/Short Circuit Quick Reference

| State | R | I | V across it |
|-------|---|---|------------|
| Open circuit | ∞ | 0 A | Full supply voltage |
| Short circuit | 0 | Maximum | 0 V |

### Interview Problem-Solving Protocol

1. **Pause** — do not answer in 2 seconds
2. **State assumptions** — "Assuming ideal components..."
3. **Identify component states** — is each diode/transistor ON or OFF?
4. **Convert ratings to R** — always start with resistance
5. **Apply one law at a time** — Ohm's Law, then KVL/KCL
6. **Sanity check** — verify voltages in parallel are equal; verify currents at each node sum to zero
7. **Think out loud** — interviewers award marks for process, not just the answer

---

## 7. Practice Problems (60 Questions)

> Attempt every problem before looking at the Answer Key. For each problem, write down your reasoning, not just the number.

---

### Section 1 Problems — SI Prefixes & Notation

**P1.1** A microcontroller draws 1.8 mA from a 3.3V supply. Express the power consumption in μW and in mW.

**P1.2** A resistor is marked "4k7". What is its value in ohms? What current flows through it when 9.4V is applied?

**P1.3** A capacitor is rated 47μF. Express this in nF and in pF.

**P1.4 [TRAP]** An engineer writes "the oscillator runs at 100 mHz." A colleague says "that's 100 MHz — great!" Who is wrong, and by how much?

**P1.5** A signal propagates through a PCB trace in 0.5 ns. How far does it travel if the propagation speed is 2×10⁸ m/s? Express the answer in cm.

**P1.6 [GATE-style]** A transmission line has a delay of 100 ps per cm. A clock signal at 5 GHz period is ______ ps. Does 1 cm of trace introduce a significant fraction of one clock period?

**P1.7** Convert: 0.0033 A → mA, 4,700,000 Ω → MΩ, 0.000000022 F → nF, 3,300,000,000 Hz → GHz.

**P1.8 [TRAP]** A resistor is rated "1/4W". Its value is 100Ω. Someone applies 6V across it. Will it survive?

**P1.9** A datasheet says the IC has a standby current of 500 nA and active current of 8 mA. If the device is active 10% of the time and standby 90%, what is the average current draw?

**P1.10** A 2kΩ and a 500Ω resistor — express the ratio of their values and identify which prefix relationship connects them.

---

### Section 2 Problems — Physical Intuition

**P2.1** If a wire carries 2A of current, how many electrons pass a cross-section every second? (1 Coulomb = 6.25 × 10¹⁸ electrons)

**P2.2 [TRAP]** A battery has 9V between its terminals but is not connected to anything. How much current is flowing inside the battery?

**P2.3** You touch both terminals of a 9V battery simultaneously. You feel a slight tingle. Later, you touch both terminals of a 12V car battery. You feel nothing. Why might the car battery be less noticeable than expected?

**P2.4 [TRAP]** Two wires are connected: Wire A has 1000 free electrons per cm³ and Wire B has 1000 free electrons per cm³. What is the potential difference between them?

**P2.5** In a circuit diagram, conventional current flows clockwise. Which direction are the electrons physically moving?

**P2.6** A copper wire and a nichrome wire have the same dimensions. Which has higher resistance? Which would you use for a heater element and why?

**P2.7 [GATE-style]** A conductor carries 3A. The charge that flows through it in 2 minutes is ______ Coulombs.

**P2.8** A circuit is open. 12V supply is connected. What is the voltage across the open gap? What is the current through the circuit? What is the power consumed?

**P2.9 [TRAP]** A node in a circuit is "floating." A digital logic gate connected to this node reads HIGH or LOW unpredictably. Why? What is the fix?

**P2.10** Explain in physical terms (using electron movement) why a filament bulb glows but the copper wires connecting it do not.

---

### Section 3 Problems — Ohm's Law, Power & Square Laws

**P3.1** A 230W bulb is rated at 230V. Calculate: (a) its resistance, (b) the current it draws at rated voltage, (c) the current it draws if the supply drops to 115V, (d) the power it consumes at 115V.

**P3.2 [TRAP]** A 60W @ 230V bulb and a 100W @ 230V bulb are compared. Which has higher resistance? Most students get this wrong.

**P3.3** A resistor is rated 470Ω, 2W. (a) What is the maximum voltage you can apply? (b) What is the maximum current? (c) If you apply 40V, will it survive?

**P3.4 [TRAP]** The voltage across a resistor is doubled. By how much does the current change? By how much does the power change?

**P3.5 [GATE-style]** A heater element has a resistance of 100Ω and is rated for 230V. If the supply voltage drops by 10% (to 207V), by approximately what percentage does the heating power change?

**P3.6** A 100W, 200V bulb is connected to a 100V supply. Calculate the actual power consumed. (Do not use the 1/4 shortcut — show the full working.)

**P3.7 [TRAP]** Two identical 100W @ 230V bulbs are available. Which arrangement gives more total light: (a) both in series at 230V, or (b) both in parallel at 230V?

**P3.8** A wire has resistance 0.01Ω per meter. 10A flows through it. Calculate the power lost per meter of wire as heat.

**P3.9 [Interview Classic]** A 40W and a 60W bulb, both rated at 230V, are connected in **series** to a 230V supply. Which one glows brighter? Most people get this wrong.

**P3.10 [TRAP]** A resistor's power rating is exceeded by a factor of 4 (four times the rated power is dissipated). By what factor does the current exceed the rated maximum current?

---

### Section 4 Problems — Series, Parallel & Dividers

**P4.1** Three resistors 10Ω, 20Ω, and 30Ω are in series across a 120V supply. Find: (a) total resistance, (b) current, (c) voltage across each resistor, (d) power dissipated by each resistor.

**P4.2** The same three resistors (10Ω, 20Ω, 30Ω) are in parallel across a 120V supply. Find: (a) total resistance, (b) total current, (c) current through each resistor, (d) which resistor dissipates the most power.

**P4.3 [TRAP]** Two resistors are in parallel: 1kΩ and 1MΩ. Without calculating, what is the approximate combined resistance? Why?

**P4.4** A voltage divider uses R1 = 15kΩ and R2 = 5kΩ connected to 20V. Find V_R2 using (a) the full formula and (b) the ratio shortcut.

**P4.5 [TRAP]** A voltage divider output is connected to a load resistor equal to R2. The actual output voltage is no longer V × R2/(R1+R2). Why? Calculate the new output voltage for R1=10kΩ, R2=10kΩ, load=10kΩ, V=10V.

**P4.6** 12A total current enters a parallel junction with R1=4Ω and R2=12Ω. Using the current divider shortcut, find the current in each branch without calculating R_parallel first.

**P4.7 [TRAP — Wheatstone Bridge]** Four resistors form a bridge: R1=100Ω (top-left), R2=100Ω (top-right), R3=100Ω (bottom-left), R4=200Ω (bottom-right). Supply = 10V. Is the bridge balanced? If not, find the potential difference between the midpoints.

**P4.8 [Interview Classic]** A 40W bulb and a 60W bulb, both rated 230V, are in series on a 460V supply. Find the voltage across each bulb.

**P4.9 [TRAP]** In a parallel circuit, you add another resistor in parallel. Does the total resistance increase, decrease, or stay the same? Does the total current increase, decrease, or stay the same? Does the voltage across the original resistors change?

**P4.10 [GATE-style]** A circuit has a 100V supply, a 50Ω series resistor, and a parallel combination of 100Ω and 100Ω as the load. Find: (a) the voltage across the load, (b) the total power delivered by the source, (c) the power wasted in the series resistor.

---

### Section 5 Problems — Ground, Sources & Circuit Traps

**P5.1 [TRAP]** Three diodes (ideal, same type) have their anodes connected to 5V, 10V, and 15V respectively. All cathodes are tied together and connected to a 12V supply through a 1kΩ resistor (cathode side to supply positive). What is the voltage at the common cathode node?

**P5.2 [Interview Classic]** A 9V ideal battery and a 9V ideal battery are connected in parallel. What is the output voltage? Now, what if one is 9V and the other is 6V?

**P5.3 [TRAP]** A 2A ideal current source is in series with a 10V ideal voltage source and a 5Ω resistor (all in a single loop). (a) What is the current through the resistor? (b) What is the voltage across the current source?

**P5.4** A circuit node has: 5A flowing in from the left, 2A flowing out to the right, and a third branch. What current flows in the third branch, and in which direction?

**P5.5 [GATE-style]** Apply KVL to this loop: 12V source, 3Ω resistor, 6Ω resistor, all in series. Find current and voltage across each resistor. Then add a 6V source (opposing polarity) in series. Find the new current.

**P5.6 [TRAP — Diode Direction]** Three diodes have their **cathodes** connected to 3V, 6V, and 9V. All anodes are tied together to ground through a resistor. Which diode conducts? What is the voltage at the common anode?

**P5.7** A 1kΩ resistor is connected between a 5V node and ground. A plain wire (short circuit) is then connected directly across the resistor (from 5V node to ground). (a) What current flows through the wire? (b) What current flows through the resistor? (c) What is the voltage at the 5V node?

**P5.8 [Interview Classic]** A CMOS logic input pin is left unconnected (floating). Sometimes it reads logic '1', sometimes '0'. Explain why, and state the fix.

**P5.9 [TRAP]** In the circuit: 10V → 2kΩ → Node A → 3kΩ → GND. A voltmeter (ideal, infinite impedance) is connected from Node A to GND. What does it read? Now replace the voltmeter with a 6kΩ resistor. What is the voltage at Node A?

**P5.10 [GATE-style]** A delta (Δ) network has three equal resistors of 30Ω. Convert it to an equivalent star (Y) network. What is the value of each star resistor?

---

### Section 6 Problems — Mixed / Advanced

**P6.1** A 230V, 1000W heater element is used in a 115V region. (a) What is the power output? (b) Is this safe for the element?

**P6.2 [TRAP]** Two resistors are in series. R1 = 1Ω, R2 = 10,000Ω. The supply is 100V. Calculate the voltage across R1. What useful circuit does this approximate?

**P6.3 [GATE-style]** The power dissipated in a circuit is 100W when the supply is 200V. If the supply changes to 300V (resistance stays constant), what is the new power?

**P6.4** You have a 12V supply and need a 5V output for a microcontroller that draws 20mA maximum. Design a resistive voltage divider. State the limitation of this design.

**P6.5 [TRAP]** A capacitor charged to 10V is connected to a 5V battery. In which direction does current flow initially? (Assume the capacitor's positive plate is connected to the battery's positive terminal.)

**P6.6** A resistor of unknown value is connected to a 24V supply. A voltmeter reads 24V. An ammeter reads 0A. What is wrong with the circuit?

**P6.7 [Interview Classic]** You have three resistors, each 12Ω. By connecting them in different series/parallel combinations, what distinct resistance values can you create?

**P6.8 [GATE-style]** A Wheatstone bridge has R1=R2=R3=R4=1kΩ and a 10V supply. A galvanometer is connected across the midpoints. (a) Is it balanced? (b) If R4 changes to 1.001kΩ, what tiny voltage appears across the galvanometer?

**P6.9 [TRAP]** Two light bulbs are connected in parallel to a supply. Bulb A is rated 60W@120V; Bulb B is rated 100W@120V. Connected to a 120V supply in parallel, which is brighter? Now connect them in series to 240V — which is brighter?

**P6.10 [Interview Classic]** A fuse rated at 500mA is in series with a 100Ω load connected to a 12V supply. (a) Does the fuse blow under normal operation? (b) If the load short-circuits to 0Ω, does the fuse blow? (c) Why are fuses rated in current, not in power or voltage?

---

## 8. Answer Key

> Full solutions with reasoning. Study the *logic*, not just the number.

---

### Section 1 Answers

**P1.1:** P = 1.8 mA × 3.3V = 5.94 mW = **5940 μW**.
Conversion: 5.94 mW × 1000 = 5940 μW.

**P1.2:** 4k7 = **4700 Ω**. Current = V/R = 9.4/4700 = **0.002 A = 2 mA**.

**P1.3:** 47 μF = **47,000 nF** = **47,000,000,000 pF = 47×10⁹ pF**.

**P1.4 [TRAP]:** The engineer is wrong. mHz = millihertz = 0.001 Hz (one cycle every 1000 seconds — almost stationary). MHz = megahertz = 1,000,000 Hz. The difference is **10⁹ — a billion-fold error**. "mHz" in an oscillator spec is almost certainly a typo for MHz, but always clarify.

**P1.5:** Distance = speed × time = 2×10⁸ m/s × 0.5×10⁻⁹ s = **0.1 m = 10 cm**.

**P1.6:** Clock period at 5 GHz = 1/5×10⁹ = **200 ps**. 1 cm of trace = 100 ps delay = 100/200 = **50% of one clock period**. This is enormous — at 5 GHz, PCB trace length is a critical design parameter, not an afterthought.

**P1.7:**
- 0.0033 A = **3.3 mA**
- 4,700,000 Ω = **4.7 MΩ**
- 0.000000022 F = **22 nF**
- 3,300,000,000 Hz = **3.3 GHz**

**P1.8 [TRAP]:** P = V²/R = 36/100 = **0.36 W**. The rating is 1/4W = 0.25W. 0.36 > 0.25 — **it will overheat and fail**. 6V seems small but the 100Ω, 0.25W resistor is only safe up to V_max = √(0.25 × 100) = 5V.

**P1.9:** Average current = (0.1 × 8 mA) + (0.9 × 500 nA) = 0.8 mA + 0.00045 mA = **≈ 0.8 mA**. The 500 nA standby is negligible — active current dominates even at 10% duty cycle.

**P1.10:** 2kΩ / 500Ω = 4. They differ by a factor of 4, which doesn't correspond to a single prefix step (prefix steps are ×1000). The relationship is simply a factor of 4 within the same prefix range. 2kΩ = 2000Ω; 500Ω = 0.5kΩ.

---

### Section 2 Answers

**P2.1:** 2A = 2 C/s. Electrons per second = 2 × 6.25×10¹⁸ = **1.25 × 10¹⁹ electrons per second**.

**P2.2 [TRAP]:** **Zero current** flows inside an unconnected battery. Current requires a closed loop. The battery has internal chemistry maintaining the potential difference, but without an external path, no charge moves. (A very tiny amount of internal self-discharge occurs, but for circuit analysis this is zero.)

**P2.3:** The key factor is skin resistance and contact area. The sensation depends on the current through your body (I = V/R_body). Both batteries may push similar currents depending on your skin resistance. Also, a car battery has very low internal resistance and can deliver thousands of amps — the danger is not "no sensation" but rather the risk of arc flash or explosion from metallic shorting. The lack of sensation does not mean it is safer.

**P2.4 [TRAP]:** **0 V**. If both materials have the same free electron density, there is no imbalance — no potential difference. This is the definition of equipotential. Current only flows when there is a potential difference.

**P2.5:** **Counter-clockwise** (opposite to conventional current). Electrons flow from negative terminal, counter-clockwise, to positive terminal.

**P2.6:** Nichrome has higher resistance. Copper's free electron density is very high (low resistance) — ideal for wires. Nichrome has lower free electron density and higher resistivity — it heats up significantly at normal currents. **Nichrome for the heater** (high R → high heat per unit current). **Copper for wiring** (low R → minimal heat loss in transmission).

**P2.7 [GATE-style]:** Q = I × t = 3 A × (2 × 60 s) = 3 × 120 = **360 Coulombs**.

**P2.8:** Voltage across open gap = **12V** (full supply appears across the gap — nothing else to drop it). Current = **0 A**. Power = V × I = 12 × 0 = **0 W**. No current → no power consumed.

**P2.9 [TRAP]:** A floating node has no defined voltage — it drifts based on nearby electric fields, capacitive coupling, and noise. The gate input capacitance charges and discharges randomly → unpredictable logic level. **Fix: pull-up resistor** (to VCC, ensuring default HIGH) or **pull-down resistor** (to GND, ensuring default LOW). This is standard practice in all embedded digital design.

**P2.10:** Both the filament and copper wires carry the same current (series circuit). However: Filament resistance ≈ hundreds of ohms at operating temperature. Copper wire resistance ≈ milliohms per meter. P = I²R: the filament dissipates hundreds of watts per cm of length; the copper dissipates microwatts per meter. Heat concentration in the high-R filament raises it to ~2700°C → incandescence.

---

### Section 3 Answers

**P3.1:**
- (a) R = V²/P = 230²/230 = **230 Ω**
- (b) I = P/V = 230/230 = **1 A**
- (c) I = V/R = 115/230 = **0.5 A** (R is constant)
- (d) P = V²/R = 115²/230 = 13225/230 = **57.5 W** (not 115W — square law!)

**P3.2 [TRAP]:** The **60W bulb has higher resistance**. R = V²/P: higher P → lower R. Many students assume higher wattage = higher resistance because "bigger." Wrong. Higher wattage at the same voltage means more current draws, which means lower resistance. R₆₀ = 230²/60 = 882Ω; R₁₀₀ = 230²/100 = 529Ω.

**P3.3:**
- (a) V_max = √(P×R) = √(2×470) = √940 = **30.66 V**
- (b) I_max = √(P/R) = √(2/470) = **0.065 A = 65 mA**
- (c) P at 40V = V²/R = 1600/470 = **3.4 W**. Rated at 2W. 3.4W > 2W → **it will NOT survive**.

**P3.4 [TRAP]:** V doubled → current doubles (I = V/R, linear). But power: P = V²/R → **power quadruples (×4)**. Current: linear. Power: square. This is the core trap. If someone says "voltage doubled, so power doubled" — they are wrong.

**P3.5 [GATE-style]:** Original P = V²/R = 230²/100 = 529W. New P = 207²/100 = 42849/100 = 428.49W. Change = (428.49 - 529)/529 = -100.51/529 = **-19% approximately**. Note: a 10% voltage drop causes nearly a 20% power drop (square law — 0.9² = 0.81 → 19% reduction).

**P3.6:** R = V²_rated / P_rated = 200²/100 = 400Ω. P_actual = V²_actual / R = 100²/400 = 10000/400 = **25 W**. Shortcut: voltage halved → P = 100 × (1/2)² = 100/4 = 25W. ✓

**P3.7 [TRAP]:** Both bulbs have equal resistance (same rating). In series: each gets 115V, draws 0.5A, dissipates 57.5W each = 115W total. In parallel: each gets 230V, draws 1A, dissipates 230W each = **460W total**. **Parallel gives 4× more total light.** In series, each bulb gets half voltage → quarter power. Parallel wins dramatically.

**P3.8:** P = I²R = 10² × 0.01 = 100 × 0.01 = **1 W per meter**. A 10m cable loses 10W as heat. At higher currents, this scales as I² — wire selection is a safety-critical calculation.

**P3.9 [Interview Classic — Most Get Wrong]:** R₄₀ = 230²/40 = 1322.5Ω. R₆₀ = 230²/60 = 881.7Ω. In series, current is equal. P = I²R. Higher R → more power → **brighter. The 40W bulb glows brighter in series**, despite having a lower power rating. Why? Its higher resistance (designed for less power in normal use) dissipates more when forced to carry the same current as the 60W bulb.

**P3.10 [TRAP]:** Power exceeded by 4× means P_actual = 4 × P_rated. P = I²R. If P quadruples and R is constant, I² quadruples → I is doubled (√4 = 2). The current exceeds rated maximum by a factor of **2**. A 4× power overload = 2× current overload.

---

### Section 4 Answers

**P4.1:**
- (a) R_total = 10+20+30 = **60 Ω**
- (b) I = 120/60 = **2 A**
- (c) V₁₀ = 2×10 = **20V**, V₂₀ = 2×20 = **40V**, V₃₀ = 2×30 = **60V**. Check: 20+40+60 = 120V ✓
- (d) P₁₀ = 4×10 = **40W**, P₂₀ = 4×20 = **80W**, P₃₀ = 4×30 = **120W**. Higher R → more power in series.

**P4.2:**
- (a) 1/R = 1/10+1/20+1/30 = 6/60+3/60+2/60 = 11/60. R_total = **60/11 ≈ 5.45 Ω**
- (b) I_total = 120/5.45 = **22 A**
- (c) I₁₀ = 120/10 = 12A, I₂₀ = 120/20 = 6A, I₃₀ = 120/30 = 4A. Check: 12+6+4 = 22A ✓
- (d) **10Ω dissipates most**: P = V²/R = 14400/10 = 1440W. Lower R → more power in parallel.

**P4.3 [TRAP]:** Approximately **1kΩ**. The 1MΩ resistor is 1000× larger. In parallel, the combination is always less than the smaller value, and the 1MΩ adds almost nothing. Exact: (1000 × 1,000,000)/(1000 + 1,000,000) = 10⁹/1,001,000 ≈ **999 Ω**. Mental shortcut: when one parallel resistor is ≥10× larger than the other, the combination ≈ the smaller resistor.

**P4.4:**
- (a) V_R2 = 20 × 5/(15+5) = 20 × 5/20 = **5V**
- (b) Ratio: R1/R2 = 15/5 = 3. R1 is 3× R2. R2 gets 1/(3+1) = 1/4. V_R2 = 20 × 1/4 = **5V** ✓

**P4.5 [TRAP]:** The load (10kΩ) is in parallel with R2 (10kΩ). R2_effective = (10k × 10k)/(10k+10k) = **5kΩ**. New output = 10 × 5/(10+5) = 50/15 = **3.33V** (instead of 5V). Loading a voltage divider reduces the output. This is why voltage dividers are only used to drive high-impedance loads (or an op-amp buffer is inserted).

**P4.6:** R1=4Ω, R2=12Ω. Ratio = 3:1 (R2 is 3× R1). I_R1 = 12A × R2/(R1+R2) = 12 × 12/16 = **9A**. I_R2 = 12 × 4/16 = **3A**. Check: 9+3=12A ✓. Sanity: V across R1 = 9×4 = 36V; V across R2 = 3×12 = 36V ✓.

**P4.7 [TRAP]:** Left midpoint: V_L = 10 × R3/(R1+R3) = 10 × 100/200 = **5V**. Right midpoint: V_R = 10 × R4/(R2+R4) = 10 × 200/300 = **6.67V**. Bridge is **not balanced** (5V ≠ 6.67V). V_diff = |6.67 - 5| = **1.67V**. For balance: R1/R3 = R2/R4 → 100/100 = 100/200 → 1 ≠ 0.5. Not balanced.

**P4.8 [Interview Classic]:**
R₄₀ = 230²/40 = 1322.5Ω, R₆₀ = 230²/60 = 881.7Ω. R_total = 2204.2Ω.
I = 460/2204.2 = **0.2087A**.
V across 40W bulb = 0.2087 × 1322.5 = **276V**.
V across 60W bulb = 0.2087 × 881.7 = **184V**.
The **40W bulb has higher voltage across it** (it has higher resistance). Note: 276V > 230V rating — the 40W bulb may be over-stressed.

**P4.9 [TRAP]:**
- Total resistance: **decreases** (parallel paths always reduce total R)
- Total current: **increases** (I = V/R; V same, R drops, so I rises)
- Voltage across original resistors: **unchanged** (parallel circuits maintain constant voltage — V_supply)

**P4.10 [GATE-style]:**
R_load = 100Ω ∥ 100Ω = 50Ω. R_total = 50+50 = 100Ω.
(a) I = 100/100 = 1A. V_load = 1 × 50 = **50V**.
(b) P_source = V×I = 100×1 = **100W**.
(c) P_series = I²×R = 1×50 = **50W**. (Half the power is wasted in the series resistor — poor efficiency.)

---

### Section 5 Answers

**P5.1 [TRAP]:** The cathodes go through a 1kΩ resistor to +12V (supply positive). The cathodes face the supply. Diodes with anodes at 5V, 10V, 15V. For a diode to conduct, anode > cathode. The common cathode node will sit at the voltage such that one diode just forward-biases. The diode with the **highest anode (15V)** pulls the cathode node toward 15V. Other diodes: 10V anode vs 15V cathode → reverse biased; 5V anode vs 15V cathode → reverse biased. Output = **15V** (ideal diodes). With real diodes: 15V − 0.7V = 14.3V.

**P5.2 [Interview Classic]:** Two 9V ideal sources in parallel: **9V output** (equal sources — legal, no current flows between them). A 9V and a 6V ideal source in parallel: **undefined/illegal**. It creates a short between two voltage levels. In reality: V_out = somewhere between 6V and 9V depending on internal resistances; destructive current flows: I = (9-6)/(r₁+r₂).

**P5.3 [TRAP]:**
- (a) Current = **2A** (the current source defines the loop current entirely — the 10V and 5Ω cannot override it)
- (b) KVL: +10V − V_current_source − (2A × 5Ω) = 0 → 10 − V_CS − 10 = 0 → V_CS = **0V**. If the resistor changes to 10Ω: V_CS = 10 − (2×10) = −10V. The current source generates a negative voltage to maintain 2A.

**P5.4:** KCL: Currents in = Currents out. 5A in = 2A out + I_third. I_third = 5 − 2 = **3A flowing out**.

**P5.5 [GATE-style]:**
Loop 1 (no opposing source): I = 12/(3+6) = **12/9 = 1.33A**. V₃ = 1.33×3 = 4V, V₆ = 1.33×6 = 8V. Check: 4+8=12V ✓.
With 6V opposing source: Net voltage = 12−6 = 6V. I = 6/9 = **0.67A**. V₃ = 0.67×3 = 2V, V₆ = 0.67×6 = 4V.

**P5.6 [TRAP — Diode Direction]:** Cathodes at 3V, 6V, 9V; anodes tied together. For a diode to conduct, anode > cathode. The common anode will be pulled to the **lowest cathode voltage** minus the forward voltage. The diode with cathode at 3V will conduct first (easiest to forward-bias with anode pulled toward 3V). The 6V and 9V cathode diodes will be reverse-biased. Common anode voltage ≈ **3V − 0.7V = 2.3V** (real diode) or **3V** (ideal). **Lowest cathode voltage wins** when diodes point away from output.

**P5.7:**
- (a) Short circuit current: I_wire = V/R = 5/0 = **infinite** in theory; limited by source impedance in practice
- (b) V across resistor = 0V (short holds node at 0V); I_resistor = **0A**
- (c) Voltage at the "5V node" becomes **0V** — the short overrides the supply, creating a short circuit. The supply must be able to source this current or its output will also collapse.

**P5.8 [Interview Classic]:** A floating CMOS input has extremely high impedance — the input gate capacitance charges and discharges via electromagnetic coupling, body capacitance, and stray fields. Any tiny charge accumulation shifts the voltage above or below the switching threshold unpredictably → random logic level. **Fix:** 10kΩ pull-up to VDD (default HIGH) or pull-down to GND (default LOW). In embedded design, *every unused logic input must be terminated*.

**P5.9 [TRAP]:**
Ideal voltmeter (∞ impedance): it does not load the circuit. Node A = 100 × 3/(2+3) = **60V**. With 6kΩ at Node A: the 3kΩ and 6kΩ are in parallel = (3k×6k)/(3k+6k) = 18M/9k = **2kΩ**. New Node A = 100 × 2/(2+2) = 100 × 0.5 = **50V**. Loading reduces the measured voltage from 60V to 50V — a 17% error. This is why voltmeters must have very high impedance.

**P5.10 [GATE-style]:** Delta to Star (Y) conversion: R_star = R_delta / 3 (for equal resistors). Each star resistor = 30/3 = **10 Ω**. General formula (unequal): R_Y1 = (R_Δ12 × R_Δ13) / (R_Δ12 + R_Δ23 + R_Δ13).

---

### Section 6 Answers

**P6.1:**
R = 230²/1000 = 52.9Ω.
P_115V = 115²/52.9 = 13225/52.9 = **250W** (one-quarter of rated 1000W, as expected from square law).
Is it safe? The element is designed for 1000W. It only produces 250W at 115V — it will work but give much less heat output. It will not burn out (lower power = less thermal stress). **Safe, but inefficient.**

**P6.2 [TRAP]:**
V_R1 = 100 × 1/(1+10000) = 100/10001 ≈ **0.01V = 10mV**.
Nearly all of the 100V drops across R2. This approximates a **constant current source** — the large resistor limits current to I = 100/10001 ≈ 10mA regardless of small changes in R1.

**P6.3 [GATE-style]:**
R = V²/P = 200²/100 = 400Ω. New P = 300²/400 = 90000/400 = **225W**. Ratio check: (300/200)² = 1.5² = 2.25. 100 × 2.25 = 225W ✓.

**P6.4:**
MCU needs 5V at 20mA. Use a voltage divider: V_out = 5V, V_in = 12V, I_load = 20mA.
Choose I_divider >> I_load for stability (say 10× → 200mA): R_total = 12/200mA = 60Ω.
R2 (to GND) = 5V/200mA = 25Ω. R1 = 60−25 = 35Ω.
**Limitation:** Output voltage changes when load current changes. Heavy loads pull V_out down. A voltage regulator (7805 or LDO) is the proper solution for microcontroller power — a resistive divider wastes power and has poor regulation.

**P6.5 [TRAP]:** Capacitor is at 10V; battery is at 5V. The capacitor voltage (10V) is **greater** than the battery (5V). Current flows from the capacitor's positive plate, through the external circuit, **back into the battery** (charging it). The capacitor discharges from 10V, the battery charges slightly, until the capacitor reaches 5V. Direction: **from capacitor to battery**, opposite to what you'd expect if you only considered the battery.

**P6.6:** Voltmeter reads 24V (full supply). Ammeter reads 0A (no current). This means **the circuit is open**. The full supply voltage appears across the open gap (which is where the resistor would be). The resistor is either missing, disconnected at one terminal, or the wire is broken somewhere in the loop.

**P6.7:** With three 12Ω resistors, possible values:
- All series: 12+12+12 = **36Ω**
- All parallel: 12/3 = **4Ω**
- Two in series + one in parallel: (24×12)/(24+12) = 288/36 = **8Ω**
- Two in parallel + one in series: 6+12 = **18Ω**
- One alone: **12Ω**
Distinct values: **4Ω, 8Ω, 12Ω, 18Ω, 36Ω** (five values).

**P6.8 [GATE-style]:**
(a) R1/R2 = R3/R4 → 1/1 = 1/1 → **balanced**. V_galvanometer = 0V.
(b) With R4 = 1.001kΩ: Left mid = 10 × 1000/2000 = 5.000V. Right mid = 10 × 1001/2001 = 5.0025V. V_diff = **2.5mV**. This tiny voltage is what precision Wheatstone bridges use to detect minute resistance changes (strain gauges, temperature sensors).

**P6.9 [TRAP]:**
R_A = 120²/60 = 240Ω (60W bulb has more resistance). R_B = 120²/100 = 144Ω.
In parallel at 120V: P_A = 120²/240 = 60W, P_B = 120²/144 = 100W. **Bulb B (100W) is brighter in parallel.**
In series at 240V: Same current through both. I = 240/(240+144) = 240/384 = 0.625A.
P_A = (0.625)² × 240 = 93.75W. P_B = (0.625)² × 144 = **56.25W**.
**Bulb A (60W rated) is brighter in series** — because its higher resistance dissipates more power at the same current. The labels "60W" and "100W" are only valid at rated voltage.

**P6.10 [Interview Classic]:**
(a) Normal: I = 12V/100Ω = **0.12A = 120mA**. Fuse rated 500mA. 120mA < 500mA → **fuse does NOT blow**.
(b) Short circuit: R_load = 0Ω. I = 12V/0Ω → limited only by wire resistance (milliohms). Current >> 500mA → **fuse blows**.
(c) Fuses are rated in current because **heat = I²R** and the fuse element fails at a set temperature determined by how much current flows through its fixed resistance. Voltage and power both depend on the load (which changes); current through a series fuse is directly measurable and independent of what's downstream.

---

## Appendix: Common Interview Trap Summary

| Trap | Wrong Answer | Correct Answer |
|------|-------------|----------------|
| V halved → Power? | P halved | P drops to 1/4 (square law) |
| Higher wattage bulb = higher R? | Yes | No — higher W = lower R at same voltage |
| Parallel diodes with different V — output? | Add all voltages | Highest anode voltage wins |
| Current source in series — I through resistor? | V/R | Defined by current source |
| Two different ideal V sources in parallel | Average voltage | Undefined/illegal |
| Floating input reads? | Stable 0 or 1 | Random — undefined |
| Which series resistor is hotter? | Lower R (more current) | Higher R (P=I²R, I same) |
| Which parallel resistor is hotter? | Higher R (more resistance) | Lower R (P=V²/R, V same) |
| Capacitor at t=0, voltage across it? | V_supply | 0V (acts as short circuit) |
| Power rating exceeded 4× → current exceeded? | 4× | 2× (square root relationship) |

---

*This document is part of an embedded/VLSI interview preparation series.*
*Section 2: Digital Electronics, Number Systems & Logic Gates — coming next.*
