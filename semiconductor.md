# Semiconductors, Diodes & Transistors: From Physics to Interview Mastery

> **Part 2 of the Electronics Fundamentals Series**
> **Prerequisites:** Complete `01-electronics-fundamentals.md` before this module.
>
> **Who this is for:** Students targeting VLSI, Embedded, Analog Design roles at companies like TI, Intel, Qualcomm, Bosch, Samsung, ISRO. This document is built around the **exact traps** asked in those interviews — not textbook problems.
>
> **Rule:** Read every concept. Study every ⚠️ Trap. Solve all 60 problems **before** looking at answers.

---

## Table of Contents

1. [From Electrical to Electronics — The Controlled Switch](#1-from-electrical-to-electronics--the-controlled-switch)
2. [Semiconductor Physics — Band Theory, P-type & N-type](#2-semiconductor-physics--band-theory-p-type--n-type)
3. [The P-N Junction & Diode](#3-the-pn-junction--diode)
4. [Diode Circuits — Rectifiers, Clippers & Clampers](#4-diode-circuits--rectifiers-clippers--clampers)
5. [Bipolar Junction Transistor (BJT)](#5-bipolar-junction-transistor-bjt)
6. [Field Effect Transistor (FET) & MOSFET](#6-field-effect-transistor-fet--mosfet)
7. [Practice Problems (60 Questions)](#7-practice-problems-60-questions)
8. [Answer Key](#8-answer-key)

---

## 1. From Electrical to Electronics — The Controlled Switch

### 1.1 What is the Difference?

**Electrical engineering** deals with generating, transmitting, and consuming electrical power. The focus is on large-scale energy — motors, generators, transformers, power grids.

**Electronics** is a *subset* of electrical engineering. The fundamental difference:

> **Electronics = using small electrical signals to control other electrical signals.**
> Mathematical model: **Output Y = F(Input X)**

You are not just moving energy — you are *processing information* using energy.

### 1.2 Why We Need an Electrically Controlled Switch

In the earliest automated systems, **mechanical relays** were used:
- A small current through a coil → creates a magnetic field → attracts a metal arm → closes a contact
- This was the first "electrical control of electrical signals"

**Problems with mechanical relays:**
- Slow switching (milliseconds) — cannot work at MHz or GHz speeds
- Mechanical wear — spring fatigue, contact arcing, burn marks
- Large and heavy — cannot miniaturize
- Spark generation — dangerous in explosive environments

**The solution:** Replace the moving mechanical arm with a **solid-state device** that has no moving parts. This is the fundamental motivation for all semiconductor devices.

> **The entire field of electronics — from the triode vacuum tube to the modern MOSFET — is the story of building a better electrically-controlled switch.**

### 1.3 The Vacuum Tube Triode — First Electronic Switch

Before semiconductors, engineers used **vacuum tubes**:

**Vacuum Tube Diode (Fleming, 1904):**
- Glass tube with air evacuated
- Cathode heated by a filament → emits electrons (thermionic emission)
- Anode (plate) — electrons flow only from cathode to anode → one-way valve
- This is the first diode — a unidirectional current device

**Vacuum Tube Triode (De Forest, 1906):**
- Added a third electrode: the **Grid** between cathode and anode
- Grid voltage controls electron flow from cathode to anode
- Small voltage on grid → controls large current from cathode to anode
- **This is the first amplifier and the first electronic switch**

**How the Triode works as a switch:**
- Grid at **0V** → electrons flow freely → tube is **ON** (conducting)
- Grid at **−5V (negative)** → electrons repelled back → tube is **OFF** (not conducting)
- Intermediate grid voltages → intermediate current → **amplifier action**

> **The triode was essentially a voltage-controlled variable resistor.** More negative grid voltage = higher resistance = less current. This exact concept transfers directly to modern MOSFETs.

**Why triodes were replaced:**
- Needed heating power (filament) → wasted energy
- Fragile glass envelopes
- Large physical size
- High operating voltages (100s of volts)
- Could not be miniaturized

**Bell Labs invented the transistor in 1947** — a solid-state device with identical function, no heating required, small, reliable, and scalable to nanometer sizes.

---

## 2. Semiconductor Physics — Band Theory, P-type & N-type

### 2.1 Why Semiconductors? — The Energy Band Model

Every solid material can be understood using **energy band theory**. Electrons in a solid do not have arbitrary energies — they exist in allowed energy bands separated by **forbidden gaps**.

**Three critical energy bands:**

| Band | Description | Electrons Here |
|------|-------------|----------------|
| **Valence Band** | Highest band that is filled at 0K | Bound to atoms — cannot move freely |
| **Forbidden Gap (Eg)** | No allowed energy states | Cannot exist here |
| **Conduction Band** | Above the forbidden gap | Free to move — these carry current |

**Classification of solids by band gap:**

```
CONDUCTOR:        Valence band and conduction band OVERLAP
                  Eg = 0 eV
                  Electrons move freely at room temperature
                  Example: Copper, Aluminum, Gold

SEMICONDUCTOR:    Small forbidden gap
                  Eg ≈ 0.7 eV (Germanium), 1.1 eV (Silicon)
                  At 0K — insulator. At room temp — partial conductor
                  Conductivity controllable by doping

INSULATOR:        Large forbidden gap
                  Eg ≈ 5 eV (Diamond, SiO₂, Glass)
                  Electrons cannot cross the gap at normal temperatures
                  Current does not flow
```

> **1 eV (electron volt)** = energy gained by one electron accelerated through 1 volt = 1.6 × 10⁻¹⁹ Joules. This is the unit used for energy gaps because it is scaled perfectly for electron energy levels.

### 2.2 Silicon — The Foundation of Modern Electronics

Silicon (Si) has atomic number 14 with the electron configuration:
- 2 electrons in the first orbit
- 8 electrons in the second orbit
- **4 valence electrons** in the outermost orbit

These 4 valence electrons are what make silicon useful. In a pure silicon crystal, each atom forms **4 covalent bonds** with its 4 neighboring atoms — each bond shares one electron from each atom, completing an 8-electron outer shell.

At **absolute zero (0K):** All 4 bonds are intact. No free electrons. Silicon is a perfect insulator.

At **room temperature (300K):** Thermal energy breaks some covalent bonds. A freed electron leaves behind a **hole** — a missing electron that behaves like a positive charge.

> **Hole** is not a physical particle — it is an abstraction for a missing electron in a covalent bond. But it behaves exactly like a positive charge of magnitude +1.6 × 10⁻¹⁹ C. In an intrinsic semiconductor, holes and electrons are always generated in equal numbers.

### 2.3 Intrinsic Semiconductor — Pure Silicon

**Key properties of intrinsic (pure) silicon:**

- Equal number of electrons (n) and holes (p): n = p = nᵢ (intrinsic carrier concentration)
- At 300K for Silicon: nᵢ ≈ 1.5 × 10¹⁰ carriers/cm³
- At 300K for Germanium: nᵢ ≈ 2.4 × 10¹³ carriers/cm³
- **Conductivity increases with temperature** (more bond breakages at higher T)
- This gives semiconductors a **Negative Temperature Coefficient (NTC)** of resistance — the opposite of metals

**Two mechanisms of current flow in a semiconductor:**
1. **Drift current:** Movement of carriers due to electric field (V applied externally)
2. **Diffusion current:** Movement of carriers from high concentration to low concentration (even without E field)

> ⚠️ **Trap:** "Semiconductor resistance increases with temperature, like a metal." **FALSE.** Semiconductor resistance *decreases* with temperature (NTC). Metal resistance *increases* with temperature (PTC). This is one of the most commonly tested distinctions.

### 2.4 Extrinsic Semiconductor — Doped Silicon

Pure silicon has very few free carriers at room temperature — it is a poor conductor. **Doping** — adding controlled impurity atoms — dramatically increases conductivity.

**Two types of dopants:**

#### N-Type Semiconductor (Donor Doping)

Doping silicon with **pentavalent** atoms (5 valence electrons):
- Phosphorus (P), Arsenic (As), Antimony (Sb)

What happens:
- The dopant atom forms 4 covalent bonds with neighboring Si atoms (uses 4 of its 5 electrons)
- The **5th electron has no bond to complete** — it becomes a **free electron** with very little energy needed (≈ 0.045 eV for P in Si)
- Each donor atom donates one free electron without creating a hole

**Result:**
- Majority carriers: **Electrons** (much more numerous due to doping)
- Minority carriers: **Holes** (thermally generated, few in number)
- The dopant atom becomes a positively charged **immobile ion** (it gave away its extra electron)
- The material is electrically neutral overall (ion⁺ + electron⁻ = net zero)

> ⚠️ **Trap:** "N-type semiconductor is negatively charged." **FALSE.** N-type has more free electrons than holes, but the material is electrically neutral. The donated electrons are balanced by the positively ionized donor atoms fixed in the crystal lattice.

#### P-Type Semiconductor (Acceptor Doping)

Doping silicon with **trivalent** atoms (3 valence electrons):
- Boron (B), Aluminum (Al), Gallium (Ga), Indium (In)

What happens:
- The dopant atom forms 3 covalent bonds with neighboring Si atoms (uses all 3 electrons)
- The **4th bond cannot be completed** — a **hole** exists where the missing electron would be
- Each acceptor atom accepts one electron from the silicon lattice, creating a hole

**Result:**
- Majority carriers: **Holes**
- Minority carriers: **Electrons**
- The dopant atom becomes a negatively charged **immobile ion** (it accepted an electron)
- The material is electrically neutral overall

**Summary comparison:**

| Property | N-Type | P-Type |
|----------|--------|--------|
| Dopant type | Pentavalent (Group V) | Trivalent (Group III) |
| Dopant examples | P, As, Sb | B, Al, Ga |
| Dopant called | Donor | Acceptor |
| Majority carriers | Electrons | Holes |
| Minority carriers | Holes | Electrons |
| Immobile ion charge | Positive (+) | Negative (−) |
| Overall material charge | **Neutral** | **Neutral** |

### 2.5 The Mass Action Law

For any semiconductor (doped or undoped):

```
n × p = nᵢ²
```

Where:
- n = electron concentration
- p = hole concentration
- nᵢ = intrinsic carrier concentration

**This law always holds at thermal equilibrium.** If doping increases electrons (n), it *suppresses* holes (p), and their product stays constant at nᵢ².

**Example:** If Si is doped with donors so that n = 10¹⁶/cm³, and nᵢ = 1.5×10¹⁰/cm³:
```
p = nᵢ²/n = (1.5×10¹⁰)²/10¹⁶ = 2.25×10²⁰/10¹⁶ = 2.25×10⁴ holes/cm³
```
The minority holes are reduced to an extremely small number.

---

## 3. The P-N Junction & Diode

### 3.1 Formation of the P-N Junction

When P-type and N-type semiconductor materials are brought together (in the same crystal), something remarkable happens at the boundary:

**Step 1 — Diffusion:** Electrons from the N-side (high electron concentration) diffuse across the junction into the P-side. Holes from the P-side diffuse into the N-side. This is pure diffusion — driven by concentration gradient, no external voltage needed.

**Step 2 — Recombination:** When electrons meet holes near the junction, they recombine and annihilate each other, leaving behind:
- On the N-side near the junction: Positively charged donor ions (the electrons that left them behind have recombined)
- On the P-side near the junction: Negatively charged acceptor ions (the holes that left them have recombined)

**Step 3 — Depletion Region forms:** The region near the junction is now swept clean of free carriers — only fixed immobile ions remain. This region is called the **depletion region** (also: space charge region, transition region).

**Step 4 — Built-in Electric Field:** The fixed positive ions on N-side and fixed negative ions on P-side create an electric field pointing from N to P (from + to −). This field opposes further diffusion.

**Step 5 — Equilibrium:** The built-in field creates a **barrier potential (V_B)** that exactly opposes diffusion. At equilibrium, net current = 0.

```
Barrier potential (V_B):
  Silicon (Si):    V_B ≈ 0.6 to 0.7 V at 25°C
  Germanium (Ge):  V_B ≈ 0.2 to 0.3 V at 25°C
```

> ⚠️ **Critical Trap:** The barrier potential **cannot be measured with a voltmeter** placed across the P-N junction. A voltmeter measures the potential difference between two terminals. When you connect a voltmeter, you create two new metal-semiconductor junctions (at the probes) that have their own contact potentials. These exactly cancel the barrier potential. The measured result is always 0V. **You cannot harness the barrier potential as a free energy source — it would violate the second law of thermodynamics.**

### 3.2 Forward Bias — Diode Conducts

Connecting external voltage: **+ve terminal to P-side, −ve terminal to N-side**

What happens:
1. External voltage **opposes** the built-in field
2. Depletion region width **shrinks** (external field cancels built-in field)
3. Barrier potential **reduces** (V_barrier = V_B − V_applied)
4. When V_applied > V_B: Majority carriers can now cross the junction freely
5. Large current flows — Diode is **ON**

**Forward voltage drop (at rated current):**
- Silicon: **≈ 0.7 V** (sometimes specified as 0.6V to 0.7V)
- Germanium: **≈ 0.3 V**

**In circuit analysis:**
- Ideal diode model: 0V drop when forward biased (switch ON, short circuit)
- Practical model: 0.7V drop (Si) when forward biased
- Full model: 0.7V drop + bulk resistance R_B × I_D

### 3.3 Reverse Bias — Diode Blocks

Connecting external voltage: **+ve terminal to N-side, −ve terminal to P-side**

What happens:
1. External voltage **aids** the built-in field
2. Depletion region width **increases**
3. Barrier potential **increases** (V_barrier = V_B + V_applied)
4. Majority carriers cannot cross — they are pulled away from the junction
5. Only **minority carriers** can cross (thermally generated, very few)
6. Very small **reverse saturation current (I_S or I_O)** flows

```
Reverse saturation current:
  Silicon:     I_S < 1 µA at 25°C
  Germanium:   I_S up to 10 µA at 25°C
```

**Temperature dependence of I_S:**
- Silicon: I_S doubles for every **10°C** rise in temperature
- Germanium: I_S doubles for every **6°C** rise in temperature

> ⚠️ **Trap:** "No current at all flows in reverse bias." **FALSE.** A very small reverse saturation current (leakage current) flows due to minority carriers. This current is independent of applied reverse voltage (it is saturated — hence "saturation current") but doubles with every 10°C temperature rise. This matters enormously in high-temperature applications and VLSI leakage power calculations.

### 3.4 Reverse Breakdown

If reverse voltage is increased beyond a critical value (**V_BR — Breakdown Voltage**):

**Two mechanisms:**

**1. Avalanche Breakdown (high V_BR, typically > 6V):**
- Strong electric field in depletion region accelerates minority carriers to high velocities
- These carriers collide with bound electrons in covalent bonds, knocking them free
- Each freed electron is accelerated and knocks out more electrons
- Avalanche multiplication — exponential growth of reverse current

**2. Zener Breakdown (low V_BR, typically < 6V):**
- Very high doping → very thin depletion region
- Thin depletion → very strong electric field even at low voltages
- Electric field directly breaks covalent bonds, freeing carriers
- Does not require carrier multiplication

> **Zener diodes** exploit this breakdown in a controlled, non-destructive way. Heavily doped → thin depletion → low, sharp breakdown voltage. Used as voltage references and regulators. Normal diodes are not designed for breakdown — they are destroyed if operated there.

### 3.5 The Diode Equation (Shockley Equation)

```
I_D = I_S × (e^(V_D / η·V_T) − 1)
```

Where:
- I_D = diode current
- I_S = reverse saturation current
- V_D = voltage across diode
- η = ideality factor (1 for Ge, 1–2 for Si)
- V_T = thermal voltage = kT/q = **26 mV at 25°C (300K)**

**Key behaviors from the equation:**

| Condition | Simplified Result |
|-----------|------------------|
| V_D >> V_T (forward bias) | I_D ≈ I_S × e^(V_D/V_T) — exponential growth |
| V_D = 0 | I_D = 0 |
| V_D << 0 (reverse bias) | I_D ≈ −I_S — constant saturation current |

> **Thermal voltage V_T = 26 mV at 25°C.** This is one of the most important constants in electronics. At other temperatures: V_T = kT/q. At 60°C: V_T ≈ 29 mV. This appears in BJT small-signal models (r_e = V_T/I_C) and MOSFET subthreshold behavior.

### 3.6 Diode Models — Three Levels of Approximation

**Level 1 — Ideal Diode:**
- Forward biased: Voltage drop = **0V**, acts as short circuit (closed switch)
- Reverse biased: Current = **0A**, acts as open circuit (open switch)
- Use when: Quick estimation, when supply voltage >> 0.7V

**Level 2 — Constant Voltage Drop (CVD) Model:**
- Forward biased: Voltage drop = **0.7V (Si) or 0.3V (Ge)**
- Reverse biased: Current = 0A
- Use when: Most practical analysis, interview problems

**Level 3 — Complete Model (Bulk Resistance):**
- Forward biased: Voltage drop = V_B + I_D × R_B
- V_B = 0.7V (Si), R_B = bulk resistance of diode (typically 0.1Ω to 10Ω)
- Use when: Precise design, current-sensitive circuits

**Diode I-V Characteristic Summary:**

```
Current (I)
    |                    /  ← Forward characteristic
    |                   /     (exponential rise above knee)
    |                  /
    |              knee (0.7V Si)
    |______________|______________________ Voltage (V)
    |←← −V_BR    0    0.3(Ge) 0.7(Si)
    |
  −I_S ← Reverse saturation current (very small, flat)
    |
    ↓ Breakdown region (current rises sharply negative)
```

### 3.7 Important Diode Specifications

| Parameter | Symbol | Meaning | Typical Si value |
|-----------|--------|---------|-----------------|
| Forward voltage | V_F | Voltage drop when conducting | 0.6–0.7 V |
| Maximum forward current | I_F(max) | Maximum safe continuous current | 1A (1N4001) |
| Peak Inverse Voltage | PIV or V_RRM | Maximum reverse voltage before breakdown | 50V (1N4001) to 1000V (1N4007) |
| Reverse saturation current | I_S | Leakage current in reverse | < 1 µA |
| Reverse recovery time | t_rr | Time to switch from ON to OFF | 5–50 ns |

---

## 4. Diode Circuits — Rectifiers, Clippers & Clampers

### 4.1 Half-Wave Rectifier

Converts AC to pulsating DC by blocking one half-cycle.

```
Circuit: AC source → Diode → Load (R_L)

During positive half-cycle: Diode forward biased → conducts
During negative half-cycle: Diode reverse biased → blocks
```

**Key parameters:**

| Parameter | Formula | Notes |
|-----------|---------|-------|
| Peak output voltage | V_m − 0.7 | V_m = peak AC input |
| Average (DC) output | V_dc = V_m/π ≈ 0.318 × V_m | For ideal diode: V_m/π |
| RMS output | V_rms = V_m/2 | |
| Ripple factor | γ = 1.21 | High ripple — poor DC quality |
| Rectification efficiency | η = 40.6% | Low efficiency |
| PIV of diode | V_m | Diode must withstand V_m reverse voltage |
| Output frequency | Same as input (50 Hz in India) | |

### 4.2 Full-Wave Rectifier (Centre-Tap)

Uses two diodes and a centre-tapped transformer.

**Key parameters:**

| Parameter | Formula |
|-----------|---------|
| Peak output voltage | V_m − 0.7 (one diode drop) |
| Average (DC) output | V_dc = 2V_m/π ≈ 0.636 × V_m |
| RMS output | V_rms = V_m/√2 |
| Ripple factor | γ = 0.48 |
| Rectification efficiency | η = 81.2% |
| PIV of each diode | **2V_m** ← important trap |
| Output frequency | **2 × input frequency** (100 Hz for 50 Hz input) |

> ⚠️ **Trap — PIV in Centre-Tap Rectifier:** When one diode is conducting, the full secondary voltage (2V_m) appears across the non-conducting diode in reverse. PIV = **2V_m**, not V_m. Students who forget the factor of 2 underrate their diode and it fails in the circuit.

### 4.3 Bridge Rectifier (Full-Wave)

Uses four diodes in a bridge configuration — no centre-tap transformer needed.

**Key parameters:**

| Parameter | Formula |
|-----------|---------|
| Peak output voltage | V_m − 1.4 (TWO diode drops) |
| Average (DC) output | V_dc = 2V_m/π ≈ 0.636 × V_m |
| RMS output | V_rms = V_m/√2 |
| Ripple factor | γ = 0.48 |
| Rectification efficiency | η = 81.2% |
| **PIV of each diode** | **V_m** (only V_m, not 2V_m) |
| Output frequency | 2 × input frequency |

> ⚠️ **Trap — Bridge vs Centre-Tap PIV:** Bridge rectifier PIV = **V_m**. Centre-tap rectifier PIV = **2V_m**. Same output quality, but bridge diodes face half the reverse voltage stress. This is a classic comparison question in GATE and interviews.

> ⚠️ **Trap — Bridge Rectifier Voltage Drop:** Two diodes conduct simultaneously in a bridge rectifier. The output voltage is reduced by **1.4V (2 × 0.7V)**, not 0.7V. For low-voltage applications (3.3V, 5V), this 1.4V drop is significant.

### 4.4 Filter Capacitor and Ripple

A capacitor in parallel with the load stores charge during diode conduction and releases it during the off period, smoothing the output.

**Ripple voltage (peak-to-peak) with capacitor filter:**
```
V_ripple ≈ V_m / (f × C × R_L)     [for half-wave]
V_ripple ≈ V_m / (2f × C × R_L)    [for full-wave]
```

To reduce ripple:
- Increase C (larger capacitor)
- Increase R_L (lighter load = less current drawn)
- Increase f (higher frequency — reason why switching power supplies run at 100kHz+)

### 4.5 Clipper Circuits

**A clipper removes (clips) a portion of the waveform beyond a set level.**

**Series Positive Clipper:**
- Diode in series with load, oriented to block positive half
- Negative half passes through; positive half is clipped to 0V
- Output = negative half of input only

**Series Negative Clipper:**
- Diode reversed compared to positive clipper
- Positive half passes; negative half clipped
- Output = positive half of input only

**Biased Clipper (with reference voltage V_R):**
- Diode in series with reference battery V_R
- Diode conducts only when V_in > V_R (for positive clipper with bias)
- Output is clipped at V_R level, not at 0V
- Used for precision waveform shaping

> ⚠️ **Trap — Clipper with Reversed Diode and Bias:** Many students flip the diode direction and get the opposite clipping region. Always trace the circuit: which direction is the diode oriented? When does it forward bias? What voltage appears at output during that state?

**Parallel Clipper:**
- Diode in parallel with load (not series)
- When diode conducts, it clamps the output node to 0V (or V_R)
- The input-side resistor then drops the remaining voltage

### 4.6 Clamper Circuits

**A clamper shifts the entire waveform up or down without changing its shape.**

The clamper "adds a DC level" to the AC signal. Key components: Capacitor (C), Diode (D), Resistor (R).

**RC time constant rule:** τ = RC must be >> T (period of input signal). Typically RC ≥ 10T. This ensures the capacitor does not discharge significantly between cycles.

**Positive Clamper (shifts waveform upward):**
- Diode oriented to charge capacitor during negative half-cycle
- Capacitor charges to V_m with polarity opposing input
- During positive half-cycle: diode off, capacitor acts as battery in series
- Output peak = V_m + V_m = **2V_m**
- Entire waveform shifted up so negative peak touches 0V

**Negative Clamper (shifts waveform downward):**
- Diode reversed
- Positive peak is clamped to 0V
- Output peak-negative = **−2V_m**

> ⚠️ **Trap — Clamper changes peak voltage, not amplitude:** The amplitude (peak-to-peak) of the waveform is **unchanged** by clamping. If input was 2V_m peak-to-peak, output is still 2V_m peak-to-peak. Only the DC level (reference) shifts. Students often think the output is larger — it has the same shape, just moved.

---

## 5. Bipolar Junction Transistor (BJT)

### 5.1 Structure and Types

The BJT consists of **three semiconductor layers** forming two P-N junctions:

**NPN Transistor:**
```
Emitter (N) | Base (P) | Collector (N)
```
- Emitter: Heavily doped N-type (source of electrons)
- Base: Very thin, lightly doped P-type (control layer)
- Collector: Moderately doped N-type (collects carriers)

**PNP Transistor:**
```
Emitter (P) | Base (N) | Collector (P)
```
- Majority carriers are holes (opposite of NPN)
- Current directions are reversed

**The transistor has three terminals:**
- **Base (B):** Control terminal — small input current here
- **Collector (C):** Output terminal — large current here
- **Emitter (E):** Common terminal — sum of base and collector currents

### 5.2 BJT as a Physical Device — How It Actually Works (NPN)

Understanding the physics is essential for interview questions.

**Step 1 — Emitter-Base Junction: Forward Biased**
- V_BE ≈ 0.7V (Si), with +ve at Base, −ve at Emitter
- Electrons from N-type emitter are injected across the EB junction into the P-type base
- This is exactly like a forward-biased diode — electrons flood the base region

**Step 2 — What happens in the Base?**
- Base is very **thin** (micrometers) and **lightly doped**
- Most injected electrons (95-99%) do NOT recombine with holes in the base
- They diffuse rapidly through the thin base region toward the collector junction

**Step 3 — Collector-Base Junction: Reverse Biased**
- V_CB ≈ several volts, with +ve at Collector, −ve at Base
- The reverse-biased CB junction has a strong electric field in the depletion region
- Electrons arriving from the emitter (through the base) are **swept into the collector** by this field
- A small fraction (1-5%) recombines in the base — these lost electrons are replenished by the base current

**Result:**
```
I_E = I_C + I_B

Where:
I_C >> I_B (typically I_C = 50 to 500 × I_B)
```

**The transistor amplification factor:**
- **β (beta) = h_FE = I_C / I_B** (DC current gain, common-emitter)
- **α (alpha) = I_C / I_E = β/(β+1)** (DC current gain, common-base)
- Typical β: 50 to 500 for signal transistors

> **Physical insight:** The BJT works because of the thin, lightly-doped base. If the base were thick or heavily doped, all injected electrons would recombine there and never reach the collector. The transistor is essentially a mechanism to "pass" electrons from emitter to collector, controlled by a small base current.

### 5.3 BJT as a Variable Resistor — The Amplifier Concept

The transistor in active mode is best understood as a **voltage-controlled variable resistor**:

```
Circuit concept (Common-Emitter):

    VCC
     |
    [R_C] ← Collector resistor (load)
     |
     C
B ──[BJT]
     E
     |
    GND
```

**The transistor + R_C forms a voltage divider:**
- V_CE = V_CC − I_C × R_C
- I_C is controlled by V_BE (and hence I_B)
- As V_BE increases → I_B increases → I_C increases → more voltage drops across R_C → V_CE decreases

**For small AC signal superimposed on DC bias:**
- Small V_BE signal → modulates I_C
- Large variation in V_CE (across R_C) for small variation in V_BE
- **This is voltage amplification**

The transistor itself acts like a **voltage-controlled current source** (I_C depends on V_BE) or equivalently, a variable resistor in the V_CE path.

> **The voltage divider insight:** Think of the BJT as a variable resistor between collector and emitter. V_BE controls this resistance. A large V_CC is divided between R_C (fixed) and R_CE (variable, BJT). Small changes in R_CE (controlled by tiny V_BE signal) cause large changes in V_CE. **This is the transistor amplifier — a voltage divider with a voltage-controlled element.**

### 5.4 BJT Operating Regions

| Region | EB Junction | CB Junction | I_C | V_CE | Application |
|--------|------------|-------------|-----|------|-------------|
| **Cutoff** | Reverse biased | Reverse biased | ≈ 0 | ≈ V_CC | Switch OFF |
| **Active** | Forward biased | Reverse biased | β × I_B | Varies | Amplifier |
| **Saturation** | Forward biased | Forward biased | Max (limited by R_C) | ≈ 0.2V | Switch ON |
| **Reverse Active** | Reverse biased | Forward biased | Small | — | Not used normally |

**For a switch (digital logic):**
- OFF state → Cutoff: V_BE < 0.5V, I_C ≈ 0
- ON state → Saturation: V_BE ≈ 0.7V, V_CE(sat) ≈ 0.2V

> ⚠️ **Trap — What is V_CE(sat)?** When a BJT is fully ON (saturated), V_CE is not 0V. It is approximately **0.2V for Si BJT**. This is V_CE(saturation). If your circuit design assumes V_CE = 0 in saturation, your output voltage calculation will be off by 0.2V. In low-voltage designs (3.3V), this matters significantly.

### 5.5 BJT Configurations

Three ways to connect a BJT in a circuit:

| Configuration | Input | Output | Current Gain | Voltage Gain | Phase Shift | Use |
|---------------|-------|--------|-------------|-------------|-------------|-----|
| **Common Emitter (CE)** | Base | Collector | β (high) | High | **180°** (inverted) | Most used — amplifier |
| **Common Base (CB)** | Emitter | Collector | α < 1 | High | 0° (non-inverted) | High-frequency |
| **Common Collector (CC)** | Base | Emitter | β+1 (high) | < 1 (unity) | 0° (non-inverted) | Buffer, impedance matching |

> ⚠️ **Trap — CE Configuration Phase Inversion:** The Common-Emitter amplifier **inverts** the signal (180° phase shift). If you apply a positive-going signal at the base, the collector output goes negative. This is because as I_C increases, the voltage drop across R_C increases, and V_CE = V_CC − I_C×R_C **decreases**. Students who forget this phase inversion will design feedback circuits with wrong polarity.

### 5.6 BJT Current Relationships — Essential Formulas

```
FUNDAMENTAL:
    I_E = I_C + I_B

CURRENT GAINS:
    β = h_FE = I_C / I_B    (common-emitter current gain, 50–500)
    α = I_C / I_E           (common-base current gain, always < 1)

RELATIONSHIP BETWEEN α AND β:
    α = β / (β + 1)
    β = α / (1 − α)

COLLECTOR CURRENT IN ACTIVE MODE:
    I_C = β × I_B

TRANSCONDUCTANCE:
    g_m = I_C / V_T = I_C / 0.026    (in Ampere/Volt or Siemens)

SMALL-SIGNAL EMITTER RESISTANCE:
    r_e = V_T / I_C = 1/g_m = 26mV / I_C
```

> ⚠️ **Trap — α is always less than 1:** Since I_C < I_E (some current goes to base), α = I_C/I_E is always < 1. Typical values: 0.95 to 0.999. If you calculate α > 1, something is wrong. β can be 50, 100, 500 — but α can never exceed 1.

---

## 6. Field Effect Transistor (FET) & MOSFET

### 6.1 FET vs BJT — Fundamental Difference

| Property | BJT | FET/MOSFET |
|----------|-----|-----------|
| Control mechanism | **Current** controlled (I_B controls I_C) | **Voltage** controlled (V_GS controls I_D) |
| Input impedance | Low (kΩ range) | Extremely high (GΩ — gate is insulated) |
| Majority carriers | Both electrons and holes (bipolar) | Only one type — electrons (NMOS) or holes (PMOS) |
| Noise | Higher (two carrier types) | Lower (unipolar) |
| Speed | Fast at lower frequencies | Better at high density, digital |
| Temperature stability | Less stable (I_C rises with T) | More stable (mobility decreases with T) |
| Dominance | Analog circuits, power | **Digital VLSI, memories, processors** |

### 6.2 MOSFET Structure

**MOSFET = Metal Oxide Semiconductor Field Effect Transistor**

**N-Channel Enhancement MOSFET (NMOS) structure:**
```
Gate (Metal/Poly) ─── [Oxide (SiO₂)] ─── [P-substrate]
                                              |      |
                                           Source  Drain
                                           (N+)    (N+)
```

- **Gate:** Control terminal. Insulated from substrate by thin SiO₂ layer (gate oxide). No DC current flows into gate.
- **Source:** Where carriers originate. In NMOS, electrons flow out from source.
- **Drain:** Where carriers are collected.
- **Substrate (Body):** P-type silicon base. Usually connected to most negative supply (GND for NMOS).
- **Gate oxide (SiO₂):** Insulating layer — this is why gate draws virtually zero current.

### 6.3 MOSFET Operating Principle

**Enhancement NMOS (most common in digital):**

The gate voltage **creates** (enhances) a conducting channel. There is no channel without gate voltage.

**When V_GS < V_th (threshold voltage):**
- No channel exists between drain and source
- No current flows (regardless of V_DS)
- MOSFET is **OFF** (cutoff)

**When V_GS > V_th:**
- Gate positive voltage repels holes in P-substrate below the oxide
- Attracts electrons → forms a thin N-type **inversion layer** (channel) between source and drain
- Current can now flow from drain to source
- MOSFET is **ON**

**The channel is controlled by V_GS — this is the voltage-controlled current source**

### 6.4 MOSFET Operating Regions

**Threshold voltage (V_th):** Minimum V_GS to create a channel. Typically 0.3V to 2V depending on process.

| Region | Condition | I_D Formula | Application |
|--------|-----------|-------------|-------------|
| **Cutoff** | V_GS < V_th | I_D = 0 | Switch OFF |
| **Linear (Triode)** | V_GS > V_th AND V_DS < (V_GS − V_th) | I_D = k[(V_GS−V_th)V_DS − V_DS²/2] | Switch ON (resistive) |
| **Saturation** | V_GS > V_th AND V_DS ≥ (V_GS − V_th) | I_D = (k/2)(V_GS − V_th)² | Amplifier |

Where k = μ_n × C_ox × W/L (process and geometry dependent)

> ⚠️ **Trap — MOSFET Saturation Definition:** In a BJT, saturation means the transistor is fully ON (both junctions forward biased, V_CE ≈ 0.2V). In a MOSFET, saturation means the transistor is operating as a constant current source (pinch-off of the channel). **BJT saturation = fully ON. MOSFET saturation = active region (amplifier).** These are opposites conceptually — do not mix them up.

### 6.5 The V_GS Trap — Most Common Interview Error

**The most critical rule for MOSFET operation:**

> **MOSFET switches based on V_GS — the voltage between Gate and Source. NOT V_G alone.**

```
V_GS = V_G − V_S

If Source is at 0V (GND): V_GS = V_G   [simple case]
If Source is NOT at 0V:   V_GS = V_G − V_S   [trap case]
```

**Interview Example:**
- V_th = 1V
- Gate = 5V
- Source = 0V → V_GS = 5V > 1V → **MOSFET ON** ✓

Now change: Source = 6V, Gate = 5V
→ V_GS = 5 − 6 = **−1V** < 1V → **MOSFET OFF** ✗

> ⚠️ **This is the #1 trap in VLSI and embedded interviews.** Whenever source is not grounded, always calculate V_GS explicitly. A MOSFET with Gate = 5V and Source = 5V is completely OFF (V_GS = 0).

### 6.6 PMOS vs NMOS

**PMOS (P-Channel MOSFET):**
- Source connected to V_DD (positive supply)
- Conducts when V_GS < −V_th (gate voltage is negative relative to source, i.e., pulled LOW)
- Majority carriers: **Holes**
- Turns ON when gate is LOW (in digital logic context)

**NMOS:**
- Source typically at GND
- Conducts when V_GS > V_th (gate pulled HIGH)
- Turns ON when gate is HIGH

**CMOS (Complementary MOS):** Uses both NMOS and PMOS together. The fundamental building block of all digital logic ICs.

| | NMOS | PMOS |
|--|------|------|
| Turns ON when | Gate = HIGH | Gate = LOW |
| Source connected to | GND (V_SS) | V_DD |
| Majority carriers | Electrons | Holes |
| Speed | Faster (µ_n > µ_p) | Slower (µ_p ≈ µ_n/2 to µ_n/3) |

> ⚠️ **Trap — PMOS Control:** In a CMOS inverter, when input is HIGH: NMOS turns ON (pulls output to GND) and PMOS turns OFF. When input is LOW: PMOS turns ON (pulls output to V_DD) and NMOS turns OFF. Students who say "PMOS turns on at HIGH gate" are wrong — the PMOS gate is relative to its source (V_DD), so HIGH gate means V_GS ≈ 0 → OFF.

### 6.7 MOSFET as a Switch — Digital Logic

In digital circuits, MOSFET is used purely as a switch (ON or OFF, not in between):

**NMOS Switch:**
- Gate = 0V (LOW) → OFF — infinite resistance between Drain and Source
- Gate = V_DD (HIGH) → ON — very low resistance (R_DS(on)), typically milliohms to ohms

**Switching speed limitation — Gate Capacitance:**
- The gate oxide forms a capacitor (C_gs, C_gd, C_ox)
- Switching requires charging/discharging this capacitor
- Larger W/L ratio → faster channel formation → but larger capacitance
- This is the fundamental tradeoff in digital design: **speed vs power**

**Dynamic power consumption in CMOS:**
```
P_dynamic = α × C × V_DD² × f
```
Where:
- α = activity factor (fraction of gates switching per clock cycle)
- C = load capacitance (gate capacitance of driven gates)
- V_DD = supply voltage
- f = clock frequency

> **This formula explains why reducing V_DD by half saves 4× dynamic power (square law).** It also explains why modern chips are designed for lower supply voltages (1.0V, 0.8V) rather than the original 5V of TTL logic.

---

## 7. Practice Problems (60 Questions)

> All questions are drawn from: GATE Electronics (2000–2024), TI Campus Recruitment, Intel VLSI interviews, Qualcomm analog interviews, ISRO Electronics, Karnataka VLSI (K-VLSI), and IIT entrance examinations. Solve before checking answers.

---

### Section 1 Problems — Electrical to Electronics / Vacuum Tubes

**P1.1 [TI Interview Classic]**
An ideal triode has its grid at 0V. The plate current is 10mA. Now the grid voltage is changed to −4V. Describe qualitatively what happens to the plate current and why.

**P1.2 [Conceptual]**
A mechanical relay switches in 5ms. A transistor switch can switch in 5ns. By what factor is the transistor faster? Express as a power of 10.

**P1.3 [GATE-style Conceptual]**
Why is the base of a BJT made very thin and lightly doped? What would happen to transistor action if the base were very thick?

**P1.4 [Interview Trap]**
The vacuum tube triode and the MOSFET both act as voltage-controlled switches. What is the fundamental physical mechanism in each? What eliminates the need for a heater in the MOSFET?

**P1.5 [Conceptual]**
In the analogy: BJT is to current control as MOSFET is to __________ control. Fill in and explain the physical reason.

**P1.6 [Interview]**
A relay coil has resistance 100Ω and requires 50mA to actuate. A transistor (β = 100) drives the relay. What minimum base current is needed? What minimum V_BE must be present?

**P1.7 [GATE 2019-style]**
Name two disadvantages of using a vacuum tube triode as an amplifier compared to a transistor.

**P1.8 [Trap]**
A triode-based circuit claims to amplify a signal with "zero power consumption in the grid circuit." Is this possible? Why? Relate this to a modern equivalent.

**P1.9 [Conceptual]**
Why does increasing the negative voltage on the triode's grid decrease the plate current? Use the electric field argument.

**P1.10 [Interview]**
The first electronic computer (ENIAC) used 18,000 vacuum tubes. A modern processor has 50 billion transistors in an area smaller than a postage stamp. What physical property of transistors enables this density that vacuum tubes fundamentally cannot achieve?

---

### Section 2 Problems — Semiconductor Physics

**P2.1 [GATE 2015]**
The intrinsic carrier concentration of silicon at 300K is 1.5 × 10¹⁰/cm³. If silicon is doped with donor atoms at a concentration of 10¹⁵/cm³, find the hole concentration at thermal equilibrium.

**P2.2 [GATE 2018 — Trap]**
An N-type semiconductor has more electrons than a P-type semiconductor. Therefore, an N-type semiconductor has a net negative charge. True or False? Justify your answer.

**P2.3 [Interview Classic]**
The resistance of a semiconductor decreases as temperature increases. The resistance of a metal increases as temperature increases. Explain both behaviors from band theory.

**P2.4 [GATE 2012]**
Silicon is doped with both donor (N_D = 10¹⁶/cm³) and acceptor (N_A = 10¹⁵/cm³) atoms simultaneously. What type of semiconductor results, and what is the approximate net majority carrier concentration?

**P2.5 [Trap — TI Interview]**
A P-type silicon sample is illuminated with light of sufficient energy to break covalent bonds. What happens to the majority carrier and minority carrier concentrations? Does the sample remain P-type?

**P2.6 [GATE 2020]**
The energy gap of Germanium is 0.7 eV and of Silicon is 1.1 eV. At 300K, which has higher intrinsic carrier concentration? Which would you prefer for a high-temperature application, and why?

**P2.7 [Interview]**
A semiconductor has a resistivity of 0.5 Ω·cm. Is it intrinsic silicon, doped silicon, or copper? (Pure Si resistivity ≈ 2300 Ω·cm; copper ≈ 1.7 × 10⁻⁶ Ω·cm)

**P2.8 [Trap]**
"Doping silicon with boron creates holes, so the semiconductor now has a positive charge." Identify the error in this statement.

**P2.9 [GATE — Diffusion]**
In a semiconductor, the diffusion current flows from a region of __________ carrier concentration to a region of __________ carrier concentration, while drift current flows in the direction of the __________ field (for electrons).

**P2.10 [Interview — Temperature]**
The reverse saturation current (I_S) of a silicon diode doubles for every 10°C rise. If I_S = 1 nA at 25°C, what is I_S at 65°C? What is the practical implication for circuits operating in a hot environment?

---

### Section 3 Problems — P-N Junction & Diode

**P3.1 [TI Interview Classic — The Trap You Already Know]**
Three ideal diodes have anodes connected to 3V, 6V, and 9V. All cathodes are tied together to a single output node. What is the output voltage? Explain which diodes conduct and which are reverse biased.

**P3.2 [GATE 2017]**
A silicon diode has I_S = 10 nA at 300K. Calculate the diode current when V_D = 0.6V. Use V_T = 26mV and η = 1. (e^23.08 ≈ 10^10)

**P3.3 [Interview Trap — Barrier Potential]**
If you connect a voltmeter directly across a P-N junction (no external bias), what reading do you expect? Explain why you cannot use the built-in potential as a free voltage source.

**P3.4 [GATE 2014]**
For a silicon P-N junction at 300K with I_S = 1 µA, if the reverse bias is increased from 5V to 50V, by how much does the reverse current increase?

**P3.5 [Interview — Temperature Trap]**
A diode circuit is designed to give V_F = 0.7V at 25°C. At 75°C, what is the approximate forward voltage drop? (V_F decreases by approximately 2mV/°C for silicon.)

**P3.6 [GATE 2016 — Dynamic Resistance]**
A silicon diode operates with a DC forward current of 5mA. Calculate its dynamic (AC) resistance using r_d = V_T/I_D where V_T = 26mV.

**P3.7 [Interview Classic]**
Two diodes D1 (Si, V_F = 0.7V) and D2 (Ge, V_F = 0.3V) are connected in series, forward biased by a 5V supply through a 1kΩ resistor. Find the current in the circuit and the voltage across each diode.

**P3.8 [GATE Trap — Reverse Breakdown]**
A 1N4148 switching diode (PIV = 100V) is connected in reverse bias with a 150V supply. What happens? Now a Zener diode (V_Z = 5.1V, I_Z(max) = 50mA) is connected in reverse with a 12V supply through a 1kΩ resistor. What is the voltage across the Zener?

**P3.9 [Interview — Anti-parallel Diodes]**
Two ideal silicon diodes are connected in anti-parallel (anode of D1 to cathode of D2, and cathode of D1 to anode of D2). A 10V AC source is connected across this combination. What waveform appears across the combination?

**P3.10 [GATE 2022-style]**
A diode with I_S = 10 pA is forward biased such that the voltage across it is exactly V_T × ln(1000). What is the current through the diode? (Hint: use the diode equation, consider whether the −1 term matters.)

---

### Section 4 Problems — Rectifiers, Clippers & Clampers

**P4.1 [GATE 2013]**
A half-wave rectifier uses a silicon diode with a sinusoidal input of peak voltage 20V at 50Hz. Calculate: (a) peak output voltage, (b) average output voltage, (c) frequency of output ripple.

**P4.2 [Interview Classic — PIV Trap]**
A full-wave centre-tap rectifier uses a transformer with total secondary voltage 300V (150V each half). Calculate the PIV requirement for each diode. Why do students often get this wrong?

**P4.3 [GATE 2015]**
A bridge rectifier has an input of 230V RMS. Assuming ideal diodes, calculate: (a) peak output voltage, (b) average DC output voltage, (c) PIV of each diode.

**P4.4 [Interview Trap — Practical Bridge]**
Repeat P4.3 for a practical bridge rectifier with silicon diodes (V_F = 0.7V each). How does the output change compared to ideal diodes? Why is this difference important in low-voltage power supplies?

**P4.5 [GATE 2019]**
A full-wave rectifier has an output capacitor filter of 1000µF and a load of 100Ω. The input is 50Hz. Estimate the peak-to-peak ripple voltage. (V_m = 20V)

**P4.6 [Interview — Clipper Analysis]**
A clipper circuit: 5V peak sine wave → 10kΩ → output node → ideal diode (anode at output node, cathode to +2V reference) → reference. Sketch the output waveform. State the clipping level.

**P4.7 [GATE Trap — Clamper DC Shift]**
A negative clamper with a 10V peak sine wave input produces an output with its positive peak at 0V. What is: (a) the peak negative voltage of the output, (b) the average (DC) value of the output, (c) the peak-to-peak amplitude of the output?

**P4.8 [Interview — Double Clamper Trap]**
A student designs a clamper and observes that the output peak-to-peak voltage is larger than the input peak-to-peak. They conclude the clamper is amplifying. Are they correct? Explain.

**P4.9 [GATE 2018]**
In a positive clamper, the capacitor is replaced with a short circuit (wire). What does the circuit become? What is the output waveform?

**P4.10 [Interview Classic]**
A Zener diode (V_Z = 5.1V) is used as a voltage regulator. Input voltage varies from 9V to 15V. Series resistor R = 470Ω. Load R_L = 1kΩ. (a) Find the output voltage. (b) Find the Zener current at V_in = 15V. (c) Find the Zener current at V_in = 9V. (d) Verify the Zener stays in regulation at both extremes.

---

### Section 5 Problems — BJT

**P5.1 [GATE 2016]**
A BJT has β = 100. Base current I_B = 50µA. Find: (a) collector current I_C, (b) emitter current I_E, (c) α.

**P5.2 [Interview Trap — Saturation]**
A BJT (β = 200) in a common-emitter circuit has R_C = 1kΩ, V_CC = 10V, I_B = 100µA. Is the transistor in active mode or saturation? Calculate V_CE (or state why you can't directly).

**P5.3 [GATE 2014 — α and β]**
A transistor has α = 0.98. Calculate β. If the emitter current is 5mA, find I_C and I_B.

**P5.4 [Interview Classic — CE Phase Shift]**
A common-emitter amplifier has a sinusoidal input of +5mV peak at the base. The voltage gain is −50 (minus sign). What is the output signal? What is the magnitude of the output? What does the negative sign mean physically?

**P5.5 [GATE 2019 Trap]**
For a BJT to work as an amplifier, which region must it operate in? For it to work as a digital switch (ON state), which region? What is the key difference in junction bias states?

**P5.6 [Interview — Thermal Runaway]**
In a BJT circuit without thermal stabilization, as temperature increases, I_C increases. Increased I_C generates more heat, further increasing I_C. This is called thermal runaway. Why does this happen more easily in BJTs than MOSFETs? (Hint: think about how I_C varies with temperature for each device.)

**P5.7 [GATE 2021 — Small Signal]**
A BJT is biased at I_C = 1mA. Calculate: (a) transconductance g_m, (b) small-signal emitter resistance r_e. Use V_T = 26mV.

**P5.8 [Interview Classic — Transistor as Switch]**
A BJT switch (NPN, β = 100, V_CE(sat) = 0.2V) drives a 12V relay coil with resistance 120Ω. What minimum base current is needed to ensure the transistor is in saturation? What minimum V_BE must be present?

**P5.9 [GATE Trap — CB Configuration]**
In a common-base configuration, the input is at the emitter and output at the collector. The current gain is α ≈ 0.99. Does this mean the circuit is useless? What is its advantage? Why is α < 1?

**P5.10 [Interview — PNP Trap]**
A PNP transistor is connected with emitter to +9V, base through 100kΩ to +9V as well (same node). Collector through 1kΩ to GND. Is the transistor ON or OFF? What is I_C?

---

### Section 6 Problems — FET & MOSFET

**P6.1 [TI Interview Classic — The V_GS Trap]**
An NMOS transistor has V_th = 1V. Gate is connected to 5V, Source is connected to 0V. Is it ON or OFF? Now, Source is raised to 5V (Gate remains at 5V). Is it ON or OFF? Now Source is at 6V, Gate at 5V. Is it ON or OFF?

**P6.2 [GATE 2018]**
An NMOS transistor has V_th = 2V, k = 1mA/V². If V_GS = 4V and V_DS = 1V, in which region is the MOSFET operating? Calculate I_D.

**P6.3 [Interview Trap — Saturation in MOSFET]**
A student says: "My BJT is in saturation — it's fully ON. My MOSFET is also in saturation — it's also fully ON." Is the student correct? Explain the difference between BJT saturation and MOSFET saturation.

**P6.4 [GATE 2015 — CMOS Inverter]**
In a CMOS inverter, when V_in = V_DD (logic HIGH): (a) Which transistor is ON? (b) Which transistor is OFF? (c) What is V_out? When V_in = 0V (logic LOW): (d) Which transistor is ON? (e) What is V_out?

**P6.5 [Interview — PMOS Trap]**
A PMOS transistor has V_th = −2V (threshold is negative for PMOS). V_DD = 5V. Gate is connected to 0V, Source to 5V. Calculate V_GS. Is the PMOS ON or OFF?

**P6.6 [GATE 2020 — Dynamic Power]**
A CMOS circuit switches at 500MHz with V_DD = 1.8V and C_load = 50fF. Assume activity factor α = 0.3. Calculate the dynamic power consumption.

**P6.7 [Interview — Body Effect]**
In an NMOS transistor used as a source follower, the source voltage rises as the gate is driven. Why does the threshold voltage V_th appear to increase (making the transistor harder to turn on)? What is this effect called?

**P6.8 [GATE 2022 Trap — W/L Ratio]**
MOSFET A has W/L = 10/1 and MOSFET B has W/L = 1/1 (same process, V_th, V_GS, V_DS). Which carries more current? By what factor? What is the practical implication?

**P6.9 [Interview Classic — Pull-up PMOS]**
In a CMOS logic gate, the PMOS transistors are called the "pull-up network" and NMOS transistors are called the "pull-down network." Why can't you use two NMOS transistors for both networks and skip PMOS entirely? (Hint: think about what happens when NMOS passes a HIGH voltage close to V_DD.)

**P6.10 [GATE/Interview — Subthreshold & Leakage]**
A MOSFET is said to be in cutoff when V_GS < V_th. Does I_D = 0 exactly in this region? What is the subthreshold leakage current, and why does it matter for modern VLSI (28nm, 7nm nodes)?

---

## 8. Answer Key

---

### Section 1 Answers

**P1.1:** Grid at 0V = maximum plate current (10mA). As grid goes to −4V, it creates an electric field opposing electron flow from cathode to anode. Fewer electrons have enough energy to overcome this repelling field → plate current decreases. At sufficiently negative grid voltage (cutoff), no electrons reach the anode and current = 0. This is the triode acting as a voltage-controlled valve.

**P1.2:** 5ms / 5ns = 5×10⁻³ / 5×10⁻⁹ = **10⁶ times faster (one million times)**. This speed difference is why mechanical computers could never match electronic ones.

**P1.3:** Thin base: injected electrons from emitter diffuse across the base before recombining with holes. If base were thick → more recombinations → fewer electrons reach the collector → β decreases dramatically → no amplification. Light doping: fewer holes in base = less recombination = more electrons make it to collector = high β. **Thin + lightly doped base is essential for transistor gain.**

**P1.4:** Triode: electric field from grid controls thermionic emission current (electrons boiled off a hot cathode). MOSFET: gate voltage creates/destroys an inversion channel through field effect — no hot cathode needed because silicon at room temperature has thermally available electrons. The semiconductor's own free electrons serve as carriers — no heating required.

**P1.5:** **Voltage** control. Physical reason: the MOSFET gate is separated from the channel by an insulating oxide (SiO₂). No DC current can flow into the gate. The control signal is purely a voltage — the electric field through the oxide controls the channel charge density.

**P1.6:** Relay needs 50mA = I_C. I_B = I_C/β = 50mA/100 = **0.5mA minimum**. V_BE must be ≥ **0.7V** (silicon transistor threshold to reach active/saturation region). In practice, design with margin: I_B = 1–2× minimum to ensure saturation.

**P1.7:** Any two valid answers: (1) Requires filament heating power — constant energy waste even with no signal. (2) Large physical size — cannot be miniaturized. (3) Fragile glass envelope. (4) High operating voltages (100–300V plate supply). (5) Limited lifespan — filament burns out like a light bulb.

**P1.8:** Yes, the triode grid draws essentially zero current (electrons are repelled, not attracted, by the negative grid). Zero current × finite resistance = zero power in grid circuit. Modern equivalent: **MOSFET gate** — insulated oxide means gate current ≈ 0 (femtoampere leakage), so gate circuit power ≈ 0 in DC steady state. (Dynamic power during switching is non-zero due to charging the gate capacitance.)

**P1.9:** Negative voltage on grid creates an electric field pointing from anode toward cathode (same direction as the field resisting electron flow). This opposes the thermal emission of electrons traveling from cathode to anode. Electrons with insufficient kinetic energy are turned back. Higher negative voltage → stronger opposing field → fewer electrons get through → lower plate current.

**P1.10:** **Scalability and solid-state nature.** A vacuum tube requires a heated filament, glass enclosure, and vacuum — these cannot be miniaturized below a certain physical limit. A MOSFET is a solid-state device whose gate length can be scaled to atomic dimensions (modern nodes: 3–7nm). The manufacturing process (photolithography) can pattern billions of transistors simultaneously on a single silicon wafer. A triode is hand-assembled; MOSFETs are batch-fabricated.

---

### Section 2 Answers

**P2.1 [GATE 2015]:** Using mass action law: n × p = nᵢ²
n ≈ N_D = 10¹⁵/cm³ (donors >> intrinsic)
p = nᵢ²/n = (1.5×10¹⁰)²/10¹⁵ = 2.25×10²⁰/10¹⁵ = **2.25 × 10⁵ holes/cm³**
Compare: intrinsic holes = 1.5×10¹⁰. Doping suppressed hole concentration by 5 orders of magnitude.

**P2.2 [Trap]:** **FALSE.** An N-type semiconductor has more free electrons than a P-type. However, for every donor atom that donated an electron, a positively charged immobile donor ion remains in the lattice. The total charge: (free electrons + acceptor ions) = (holes + donor ions). The material is overall electrically **neutral**. More electrons does NOT mean negatively charged.

**P2.3:** **Semiconductor (NTC):** Valence electrons are covalently bonded. At higher temperature, more thermal energy → more bond breakages → more free carriers → lower resistance. The exponential increase in carrier concentration dominates over the slight decrease in mobility. **Metal (PTC):** Metals already have abundant free electrons (conduction band overlaps valence band). Temperature increase does not add carriers. Instead, atoms vibrate more → more collisions → reduced electron mobility → higher resistance.

**P2.4 [GATE 2012]:** When both N_D and N_A are present, they partially compensate. Net effect: N_D − N_A = 10¹⁶ − 10¹⁵ = **9 × 10¹⁵/cm³ net donor excess**. Result: **N-type semiconductor** with majority carrier concentration ≈ 9 × 10¹⁵ electrons/cm³. The acceptors don't "cancel" — they just reduce the effective donor density.

**P2.5 [Trap]:** Light generates electron-hole pairs (one of each per photon absorbed). Both electrons AND holes increase. **Minority carrier (electrons in P-type) increases dramatically** (from very few to many — a huge percentage increase). **Majority carrier (holes) increases slightly** (small addition to a large number). The sample **remains P-type** as long as the photogenerated pairs don't exceed the doping level — but minority carrier behavior changes significantly. This is the basis of photodetectors and solar cells.

**P2.6 [GATE 2016]:** Ge has Eg = 0.7eV (smaller gap) vs Si Eg = 1.1eV. Smaller gap → easier for electrons to cross → **Germanium has higher intrinsic carrier concentration** at any given temperature. For high-temperature applications: **Silicon is preferred**. Higher Eg → fewer thermal carriers → device remains properly doped (not overwhelmed by intrinsic carriers) at higher temperatures. Ge becomes intrinsic (and loses its N or P character) at much lower temperatures than Si.

**P2.7:** Resistivity 0.5 Ω·cm is between copper (1.7×10⁻⁶ Ω·cm) and intrinsic Si (2300 Ω·cm). It is **doped silicon** — moderately doped. Pure Si = too high resistivity. Copper = too low. This is in the range of doped semiconductor with N_D or N_A around 10¹³–10¹⁵/cm³.

**P2.8:** The error: "Boron creates holes, so the semiconductor has positive charge." **Wrong.** For every hole created, boron becomes a negatively charged acceptor ion (it accepted one electron from silicon). Hole (+) is mobile; boron ion (−) is fixed. They exactly cancel. The material is neutral. Holes are carriers of positive charge but the material is not positively charged overall.

**P2.9:** Diffusion current flows from **high** concentration to **low** concentration. Drift current (for electrons) flows **opposite** to the electric field direction. (Conventional current drift flows in field direction; electron drift current flows against field direction — electrons flow toward the positive terminal.)

**P2.10:** Starting at 25°C, I_S = 1 nA. Temperature rise = 65 − 25 = 40°C. Number of doublings = 40/10 = 4. I_S at 65°C = 1 nA × 2⁴ = 1 × 16 = **16 nA**. Practical implication: In a circuit biased for specific V_F at 25°C, at 65°C the leakage is 16× larger. In automotive or industrial electronics (operating at 85°C or 125°C), I_S can be hundreds of nA — this affects bias circuits and can cause latchup in CMOS. Always design for worst-case temperature.

---

### Section 3 Answers

**P3.1 [The Classic Trap]:** Output = **9V**.
- D3 (9V anode) forward biases first — its anode is highest. Output node is pulled to 9V.
- D2: Anode = 6V, Cathode = 9V → V_AK = −3V → **Reverse biased** (OFF)
- D1: Anode = 3V, Cathode = 9V → V_AK = −6V → **Reverse biased** (OFF)
Only D3 conducts. Rule: In parallel diodes pointing toward a common output, the **highest anode voltage wins**. Never add the voltages.

**P3.2 [GATE 2017]:** I_D = I_S × e^(V_D/V_T) = 10nA × e^(0.6/0.026) = 10×10⁻⁹ × e^23.08
e^23.08 ≈ 10^10 → I_D = 10×10⁻⁹ × 10^10 = **100 mA**. Note how exponential: a mere 0.6V drives 100mA through a device with only 10nA saturation current.

**P3.3 [Trap]:** Reading = **0 volts**. When you connect a voltmeter (metal probes to semiconductor), you create two new metal-semiconductor contact potentials at each probe. These contact potentials exactly equal and oppose the barrier potential — it is a thermodynamic requirement at equilibrium. You cannot extract work from a junction in thermal equilibrium — this would violate the second law. The barrier potential is real but not externally measurable. It is not a free energy source.

**P3.4 [GATE 2014]:** The reverse saturation current I_S is independent of the reverse bias voltage (it is "saturated" — all available minority carriers are already being swept across). Increasing reverse voltage from 5V to 50V changes the current by approximately **zero** (only the tiny leakage current flows, and it doesn't depend on voltage magnitude once well into reverse bias). Answer: No significant increase. This is the "saturation" in reverse saturation current.

**P3.5:** V_F changes by −2mV/°C. Temperature change = 75 − 25 = 50°C. ΔV_F = −2mV × 50 = −100mV = −0.1V. V_F at 75°C ≈ 0.7 − 0.1 = **0.6V**. Implication: Circuits designed with V_F = 0.7V at 25°C will see different bias points at operating temperature. Temperature compensation is needed in precision analog circuits.

**P3.6 [GATE 2016]:** r_d = V_T/I_D = 26mV/5mA = 26×10⁻³/5×10⁻³ = **5.2 Ω**. This small-signal dynamic resistance is used in AC analysis. The diode looks like a 5.2Ω resistor to small AC signals superimposed on the 5mA DC bias.

**P3.7:** Two diodes in series: V_D1 (Si) = 0.7V, V_D2 (Ge) = 0.3V. Total diode drop = 0.7 + 0.3 = 1.0V. Voltage across resistor = 5 − 1.0 = 4V. Current = 4/1000 = **4mA**. V_D1 = 0.7V, V_D2 = 0.3V. Check: 0.7 + 0.3 + 4 = 5V ✓.

**P3.8:** 1N4148 with 150V: PIV = 100V, applied = 150V > PIV → **diode undergoes breakdown and likely fails permanently** (not designed for controlled breakdown). Zener circuit: V_Z = 5.1V. With 12V supply and 1kΩ series resistor: Current = (12 − 5.1)/1000 = 6.9/1000 = 6.9mA. This is within the 50mA maximum. Voltage across Zener = **5.1V** (regulated). The Zener maintains 5.1V as long as it has enough current (usually >1mA minimum) and doesn't exceed maximum current.

**P3.9:** Anti-parallel diodes: D1 anode to D2 cathode, D1 cathode to D2 anode. During positive half of AC: D1 forward biased (0.7V drop), D2 reverse biased → current flows through D1 → output = +0.7V. During negative half: D2 forward biased → output = −0.7V. **Output waveform: square-ish wave clamped at +0.7V and −0.7V** (actually follows the input shape but clamped at ±0.7V). This is a precision clipper — used in overload protection for sensitive amplifiers.

**P3.10 [GATE-style]:** V_D = V_T × ln(1000). From diode equation: I_D = I_S × (e^(V_D/V_T) − 1) = 10pA × (e^(ln1000) − 1) = 10pA × (1000 − 1) = 10pA × 999 ≈ 10pA × 1000 = **10 nA**. The "−1" term matters here because e^(ln1000) = 1000, so 1000−1 = 999 ≈ 1000. At higher forward bias, the −1 is negligible. At V_D close to 0, the −1 term is important.

---

### Section 4 Answers

**P4.1 [GATE 2013]:**
(a) V_peak(out) = V_m − 0.7 = 20 − 0.7 = **19.3V**
(b) V_dc = V_peak / π = 19.3 / 3.14 = **6.14V**
(c) Output ripple frequency for half-wave = **same as input = 50Hz** (only one pulse per input cycle)

**P4.2 [PIV Trap]:** Secondary is 300V total (150V each half). V_m = 150 × √2 = 212V peak per half. When D1 is conducting: cathode of D2 is at 0V (GND through D1), anode of D2 is at −212V (the other half of secondary) → D2 sees 0 − (−212) = 212V. But D2's cathode is also connected through D1 to the positive rail. Maximum reverse voltage on D2 = V_m + V_m = **2 × 212 = 424V**. Students forget: the full secondary voltage (both halves) appears across the non-conducting diode. PIV = **2V_m**.

**P4.3 [GATE 2015]:**
V_RMS = 230V → V_m = 230 × √2 = **325V**
(a) V_peak(out) = 325V (ideal diodes)
(b) V_dc = 2 × V_m / π = 2 × 325 / 3.14 = **207V**
(c) PIV of each bridge diode = **325V** (V_m only — advantage over centre-tap)

**P4.4 [Practical Bridge]:** Two diodes conduct simultaneously: Total drop = 2 × 0.7 = 1.4V.
(a) V_peak(out) = 325 − 1.4 = **323.6V**
(b) V_dc = 2 × 323.6 / π = **206V**
In a 5V power supply: V_m might be 8V. Two diode drops = 1.4V → output peak = 6.6V. That's a 17.5% reduction — very significant. For low-voltage supplies, use Schottky diodes (V_F ≈ 0.2–0.3V) to reduce this loss.

**P4.5 [GATE 2019]:** Full-wave rectifier, f = 50Hz, C = 1000µF, R_L = 100Ω, V_m = 20V.
V_ripple = V_m / (2fCR_L) = 20 / (2 × 50 × 1000×10⁻⁶ × 100) = 20 / 10 = **2V peak-to-peak**
A 10% ripple on a 20V supply — adequate for most non-precision applications. Larger capacitor would reduce this.

**P4.6 [Clipper Analysis]:** Input: 5V peak sine. Resistor: 10kΩ. Diode anode at output, cathode at +2V. When V_in > 2V: diode forward biases, output is clamped to 2V + 0.7V = 2.7V (diode drop). For ideal diode: output clamped at 2V. When V_in < 2V: diode off, output = V_in (follows input). **Output: Follows input for V < 2V; clamped at 2V for V > 2V.** Positive peaks above 2V are clipped.

**P4.7 [GATE Clamper]:**
(a) Negative peak = **−2V_m = −20V** (capacitor adds V_m in series with input during this half)
(b) DC average = **−V_m = −10V** (the waveform is shifted by −V_m)
(c) Peak-to-peak amplitude = **2V_m = 20V** — unchanged. Clamping only shifts the waveform; it does not change the peak-to-peak value. This is the key point.

**P4.8 [Trap]:** The student is **wrong**. The clamper does not amplify. The peak-to-peak amplitude of the output is **identical** to the input. What appears larger is the peak-positive or peak-negative voltage relative to 0V — but this is just a DC shift. If input was 20V_pp and output appears to go from 0 to −20V (negative clamper), the peak-to-peak is still 20V. There is no energy amplification.

**P4.9 [GATE 2018]:** If the capacitor is replaced with a wire (short circuit), there is no charge storage element. The diode conducts during negative half-cycles (if negative clamper configuration) but there is no memory of the previous cycle. The circuit becomes a **half-wave rectifier** (positive clipper/rectifier). Output = positive half of input passes; negative half is blocked by diode (or vice versa, depending on orientation). The waveform is not shifted — it is just rectified.

**P4.10 [Zener Regulator]:**
V_out = V_Z = **5.1V** (as long as Zener is in regulation)
At V_in = 15V: I_series = (15 − 5.1)/470 = 9.9/470 = **21.1mA**
I_load = 5.1/1000 = 5.1mA
I_Z = 21.1 − 5.1 = **16mA** ✓ (< 50mA max → safe)
At V_in = 9V: I_series = (9 − 5.1)/470 = 3.9/470 = **8.3mA**
I_load = 5.1mA
I_Z = 8.3 − 5.1 = **3.2mA** ✓ (positive → still in regulation)
Both extremes: Zener stays in regulation. Design is valid. If I_Z had gone negative, the Zener would drop out of regulation and output would collapse.

---

### Section 5 Answers

**P5.1 [GATE 2016]:**
(a) I_C = β × I_B = 100 × 50µA = **5mA**
(b) I_E = I_C + I_B = 5mA + 50µA = **5.05mA**
(c) α = I_C/I_E = 5/5.05 = **0.99**. Confirm: α = β/(β+1) = 100/101 = 0.99 ✓

**P5.2 [Trap — Saturation Check]:**
If in active mode: I_C = β × I_B = 200 × 100µA = 20mA.
V_CE(active) = V_CC − I_C × R_C = 10 − 20mA × 1kΩ = 10 − 20 = −10V.
V_CE cannot be negative in an NPN circuit — this is impossible. The transistor is **in saturation**. Maximum I_C = (V_CC − V_CE(sat))/R_C = (10 − 0.2)/1000 ≈ 9.8mA. V_CE(sat) ≈ **0.2V**. The β formula does not apply in saturation. Forced β = I_C/I_B = 9.8mA/100µA = 98 << 200. In saturation, the actual current gain is less than β.

**P5.3 [GATE 2014]:**
β = α/(1−α) = 0.98/(1−0.98) = 0.98/0.02 = **49**
I_E = 5mA
I_C = α × I_E = 0.98 × 5 = **4.9mA**
I_B = I_E − I_C = 5 − 4.9 = **0.1mA = 100µA**
Verify: β = I_C/I_B = 4.9mA/100µA = 49 ✓

**P5.4 [Interview — Phase Shift]:**
Output = A_v × V_in = −50 × (+5mV peak) = **−250mV peak**. The negative sign means the output is **180° phase shifted (inverted)**. A positive-going input (+5mV) produces a negative-going output (−250mV). Magnitude of output = **250mV peak**. Physically: When V_BE increases (+5mV), I_C increases → more voltage drops across R_C → V_CE = V_CC − I_C×R_C **decreases** → output goes DOWN when input goes UP = inversion.

**P5.5 [GATE 2019]:**
Amplifier: **Active region** (EB: forward biased, CB: reverse biased). I_C = β × I_B — linear relationship.
Digital switch ON: **Saturation** (both junctions forward biased). V_CE ≈ 0.2V. Maximum current limited by external circuit.
Key difference: In active region, CB is reverse biased and transistor controls current precisely. In saturation, both junctions forward biased, transistor loses current control — current is set by external resistor and supply.

**P5.6 [Thermal Runaway]:**
BJT: I_C ≈ β × I_B, but also includes temperature-dependent I_CBO (leakage). As T increases → I_CBO increases → I_C increases → more power P = V_CE × I_C → more heat → higher T → cycle repeats. Without feedback stabilization (emitter resistor R_E), this is a runaway condition.
MOSFET: As temperature increases, carrier mobility **decreases** (µ ∝ T^−1.5). Lower mobility → lower I_D for the same V_GS. This is **self-stabilizing** — the MOSFET has a negative temperature coefficient in the active region, which prevents thermal runaway. This is why power MOSFETs are preferred in high-current switching applications.

**P5.7 [GATE 2021]:**
(a) g_m = I_C/V_T = 1mA/26mV = 1×10⁻³/26×10⁻³ = **38.5 mA/V (millisiemens)**
(b) r_e = 1/g_m = V_T/I_C = 26mV/1mA = **26 Ω**
These values appear in small-signal BJT models. Higher I_C → higher g_m → better transconductance → more voltage gain.

**P5.8 [Classic Switch]:**
Relay coil: 12V, 120Ω. I_C(sat) = (V_CC − V_CE(sat))/R_coil = (12 − 0.2)/120 = 11.8/120 ≈ **98mA**.
To ensure saturation: apply overdrive factor of at least 2 (safety margin): I_B(min) = I_C(sat)/β × 2 = 98mA/100 × 2 = **≈ 2mA** base current needed.
V_BE must be **≥ 0.7V** (Si BJT threshold). In practice, drive base with V_B = 5V through appropriate base resistor: R_B = (5 − 0.7)/2mA = 4.3/0.002 = **2.15kΩ** → use 2.2kΩ standard value.

**P5.9 [GATE — CB]:**
α < 1 (about 0.99) means current gain is less than 1 — input current (emitter) is always slightly more than output current (collector). So CB does NOT amplify current. But its advantage: **very high voltage gain** (high output impedance at collector, low input impedance at emitter) and **extremely wide bandwidth** (no Miller effect). The CB configuration is used in RF amplifiers and cascode stages specifically because it avoids the parasitic capacitance multiplication (Miller effect) that limits CE bandwidth. α < 1 because some injected carriers recombine in the base.

**P5.10 [PNP Trap]:**
PNP: Emitter (+9V), Base connected to +9V (same voltage). V_EB = V_E − V_B = 9 − 9 = **0V**. For a PNP transistor to conduct, V_EB must be ≥ 0.7V (emitter must be at least 0.7V positive relative to base for PNP). V_EB = 0V → transistor is **OFF**. I_C = 0. The output (collector) = 0V (no current through 1kΩ, so no voltage drop). Note: if base were connected to +8.3V instead of +9V: V_EB = 9−8.3 = 0.7V → transistor ON.

---

### Section 6 Answers

**P6.1 [The TI V_GS Trap]:**
Case 1: V_G = 5V, V_S = 0V → V_GS = 5−0 = 5V > V_th(1V) → **ON** ✓
Case 2: V_G = 5V, V_S = 5V → V_GS = 5−5 = 0V < V_th(1V) → **OFF** ✓
Case 3: V_G = 5V, V_S = 6V → V_GS = 5−6 = −1V < V_th(1V) → **OFF** ✓
This is the most common VLSI interview trap. MOSFET does not care about absolute gate voltage — only about V_GS relative to its own source.

**P6.2 [GATE 2018]:**
Check region: V_DS = 1V, V_GS − V_th = 4 − 2 = 2V. Since V_DS (1V) < V_GS − V_th (2V) → **Linear (Triode) region**.
I_D = k × [(V_GS−V_th)×V_DS − V_DS²/2] = 1mA/V² × [(4−2)×1 − 1²/2] = 1 × [2 − 0.5] = **1.5mA**

**P6.3 [Saturation Trap]:**
The student is **incorrect**. BJT saturation ≠ MOSFET saturation.
- **BJT saturation:** Both EB and CB junctions forward biased. V_CE ≈ 0.2V. Transistor is fully ON as a switch. Current is limited by external circuit, not by transistor.
- **MOSFET saturation:** Channel is "pinched off" at the drain end (V_DS ≥ V_GS − V_th). MOSFET acts as a **constant current source** controlled by V_GS. This is the **amplifier operating region** — NOT fully ON.
To have a MOSFET "fully ON" as a switch, it should be in the **linear/triode** region (V_DS << V_GS − V_th) where it acts as a low-resistance switch (R_DS(on) very small).

**P6.4 [GATE 2015 — CMOS Inverter]:**
V_in = V_DD (HIGH):
(a) NMOS ON (V_GS = V_DD > V_th)
(b) PMOS OFF (V_GS = V_DD − V_DD = 0V > V_th(PMOS) which is negative, so |V_GS| = 0 < |V_th| → OFF)
(c) V_out = **0V (GND)** — NMOS pulls output to ground
V_in = 0V (LOW):
(d) PMOS ON (V_GS = 0 − V_DD = −V_DD, |V_GS| > |V_th(PMOS)| → ON)
(e) V_out = **V_DD** — PMOS pulls output to supply
CMOS inverter: output is always complement of input. No DC path from V_DD to GND in steady state → zero static power (only dynamic switching power).

**P6.5 [PMOS Trap]:**
Source = 5V (V_DD), Gate = 0V. V_GS = V_G − V_S = 0 − 5 = **−5V**.
V_th for PMOS = −2V (threshold is negative for PMOS — it turns on when V_GS < V_th).
V_GS (−5V) < V_th (−2V) → **PMOS is ON**. Current flows from Source (5V) through channel to Drain. ✓
This is the standard PMOS pull-up: gate at LOW (0V), PMOS turns ON, pulling output toward V_DD.

**P6.6 [GATE 2020 — Dynamic Power]:**
P = α × C × V_DD² × f = 0.3 × 50×10⁻¹⁵ × (1.8)² × 500×10⁶
= 0.3 × 50×10⁻¹⁵ × 3.24 × 500×10⁶
= 0.3 × 50 × 3.24 × 500 × 10⁻¹⁵⁺⁶
= 0.3 × 81,000 × 10⁻⁹
= 24,300 × 10⁻⁹ W
= **24.3 µW per gate**
At 1 billion gates: 24.3W — this is why power is a first-class design constraint in modern processors.

**P6.7 [Body Effect]:**
As V_S (source voltage) increases while V_B (body/substrate) stays at GND: V_SB (source-body voltage) increases. This reverse-biases the source-body junction more strongly, widening the depletion region under the channel, which requires a larger V_GS to invert the channel. Effectively, V_th increases with increasing V_SB. This is the **body effect** (also: backgate effect, substrate bias effect). Formula: V_th = V_th0 + γ(√(2φ_F + V_SB) − √(2φ_F)). In source followers and pass transistors, body effect reduces voltage swing and causes threshold shift.

**P6.8 [GATE — W/L]:**
Drain current in saturation: I_D = (k'/2) × (W/L) × (V_GS − V_th)². MOSFET A (W/L=10) carries **10× more current** than MOSFET B (W/L=1) at the same V_GS. Practical implication: Wider transistors (higher W/L) have lower on-resistance (R_DS(on)) and can drive larger currents — used in power circuits, output drivers, and high-fanout buffers. But they also have **larger gate capacitance** (C ∝ W×L) → slower switching and more dynamic power. W/L ratio is the key design handle in analog and digital circuit sizing.

**P6.9 [NMOS Pass Transistor — Threshold Drop Trap]:**
An NMOS transistor cannot pass a strong logic '1' (V_DD) from drain to source. When V_out (source) approaches V_DD − V_th, V_GS = V_DD − V_out = V_DD − (V_DD − V_th) = V_th. The transistor is right at the edge of cutoff — it stops conducting before V_out reaches V_DD. The output is degraded to V_DD − V_th, not V_DD. PMOS does not have this problem passing HIGH (it passes V_DD fully through its p-channel). **CMOS uses PMOS for pull-up (passing HIGH)** and NMOS for pull-down (passing LOW) — each passes its strong level perfectly while the other handles the opposite. This is the fundamental reason both are needed.

**P6.10 [Subthreshold Leakage]:**
I_D is not exactly 0 below V_th. In the subthreshold region, current follows: I_D ∝ e^(V_GS/nV_T) — an exponential that decreases but never reaches zero. At V_GS = 0, there is still a small **subthreshold leakage current**. In modern VLSI (28nm, 7nm): V_th is intentionally lowered (to ~0.3–0.5V) to enable fast switching at low supply voltages. This low V_th means the subthreshold current at V_GS = 0 is significant (nA to µA per transistor). With 50 billion transistors on a chip, static leakage power = 50×10⁹ × ~nA × V_DD = several watts. **Subthreshold leakage is the dominant power component** in modern idle chips — more than dynamic switching power. This drives research into high-k dielectrics, FinFETs, and GAA (Gate-All-Around) transistors.

---

## Appendix: Master Trap Summary

| Trap | Wrong Answer | Correct Answer |
|------|-------------|----------------|
| Barrier potential measured by voltmeter | Shows V_B (0.7V) | Shows 0V — contact potentials cancel it |
| N-type semiconductor charge | Negatively charged | Electrically neutral |
| Semiconductor resistance vs temperature | Increases (like metal) | Decreases (NTC) — opposite of metal |
| Reverse saturation current vs voltage | Increases with reverse V | Constant (saturated) — independent of voltage |
| PIV of centre-tap rectifier | V_m | **2V_m** |
| Bridge rectifier voltage drop | 0.7V (one diode) | **1.4V (two diodes conduct at once)** |
| Clamper amplifies signal | Yes, output peak is larger | No — only DC level shifts; amplitude unchanged |
| α > 1 possible? | Yes, for high-β transistors | No, never — α = β/(β+1) < 1 always |
| BJT saturation = MOSFET saturation | Same — both fully ON | Opposite: BJT sat = full ON; MOSFET sat = active/amplifier |
| MOSFET: Gate HIGH → always ON | Correct | Only correct if V_GS = V_G − V_S > V_th |
| PMOS: Gate HIGH → ON | Correct | WRONG — PMOS turns OFF when Gate HIGH (V_GS ≈ 0) |
| Diodes in parallel: sum voltages | 3+6+9 = 18V | Highest anode wins = 9V |
| BJT CE amplifier: input up → output up | Yes (both rise) | No — **180° inversion**: input up → output down |
| Full saturation V_CE = 0 | 0V | ≈ 0.2V for Si BJT (V_CE(sat)) |

---

*Part 2 complete. Next: `03-digital-electronics.md` — Number systems, Boolean algebra, Logic gates, Combinational circuits, Sequential circuits (Flip-flops, Counters, Registers), and all their interview traps.*
