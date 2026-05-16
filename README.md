# CMOS 8:1 Multiplexer & Majority Function Implementation

This repository contains the design and simulation of an **8:1 Multiplexer** built using a hierarchical tree structure of custom-designed **2:1 CMOS Multiplexers**. The final circuit is used to implement a **3-variable Majority Function**.

All schematics and simulations were performed using **LTspice**.

---

# Project Overview

The project is divided into three design levels:

### 1. Transistor Level
A custom **2:1 MUX** designed using static CMOS logic.

### 2. Gate/Block Level
An **8:1 MUX tree architecture** utilizing seven 2:1 MUX blocks.

### 3. Application Level
Implementation of a Boolean function by mapping the MUX data inputs to constant voltage levels (`VDD` or `GND`).

---

# Hardware Design

## 1. The 2:1 Multiplexer (Sub-circuit)

The 2:1 MUX is the fundamental building block. It selects between two inputs (`I0`, `I1`) based on a select signal (`A`).

### Technology
- CMOS (PMOS and NMOS transistors)

### Logic Expression

\[
Out = (I_0 \cdot \bar{A}) + (I_1 \cdot A)
\]

### Implementation
The design uses a combination of:
- Inverters
- AOI (AND-OR-Invert) logic

This ensures:
- Full-swing output
- Reduced transistor count
- Improved noise margins

---

## 2. The 8:1 Multiplexer Tree

To select 1 out of 8 lines, a three-stage **Tree Architecture** is used.

### Stage 1
- Four 2:1 MUXs
- Controlled by select bit `A1` (LSB)

### Stage 2
- Two 2:1 MUXs
- Controlled by select bit `A2`

### Stage 3
- One 2:1 MUX
- Controlled by select bit `A3` (MSB)

This modular approach:
- Simplifies debugging
- Improves scalability
- Encourages reusable design blocks

---

# Majority Function Implementation

The 8:1 MUX acts as a **universal logic element**. By connecting the data inputs (`I0`–`I7`) to either:
- Logic HIGH (`VDD = 5V`)
- Logic LOW (`GND = 0V`)

the circuit can implement any 3-variable Boolean function.

In this project, the implemented logic is the **Majority Function**, where the output becomes HIGH when **two or more inputs are HIGH**.

---

# Truth Table for Majority Function

| A3 | A2 | A1 | Selected Input | Output |
|----|----|----|----------------|--------|
| 0  | 0  | 0  | I0             | 0 |
| 0  | 0  | 1  | I1             | 0 |
| 0  | 1  | 0  | I2             | 0 |
| 0  | 1  | 1  | I3             | 1 |
| 1  | 0  | 0  | I4             | 0 |
| 1  | 0  | 1  | I5             | 1 |
| 1  | 1  | 0  | I6             | 1 |
| 1  | 1  | 1  | I7             | 1 |

### Input Configuration
To implement the Majority Function:

- `I3 = VDD`
- `I5 = VDD`
- `I6 = VDD`
- `I7 = VDD`

All other inputs are connected to `GND`.

---

# Simulation Details

| Parameter | Value |
|----------|-------|
| Software | LTspice XVII / XVII64 |
| Simulation Type | Transient Analysis (`.tran`) |
| Power Supply (`VDD`) | 5V |
| Input Signals | Pulse generators |
| Select Lines | `A1`, `A2`, `A3` |

Pulse generators were used to cycle through all 8 binary input combinations.

---

# How to Run

1. Download the `.asc` files and the `.asy` symbol file.
2. Place the custom `2:1 MUX` symbol in the same directory as the `8:1 MUX` schematic.
3. Open `MUX8to1.asc` in LTspice.
4. Click **Run**.
5. Observe the output waveforms in the waveform viewer.

---

# Key Concepts Demonstrated

- CMOS transistor-level design
- Hierarchical digital design
- Multiplexer tree architecture
- Boolean function implementation using MUXs
- LTspice circuit simulation
- Static CMOS logic optimization

---

# Tools Used

- **LTspice XVII**
- CMOS transistor models
- Digital logic design techniques

---

# Author

**Sichet Andrei**  
B.S. Communication Systems and Technologies Engineering Student
