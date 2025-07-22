## Chapter 3: Syntax and Directive Reference

### Source Format and Syntax Rules

ArgSfx source files follow a format similar to traditional 65xx assemblers, with stricter indentation and stricter parsing (if using ArgSfx).

- **Labels and constants must start at column 1** with no leading spaces or tabs. **Labels must not begin with numbers.**
- **Instructions, directives, parameters, and macro invocations must be indented** with at least one tab or space. (Tabs are recommended.) Comma-separated lists of parameters for macros should not contain any whitespace.
- **Macro names in definitions** follow the same indentation and naming rules as labels.
- **Comments** can begin with either a semicolon (`;`) or an asterisk (`*`). For modern conventions, semicolons are preferred.
- **Line endings must be DOS/Windows CRLF.** Files with Unix (LF) or Classic Mac (CR) line endings will fail to assemble. Ensure that your editor has been configured to use the correct line ending scheme.

Example:

```asm6502
my_label
    bra    .my_sublabel
.my_sublabel
    rts

my_macro    MACRO    [param1,param2]
    lda    #{param1}
    sta    #{param2}
    ENDM

    my_macro    param1,param2

my_equate    equ    $01
my_variable    = 1
_123    equ    $20

; this is a comment
* this is also a comment
```

---

### Directives Overview

ArgSfx supports a wide set of directives that control assembly behavior, conditional logic, file output, macro processing, and more.

All directives must be indented, and arguments must follow proper syntax. Common directives include:

| Directive                  | Description                                          |
| -------------------------- | ---------------------------------------------------- |
| `ORG`                      | Sets bank address and/or ROM location                |
| `EQU` / `=`                | Defines constant / variable                          |
| `MACRO`                    | Begins macro definition (use `ENDM` to close)        |
| `REPT` / `ENDR`            | Repeat block of code                                 |
| `IRP` / `IRS`              | Iterate over values or strings within a `REPT` block |
| `IFxx` / `ELSEIF` / `ENDC` | Conditional logic using expression or symbol state   |
| `INCLUDE`                  | Includes a source file                               |
| `INCBIN` / `INCCOL`        | Includes raw binary or `.COL` palette data           |
| `PUBLIC` / `EXTERN`        | Marks symbol for linker export or import             |
| `PRINTF`                   | Prints formatted text during assembly                |
| `FOPEN` / `FCLOSE`         | Redirects `PRINTF` output to a file                  |
| `WRITE ON/OFF`             | Enables or disables object file output for a region  |
| `SUPPRESS` / `RELEASE`     | Enables or disables specific output categories       |
| `LONGA` / `SHORTA`         | Set accumulator width (16-bit or 8-bit)              |
| `LONGI` / `SHORTI`         | Set index register width                             |
| `SETDBR`                   | Sets the current Data Bank Register                  |
| `DATE` / `TIME`            | Assign current DOS format date/time to a label       |
| `RUN`                      | Inserts a printf-formatted string as code            |
| `DEFS` / `STRLEN` / `ROLS` | String manipulation functions                        |

Additional details regarding directives are covered in Chapter 4 and the Appendix.

---

Next: Macros and conditionals.
