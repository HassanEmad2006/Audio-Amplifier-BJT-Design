# 🔊 Audio Amplifier Design and Implementation

<div align="center">

![Course](https://img.shields.io/badge/Course-NANENG%20222-blue?style=flat-square)
![Simulation](https://img.shields.io/badge/Simulation-LTspice-brightgreen?style=flat-square)
![Type](https://img.shields.io/badge/Type-Analog%20Design%20%2B%20Hand%20Analysis-orange?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)

**A two-stage BJT audio amplifier — a variable-gain Common Emitter stage cascaded with an Emitter Follower buffer — designed by hand and validated in SPICE to drive an 8 Ω load without PVT-dependent gain drift.**

</div>

---

## TL;DR

Designed a discrete BJT audio amplifier from a fixed 12 V single supply, targeting a base voltage gain of **A_v = 4** (tunable up to **~10**) while driving a demanding **8 Ω load** from a **32 Ω source**. The core design challenge was that a low-impedance speaker load would normally collapse the gain of a simple amplifier stage through voltage-divider loading — solved here with a dedicated low-output-impedance buffer stage. Gain stability against **Process, Voltage, and Temperature (PVT)** variation was achieved through emitter degeneration, and gain tunability was added without disturbing the DC bias point, using a split-emitter-resistor + bypass-capacitor technique.

---

##  Simulation: Schematic & Output Waveform


Two-stage LTspice schematic (Common Emitter stage Q1 + Emitter Follower buffer Q2 driving an 8 Ω load) alongside the transient simulation output — a clean, undistorted waveform confirming signal integrity is preserved across the load.

---

## Circuit Architecture

| Stage | Role | Key Property |
|---|---|---|
| **Stage 1 — Common Emitter w/ Degeneration** | Voltage gain | Gain set by resistor ratio (R_C/R_E), immune to PVT shifts |
| **Coupling (AC)** | Inter-stage interface | Blocks DC, passes AC — preserves independent bias points |
| **Stage 2 — Emitter Follower (Buffer)** | Current gain / impedance matching | High input impedance, ultra-low output impedance (~42 Ω) |

**Design constraints:**
- Supply: V_CC = 12 V, single-supply operation
- Target gain: A_v = 4 (baseline), tunable to ~10
- Source impedance: R_signal = 32 Ω
- Load impedance: R_load = 8 Ω (typical speaker load)

---

## Key Design Decisions

- **Emitter degeneration** trades raw gain for stability — gain becomes a function of resistor ratios (R_C, R_E) rather than the transistor's intrinsic, temperature-sensitive parameters (β, r_π).
- **Voltage divider biasing** anchors the base voltage independently of β, keeping the DC operating point stable across part-to-part variation.
- **Variable gain without re-biasing:** the emitter resistance is split into R_E1 + R_E2 (kept constant in sum for stable DC bias); a bypass capacitor across one segment makes the AC gain tunable in real time while the DC bias never moves.
- **The loading problem:** connecting a ~4 kΩ first-stage output impedance directly to an 8 Ω load would form a massive voltage divider and destroy the gain. An **Emitter Follower buffer** (R_out ≈ 42 Ω) solves this, preserving voltage gain while supplying the current the load demands.
- **AC coupling capacitors** interface the stages, blocking DC so each stage keeps its own independent, calculated bias point.

---

## Simulation Validation

- Swept 20 Hz → 100 kHz with input amplitudes from 1 mV to 50–100 mV.
- Verified the variable-gain mechanism (via R_E1/R_E2 split) shifts gain smoothly up to A_v ≈ 10 **without disturbing the DC operating point**.
- Full cascaded system (Stage 1 + buffer) simulated driving the real 8 Ω load: output waveform confirms the predicted voltage collapse from loading is fully mitigated by the buffer stage.

---

## Project Lifecycle

1. **Research & Theory** — derivation of PVT-independent gain equations, hand analysis, static component selection.
2. **Simulation Validation** — SPICE transient simulation, mitigation of the loading effect via the buffer stage.
3. **Prototype Deployment** *(future work)* — physical PCB realization and hardware measurement correlation against theoretical predictions.

---

## 📁 Project Structure

```
Audio-Amplifier-Design/
│
├── README.md
├── Audio_Amplifier_Design.md          # Slide-deck style design walkthrough
├── NANENG_222_Final_Project.md         # Full theoretical derivation & report
└── simulation-schematic-and-waveform.png
```

## Skills & Topics

BJT analog design · Common Emitter with degeneration · Emitter Follower buffer stages · biasing (voltage divider) · AC coupling · variable gain design · PVT-robust circuit design · SPICE simulation.

## References

Course materials, NANENG 222 · Standard BJT small-signal analysis (Sedra & Smith conventions)

---

## 👥 Team

Collaborative undergraduate team project — **NANENG 222, Zewail City of Science and Technology**.

- Mohamed Khaled Mohamed (202401477)
- Mohab Mahmoud (202402208)
- Youssef Ahmed (202401212)
- Marwan Darrag (202300661)
- Hassan Emad (202401299)

## 📄 License

No license — educational use only.
