# 8-Bit Left Shift Register

**ED221: Digital IC Design — Tape-in & Tape-out Lab**  
Dhirubhai Ambani University (formerly DA-IICT)

**Authors:** Mansi Mangukiya (202404021) · Rashi Krishnani (202404018) · Yash Judal (202404014)  
**Supervisor:** Biswajit Mishra

---

## Overview

CMOS implementation of an 8-bit logical left shift register, designed and simulated in **Cadence Virtuoso**. The circuit combines PISO (Parallel-In Serial-Out), SIPO (Serial-In Parallel-Out) registers, multiplexers, and logic gates to perform configurable left-shift operations on 8-bit serial data.

- Supply voltage: **1.8 V**
- Clock-driven, synchronous operation
- Supports serial data input, parallel loading, and variable-length left shifts

---

## Pin Configuration

| Pin | Description |
|---|---|
| VDD | Supply voltage (1.8 V) |
| GND | Ground (0 V) |
| CLK | Clock input |
| IN | Serial data input (MSB first) |
| LOADSTORE | Load/shift control — `0` = load, `1` = shift |
| SELECT | MUX shift select — `0` = insert zeros, `1` = data in |
| EN | Clock enable for PISO/SIPO gating |
| OUT | Serial output (MSB first) |

---

## Architecture

The design is composed of four functional blocks:

**SIPO** — Receives serial input bit-by-bit on each clock edge and presents the full 8-bit word in parallel for the next stage.

**PISO** — Loads the parallel output of the SIPO and shifts it out serially (MSB first). Controlled by the LOADSTORE signal.

**MUX** — Selects the shift operand fed into the SIPO. When `SELECT = 1`, live data is fed in; when `SELECT = 0`, zeros are inserted to implement the left shift.

**AND Gates** — Gate the clock to PISO and SIPO independently using the EN signal:
- `CLK_PISO = CLK · EN`
- `CLK_SIPO = CLK · EN̄`

---

## Operation — Example: 7-bit Left Shift of `11111111`

1. `SELECT = 1`, `LOADSTORE = 1` → Serial data `11111111` is clocked into SIPO over 8 cycles (160 ns).
2. `SELECT = 0` → Seven zeros are shifted in, producing `00000001` in the SIPO (140 ns).
3. `LOADSTORE = 0` for one clock cycle (20 ns) → Shifted data is loaded into PISO.
4. `EN = 1`, `LOADSTORE = 1` → PISO shifts out `00000001` serially over 8 clock cycles (160 ns).

### Signal Timing Summary

| Signal | Phase | Duration |
|---|---|---|
| SELECT | High (data load) | 159 ns |
| SELECT | Low (shift zeros) | 140 ns |
| LOADSTORE | High (no PISO load) | ~320 ns |
| LOADSTORE | Low (PISO load pulse) | 20 ns |
| ENABLE | Low (PISO disabled) | ~300 ns |
| ENABLE | High (PISO output) | 160 ns |
| Total simulation window | — | 500 ns |

Clock: 20 ns period, 50% duty cycle (10 ns ON / 10 ns OFF).

---

## Component Delays (Pre-Layout)

| Component | Propagation Delay |
|---|---|
| AND Gate | 227.7 ps |
| OR Gate | 174.05 ps |
| MUX | 189.72 ps |
| Latch | 428.395 ps |
| D Flip-Flop | 506.35 ps |
| **8-bit Left Shift Register** | **0.74 ns** |

---

## Power Characteristics (Pre-Layout, DATA = `11111111`)

| Parameter | Value |
|---|---|
| Average Current (I_avg) | 64.18 µA |
| Peak Current (I_peak) | 2.92 mA |
| Average Power (P_avg) | 115.524 µW |
| Energy (500 ns sim) | 57.762 µJ |

---

## Layout & Area

| Dimension | Value |
|---|---|
| Height | 98.85 µm |
| Width | 316.06 µm |
| Total Area | 3.124 × 10⁴ µm² |

Layout was completed in Cadence Virtuoso and includes separate PISO, SIPO, and MUX blocks arranged in a row-based floorplan.

---

## Post-Layout vs. Pre-Layout Comparison

| Parameter | Pre-Layout | Post-Layout |
|---|---|---|
| Delay | 0.74 ns | 1.2407 ns |
| Parasitic overhead | — | +0.5003 ns |
| Average Current | 64.18 µA | 103.2 µA |
| Peak Current | 2.92 mA | 3.616 mA |
| Average Power | 115.524 µW | 185.76 µW |
| Energy (500 ns) | 57.762 µJ | 92.88 µJ |

Post-layout parasitics (routing resistance and capacitance) account for a ~68% increase in propagation delay and ~61% increase in average power.

---

## Tools

- **Cadence Virtuoso** — Schematic entry, simulation (ADE Explorer/XL), layout (GXL)
- **Calibre** — Physical verification (DRC/LVS)
- **Process** — SCL (Standard Cell Library), 1.8 V CMOS
