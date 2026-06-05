# VSD-TCL-WORKSHOP
VSD TCL COURSE
# TCL Scripting for VLSI System Design (VSD) Workshop

## Overview

This repository documents my learning journey through the **TCL Scripting for VLSI System Design (VSD) Workshop**, where I explored the use of TCL scripting for automating various stages of the digital VLSI synthesis flow.

The workshop focused on developing a TCL-based synthesis framework capable of automating design validation, constraint generation, hierarchy checking, and RTL synthesis using open-source EDA tools such as **Yosys**.
## What is TCL?

TCL (Tool Command Language) is a high-level scripting language widely used in Electronic Design Automation (EDA) tools for process automation, tool integration, report generation, constraint handling, and design flow development. It provides a simple yet powerful interface for automating repetitive tasks and building customized design workflows.

In VLSI design environments, TCL is extensively used in tools such as synthesis, static timing analysis, place-and-route, formal verification, and simulation platforms. Its flexibility makes it an ideal choice for creating reusable automation frameworks and improving productivity in digital design flows.

---
## Workshop Agenda

| Day | Topics Covered |
|------|----------------|
| Day 1 | Creating a TCL command and passing a CSV file from UNIX shell to a TCL script |
| Day 2 | Variable creation and processing constraints from CSV |
| Day 3 | Processing clock and input constraints |
| Day 4 | Complete scripting and Yosys synthesis |
| Day 5 | Advanced scripting techniques and Quality of Results (QoR) generation |

---
## Project Workflow

```text
RTL Netlists + CSV Constraints
│
▼
Design Validation
│
▼
CSV Processing
│
▼
SDC Generation
│
▼
Hierarchy Verification
│
▼
Yosys Script Generation
│
▼
RTL Synthesis
│
▼
Gate-Level Netlist & Reports
```

---

## Technologies Used

| Tool | Purpose |
|--------|---------|
| TCL | Automation scripting |
| Yosys | RTL synthesis |
| OpenTimer | Timing analysis |
| Verilog HDL | RTL design |
| CSV Package | Constraint processing |
| Struct::Matrix | Matrix handling |

---
### Project Highlights

The final TCL-based synthesis framework (**vsdsynth**) is capable of:

- Reading RTL netlists and design constraints
- Validating design files and directory structures
- Parsing CSV-based constraint files
- Automatically generating SDC constraints
- Performing RTL hierarchy verification
- Handling synthesis errors gracefully
- Generating Yosys synthesis scripts
- Producing synthesized gate-level netlists
- Generating synthesis and timing reports

---

## Table of Contents

- [Overview](#overview)
- [What is TCL?](#what-is-tcl)
- [Workshop Agenda](#workshop-agenda)
- [Day 1 – Introduction to TCL-Based Synthesis Flow](#day-1--introduction-to-tcl-based-synthesis-flow)
- [Day 2 – TCL Variables, Arrays and CSV Parsing](#day-2--tcl-variables-arrays-and-csv-parsing)
- [Day 3 – Constraint Processing and SDC Generation](#day-3--constraint-processing-and-sdc-generation)
- [Day 4 – RTL Synthesis Using Yosys](#day-4--rtl-synthesis-using-yosys)
- [Day 5 – Hierarchy Checking and Error Handling](#day-5--hierarchy-checking-and-error-handling)
- [Conclusion](#conclusion)
- [Acknowledgements](#acknowledgements)

---
# Day 1 – Introduction to TCL-Based Synthesis Flow

## Objectives

- Understand the VSD synthesis framework
- Execute shell scripts in Linux
- Learn the overall RTL synthesis flow
- Validate user inputs before synthesis

## Making Scripts Executable

```bash
chmod +x vsdsynth
```

This command grants execution permissions to the synthesis script.

## Running the Script

```bash
./vsdsynth
```

This launches the TCL-based synthesis environment.

## Understanding the Synthesis Flow

The synthesis framework:

1. Accepts RTL netlists and SDC constraints.
2. Processes design and timing requirements.
3. Uses Yosys as the synthesis engine.
4. Generates:
   - Synthesized gate-level netlists
   - Timing reports
   - Output directories
   - Log files

## Error Handling for Missing Inputs

Before execution, the framework validates the availability of:

- CSV constraint files
- RTL source files
- Standard cell libraries
- Output directories

This prevents failures during later stages of synthesis.

### Key Learnings

- Linux file permissions
- Shell script execution
- Synthesis flow fundamentals
- User input validation
- Automation workflow basics

### Screenshots

<img width="940" height="324" alt="image" src="https://github.com/user-attachments/assets/f581fc43-c558-41a7-8319-48a94518230e" />

<img width="940" height="664" alt="image" src="https://github.com/user-attachments/assets/b5ebd8c6-190e-42f9-9701-2643fd217a2d" />

<img width="940" height="323" alt="image" src="https://github.com/user-attachments/assets/46a854dc-f233-4341-830b-ea82388d35bf" />

<img width="940" height="323" alt="image" src="https://github.com/user-attachments/assets/2501eb13-4af6-40cf-9e89-c73da41656fe" />
<img width="940" height="300" alt="image" src="https://github.com/user-attachments/assets/ab7989fd-019c-43c4-9f91-b740eb8748e9" />
<img width="940" height="572" alt="image" src="https://github.com/user-attachments/assets/b6b0455b-9304-4f56-a015-a8b33d292077" />

---

# Day 2 – TCL Variables, Arrays and CSV Parsing

## Objectives

- Understand TCL variables and arrays
- Process command-line arguments
- Read and parse CSV files
- Perform matrix operations

## Reading Command-Line Arguments

```tcl
set filename [lindex $argv 0]
```

TCL stores command-line arguments inside `$argv`.

| Index | Description |
|---------|------------|
| argv[0] | First argument |
| argv[1] | Second argument |
| argv[2] | Third argument |

## Reading CSV Files

```tcl
package require csv
package require struct::matrix

struct::matrix m

set f [open $filename]
csv::read2matrix $f m auto
close $f
```

This loads CSV data into a matrix structure.

## Converting Matrix to Array

```tcl
m link my_arr
```

This allows matrix elements to be accessed using array notation.

## String Manipulation

### Removing Spaces

```tcl
string map {" " ""} $value
```

### Replacing Strings

```tcl
string map {_ghosh _vsd} kunal_ghosh
```

Output:

```text
kunal_vsd
```

## Dynamic Variable Creation

```tcl
set DesignName $my_arr(1,0)

puts $DesignName
```

Output:

```text
openMSP430
```

## File and Directory Validation

The script verifies:

- Output directory existence
- RTL netlist directory
- Library files
- Constraint files

before starting synthesis.

### Key Learnings

- TCL variable declaration
- Arrays and matrices
- CSV parsing techniques
- Dynamic variable creation
- Path and file validation

### Screenshots

<img width="940" height="468" alt="image" src="https://github.com/user-attachments/assets/9e5bde17-a751-4238-a83c-5b95f02cf8be" />

<img width="940" height="474" alt="image" src="https://github.com/user-attachments/assets/36164971-1f9a-48ca-8376-6743556d808c" />
<img width="940" height="505" alt="image" src="https://github.com/user-attachments/assets/0e09d3db-90c1-4275-af65-2c43634d6859" />
<img width="940" height="494" alt="image" src="https://github.com/user-attachments/assets/1698d992-4ed0-4c2b-a7d6-d57954e53c18" />

---

# Day 3 – Constraint Processing and SDC Generation

## Objectives

- Convert CSV constraints into SDC format
- Search and extract timing parameters
- Generate timing constraints automatically

## Creating the Constraint Matrix

```tcl
struct::matrix constraints

set chan [open $ConstraintsFile]
csv::read2matrix $chan constraints auto
close $chan
```

## Searching Constraint Parameters

```tcl
constraints search rect 0 0 10 3 early_rise_delay
```

This searches the matrix and returns the location of the specified parameter.

## Reading Constraint Values

```tcl
constraints get cell $clock_early_rise_delay_start $i
```

Used to retrieve timing values from the matrix.

## Automatic SDC Generation

Generated example:

```tcl
set_clock_latency -source -early -rise 150 [get_clocks dco_clk]

set_clock_latency -source -late -fall 153 [get_clocks dco_clk]
```

## Clock Creation

```tcl
create_clock \
-name dco_clk \
-period 1500 \
-waveform {0 750} \
[get_ports dco_clk]
```

### Duty Cycle Calculation

For:

- Period = 1500 ps
- Duty Cycle = 50%

Generated waveform:

```tcl
{0 750}
```

## Input Port Processing

The framework automatically identifies:

- Scalar inputs
- Bus inputs

Example:

```verilog
input [6:0] dbg_i2c_addr;
```

Converted to:

```text
dbg_i2c_addr*
```

for wildcard matching.

## Verilog Parsing

```tcl
glob -dir $NetlistDirectory *.v
```

The parser:

- Finds Verilog files
- Reads source code line-by-line
- Extracts input declarations
- Generates corresponding SDC constraints

## String Cleanup

```tcl
regsub -all {\s+} $s1 ""
```

Removes all whitespace characters.

### Key Learnings

- Constraint matrix searching
- Automatic SDC generation
- Clock modeling
- Bus handling
- Verilog parsing using TCL

### Screenshots

<img width="940" height="466" alt="image" src="https://github.com/user-attachments/assets/0ec30ee8-3f9f-4b43-90aa-d8d9d4e1893d" />

<img width="940" height="408" alt="image" src="https://github.com/user-attachments/assets/b02ab289-6005-410d-9deb-c316a6f8943c" />

---

# Day 4 – RTL Synthesis Using Yosys

## Objectives

- Perform RTL synthesis
- Generate gate-level netlists
- Understand synthesis optimization techniques

## Example RTL Design

```verilog
module memory(
    CLK,
    ADDR,
    DIN,
    DOUT
);
```

## Yosys Synthesis Script

```tcl
read_liberty osu018_stdcells.lib

read_verilog memory.v

synth -top memory

dfflibmap -liberty osu018_stdcells.lib

abc -liberty osu018_stdcells.lib

flatten

clean

write_verilog memory_synth.v
```

## Running Yosys

```bash
yosys memory.ys
```

## Generated Output

The RTL design is mapped into standard cells such as:

- NAND gates
- NOR gates
- AOI gates
- OAI gates
- Flip-flops

## Logic Optimizations Performed

Yosys automatically performs:

- Constant propagation
- Dead code elimination
- Logic simplification
- Technology mapping

### Key Learnings

- RTL synthesis flow
- Standard-cell mapping
- Gate-level netlist generation
- Logic optimization techniques

### Screenshots

<img width="895" height="644" alt="image" src="https://github.com/user-attachments/assets/8cf412f3-5b8f-4a2f-86dd-5e58ab37a311" />

<img width="940" height="411" alt="image" src="https://github.com/user-attachments/assets/97996bac-babc-48d3-9758-42cfaa03a5f7" />
<img width="940" height="874" alt="image" src="https://github.com/user-attachments/assets/0a46084b-309e-4d2c-8ed4-748d27da7a4b" />
<img width="940" height="500" alt="image" src="https://github.com/user-attachments/assets/e80ed080-cd39-42bf-984f-a7a8f486ba49" />
<img width="940" height="947" alt="image" src="https://github.com/user-attachments/assets/c5a8b917-ce81-46d9-9cc6-8ef1c6e73a94" />
<img width="940" height="486" alt="image" src="https://github.com/user-attachments/assets/d73966a4-0419-4aab-bb55-aa04cf46308a" />
<img width="940" height="433" alt="image" src="https://github.com/user-attachments/assets/7941ac8f-3031-4fa1-8fb7-6afe43c82521" />
<img width="940" height="227" alt="image" src="https://github.com/user-attachments/assets/70ffe9ac-714d-456f-86f8-d015b8136552" />
<img width="940" height="505" alt="image" src="https://github.com/user-attachments/assets/8dda11e1-633e-43b6-a650-f815769b7af2" />
<img width="940" height="557" alt="image" src="https://github.com/user-attachments/assets/32145103-1957-42c5-94ca-c257109d0088" />

<img width="940" height="174" alt="image" src="https://github.com/user-attachments/assets/e33b1aa1-8bd2-4bbd-8926-3c71502880e1" />

---

# Day 5 – Hierarchy Checking and Error Handling

## Objectives

- Verify RTL hierarchy correctness
- Detect missing modules
- Improve synthesis robustness

## Why Hierarchy Checking?

Consider:

```verilog
module top();

alu u1();

memory u2();

endmodule
```

Before synthesis, the framework verifies:

- Does `alu` exist?
- Does `memory` exist?
- Are all referenced modules available?
- Is the hierarchy complete?

## Error Handling

Without proper error handling:

- Scripts may crash unexpectedly
- Logs become difficult to debug
- Partial outputs may be generated

## Running Shell Commands from TCL

```tcl
exec yosys $OutputDirectory/$DesignName.hier.ys
```

## Redirecting Logs

```tcl
>&
```

Used to redirect output into log files.

## Hierarchy Verification Results

### PASS

```text
err flag = 0
```

All modules were found successfully.

### FAIL

```text
err flag = 1
```

One or more modules are missing.

## Benefits of Hierarchy Verification

- Faster debugging
- Early failure detection
- Cleaner synthesis flow
- Improved automation reliability

### Key Learnings

- Hierarchy validation
- Error handling strategies
- TCL `exec` command
- Log generation and analysis
- Robust automation practices

### Screenshots

<img width="1093" height="289" alt="image" src="https://github.com/user-attachments/assets/3fd50130-9d3b-4603-85b3-aa101ccb52a3" />
<img width="1093" height="634" alt="image" src="https://github.com/user-attachments/assets/dce22a2b-d7d6-4d7e-adcb-2e9e4bcc7297" />
<img width="1093" height="366" alt="image" src="https://github.com/user-attachments/assets/16b773cc-6604-4287-a85d-f593c4025f1d" />
<img width="831" height="322" alt="image" src="https://github.com/user-attachments/assets/af13247d-9531-4fc0-bf53-f7b4df9df8ea" />
<img width="1093" height="293" alt="image" src="https://github.com/user-attachments/assets/e305e38e-73e2-4543-a986-7cb4696f1af8" />
<img width="1093" height="204" alt="image" src="https://github.com/user-attachments/assets/29b1bdb5-48f2-4d46-b2dc-18b6015328a3" />
<img width="919" height="311" alt="image" src="https://github.com/user-attachments/assets/eebdc91b-eeef-404d-8412-af0740c50061" />
<img width="1093" height="113" alt="image" src="https://github.com/user-attachments/assets/8a31fc7f-53ff-4f77-a5b4-622d834a7bf1" />
<img width="949" height="1117" alt="image" src="https://github.com/user-attachments/assets/e691223f-edaf-4738-8043-79fce8b5735e" />
<img width="1093" height="389" alt="image" src="https://github.com/user-attachments/assets/504dee83-2acc-41b7-a2a7-b0131f31702c" />

---

# Conclusion

Over the course of this five-day workshop, I developed a strong understanding of TCL scripting for EDA automation and digital VLSI design flows.

The major concepts covered include:

- TCL fundamentals and scripting
- CSV parsing and matrix operations
- Automatic SDC generation
- Verilog netlist parsing
- RTL synthesis automation using Yosys
- Gate-level netlist generation
- Hierarchy verification and error handling

This project demonstrates how TCL can be used to build a complete automation framework for RTL synthesis and timing constraint generation in modern VLSI design environments.

---

# Acknowledgements

- VLSI System Design (VSD)
- Yosys Open Source Synthesis Suite
- TCL/Tk Community
- OpenMSP430 Design Example
- VSD Workshop on TCL Scripting for VLSI Design Automation

---

# Repository Information

## Technologies Used

- TCL
- Shell Scripting
- Verilog HDL
- Yosys
- OpenTimer

## Language Distribution

| Language | Percentage |
|-----------|-----------|
| TCL | 86.6% |
| Shell | 11.9% |
| Verilog | 1.5% |

---

## Author

**Gowri Nandana**

*TCL Scripting for VLSI System Design using Open-Source EDA Tools*
