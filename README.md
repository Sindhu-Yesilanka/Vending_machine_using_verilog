# ​ Vending Machine FSM — Verilog Project

A simple Verilog implementation of a vending machine using a Finite State Machine (FSM). The machine accepts 5-unit and 10-unit coins, and dispenses a product when the total inserted reaches 15 units or more.

---

##  EDA Playground Link

Try it out and see the simulation live:
**[Vending Machine FSM on EDA Playground](https://edaplayground.com/x/Cxaz)**

---

##  Project Overview

- **FSM Type**: Mealy Machine  
- **States**:
  - `S0` – 0 units inserted  
  - `S5` – 5 units inserted  
  - `S10` – 10 units inserted  
  - `S15` – ≥15 units inserted (trigger dispense then reset)  
- **Inputs**:  
  - `coin[1:0]` – `00 = no coin`, `01 = 5 units`, `10 = 10 units`  
- **Output**:  
  - `dispense` – HIGH when product is released  
- **Includes**: Synthesizable RTL, testbench, simulator-ready environment (via EDA Playground)

---

##  How It Works

1. **State Transitions**:
   - **S0** (0 units):  
     - Insert 5 → **S5**  
     - Insert 10 → **S10**  
   - **S5** (5 units):  
     - Insert 5 → **S10**  
     - Insert 10 → **S15** (dispense)  
   - **S10** (10 units):  
     - Insert 5 or 10 → **S15** (dispense)  
   - **S15** (15+ units):  
     - `dispense` = 1 → then reset to **S0**

2. **Mealy Logic Behavior**:
   - `dispense` is asserted in the **S15** cycle.
   - The machine does **not return change**—it simply dispenses once the threshold is met and resets.

---

##  Example Coin Sequences

| Sequence         | Outcome                  |
|------------------|--------------------------|
| 5 + 10           | Dispense at 15 units     |
| 10 + 5           | Dispense at 15 units     |
| 10 + 10          | Dispense at 15 units (20 inserted but no change) |
| 5 + 5 + 5        | Dispense at 15 units     |



