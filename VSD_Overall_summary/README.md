# 🔬 Digital VLSI Laboratory — RTL Design, Synthesis & Physical Design


## 📌 Table of Contents

- [1. Introduction](#-1-introduction)
- [2. Objectives](#-2-objectives)
- [3. Digital IC Design Flow](#-3-digital-ic-design-flow)
- [4. Tools and Technologies](#️-4-tools-and-technologies)
- [5. Repository Structure](#-5-repository-structure)
- [6. Lab 01 — 2:1 Multiplexer Design and Simulation](#-6-lab-01--21-multiplexer-design-and-simulation)
- [7. Lab 02 — RTL Design and Synthesis Using Yosys](#-7-lab-02--rtl-design-and-synthesis-using-yosys)
- [8. Standard-Cell Libraries and SKY130](#-8-standard-cell-libraries-and-sky130)
- [9. Timing Libraries and PVT Corners](#-9-timing-libraries-and-pvt-corners)
- [10. Hierarchical and Flat Synthesis](#-10-hierarchical-and-flat-synthesis)
- [11. Sequential Logic and Flip-Flop Coding](#-11-sequential-logic-and-flip-flop-coding)
- [12. Combinational Logic Optimization](#-12-combinational-logic-optimization)
- [13. Sequential Logic Optimization](#-13-sequential-logic-optimization)
- [14. Gate-Level Simulation](#-14-gate-level-simulation)
- [15. Blocking and Non-Blocking Assignments](#-15-blocking-and-non-blocking-assignments)
- [16. Synthesis-Simulation Mismatches](#️-16-synthesis-simulation-mismatches)
- [17. Synthesis Constructs and Latch Inference](#-17-synthesis-constructs-and-latch-inference)
- [18. Introduction to Physical Design](#️-18-introduction-to-physical-design)
- [19. Floorplanning and Placement](#-19-floorplanning-and-placement)
- [20. Clock Tree Synthesis](#-20-clock-tree-synthesis)
- [21. Static Timing Analysis](#-21-static-timing-analysis)
- [22. Setup and Hold Timing](#-22-setup-and-hold-timing)
- [23. Timing Closure and Optimization](#-23-timing-closure-and-optimization)
- [24. Routing and TritonRoute](#️-24-routing-and-tritonroute)
- [25. Design Rule Checking](#-25-design-rule-checking)
- [26. OpenSTA and Post-Route Analysis](#-26-opensta-and-post-route-analysis)
- [27. Complete RTL-to-GDS Flow](#-27-complete-rtl-to-gds-flow)
- [28. Practical Commands Reference](#-28-practical-commands-reference)
- [29. Learning Outcomes](#-29-learning-outcomes)
- [30. Conclusion](#-30-conclusion)
- [31. References and Resources](#-31-references-and-resources)

---

# 🔍 1. Introduction

Welcome to my **Digital VLSI Laboratory** repository.

This repository documents my learning and practical work in digital Very Large Scale Integration (VLSI) design. It focuses on understanding how digital hardware is described using Verilog HDL, simulated to verify its functionality, synthesized into a gate-level representation, and analyzed using standard-cell libraries and timing concepts.

The repository includes practical work on a **2:1 Multiplexer**, RTL simulation using Icarus Verilog, waveform analysis using GTKWave, and RTL synthesis using Yosys with the SKY130 standard-cell library.

My accompanying notes extend these fundamentals to combinational and sequential optimization, gate-level simulation, timing analysis, clock tree synthesis, routing, and the broader RTL-to-GDS implementation flow.

The objective is to understand not only how to write RTL code, but also how that code is interpreted by synthesis tools and translated into hardware structures.

## Why Digital VLSI?

Digital VLSI design connects hardware description, logic design, verification, synthesis, and physical implementation.

A small RTL description can eventually become a network of interconnected standard cells. Understanding this transformation is essential for learning ASIC design, digital hardware implementation, and semiconductor engineering.

The work documented here builds a foundation in:

- Digital logic design
- Verilog RTL development
- Functional simulation and waveform analysis
- Logic synthesis and technology mapping
- Standard-cell libraries
- Sequential circuit design
- Synthesis optimization
- Static timing analysis
- Physical-design concepts
- Open-source EDA tools

---

# 🎯 2. Objectives

The primary objectives of this laboratory work are:

1. Understand the fundamentals of Verilog HDL and RTL design.
2. Design a simple digital circuit using Verilog.
3. Create a testbench to verify the functionality of the design.
4. Compile and simulate Verilog code using Icarus Verilog.
5. Generate and inspect simulation waveforms using GTKWave.
6. Understand the purpose of RTL synthesis.
7. Use Yosys to synthesize a digital design.
8. Understand the role of ABC in logic optimization and technology mapping.
9. Explore the SKY130 standard-cell library and Liberty `.lib` files.
10. Understand the relationship between RTL, logic gates, and a mapped netlist.
11. Study hierarchical and flat synthesis.
12. Understand synchronous and asynchronous reset behavior.
13. Explore combinational and sequential logic optimization.
14. Understand blocking and non-blocking assignments.
15. Learn why gate-level simulation is useful after synthesis.
16. Study setup time, hold time, clock period, slack, WNS, and TNS.
17. Understand physical-design stages such as floorplanning, placement, clock tree synthesis, and routing.
18. Explore the purpose of design rule checking and post-route timing analysis.
19. Develop a structured understanding of the digital ASIC implementation flow.

---

# 🔄 3. Digital IC Design Flow

A digital ASIC design passes through multiple stages before it becomes a physical layout.

The fundamental flow can be represented as follows:

```text
                 DIGITAL DESIGN SPECIFICATION
                            |
                            v
                      RTL DEVELOPMENT
                         Verilog
                            |
                            v
                    FUNCTIONAL SIMULATION
                     Icarus Verilog
                            |
                            v
                    WAVEFORM VERIFICATION
                         GTKWave
                            |
                            v
                      RTL SYNTHESIS
                          Yosys
                            |
                            v
                  LOGIC OPTIMIZATION / ABC
                            |
                            v
                  TECHNOLOGY MAPPING
                    SKY130 Cell Library
                            |
                            v
                   GATE-LEVEL NETLIST
                            |
                            v
                   GATE-LEVEL SIMULATION
                            |
                            v
                      FLOORPLANNING
                            |
                            v
                         PLACEMENT
                            |
                            v
                  CLOCK TREE SYNTHESIS
                            |
                            v
                          ROUTING
                            |
                            v
                DESIGN RULE AND TIMING CHECKS
                            |
                            v
                    FINAL LAYOUT / GDS
```

**Important:** The repository directly documents the early RTL, simulation, and synthesis stages. The later stages are also covered in my learning notes as concepts in the complete digital implementation flow. Their inclusion in this overview does not imply that every design in this repository has completed every physical-design stage.

## Front-End and Back-End Design

| Front-End Design | Back-End Design |
|---|---|
| RTL development | Floorplanning |
| Functional verification | Placement |
| RTL synthesis | Clock tree synthesis |
| Logic optimization | Routing |
| Technology mapping | Parasitic extraction |
| Gate-level verification | Physical verification |
| Initial timing analysis | Post-route timing analysis |

The front end focuses on describing and verifying the intended digital functionality. The back end focuses on implementing the design physically while satisfying timing, area, and electrical constraints.

---

# 🛠️ 4. Tools and Technologies

The practical work and accompanying notes cover the following tools and technologies.

| Tool / Technology | Purpose |
|---|---|
| Verilog HDL | Hardware description and RTL design |
| Icarus Verilog | Compilation and simulation of Verilog designs |
| GTKWave | Visualization of simulation waveforms |
| Yosys | RTL synthesis and logic transformation |
| ABC | Logic optimization and technology mapping |
| SKY130 | Open-source 130 nm process design ecosystem |
| Liberty `.lib` | Standard-cell functionality and timing information |
| Linux / Ubuntu | Environment for running open-source EDA tools |
| OpenLane | Automated RTL-to-GDS implementation flow |
| OpenSTA | Static timing analysis |
| TritonRoute | Detailed routing in the OpenROAD ecosystem |
| Magic | Layout viewing and physical-design operations |
| NGSpice | Circuit-level simulation |

The exact tools used depend on the individual experiment. Icarus Verilog, GTKWave, Yosys, ABC, and SKY130 are particularly relevant to the first two documented labs.

---

# 📁 5. Repository Structure

The repository organizes the documented practical work into individual laboratory folders.

```text
VLSI_LAB/
│
├── README.md
│
├── Lab-01-2x1-Multiplexer/
│   └── README.md
│
├── Lab-02-YOSYS-mux/
│   ├── README.md
│   └── images/
│
└── Module-2:Timing libs,hierarchial vs flat synthesis,
    efficient flop coding styles/
```

The structure above reflects the main documented folders. Additional notes on optimization, gate-level simulation, timing, and routing expand on the concepts introduced by these labs.

---

# 🔀 6. Lab 01 — 2:1 Multiplexer Design and Simulation

## 6.1 Aim

To design and simulate a 2:1 multiplexer using Verilog HDL, verify its functionality with a testbench, and observe the output waveform using Icarus Verilog and GTKWave.

## 6.2 Theory

A 2:1 multiplexer (MUX) is a combinational circuit that selects one of two input signals based on a select signal.

It has three inputs:

- `i0` — First data input
- `i1` — Second data input
- `sel` — Select input

It has one output:

- `y` — Selected output

The output equation is:

\[
Y = \overline{S}I_0 + SI_1
\]

When `sel = 0`, the output follows `i0`.

When `sel = 1`, the output follows `i1`.

## 6.3 Truth Table

| Select (`sel`) | Input `i0` | Input `i1` | Output `y` |
|---|---|---|---|
| 0 | 0 | X | 0 |
| 0 | 1 | X | 1 |
| 1 | X | 0 | 0 |
| 1 | X | 1 | 1 |

`X` indicates that the corresponding input does not affect the output for that select value.

## 6.4 Verilog RTL Code

```verilog
module good_mux (
    input i0,
    input i1,
    input sel,
    output y
);

assign y = sel ? i1 : i0;

endmodule
```

## 6.5 Code Explanation

- `module good_mux` declares the module named `good_mux`.
- `input i0` declares the first data input.
- `input i1` declares the second data input.
- `input sel` declares the select signal.
- `output y` declares the output.
- `assign y = sel ? i1 : i0;` implements the multiplexer using a conditional operator.
- `endmodule` marks the end of the module.

The conditional operator evaluates the select signal and chooses the corresponding input.

## 6.6 Testbench

A testbench applies input combinations to the design and checks the resulting output.

```verilog
module tb_good_mux;

reg i0;
reg i1;
reg sel;
wire y;

good_mux uut (
    .i0(i0),
    .i1(i1),
    .sel(sel),
    .y(y)
);

initial begin
    $dumpfile("tb_good_mux.vcd");
    $dumpvars(0, tb_good_mux);

    i0 = 0; i1 = 0; sel = 0;
    #10;

    i0 = 1; i1 = 0; sel = 0;
    #10;

    i0 = 0; i1 = 1; sel = 1;
    #10;

    i0 = 1; i1 = 1; sel = 1;
    #10;

    $finish;
end

endmodule
```

## 6.7 Testbench Explanation

- `reg` variables are used to drive the inputs.
- `wire y` observes the output from the instantiated module.
- `good_mux uut` creates an instance of the multiplexer.
- `$dumpfile` specifies the waveform output file.
- `$dumpvars` records signals for waveform inspection.
- `#10` introduces a simulation delay of 10 time units.
- `$finish` ends the simulation.

## 6.8 Simulation Using Icarus Verilog

Compile the RTL and testbench:

```bash
iverilog -o mux_sim good_mux.v tb_good_mux.v
```

Run the simulation:

```bash
vvp mux_sim
```

The simulation generates a VCD waveform file if the testbench includes the appropriate dump commands.

## 6.9 View the Waveform Using GTKWave

```bash
gtkwave tb_good_mux.vcd
```

Inspect the signals `i0`, `i1`, `sel`, and `y`.

Verify that the output follows `i0` when `sel = 0` and follows `i1` when `sel = 1`.

## 6.10 Expected Observation

The output changes according to the select signal and the selected data input. The simulation verifies the basic functionality of the 2:1 multiplexer for the applied input combinations.

---

# ⚙️ 7. Lab 02 — RTL Design and Synthesis Using Yosys

## 7.1 Aim

To synthesize the 2:1 multiplexer using Yosys and understand how RTL is transformed into a logic representation.

## 7.2 What Is RTL Synthesis?

RTL synthesis is the process of converting a register-transfer-level description into a hardware implementation represented by logic cells and connections.

The synthesis tool interprets the RTL, performs logic transformations and optimizations, and produces a netlist.

The final implementation depends on the design, synthesis settings, target technology, and available cell library.

## 7.3 Basic Synthesis Flow

```text
Verilog RTL
    |
    v
Read Design
    |
    v
Process and Elaborate
    |
    v
Optimize Logic
    |
    v
Map to Target Cells
    |
    v
Generate Netlist
```

## 7.4 Read and Synthesize the Design

Start Yosys:

```bash
yosys
```

Read the Verilog source:

```tcl
read_verilog good_mux.v
```

Synthesize the selected top module:

```tcl
synth -top good_mux
```

Display the synthesized design:

```tcl
show
```

Write the synthesized netlist:

```tcl
write_verilog -noattr good_mux_netlist.v
```

## 7.5 Understanding the Synthesized Netlist

The synthesized netlist represents the circuit using logic elements and connections.

For a simple multiplexer, the implementation may use a multiplexer cell or an equivalent combination of logic gates, depending on the synthesis and mapping flow.

The synthesized netlist should be inspected to determine which structure was actually generated.

## 7.6 Why Synthesis Is Important

Synthesis helps transform a behavioral hardware description into an implementation that can be mapped to a target technology.

It is used to:

- Infer hardware structures from RTL.
- Simplify Boolean expressions.
- Remove redundant logic.
- Optimize logic for implementation goals.
- Map logic to cells in a target library.
- Produce a netlist for downstream design stages.

## 7.7 Role of ABC

ABC is a logic synthesis and technology-mapping tool that can optimize logic networks and map them to cells described by a target library.

The exact transformations depend on the synthesis script, the input network, and the selected library.

## 7.8 Expected Observation

The RTL description is transformed into a synthesized netlist. Examining that netlist helps connect the Verilog code with the logic structure selected by the synthesis flow.

---

# 🧱 8. Standard-Cell Libraries and SKY130

## 8.1 What Is a Standard-Cell Library?

A standard-cell library contains predefined digital logic cells that can be used to implement a circuit.

Examples include:

- Inverters
- AND gates
- OR gates
- NAND gates
- NOR gates
- XOR gates
- Multiplexers
- Flip-flops
- Buffers

Each cell has a defined logical function and physical implementation. Libraries can also provide timing, power, and electrical characteristics.

## 8.2 What Is SKY130?

SKY130 is an open-source 130 nm process design ecosystem used in educational and open-source integrated-circuit design.

It provides process-related files and standard-cell libraries that can be used with compatible EDA flows.

The availability of cell models and design information makes SKY130 useful for learning RTL synthesis and ASIC implementation.

## 8.3 Liberty `.lib` Files

A Liberty file describes the characteristics of standard cells.

It can include:

- Cell names
- Pin names
- Logical functions
- Input capacitance
- Timing arcs
- Setup and hold constraints
- Propagation delay tables
- Transition information
- Power-related information

The exact information depends on the library and the cell.

## 8.4 Example SKY130 Library

A library filename used in SKY130-based flows is:

```text
sky130_fd_sc_hd__tt_025C_1v80.lib
```

The exact filename varies across distributions and versions. Verify the library path in the installed PDK before using it.

The components of the filename generally identify the library family and operating corner.

| Component | Meaning |
|---|---|
| `sky130` | SKY130 process ecosystem |
| `fd_sc_hd` | Standard-cell library family |
| `tt` | Typical process corner |
| `025C` | Temperature of 25 °C |
| `1v80` | Supply voltage of 1.80 V |
| `.lib` | Liberty timing and cell-description format |

## 8.5 Why Standard-Cell Libraries Matter

The target library influences how a synthesized logic function is implemented.

Different libraries may provide different cell choices, drive strengths, timing characteristics, and area values.

Technology mapping selects suitable cells from the available library according to the synthesis flow and its optimization objectives.

---

# ⏱️ 9. Timing Libraries and PVT Corners

## 9.1 What Is a Timing Library?

A timing library describes timing-related characteristics of cells.

The synthesis and timing-analysis tools use these models to estimate or analyze the delays and timing constraints associated with a circuit.

## 9.2 What Is PVT?

PVT stands for:

- **P — Process:** Variations in semiconductor manufacturing.
- **V — Voltage:** The operating supply voltage.
- **T — Temperature:** The operating temperature.

These factors influence transistor behavior and can affect cell delay, power consumption, and circuit performance.

## 9.3 Process Corners

Common process-corner labels include:

| Corner | General Description |
|---|---|
| `TT` | Typical NMOS and typical PMOS behavior |
| `SS` | Slow NMOS and slow PMOS behavior |
| `FF` | Fast NMOS and fast PMOS behavior |
| `SF` | Slow NMOS and fast PMOS behavior |
| `FS` | Fast NMOS and slow PMOS behavior |

The precise meaning and characterization depend on the process and library.

## 9.4 Why Multiple Corners Are Used

A circuit must be evaluated under the operating conditions required by its design methodology.

For example, a slower cell corner may make setup timing more difficult, while a faster data path can create hold-timing challenges.

The relevant corners and constraints depend on the design and sign-off methodology.

## 9.5 Timing Analysis and the Liberty File

Timing analysis combines library timing information with the design netlist and timing constraints.

Typical inputs include:

- Gate-level netlist
- Liberty timing libraries
- Timing constraints
- Clock definitions
- Input and output delays
- Parasitic information, when available

The analysis identifies whether the relevant timing paths meet their required timing conditions.

---

# 🏗️ 10. Hierarchical and Flat Synthesis

## 10.1 Hierarchical Synthesis

Hierarchical synthesis preserves or works with a design's module hierarchy.

A large design can be organized into smaller submodules. These submodules can be analyzed and synthesized as part of a hierarchical flow.

### Advantages

- Maintains the organization of the RTL.
- Helps manage large designs.
- Makes module boundaries easier to inspect.
- Can support modular development and reuse.

### Considerations

- Module boundaries can restrict some optimizations across boundaries.
- The final result depends on how the synthesis flow handles hierarchy and optimization.

## 10.2 Flat Synthesis

Flat synthesis combines the logic of multiple modules into a common optimization context, subject to the synthesis tool's behavior and settings.

### Advantages

- Can enable optimization across former module boundaries.
- May simplify logic across interconnected modules.
- Can improve some area or timing results.

### Considerations

- The original module structure may be less visible in the resulting netlist.
- The flattened design can become more difficult to inspect at the original RTL hierarchy level.
- Results depend on the design and optimization settings.

## 10.3 Comparison

| Hierarchical Synthesis | Flat Synthesis |
|---|---|
| Works with preserved module structure | Combines logic into a flatter representation |
| Supports modular organization | Can enable cross-boundary optimization |
| Easier to relate some results to RTL modules | May be harder to relate netlist logic to original module boundaries |
| Optimization depends on hierarchy handling | Optimization can consider a broader logic context |

## 10.4 Key Observation

Neither approach is universally better. The appropriate choice depends on the design, synthesis strategy, optimization goals, and implementation constraints.

---

# 🔁 11. Sequential Logic and Flip-Flop Coding

Sequential circuits store state and change their outputs according to clock events and input conditions.

Flip-flops are fundamental storage elements in synchronous digital designs.

## 11.1 D Flip-Flop

A D flip-flop samples its data input at an active clock edge and updates its output according to its defined behavior.

A simplified example is:

```verilog
module dff (
    input  wire clk,
    input  wire d,
    output reg  q
);

always @(posedge clk)
    q <= d;

endmodule
```

The non-blocking assignment `<=` is appropriate for this clocked sequential process.

## 11.2 Synchronous Reset

A synchronous reset is evaluated only when the relevant clock event occurs.

```verilog
always @(posedge clk) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

When the reset is asserted, the register is assigned zero at the active clock edge.

## 11.3 Asynchronous Reset

An asynchronous reset can affect the register independently of the normal clock edge.

```verilog
always @(posedge clk or posedge rst) begin
    if (rst)
        q <= 1'b0;
    else
        q <= d;
end
```

This example uses an active-high asynchronous reset.

The reset polarity and sensitivity list must match the intended design and the target technology.

## 11.4 Why Coding Style Matters

Synthesis tools infer hardware from the RTL description.

A coding style that clearly expresses the intended sequential behavior helps avoid unintended storage elements or differences between simulation and synthesis.

Important considerations include:

- Correct event controls
- Appropriate use of blocking and non-blocking assignments
- Complete assignment of signals where required
- Clear reset behavior
- Avoidance of unintended latches
- Understanding initialization and reset assumptions

---

# 🧠 12. Combinational Logic Optimization

Combinational logic produces outputs based on the current inputs, without retaining state.

Logic optimization aims to simplify the circuit while preserving its required functionality.

## 12.1 Constant Propagation

Constant propagation identifies signals whose values are known and uses those values to simplify the design.

For example:

```verilog
assign y = a & 1'b0;
```

The output is always zero:

```verilog
assign y = 1'b0;
```

The original logic is unnecessary and can be removed.

## 12.2 Boolean Logic Optimization

Boolean algebra can simplify logic expressions.

For example:

\[
A \land 1 = A
\]

\[
A \land 0 = 0
\]

\[
A \lor 0 = A
\]

\[
A \lor 1 = 1
\]

\[
A \land A = A
\]

\[
A \lor A = A
\]

These identities can reduce redundant logic.

## 12.3 Redundant Logic Removal

Redundant logic is logic that does not affect the required output behavior.

Removing redundant logic can reduce the number of gates and simplify the implementation.

For example:

```verilog
assign y = (a & b) | (a & b);
```

The expression can be simplified to:

```verilog
assign y = a & b;
```

## 12.4 Logic Restructuring

Logic restructuring changes the organization of Boolean expressions to create a potentially more efficient implementation.

The goal may be to reduce:

- Logic depth
- Gate count
- Area
- Delay
- Switching activity

The result depends on the target library and the optimization objectives.

## 12.5 Multiplexer Optimization

A multiplexer selects one of several input signals.

```verilog
assign y = sel ? b : a;
```

The synthesis tool may implement the expression using a multiplexer cell or equivalent logic gates, depending on the target library and mapping process.

## 12.6 Why Combinational Optimization Matters

Combinational optimization can improve the logic network before technology mapping and physical implementation.

A simpler Boolean expression does not always guarantee the fastest or smallest physical circuit. Cell availability, loading, routing, and timing constraints also affect the result.

---

# 🔄 13. Sequential Logic Optimization

Sequential logic contains storage elements such as flip-flops and registers.

Optimization must preserve the required state transitions and observable behavior.

## 13.1 Common Optimization Approaches

Sequential optimization can involve:

- Removing redundant registers where equivalence can be established
- Simplifying next-state logic
- Reducing unnecessary logic around registers
- Optimizing reset structures where permitted
- Sharing equivalent logic
- Improving critical register-to-register paths

## 13.2 State Registers

A state register stores the current state of a sequential circuit.

For example:

```verilog
always @(posedge clk or posedge rst) begin
    if (rst)
        state <= 1'b0;
    else
        state <= next_state;
end
```

The next-state logic determines the value that will be stored at the next active clock edge.

## 13.3 Register Count and Area

Flip-flops contribute to the total cell area of a design.

However, reducing the register count is not always the correct optimization. The design must continue to satisfy its functional, timing, and reset requirements.

## 13.4 Timing Considerations

A sequential path commonly includes:

1. Launch flip-flop
2. Combinational logic
3. Capture flip-flop

The path must satisfy the timing requirements associated with the clock and the two sequential elements.

Sequential optimization therefore involves both functional correctness and timing behavior.

---

# 🧪 14. Gate-Level Simulation

Gate-level simulation verifies a synthesized or technology-mapped netlist using a simulation environment.

Unlike RTL simulation, which models the design at the register-transfer level, gate-level simulation operates on the gates or cells represented in the netlist.

## 14.1 Why Gate-Level Simulation Is Useful

Gate-level simulation can help identify:

- Differences between RTL and the synthesized netlist
- Incorrect cell connections
- Reset-related issues
- Problems associated with unknown or uninitialized values
- Potential timing-related behavior when suitable timing models are included

Gate-level simulation does not replace static timing analysis or physical verification.

## 14.2 RTL Simulation Versus Gate-Level Simulation

| RTL Simulation | Gate-Level Simulation |
|---|---|
| Uses the RTL description | Uses a synthesized or mapped netlist |
| Focuses on intended functional behavior | Checks behavior of the gate-level implementation |
| Generally uses abstract RTL timing | Can use cell timing models when configured |
| Does not directly represent mapped cell structure | Reflects the cells and connections in the netlist |

## 14.3 Typical Gate-Level Simulation Flow

```text
RTL Source
    |
    v
RTL Simulation
    |
    v
Synthesis
    |
    v
Gate-Level Netlist
    |
    v
Cell Models / Timing Models
    |
    v
Gate-Level Simulation
    |
    v
Compare Expected Behavior
```

## 14.4 Functional Equivalence

The RTL and gate-level implementation should preserve the required functional behavior under equivalent assumptions.

Differences can arise from reset handling, uninitialized state, simulation models, timing delays, or mismatches between the intended design and the implementation.

The source RTL, testbench, netlist, and cell models must be checked when investigating discrepancies.

---

# 📝 15. Blocking and Non-Blocking Assignments

Verilog provides blocking and non-blocking assignments.

## 15.1 Blocking Assignment

The blocking assignment operator is `=`.

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

A blocking assignment updates the assigned variable immediately within the procedural execution order.

Blocking assignments are commonly used for combinational procedural logic.

## 15.2 Non-Blocking Assignment

The non-blocking assignment operator is `<=`.

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

A non-blocking assignment schedules the update for the non-blocking assignment update region of the simulation time step.

Non-blocking assignments are commonly used for clocked sequential logic.

## 15.3 Comparison

| Blocking (`=`) | Non-Blocking (`<=`) |
|---|---|
| Updates immediately within procedural execution | Schedules the update for the non-blocking assignment region |
| Commonly used in combinational procedural blocks | Commonly used in clocked sequential blocks |
| Later statements can observe the updated value in the same procedural flow | Right-hand sides are evaluated when the statement executes, while updates occur later in the time step |

## 15.4 Example of Sequential Coding

```verilog
always @(posedge clk) begin
    a <= b;
    b <= a;
end
```

Both right-hand sides are evaluated using the values before the non-blocking updates take effect. This behavior is useful when describing simultaneous register updates.

## 15.5 Important Coding Rule

Use assignment styles that clearly match the intended hardware behavior.

- Use blocking assignments for typical combinational procedural logic.
- Use non-blocking assignments for typical clocked sequential logic.
- Avoid mixing assignment styles carelessly within the same design process.
- Ensure all combinational outputs receive assignments on every required execution path.

---

# ⚠️ 16. Synthesis-Simulation Mismatches

A synthesis-simulation mismatch occurs when the simulated RTL behavior differs from the synthesized implementation under the conditions being compared.

## 16.1 Common Causes

- Incomplete assignments in combinational logic
- Unintended latch inference
- Incorrect sensitivity lists in older Verilog coding styles
- Blocking and non-blocking assignment misuse
- Uninitialized registers
- Reset assumptions that differ between simulation and hardware
- Unsupported or synthesis-specific constructs
- Differences between simulation models and library models

## 16.2 Incomplete Combinational Assignment

Consider:

```verilog
always @(*) begin
    if (sel)
        y = a;
end
```

When `sel` is zero, `y` is not assigned in this block. Its previous value must be retained, which can infer a latch.

A complete combinational version is:

```verilog
always @(*) begin
    if (sel)
        y = a;
    else
        y = b;
end
```

The complete assignment allows the intended combinational behavior to be inferred.

## 16.3 How to Prevent Mismatches

- Write complete and synthesizable RTL.
- Use appropriate assignment styles.
- Define reset behavior clearly.
- Run RTL simulation before synthesis.
- Inspect synthesis warnings.
- Review the synthesized netlist.
- Run gate-level simulation when required.
- Use timing analysis to evaluate timing constraints.

## 16.4 Key Lesson

Successful RTL simulation alone does not prove that the complete implementation is correct. Verification must consider the RTL, synthesized netlist, timing assumptions, and target library.

---

# 🧩 17. Synthesis Constructs and Latch Inference

Synthesis tools infer hardware from Verilog statements. Coding style affects which hardware structures are inferred.

## 17.1 `if` Statements

An `if` statement describes conditional behavior.

```verilog
always @(*) begin
    if (sel)
        y = a;
    else
        y = b;
end
```

This describes a combinational selection function.

If a required assignment is omitted, storage behavior may be inferred.

## 17.2 `case` Statements

A `case` statement selects behavior based on the value of an expression.

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        2'b11: y = d;
        default: y = 1'b0;
    endcase
end
```

The `default` branch makes the assignment behavior explicit for other or unknown case values according to the simulation semantics and coding context.

## 17.3 Latch Inference

A latch may be inferred when a signal must retain its previous value because it is not assigned on every required execution path.

Example:

```verilog
always @(*) begin
    if (enable)
        q = d;
end
```

When `enable` is false, `q` retains its previous value. This describes latch-like behavior.

## 17.4 Avoiding Unintended Latches

For combinational logic, assign all relevant outputs on every execution path.

```verilog
always @(*) begin
    q = 1'b0;

    if (enable)
        q = d;
end
```

The default assignment prevents the previous value of `q` from needing to be retained in this block.

## 17.5 `for` Loops

A synthesizable `for` loop can describe repeated hardware operations. Synthesis tools generally unroll statically bounded loops during elaboration or synthesis.

The loop bounds and operations must be compatible with the synthesis tool and intended hardware.

## 17.6 Generate Constructs

Generate constructs create repeated or conditional hardware structures during elaboration.

Example:

```verilog
genvar i;

generate
    for (i = 0; i < 4; i = i + 1) begin : gen_block
        // Repeated hardware description
    end
endgenerate
```

Generate constructs are useful for parameterized and repetitive designs.

## 17.7 Important Considerations

- Use complete assignments in combinational logic.
- Use clocked processes for intended flip-flop behavior.
- Check for latch warnings.
- Ensure loops have valid static bounds.
- Review synthesis reports and the generated netlist.

---

# 🏗️ 18. Introduction to Physical Design

After synthesis, the design is represented as a netlist. Physical design transforms that logical representation into a physical layout.

The implementation must consider more than Boolean correctness. It must also account for placement, wiring, clock distribution, electrical effects, and physical design rules.

The main physical-design stages are:

1. Floorplanning
2. Power planning
3. Placement
4. Clock tree synthesis
5. Routing
6. Parasitic extraction
7. Timing analysis
8. Physical verification
9. Final layout generation

The exact order and naming of stages depend on the implementation flow.

## 18.1 Physical-Design Flow

```text
       Technology-Mapped Netlist
                   |
                   v
              Floorplanning
                   |
                   v
               Power Planning
                   |
                   v
                 Placement
                   |
                   v
          Clock Tree Synthesis
                   |
                   v
                  Routing
                   |
                   v
           Parasitic Extraction
                   |
                   v
             Timing Analysis
                   |
                   v
            Physical Verification
                   |
                   v
                Final GDS
```

## 18.2 Why Physical Design Matters

Even when the synthesized logic is functionally correct, the physical implementation may fail to meet timing or electrical requirements.

Wire length, parasitic capacitance, resistance, congestion, and clock distribution can affect the final circuit performance.

Physical design attempts to implement the circuit while satisfying the applicable design constraints.

---

# 📐 19. Floorplanning and Placement

## 19.1 Floorplanning

Floorplanning establishes the overall organization of the design within the available chip area.

Typical activities include:

- Defining the core and die dimensions
- Setting utilization targets
- Placing input/output pins
- Arranging macros, if present
- Reserving space for routing
- Establishing power-planning requirements

## 19.2 Core and Die

The **die** represents the complete physical chip area.

The **core** is the region where the main standard-cell logic is generally placed.

The core and die dimensions depend on the design requirements and implementation constraints.

## 19.3 Utilization

Utilization expresses the amount of area occupied by placed cells relative to a specified placement area.

A simplified expression is:

\[
\text{Utilization} =
\frac{\text{Total Cell Area}}{\text{Core Area}}
\times 100\%
\]

The exact definition used in a report depends on the tool and the reported metric.

High utilization can increase routing congestion. Very low utilization can increase the required core area. The appropriate target depends on the design.

## 19.4 Placement

Placement determines the physical locations of standard cells within the core.

Placement algorithms consider factors such as:

- Connectivity
- Timing requirements
- Congestion
- Cell density
- Estimated wire length
- Physical constraints

## 19.5 Global and Detailed Placement

**Global placement** establishes approximate cell locations and optimizes the overall arrangement.

**Detailed placement** legalizes cell positions and refines their locations to satisfy placement constraints.

## 19.6 Expected Outcome

After placement, the standard cells have physical locations. The implementation can then proceed to subsequent optimization and clock-distribution stages.

---

# 🕒 20. Clock Tree Synthesis

## 20.1 What Is Clock Tree Synthesis?

Clock tree synthesis (CTS) constructs a clock-distribution network that delivers the clock signal to sequential elements.

The clock network must distribute the clock while controlling skew, transition times, and other electrical constraints.

## 20.2 Why CTS Is Needed

A clock signal may drive many flip-flops across a chip.

Without a properly designed clock network, differences in wire length, load, and delay can cause clock-arrival times to vary across the design.

CTS inserts and organizes clock buffers or inverters as required by the implementation flow.

## 20.3 Clock Skew

Clock skew is the difference between clock arrival times at two relevant sequential elements.

A simplified expression is:

\[
\text{Clock Skew} =
T_{\text{capture}} - T_{\text{launch}}
\]

The interpretation of positive and negative skew depends on the selected sign convention and timing path.

Clock skew can influence both setup and hold timing.

## 20.4 Clock Latency

Clock latency is the time taken for a clock signal to travel from its defined reference point to a particular clock endpoint.

Timing reports may distinguish between source latency and network latency.

## 20.5 CTS Objectives

Typical CTS objectives include:

- Connecting the required clock sinks
- Controlling clock skew
- Meeting clock transition constraints
- Managing clock insertion delay
- Respecting electrical limits
- Supporting setup and hold timing closure

## 20.6 Post-CTS Analysis

After CTS, timing analysis must consider the implemented clock network and updated timing information.

The design may require additional setup or hold optimization after clock-tree insertion.

---

# ⏱️ 21. Static Timing Analysis

## 21.1 What Is Static Timing Analysis?

Static timing analysis (STA) evaluates timing paths in a digital design without requiring simulation of every possible input sequence.

STA uses the circuit's timing graph, cell timing models, interconnect information, clocks, and timing constraints to determine whether paths meet their required timing.

## 21.2 Common Timing Paths

### Register-to-Register Path

```text
Launch Flip-Flop
       |
       v
Combinational Logic
       |
       v
Capture Flip-Flop
```

### Input-to-Register Path

```text
Input Port
    |
    v
Combinational Logic
    |
    v
Capture Flip-Flop
```

### Register-to-Output Path

```text
Launch Flip-Flop
       |
       v
Combinational Logic
       |
       v
Output Port
```

STA analyzes relevant paths according to the constraints and analysis settings.

## 21.3 Clock Period

The clock period is the time between successive active edges of a periodic clock.

The corresponding clock frequency is:

\[
f = \frac{1}{T}
\]

where:

- \(f\) is the frequency.
- \(T\) is the clock period in seconds.

For example, a 10 ns clock period corresponds to:

\[
f = \frac{1}{10 \times 10^{-9}}
= 100\ \text{MHz}
\]

## 21.4 Slack

Slack measures the difference between the required timing and the actual or calculated arrival time, according to the analysis convention.

A simplified setup-slack expression is:

\[
\text{Setup Slack}
=
T_{\text{required}} - T_{\text{arrival}}
\]

Positive slack indicates that the path meets the calculated requirement. Negative slack indicates a timing violation under the analyzed conditions.

The complete calculation includes clock timing, setup constraints, uncertainty, and other applicable terms.

## 21.5 Worst Negative Slack (WNS)

WNS represents the worst slack among the analyzed paths for a particular timing check or report.

A negative WNS indicates that at least one analyzed path violates the timing requirement.

## 21.6 Total Negative Slack (TNS)

TNS summarizes negative slack across violating paths according to the reporting tool's definition.

It helps assess the aggregate extent of timing violations.

WNS identifies the worst violation, while TNS helps indicate the overall amount of negative slack.

## 21.7 Timing Constraints

Timing analysis commonly uses an SDC file to specify constraints such as:

- Clock definitions
- Clock uncertainty
- Input delays
- Output delays
- Input transition times
- Output loads
- Timing exceptions

Incorrect or incomplete constraints can make timing reports misleading.

---

# 🔍 22. Setup and Hold Timing

## 22.1 Setup Time

Setup time is the minimum interval for which the data input must remain stable before the active clock edge at a sequential element.

If the data arrives too late, the setup requirement may be violated.

## 22.2 Hold Time

Hold time is the minimum interval for which the data input must remain stable after the active clock edge.

If the data changes too soon after the clock edge, the hold requirement may be violated.

## 22.3 Setup Timing

Setup timing generally constrains the maximum delay of a data path.

A simplified setup relationship is:

\[
T_{\text{cq}} + T_{\text{data}} + T_{\text{setup}}
\leq T_{\text{period}}
\]

where:

- \(T_{\text{cq}}\) is the launch flip-flop clock-to-Q delay.
- \(T_{\text{data}}\) is the combinational data-path delay.
- \(T_{\text{setup}}\) is the capture flip-flop setup time.
- \(T_{\text{period}}\) is the available clock period.

This simplified relationship assumes idealized clock timing. Real timing analysis must account for skew, uncertainty, latency, and other constraints.

## 22.4 Hold Timing

Hold timing generally constrains the minimum delay of a data path.

A simplified relationship is:

\[
T_{\text{cq,min}} + T_{\text{data,min}}
\geq T_{\text{hold}}
\]

The complete hold check depends on the relative arrival times of the launch and capture clocks and other timing terms.

## 22.5 Setup Versus Hold

| Setup Timing | Hold Timing |
|---|---|
| Checks whether data arrives early enough before the capture edge | Checks whether data remains stable long enough after the capture edge |
| Related to maximum data-path delay | Related to minimum data-path delay |
| Can be improved by reducing excessive data-path delay | Can be improved by adding suitable delay to paths that are too fast |
| Often influenced by the clock period | Often influenced by clock skew and minimum path delay |

## 22.6 Common Remedies

**Setup violations** may be addressed through logic restructuring, cell resizing, buffering strategies, placement improvements, or other timing optimizations.

**Hold violations** may be addressed through delay insertion, buffering, or clock-tree and physical optimization.

Any repair must preserve functional correctness and satisfy the relevant implementation constraints.

---

# 🚀 23. Timing Closure and Optimization

## 23.1 What Is Timing Closure?

Timing closure is the process of adjusting the design and implementation until the required timing checks pass under the applicable constraints and corners.

Timing closure may require repeated optimization and timing-analysis iterations.

## 23.2 Common Timing Problems

- Excessive combinational logic depth
- High fanout
- Large net capacitance
- Long interconnects
- Poor cell placement
- Clock skew
- Setup violations
- Hold violations
- Routing congestion
- Incorrect timing constraints

## 23.3 Timing Optimization Techniques

Common techniques include:

1. Simplifying combinational logic.
2. Reducing unnecessary logic depth.
3. Selecting suitable cell drive strengths.
4. Improving placement.
5. Managing fanout and buffering.
6. Optimizing clock distribution.
7. Repairing hold violations.
8. Reviewing timing constraints.
9. Re-running STA after implementation changes.

## 23.4 Area and Timing Trade-Off

Area and timing objectives can conflict.

A larger or stronger cell may reduce delay but increase area and power. Logic restructuring may improve timing but increase the number of cells. The result depends on the design and library.

Optimization therefore considers the combined design objectives rather than a single metric.

## 23.5 Timing Reports

A timing report typically identifies:

- Startpoint
- Endpoint
- Clock information
- Cell delays
- Net delays
- Data arrival time
- Required arrival time
- Slack

Inspecting the critical paths helps determine which parts of the design require optimization.

---

# 🛣️ 24. Routing and TritonRoute

## 24.1 What Is Routing?

Routing creates the physical metal connections between the pins of placed cells and the required ports.

The routing solution must satisfy connectivity requirements while respecting manufacturing design rules and implementation constraints.

## 24.2 Global Routing

Global routing estimates routing paths and assigns connections to routing regions or resources.

It helps identify congestion and guides the detailed-routing stage.

## 24.3 Detailed Routing

Detailed routing determines the actual metal geometries and vias used to connect circuit elements.

The detailed-routing engine must respect the applicable routing layers, spacing rules, width rules, and other design constraints.

## 24.4 TritonRoute

TritonRoute is a detailed-routing engine used in the OpenROAD ecosystem.

It participates in the physical implementation flow by constructing detailed routes that connect the design's nets.

## 24.5 Routing Considerations

Routing can be affected by:

- Congestion
- Wire length
- Available routing layers
- Pin accessibility
- Via requirements
- Spacing constraints
- Antenna rules
- Signal integrity considerations

## 24.6 Why Routing Affects Timing

A routed connection has resistance and capacitance. These parasitic effects contribute to signal delay.

Consequently, a path that appears acceptable before routing may require further analysis and optimization after parasitic extraction.

## 24.7 Example Physical-Design Commands

The following commands are examples of commands that may appear in an OpenROAD-based flow:

```tcl
# Display the current design definition.
echo $::env(CURRENT_DEF)

# Generate or prepare the power distribution network.
gen_pdn

# Check the current design definition again.
echo $::env(CURRENT_DEF)

# Run detailed routing.
run_routing
```

**Important:** These commands are flow-dependent. Commands such as `gen_pdn` and `run_routing` may be wrappers provided by a particular flow rather than universal OpenROAD commands. Run them in the appropriate environment and verify that the corresponding procedures are defined.

---

# ✅ 25. Design Rule Checking

## 25.1 What Is Design Rule Checking?

Design rule checking (DRC) verifies whether a physical layout satisfies the applicable manufacturing geometry rules.

These rules are defined by the target process and its design-rule documentation.

## 25.2 Examples of Design Rules

DRC may check:

- Minimum metal width
- Minimum spacing between shapes
- Via geometry
- Enclosure requirements
- Minimum area
- Layer-specific constraints
- Other process-specific geometric requirements

The applicable checks depend on the process and verification setup.

## 25.3 Why DRC Matters

A layout can be logically correct while still violating physical manufacturing rules.

DRC helps identify such violations before the layout is considered ready for the next stage or for manufacturing sign-off.

## 25.4 DRC Versus LVS

| DRC | LVS |
|---|---|
| Checks layout geometry against design rules | Compares the extracted layout connectivity with the reference schematic or netlist |
| Focuses on physical rule compliance | Focuses on circuit correspondence |
| Identifies geometric rule violations | Identifies connectivity or device mismatches |

Passing DRC alone does not prove that the layout matches the intended circuit. Additional checks, including LVS and timing verification, may be required.

---

# 📊 26. OpenSTA and Post-Route Analysis

## 26.1 What Is OpenSTA?

OpenSTA is an open-source static timing analysis tool used to analyze timing in digital circuits.

It can read supported netlists, Liberty libraries, timing constraints, and parasitic information to perform timing calculations.

## 26.2 Common Inputs

A timing-analysis setup may include:

- Gate-level Verilog netlist
- Liberty timing libraries
- SDC timing constraints
- Parasitic information such as SPEF
- Operating-condition information
- Appropriate analysis settings

The required inputs depend on the stage and purpose of the analysis.

## 26.3 Example Timing-Analysis Commands

The following is an illustrative Tcl-style sequence. File paths and commands must be adjusted to the installed version and design environment.

```tcl
read_liberty path/to/standard_cell_library.lib
read_verilog path/to/design_netlist.v
link_design top_module
read_sdc path/to/design.sdc

report_checks
report_worst_slack
report_tns
```

If parasitic extraction has produced a supported SPEF file, the flow may also read the parasitic information before performing post-route analysis.

Consult the installed OpenSTA documentation for the exact command syntax supported by the version in use.

## 26.4 Pre-Route and Post-Route Timing

| Pre-Route Timing | Post-Route Timing |
|---|---|
| Uses estimated or partially available interconnect information | Uses extracted or more accurate routed interconnect information |
| Helps identify early timing problems | Evaluates timing with routed parasitic effects |
| Useful for guiding early optimization | Useful for implementation-stage timing assessment |
| May not capture final wire effects accurately | Better represents the implemented interconnect when extraction is accurate |

## 26.5 Post-Route Analysis

Post-route timing analysis helps determine whether the implemented design satisfies the timing constraints after accounting for the relevant cell and interconnect delays.

Any timing violations may require further physical optimization and re-analysis.

---

# 🔄 27. Complete RTL-to-GDS Flow

The RTL-to-GDS flow connects digital design specification to a physical layout.

## 27.1 Overall Flow

```text
                  DESIGN SPECIFICATION
                           |
                           v
                      RTL CODING
                           |
                           v
                   RTL FUNCTIONAL TEST
                           |
                           v
                    RTL SYNTHESIS
                           |
                           v
                   LOGIC OPTIMIZATION
                           |
                           v
                  TECHNOLOGY MAPPING
                           |
                           v
                   GATE-LEVEL NETLIST
                           |
                           v
                     FLOORPLANNING
                           |
                           v
                     POWER PLANNING
                           |
                           v
                       PLACEMENT
                           |
                           v
                 CLOCK TREE SYNTHESIS
                           |
                           v
                        ROUTING
                           |
                           v
                  PARASITIC EXTRACTION
                           |
                           v
                  POST-ROUTE TIMING
                           |
                           v
                PHYSICAL VERIFICATION
                           |
                           v
                       GDS OUTPUT
```

## 27.2 Stage Summary

| Stage | Main Purpose |
|---|---|
| RTL coding | Describe intended digital functionality |
| RTL verification | Check functionality through simulation and other verification methods |
| Synthesis | Transform RTL into a structural logic representation |
| Logic optimization | Simplify or restructure logic |
| Technology mapping | Map logic to cells in a target library |
| Floorplanning | Establish the overall physical organization |
| Power planning | Construct the power-distribution network |
| Placement | Assign physical locations to cells |
| Clock tree synthesis | Build the clock-distribution network |
| Routing | Create physical signal connections |
| Parasitic extraction | Estimate or extract interconnect electrical characteristics |
| Static timing analysis | Check timing constraints |
| Physical verification | Check applicable physical rules and connectivity |
| GDS generation | Produce the physical layout database |

## 27.3 From RTL to Hardware

The key idea is that RTL code is not itself the final physical circuit.

The implementation flow translates the RTL into logic, maps that logic to technology-specific cells, and then assigns physical locations and connections to those cells.

Each stage introduces additional implementation information and constraints.

## 27.4 Open-Source EDA Ecosystem

An open-source digital ASIC flow may combine tools such as:

- Icarus Verilog for simulation
- GTKWave for waveform viewing
- Yosys for synthesis
- ABC for logic optimization and mapping
- OpenROAD tools for physical implementation
- OpenSTA for timing analysis
- SKY130 for the process and standard-cell ecosystem
- Magic and other supported tools for layout-related tasks

The exact flow depends on the selected tools, PDK version, configuration, and target design.

---

# 💻 28. Practical Commands Reference

This section collects commonly used commands from the simulation and synthesis workflow.

## 28.1 Check Tool Availability

```bash
iverilog -V
vvp -V
gtkwave --version
yosys -V
```

The output depends on the installed versions.

## 28.2 Compile Verilog

```bash
iverilog -o mux_sim good_mux.v tb_good_mux.v
```

This compiles the Verilog source and testbench into a simulation executable.

## 28.3 Run the Simulation

```bash
vvp mux_sim
```

The simulation runs the compiled design and executes the testbench.

## 28.4 Open the Waveform

```bash
gtkwave tb_good_mux.vcd
```

This opens the generated VCD file in GTKWave.

## 28.5 Run Yosys

```bash
yosys
```

Within the Yosys prompt:

```tcl
read_verilog good_mux.v
hierarchy -top good_mux
proc
opt
check
synth -top good_mux
stat
show
write_verilog -noattr good_mux_netlist.v
```

These commands illustrate a basic synthesis and inspection sequence. Some operations may be repeated or performed internally by the `synth` command.

## 28.6 Read a Liberty Library

A technology-mapping flow may read a Liberty file, for example:

```tcl
read_liberty -lib path/to/sky130_standard_cell_library.lib
```

The path and exact library filename must match the installed PDK.

## 28.7 Technology Mapping

The exact mapping sequence depends on the target technology and synthesis script.

A Yosys flow may use commands such as `dfflibmap` and `abc` to map sequential and combinational logic to cells in the selected library.

An illustrative sequence is:

```tcl
read_verilog good_mux.v
hierarchy -top good_mux
synth -top good_mux
dfflibmap -liberty path/to/standard_cell_library.lib
abc -liberty path/to/standard_cell_library.lib
clean
stat
write_verilog -noattr mapped_netlist.v
```

**Note:** This is an illustrative sequence, not a universal technology-mapping script. A production flow must use a compatible library, appropriate mapping options, and the correct synthesis order for the installed tool version.

## 28.8 Useful Debugging Checks

When a command fails:

1. Check whether the tool is installed.
2. Confirm the current working directory.
3. Verify source-file names and paths.
4. Check the top-module name.
5. Read the complete error message.
6. Confirm the required library files are available.
7. Check that the command is supported by the installed tool version.
8. Review the synthesis or simulation log.

---

# 🎓 29. Learning Outcomes

Through the practical work and accompanying study notes, the following concepts are covered.

## 29.1 RTL Design

- Understanding hardware description using Verilog.
- Describing combinational logic.
- Understanding multiplexers and selection logic.
- Writing testbenches for functional verification.
- Understanding procedural and continuous assignments.

## 29.2 Simulation and Verification

- Compiling and running Verilog simulations.
- Generating VCD waveform files.
- Inspecting signal transitions in GTKWave.
- Comparing expected behavior with simulation results.
- Understanding the purpose of gate-level simulation.

## 29.3 Synthesis and Technology Mapping

- Understanding the role of Yosys.
- Understanding logic optimization using ABC.
- Converting RTL into a netlist.
- Exploring standard-cell library information.
- Understanding technology mapping.
- Learning why different cell variants may be selected.

## 29.4 Sequential Logic

- Understanding flip-flops and register behavior.
- Distinguishing synchronous and asynchronous resets.
- Using non-blocking assignments in clocked logic.
- Recognizing coding patterns that can infer latches.
- Understanding sequential optimization concepts.

## 29.5 Timing Analysis

- Understanding clock period and frequency.
- Learning setup and hold timing.
- Understanding timing slack.
- Recognizing the importance of critical paths.
- Understanding the relationship between cell delay and interconnect delay.
- Learning why timing must be checked at appropriate implementation stages.

## 29.6 Physical Design

- Understanding floorplanning and placement.
- Learning the purpose of clock tree synthesis.
- Understanding global and detailed routing.
- Learning the purpose of vias and metal layers.
- Understanding design rule checking.
- Exploring the role of parasitic extraction and post-route timing analysis.

## 29.7 Overall Perspective

The central learning outcome is an understanding of how several stages of the digital design process work together.

RTL describes the intended hardware behavior. Simulation checks the behavior of that description. Synthesis transforms the design into a logic implementation. Technology mapping connects the logic to a target standard-cell library. Physical design then places and routes the cells, after which timing and physical checks help evaluate the implementation.

---

# 🔑 30. Conclusion

The Digital VLSI Laboratory provides a structured foundation for understanding the transition from Verilog RTL to synthesized digital logic.

The initial practical work on a 2:1 multiplexer demonstrates how a simple digital function can be described, simulated, and inspected using open-source tools. The Yosys synthesis lab extends that understanding by showing how RTL can be transformed into a technology-mapped netlist using ABC and the SKY130 standard-cell library.

The accompanying learning notes broaden this foundation to cover sequential logic, reset behavior, coding styles, synthesis optimization, gate-level simulation, timing libraries, PVT corners, setup and hold timing, clock tree synthesis, routing, and physical verification.

Together, these topics provide a connected view of digital hardware implementation—from describing a circuit in RTL to understanding the logical and physical considerations involved in producing an integrated-circuit layout.

This repository serves as a record of my practical work, technical learning, and continued exploration of open-source digital VLSI design tools.

---

# 📚 31. References and Resources

## Repository

- **VLSI_LAB — Main GitHub Repository:** [https://github.com/DevasreeSruthi/VLSI_LAB](https://github.com/DevasreeSruthi/VLSI_LAB)
- **Lab 01 — 2:1 Multiplexer:** [Lab-01-2x1-Multiplexer](https://github.com/DevasreeSruthi/VLSI_LAB/tree/main/Lab-01-2x1-Multiplexer)
- **Lab 02 — Yosys MUX Synthesis:** [Lab-02-YOSYS-mux](https://github.com/DevasreeSruthi/VLSI_LAB/tree/main/Lab-02-YOSYS-mux)
- **Module 2 — Timing Libraries, Hierarchical vs. Flat Synthesis, and Flip-Flop Coding:** See the corresponding Module 2 folder in the repository.

## Open-Source EDA Tools

- [Icarus Verilog](https://steveicarus.github.io/iverilog/)
- [GTKWave](https://gtkwave.sourceforge.net/)
- [Yosys Open SYnthesis Suite](https://yosyshq.readthedocs.io/)
- [ABC Logic Synthesis and Verification](https://people.eecs.berkeley.edu/~alanmi/abc/)
- [OpenLane](https://openlane2.readthedocs.io/)
- [OpenSTA](https://github.com/The-OpenROAD-Project/OpenSTA)
- [OpenROAD Project](https://openroad.readthedocs.io/)
- [SKY130 PDK](https://skywater-pdk.readthedocs.io/)
- [Magic VLSI Layout Tool](http://opencircuitdesign.com/magic/)
- [NGSpice](https://ngspice.sourceforge.io/)

---


