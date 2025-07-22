## Introduction

### What is SASM / ArgSfx?

**SASM** is a cross-assembler created by **Argonaut Software** for internal development of games targeting the **65C816** processor and the **Super FX** coprocessor (known by its codename "MARIO" (**M**athematical, **A**rgonaut, **R**otation, **I**nput, **O**utput)). Originally used to develop *Star Fox*.

**ArgSfx** ("ArgAsm - Super FX") is the direct successor to SASM, created during the development of *Star Fox 2*. It improves upon SASM in several ways: new directives, automatic heap allocation, better string definition and handling, and stricter parsing. ArgSfx retains compatibility with most SASM functionality with some slight differences in behavior.

> **Note:** This manual documents **ArgSfx v1.52**, with notes where behavior differs from SASM v2.02. Almost all information from the original SASM documentation (SASM.DOC) still applies unless explicitly stated otherwise.

---

### Supported Architectures

ArgSfx supports two CPU modes:

- **65C816**: The extended 16-bit version of the 6502 used as the core of the Ricoh 5A22, the SNES CPU.
- **Super FX ("MARIO")**: A RISC coprocessor used in certain SNES games (e.g. *Star Fox*) for 3D rendering and math acceleration.

You can switch parsing modes using the `MARIO ON` / `OFF` directive or by defining the `__mario` symbol on the command line.

---

### Core Features

- Powerful macro system with named arguments and string-based substitution
- Full-featured conditional assembly with expression evaluation
- `PRINTF` support for printing messages, expressions, or formatted output to files or the terminal
- Support for special user-defined strings
- EMS memory support up to 16MB using ZPM DOS/16M extender
- Automatic branch range expansion
- Integrated linker support (`PUBLIC`, `EXTERN`, and `.SOB` object files)
- Symbol export and listing control
- Fully scriptable preprocessing using strings, macros, and directives

---

### Version Notes

| Assembler/Linker Versions           | Assembler/Linker Executable Names | Description                                                                                                              |
| ----------------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| SASMX v2.02, SL v1.01               | `SASMX.EXE`, `SL.EXE`             | Final documented release of the original assembler, used for *Star Fox*. Requires manual heap definition.                |
| **ArgSfx v1.52**, **ArgLink v1.11** | `ARGSFXX.EXE`, `ARGLINK.EXE`      | Improved fork by Argonaut, used for *Star Fox 2*. Adds directives, automates heap allocation, and uses stricter parsing. |

---

Next: Setup and Usage.
