# MIPS-Visualizer
Interactive MIPS datapath visualizer with a built-in assembler, Single-Cycle and 5-Stage Pipeline execution, register/memory inspection, and hardware fault injection.

# MIPS Datapath Visualizer & Fault-Injection Engine

An interactive browser-based simulator for exploring **MIPS processor architecture, datapaths, pipelining, control signals, and hardware fault behavior**.

The project turns abstract CPU architecture into an executable visual system: write or select MIPS assembly, step through instructions, watch data and control signals propagate through the datapath, inspect registers and memory, compare Single-Cycle and Pipeline execution, and intentionally inject hardware faults to observe their effects.

## ✨ What can it do?

### 🧩 Visualize the MIPS Datapath

The simulator renders the main datapath components and highlights the signals involved in the current instruction.

It includes:

* Program Counter (PC)
* Instruction Memory
* Register File
* Main Control Unit
* Sign / Zero Extend
* ALU Control
* ALU
* Data Memory
* Multiplexers
* Next-PC / Branch Logic
* Active data and control paths

## The datapath can be explored interactively through component information popovers that explain each unit's role and show relevant inputs/outputs.

## ▶️ Single-Cycle Execution

Instructions can be executed one at a time using **Step**, or run continuously using **Run**.

For every instruction, the simulator exposes the relevant execution flow through the classic stages:

**IF → ID → EX → MEM → WB**

and shows the current PC, instruction, control signals, datapath activity, register changes, memory operations, and console analysis.

---

## ⚙️ Built-in MIPS Assembler

The project includes a lightweight assembler that parses MIPS assembly directly in the browser.

It supports:

* register aliases such as `$t0`, `$s0`, `$ra`, etc.
* immediate values in decimal and hexadecimal
* labels
* branch targets
* jump targets
* basic syntax and register validation
* interactive loading and assembly

You can either choose one of the built-in programs or edit the assembly yourself and assemble it directly in the interface.

### Supported instruction subset

The current implementation includes:

```text
add   sub   and   or    xor   nor
slt   sll   srl
addi  andi  ori   slti
lw    sw
beq   bne
j     jal   jr
```

---

## 🧠 Pipeline Mode

A separate **5-stage pipeline** view visualizes instruction timing across:

```text
IF → ID → EX → MEM → WB
```

The simulator includes a simplified timing model for:

* load-use data hazards
* pipeline stalls
* branch / jump penalties
* pipeline registers between stages
* cycle-by-cycle execution
* Gantt-style instruction timing

For example, one of the built-in programs demonstrates a `lw` followed immediately by an instruction using the loaded register, producing the modeled one-cycle stall. Another demonstrates instruction reordering to reduce stalls, and another demonstrates loop unrolling.

> Pipeline mode uses a simplified educational timing model rather than a full industrial CPU pipeline implementation.

---

## 🚨 Hardware Fault Injection

One of the main goals of the project is to experiment with **what happens when individual hardware signals or components fail**.

Faults can be injected into control signals such as:

```text
RegDst
ALUSrc
MemtoReg
RegWrite
MemRead
MemWrite
Branch
Jump
```

as well as selected component-level signals:

```text
ALU Zero flag
Sign / Zero Extend
```

Available fault models:

```text
Stuck-at-0
Stuck-at-1
Inverted
```

## The simulator then executes the instruction using the modified signal and reports whether the injected fault changed the resulting behavior. Faulted datapath wires are highlighted visually for easier debugging and analysis.

## 🧪 Example Programs

The project comes with 15 preset programs covering several architecture concepts:

### Arithmetic & Logic

* Basic addition and subtraction
* Bitwise operations
* Logical shifts
* Set-on-less-than
* Register swapping with XOR

### Memory

* Load / store
* Base-register addressing
* Sequential RAM access and accumulation

### Control Flow

* BEQ
* BNE loops
* Jump
* JAL / JR function call and return

### Pipeline Hazards

* Load-use hazard
* Instruction reordering
* Loop unrolling

## These examples are designed as small experiments that isolate individual processor concepts.

## 📊 Processor State Inspection

The UI exposes internal processor state while the program executes:

* 32 × 32-bit registers
* Data memory contents
* PC
* current instruction
* decoded instruction fields
* control signals
* ALU inputs and result
* memory reads / writes
* next-PC decision

This makes it possible to follow the execution of an instruction both **architecturally** and **at the datapath level**.

---

## 🏗️ Architecture

The project is organized conceptually as:

```text
MIPS Assembly
      ↓
    Assembler
      ↓
Instruction Representation
      ↓
   CPU Execution
      ↓
 ┌───────────────┐
 │   Datapath    │
 │ Control Unit  │
 │ Register File │
 │     ALU       │
 │ Data Memory   │
 └───────────────┘
      ↓
 State + Visualization
```

For fault analysis:

```text
Instruction
    ↓
Control / Datapath
    ↓
Fault Injection
    ↓
Modified Hardware Behavior
    ↓
Observed Architectural Result
```

---

## 🎯 Why I built it

I wanted to move from studying processor architecture as diagrams and equations to actually **executing instructions through a simulated datapath**.

The project became a way to experiment with questions such as:

* What exactly changes when a control signal is wrong?
* How does one faulty signal propagate through the datapath?
* What happens when the ALU's Zero flag is corrupted?
* How does pipelining change execution timing?
* Why do load-use hazards require a stall?
* How can instruction reordering improve pipeline utilization?

The visual interface is designed to make those effects observable rather than treating the CPU as a black box.

---

## 🛠️ Technology

Built as a browser-based interactive application using:

* HTML
* CSS
* JavaScript
* SVG for the datapath visualization
* Custom MIPS assembler
* Custom CPU execution model
* Interactive state visualization

No backend is required to run the simulator.

---

## 🚀 Running the project

Clone the repository or download the HTML file and open it in a browser.

```bash
git clone <repository-url>
```

Then open:

```text
mips-visualizer.html
```

in your browser.

No installation or build step is required.

---

## 🔮 Possible Future Extensions

Some natural directions for extending the project:

* forwarding / hazard detection logic
* additional pipeline hazards
* branch prediction
* cache simulation
* configurable datapath architectures
* additional MIPS instructions
* more detailed fault models
* timing / performance comparisons
* FPGA / RTL implementation of selected datapath blocks

---

## 📌 Project Status

This is an **educational CPU architecture and fault-simulation project** designed to explore processor datapaths and failure modes interactively.

The implementation intentionally uses a simplified MIPS subset and simplified pipeline timing model so that the underlying architecture remains visible and understandable.
