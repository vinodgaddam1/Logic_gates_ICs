Here's the `README.md` with emojis — your source code remains **verbatim, with zero changes** ✅

# ⚡ Logic_gates_ICs 🔌

> 🧩 SystemVerilog models of standard 74-series logic gate ICs, described at the **pin level** so they can be wired together exactly like real chips on a breadboard. 🍞

---

## 📚 Contents

| 🔢 IC Number | ⚙️ Function | 🚪 Gates | 📌 Status |
|-----------|----------|-------|--------|
| 7408 | Quad 2-input AND | 4 × AND2 | ✅ Available |

---

## 🟢 IC7408 — Quad 2-Input AND Gate

### 📝 Description
The 7408 contains **four independent 2-input AND gates** 🚪🚪🚪🚪 in a 14-pin DIP package 📦. Pin 14 is `VCC` ⚡ and pin 7 is `GND` 🌍; the remaining 12 pins form the four gates (2 inputs ➡️ + 1 output ⬅️ each).

### 🔍 Pinout
```
             +---------+
  PIN   1  --|         |-- 14 PIN
  PIN   2  --|         |-- 13 PIN
  PIN   3  --|  7408   |-- 12 PIN
  PIN   4  --|         |-- 11 PIN
  PIN   5  --|         |-- 10 PIN
  PIN   6  --|         |--  9 PIN
  PIN   7  --|         |--  8 PIN
             +---------+
```

### 📌 Pin Assignment

| 🚪 Gate | 🅰️ Input A | 🅱️ Input B | 📤 Output | 🧮 Expression |
|------|---------|---------|--------|------------|
| 1️⃣ | PIN1 | PIN2 | PIN3 | `PIN3  = PIN1  & PIN2` |
| 2️⃣ | PIN4 | PIN5 | PIN6 | `PIN6  = PIN4  & PIN5` |
| 3️⃣ | PIN10 | PIN9 | PIN8 | `PIN8  = PIN10 & PIN9` |
| 4️⃣ | PIN12 | PIN13 | PIN11 | `PIN11 = PIN12 & PIN13` |

| 🔋 Power Pin | 🎯 Function |
|-----------|----------|
| PIN14 | ⚡ VCC (+5 V) |
| PIN7 | 🌍 GND (0 V) |

### 📊 Truth Table (per gate)

| 🅰️ A | 🅱️ B | 💡 Y |
|---|---|---|
| 0 | 0 | 0 ⬛ |
| 0 | 1 | 0 ⬛ |
| 1 | 0 | 0 ⬛ |
| 1 | 1 | 1 🟩 |

---

## 💻 Source Code

```systemverilog
/*==========================================================================
                       Logic_gates_ICs
============================================================================
****************************************************************************
                         IC.number IC7408(AND) 
****************************************************************************
             +---------+
  PIN   1  --|         |-- 14 PIN
  PIN   2  --|         |-- 13 PIN
  PIN   3  --|  7408   |-- 12 PIN
  PIN   4  --|         |-- 11 PIN
  PIN   5  --|         |-- 10 PIN
  PIN   6  --|         |--  9 PIN
  PIN   7  --|         |--  8 PIN
             +---------+

*/

module IC7408(
input PIN1,
input PIN2,
output PIN3,

input PIN4,
input PIN5,
output PIN6,


input PIN10,
input PIN9,
output PIN8,

input PIN12,
input PIN13,
output PIN11,

input PIN7,
input PIN14
);
logic GND; 
logic VCC;
assign PIN3 = PIN1 & PIN2;

assign PIN6 = PIN4 & PIN5;


assign PIN8 = PIN10 & PIN9;

assign PIN11 = PIN12 & PIN13;
 

endmodule
```

---

## 🚀 Usage

```systemverilog
module top (
    input  logic a, b, c, d,
    output logic y1, y2
);

    logic gnd = 1'b0;
    logic vcc = 1'b1;

    IC7408 U1 (
        // Gate 1
        .PIN1 (a),  .PIN2 (b),  .PIN3 (y1),
        // Gate 2
        .PIN4 (c),  .PIN5 (d),  .PIN6 (y2),
        // Gate 3 (unused inputs tied low)
        .PIN10(1'b0), .PIN9 (1'b0), .PIN8 (),
        // Gate 4 (unused inputs tied low)
        .PIN12(1'b0), .PIN13(1'b0), .PIN11(),
        // Power
        .PIN7 (gnd), .PIN14(vcc)
    );

endmodule
```

### ▶️ Simulation

```bash
# 🧪 Icarus Verilog
iverilog -g2012 -o ic7408_tb IC7408.sv tb_IC7408.sv
vvp ic7408_tb

# 🧪 ModelSim / Questa
vlog IC7408.sv tb_IC7408.sv
vsim -c work.tb_IC7408 -do "run -all; quit"
```

---

## 💡 Notes
* 🔌 `GND` and `VCC` are declared inside the module as internal `logic` signals; the real supply connections are made through `PIN7` and `PIN14`.
* 🧭 The pin ordering in the port list follows the physical gate grouping rather than strict numerical order (gate 3 is declared as `PIN10, PIN9, PIN8`), matching the datasheet layout.
* ⚠️ Always connect unused gate inputs to a known level (`1'b0` or `1'b1`) to avoid `X` propagation in simulation.

---

## 🗺️ Roadmap
* ⬜ IC7400 — Quad 2-input NAND
* ⬜ IC7402 — Quad 2-input NOR
* ⬜ IC7404 — Hex inverter
* ⬜ IC7432 — Quad 2-input OR
* ⬜ IC7486 — Quad 2-input XOR

---

## 🤝 Contributing
Pull requests are welcome! 🎉 Please follow the same pin-level style used in `IC7408.sv`.

## 📄 License
Released under the **MIT License** 🆓 — free to use, modify and distribute.

⭐ If you find this useful, consider starring the repo!
