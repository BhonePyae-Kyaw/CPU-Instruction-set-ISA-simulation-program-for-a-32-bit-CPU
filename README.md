# 🚀 Simple ISA Simulator

A simple CPU **Instruction Set Architecture (ISA)** simulator written in **Python**. This project demonstrates how a basic instruction set can be implemented and executed, including register operations, arithmetic processing, and cycle counting.

---

## 📚 Table of Contents
- [Overview](#overview)
- [ISA Specifications](#isa-specifications)
- [Instruction Format](#instruction-format)
- [Supported Instructions](#supported-instructions)
- [Cycle Timing](#cycle-timing)
- [Usage](#usage)
- [Test Cases](#test-cases)
- [Performance Metrics](#performance-metrics)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)

---

## 📖 Overview

This project simulates a **32-bit ISA** that supports:
- 8 General Purpose Registers (`r0` - `r7`)
- 5 Arithmetic and Move instructions (`mov`, `add`, `sub`, `mul`, `div`)
- Cycle counting and CPI (Cycles Per Instruction) calculations

The ISA simulator parses instructions, encodes them into binary, executes them, and outputs the final state of the registers along with performance metrics.

---

## 🏗️ ISA Specifications

| Field         | Size (bits) |
|---------------|-------------|
| **Opcode**    | 5           |
| **Target Reg**| 3           |
| **Source Reg**| 3           |
| **Immediate** | 21          |
| **Total**     | 32 bits     |

### General Purpose Registers (GPRs)
| Name | Binary |
|------|--------|
| r0   | `000`  |
| r1   | `001`  |
| r2   | `010`  |
| r3   | `011`  |
| r4   | `100`  |
| r5   | `101`  |
| r6   | `110`  |
| r7   | `111`  |

---

## 📝 Instruction Format

Each instruction follows this format:
```
<opcode> <target_register> <source_register_or_immediate>
```

### Example
```
mov r1 25
add r2 r1
```

---

## 🛠️ Supported Instructions

| Instruction | Opcode | Description                    | Cycles |
|-------------|--------|--------------------------------|--------|
| `mov`       | `00000`| Move immediate or register     | 1      |
| `add`       | `00001`| Add immediate or register      | 1      |
| `sub`       | `00010`| Subtract immediate or register | 1      |
| `mul`       | `00011`| Multiply immediate or register | 4      |
| `div`       | `00100`| Divide immediate or register   | 6      |

---

## ⏱️ Cycle Timing

- Simple operations like `mov`, `add`, `sub` complete in **1 cycle**
- More complex operations `mul` and `div` require **4 and 6 cycles**, respectively
- Division-by-zero is detected and the instruction is **skipped**, with a warning message

---

## 🚀 Usage

### Prerequisites
- Python 3.x installed

### Run the Program
```bash
python isa_simulator.py
```

### Example Instruction Set
```python
instructions = [
    "mov r1 25",
    "mov r2 20",
    "sub r2 r1",
    "mov r3 12",
    "mul r2 r3",
    "mov r4 r2",
    "div r4 8",
    "end 0 0"
]
```

### Expected Output
```
 PC  | Instruction      | Binary Encoded Instruction         |    Cycles
----------------------------------------------------------------------------
   0 | mov r1 25        | 00000 001 000 000000000011001     |      1
   1 | mov r2 20        | 00000 010 000 000000000010100     |      1
   2 | sub r2 r1        | 00010 010 001 000000000000000     |      1
   ...
----------------------------------------------------------------------------
Execution Completed!

Total Cycle counts after executing all the instructions = 15
Total Instruction counts = 7
CPI = 2.14

After executing instructions, each register contains -
 Reg | Value           | Binary (32-bit)
----------------------------------------------------------------------------
  r0 | 0               | 00000000000000000000000000000000
  r1 | 25              | 00000000000000000000000000011001
  r2 | -60             | 11111111111111111111111111000100
  r3 | 12              | 00000000000000000000000000001100
  r4 | -8              | 11111111111111111111111111111000
  ...
```

---

## ✅ Test Cases

### Test Case 1: Basic Arithmetic
```python
[
    "mov r1 10",
    "add r1 5",
    "sub r1 3",
    "mov r2 r1",
    "add r2 r2",
    "end 0 0"
]
```

### Test Case 2: Division by Zero
```python
[
    "mov r1 10",
    "mov r2 0",
    "div r1 r2",
    "div r1 0",
    "end 0 0"
]
```

### Test Case 3: Large Immediate Values
```python
[
    "mov r1 1048575",     # max positive 21-bit immediate
    "mov r2 -1048576",    # min negative 21-bit immediate
    "add r1 r2",
    "end 0 0"
]
```

For more, see `/tests/`.

---

## 📊 Performance Metrics Example

- **Total Cycles**: 15  
- **Instructions Executed**: 7  
- **CPI (Cycles Per Instruction)**: 2.14  

---

## 🔮 Future Improvements

- **Branch and Jump Instructions** (`jmp`, `beq`, `bne`)
- **Load/Store Operations** (simulate memory access)
- **Pipeline Simulation** (introduce stages: Fetch, Decode, Execute, etc.)
- **Hazard Detection and Resolution**
- **Interrupt Handling**

---

## 🤝 Contributing

Contributions are welcome!  
Feel free to fork the repo, submit pull requests, or open issues.

### How to Contribute
1. Fork this repository
2. Create a new branch (`git checkout -b feature-branch`)
3. Commit your changes (`git commit -m 'Added new feature'`)
4. Push to the branch (`git push origin feature-branch`)
5. Open a pull request

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements
This project was built for educational purposes to demonstrate a simplified CPU and ISA concept in Python.
