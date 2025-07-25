## Chapter 2: Setup & Usage

### System Requirements

ArgSfx is a DOS-based 16-bit cross-assembler that runs best under the following environments:

- Real MS-DOS 5.0 or later
- DOSBox, DOSBox-X or an equivalent emulation solution (for modern platforms)
- A 286 or better CPU
- EMS (Expanded Memory Specification) driver for accessing memory beyond 640KB, full 16MB of memory recommended

> **Note:** ArgSfx does *not* require manual heap configuration. Unlike SASM, it automatically allocates heap memory on startup.

---

### Getting Started

To assemble a source file:

```batch
argsfxx mycode.asm
```

This will process `mycode.asm` and output relevant logs or errors. Output files and behaviors can be customized with command-line options and assembler directives.

---

### Example Directory Layout

While not enforced, a tidy project layout helps with macro and include organization:

```
project/
├── asm/        # Main .ASM files
├── inc/        # Include files (macros, constants)
├── mario/      # .MC Super FX ("MARIO") source files
└── build/      # Output binaries
```

Use `INCDIR` or the `-i` flag to point ArgSfx to your include directory, or simply add the directory path as a prefix to the `INCLUDE` filename parameter, if you are running ArgSfx within the main project directory.

(e.g. `INCLUDE INC\MACROS.INC`)

---

### SASM Environment Variables

These optional environment variables control aspects of SASM:

| Variable   | Description                                      |
| ---------- | ------------------------------------------------ |
| `SASMDIR`  | Default path to prepend to includes and binaries |
| `SASMSRC`  | Default source filename (if none is given)       |
| `SASMHEAP` | Heap size in bytes                               |

Set these in your `AUTOEXEC.BAT` or before launching SASM.

This is not required if you have already changed to your main source directory.

```batch
SET SASMDIR=C:\path-to-your-project\
```

---

### Command-Line Options

Here are commonly used CLI flags:

| Flag           | Description                                                         |
| -------------- | ------------------------------------------------------------------- |
| `-x[filename]` | Enable symbol listing, excluding ROM symbols (optionally to a file) |
| `-eSYMBOL=VAL` | Define a symbol (`EQU`)                                             |
| `-sSYMBOL=VAL` | Set a symbol (`=`)                                                  |
| `-vfile.SOB`   | Output a linkable object file                                       |
| `-e__heap=VAL` | Define heap for SASM                                                |
| `-e__notitle`  | Suppress title banner                                               |

Full CLI options are covered in the Appendix.

---

### File Types

ArgSfx works with several file types:

- `.ASM` - Source code files
- `.MC` - Super FX ("MARIO Chip") source code files - MARIO instruction parsing must be activated manually
- `.SOB` - (SASM OBject) Linkable object files (used with the `SL.EXE` or `ARGLINK.EXE` linkers)
- `.BIN` - Binary data
- `.INC` - Included constants, macros, and data
- `.EXT` - Included externs/publics
- `.COL`, `.CGX`, `.SCR` - SNES asset files generated by Nintendo's Super CG-CAD/SCAD graphics software
- `.COL` - (COLor) S-CG-CAD color palette data
- `.CGX` - (Character Graphics) S-CG-CAD tileset data
- `.SCR` - (SCReen) S-CG-CAD tilemap data
- `.PAL` - (PALette) Generic color palette data
- `.CHR` - (CHaRacter) Generic tileset data
- `.PIC` - (PICture) Generic tilemap data

Use `INCBIN` to include binary files. For `.COL` files, use `INCCOL <file,start,end>`.

---

### Output and Logging

ArgSfx can print messages to the console or to files using the `PRINTF`, `FOPEN`, and `FCLOSE` directives.

You can suppress or re-enable categories of output with ``SUPPRESS`` and `RELEASE` (See Chapter 6, "Environment-Sensitive Output"). 

By default, when an output file is specified, object code is written immediately unless disabled with `WRITE OFF`.

---

Next: Syntax and directives.
