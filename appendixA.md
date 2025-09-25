## Appendix A: Quick Reference

### A.1 Assembler Directives

| Directive                                    | Purpose                                                                                                                                                                                                                                                           |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<lbl> = / EQU <expr>`                       | Define variable / constant                                                                                                                                                                                                                                        |
| ``CHECKMAC ON/OFF``                          | Enable/disable duplicate macro checking.<br>Enabled by default in ArgSfx v1.52.                                                                                                                                                                                   |
| `DATE / TIME <label>`                        | Assign system date/time in DOS format to label                                                                                                                                                                                                                    |
| `DB/DW <expr1>,<expr2>, etc...`              | Defines a string of bytes or words.<br>`DB` can also be used to define a text string.                                                                                                                                                                             |
| `DS <bytes>`                                 | Reserves specified amount of bytes                                                                                                                                                                                                                                |
| `DEFEND "txt"`                               | Defines the end of assembly message with a `PRINTF` string                                                                                                                                                                                                        |
| `DEFERROR / ERROR "txt"`                     | Defines the error message with a printf string                                                                                                                                                                                                                    |
| `DEFS <str>,"([len])txt"`                    | Assign a `PRINTF` result to string 1-5 (SASM) or a named string with optional length. (**ArgSfx only**).                                                                                                                                                          |
| `ERROR+`                                     | Increments the number of errors                                                                                                                                                                                                                                   |
| `END`                                        | Stops assembly of the current source file                                                                                                                                                                                                                         |
| `<lbl> EQUR <Rn>`<br>or<br>`<Rn> EQUR <lbl>` | Define a label to be an alias for a Super FX register.                                                                                                                                                                                                            |
| `FABCARD <expr>`                             | Sets the FABcard port address.                                                                                                                                                                                                                                    |
| `FAIL`                                       | Causes a fatal error.                                                                                                                                                                                                                                             |
| `FOPEN <(+)name> / FCLOSE (name /!)`         | Redirect `PRINTF` to/from a file                                                                                                                                                                                                                                  |
| `GETENV <str>,<env var>`                     | Puts the contents of the environment variable into a defined string.                                                                                                                                                                                              |
| `GETHEAP <heap>`                             | Gets as much of the heap (in bytes) as specified.<br>This is an internal directive and should never be invoked by the user.<br>(SASM only, see Chapter 7, "Known Issues")                                                                                         |
| `IFxx` / `ELSEIF` / `ENDC`                   | Define a conditional assembly block<br>(see Chapter 4, "Condition Types")                                                                                                                                                                                         |
| `INCBIN <file>`                              | Include a binary file                                                                                                                                                                                                                                             |
| `INCCOL <file,start,end>`                    | Include palette lines from Nintendo .COL palette files.                                                                                                                                                                                                           |
| `INCDIR <dir>`                               | Set default include directory                                                                                                                                                                                                                                     |
| `INCLUDE <file>`                             | Include another source file                                                                                                                                                                                                                                       |
| `IRP/IRS <sym/txt>,[val]...`                 | Iterate through values or strings                                                                                                                                                                                                                                 |
| `LIST ON/OFF`                                | Enable/disable listing output                                                                                                                                                                                                                                     |
| `<label> LOCAL`                              | Assign sublabels to a specific parent label as ``parent.local``                                                                                                                                                                                                   |
| `<lbl> MACRO` / `ENDM`                       | Define a macro block                                                                                                                                                                                                                                              |
| `MARIO ON/OFF`                               | Enable/disable Super FX ("MARIO") instruction parsing.                                                                                                                                                                                                            |
| `MEXIT`                                      | Exits the current macro, ignoring conditional levels                                                                                                                                                                                                              |
| `ORG <pcorg>(,rompos)`                       | ORGs the code.<br>ROM position is optional, if not present then code will be put at the following byte.                                                                                                                                                           |
| `OUTPUT <name>`                              | Set output binary filename                                                                                                                                                                                                                                        |
| `PRINTF "txt" or <expr>`                     | Print formatted text<br>(See Chapter 5, "The `PRINTF` Directive")                                                                                                                                                                                                 |
| `PUBLIC / EXTERN <symbol>`                   | Mark symbol for export/import in linking                                                                                                                                                                                                                          |
| `REPT <n>` / `ENDR`                          | Repeat a block of code `<n>` times                                                                                                                                                                                                                                |
| `ROLS <str>,<offset>`                        | Rotate defined string left by offset.<br>Replaced by ``SUBSTR`` in ArgSfx, and can be easily replicated with it<br>(see Chapter 7, "Quirks").                                                                                                                     |
| `RUN 'txt'`                                  | Include result of a `PRINTF` string as source code.                                                                                                                                                                                                               |
| `SEND (expr)`                                | Send the object code to a RAMboy development cartridge of type (expression). (default = $3D)                                                                                                                                                                      |
| `SETDBR <n>`                                 | Define current data bank register                                                                                                                                                                                                                                 |
| `SHORTA / LONGA`                             | Set accumulator size                                                                                                                                                                                                                                              |
| `SHORTI / LONGI`                             | Set index register size                                                                                                                                                                                                                                           |
| `SICE`                                       | Emit an invalid instruction (for debugging purposes)                                                                                                                                                                                                              |
| `STRING <str>([len])=("txt"/<lbl>)`          | (**ArgSfx only**) Define/assign contents of a `PRINTF` string or label to a named or numbered string.<br>Max length is 150 characters.<br>Length does not need to be specified when assigning contents, but must be specified when a string is initially defined. |
| `STRCPY <deststr>,<srcstr>`                  | (**ArgSfx only**) Copies the source named or numbered string to the destination named or numbered string. |
| `STRLEN (label),<str>`                       | Insert string length into label/expression (use in expressions by omitting the label parameter)                                                                                                                                                                   |
| `SUBSTR <start,end,str>`                     | Gets the portion of the specified defined string between the specified start and end. Replaces ``ROLS`` in SASM. (**ArgSfx Only.**)                                                                                                                               |
| `SUPPRESS / RELEASE <option>`                | Control output verbosity<br>(See Chapter 6, "Environment-Sensitive Output")                                                                                                                                                                                       |
| `SYMBOLS ON/OFF`                             | Emit symbol table                                                                                                                                                                                                                                                 |
| `TYPE <filename>`                            | Prints `<filename>` to the screen.                                                                                                                                                                                                                                |
| `UPPER/LOWER <str>`                          | Change case of a defined string                                                                                                                                                                                                                                   |
| `WRITE ON/OFF`                               | Enable/disable output block writing                                                                                                                                                                                                                               |

---

### A.2 Conditional Assembly Directives

| Condition                 | Meaning                                                                                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `IFEQ <exp>`              | Equal to zero                                                                                                                                  |
| `IFNE <exp>`              | Not equal to zero                                                                                                                              |
| `IFGT <exp>`              | Greater than                                                                                                                                   |
| `IFGE <exp>`              | Greater or equal to zero                                                                                                                       |
| `IFLT <exp>`              | Less than                                                                                                                                      |
| `IFLE <exp>`              | Less or equal to zero                                                                                                                          |
| `IFD <sym>`               | Symbol is defined                                                                                                                              |
| `IFND <sym>`              | Symbol is not defined                                                                                                                          |
| `IFC "str1","str2"`       | Strings equal                                                                                                                                  |
| `IFNC "str1","str2"`      | Strings not equal                                                                                                                              |
| `IFV "var"`               | Environment variable exists                                                                                                                    |
| `IFNV "var"`              | Environment variable does not exist                                                                                                            |
| `IFS <str>,<pos>,"char"`  | String character matches at position<br>**Important:** the parsing of this conditional changes slightly in ArgSfx.<br>See Chapter 7, "Quirks". |
| `IFNS <str>,<pos>,"char"` | String character does not match<br>**Important:** the parsing of this conditional changes slightly in ArgSfx.<br>See Chapter 7, "Quirks".      |
| `IFFE "fullpath"`         | File exists (**ArgSfx only**)                                                                                                                  |
| `IFFNE "fullpath"`        | File does not exist (**ArgSfx only**)                                                                                                          |

---

### A.3 Assembler CLI Options

| Option           | Description                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| `-e__notitle`    | Suppress title banner                                                                                            |
| `-e__mario`      | Default to MARIO parsing mode                                                                                    |
| `-e__heap=####`  | Set heap size (SASM only)                                                                                        |
| `-dN,"str"`      | Define string number `N` with value "str"                                                                        |
| `-eSYMBOL=value` | Define a constant (EQU)                                                                                          |
| `-f<file>`       | Set listing file                                                                                                 |
| `-i<dir>`        | Set include directory                                                                                            |
| `-l`             | Enable listing                                                                                                   |
| `-m<value>`      | Specifies maximum errors before stopping.                                                                        |
| `-o<file>`       | Set output file                                                                                                  |
| `-p<name>`       | Write stdout to file ``<name>`` (**ArgSfx only**)                                                                |
| `-r`             | Display ROM listing on screen                                                                                    |
| `-sSYMBOL=value` | Set a label (with `=`)                                                                                           |
| `-v<file.SOB>`   | Output linkable object                                                                                           |
| `-x[filename]`   | Enable symbol listing (optionally to a file)                                                                     |
| `-z`             | Generate a `.MAP` symbol map file for use with the ArgBug debugger.<br>Includes ROM addresses. (**ArgSfx only**) |

---

### A.4 SASM Environment Variables

| Variable   | Purpose                   |
| ---------- | ------------------------- |
| `SASMDIR`  | Default include directory |
| `SASMSRC`  | Default source filename   |
| `SASMHEAP` | Heap size in bytes        |

---

### A.5 Special Assembler Variables

| Symbol    | Description                                                     |
| --------- | --------------------------------------------------------------- |
| `_SASM`   | Always defined when using SASM<br>(also defined in ArgSfx 1.52) |
| `_ARGSFX` | Always defined when using ArgSfx                                |
| `NARG`    | Number of macro arguments                                       |
| `LONGA`   | Accumulator mode (nonzero = 16-bit)                             |
| `LONGI`   | Index register mode (nonzero = 16-bit)                          |
| `_DAY`    | Current day (1–31)                                              |
| `_MONTH`  | Current month (1–12)                                            |
| `_YEAR`   | Current year (e.g. 1995)                                        |
| `_DATE`   | Integer in format yyyymmdd                                      |

---

### A.6 Assembler Strings

| Index | Meaning                           |
| ----- | --------------------------------- |
| `1–5` | User-defined strings (via `DEFS`) |
| `6`   | Current filename                  |
| `7`   | Date in long text form            |
| `8`   | First included filename           |

---

### A.7 `PRINTF` Commands

| Code        | Meaning                                                                 |
| ----------- | ----------------------------------------------------------------------- |
| `%$<n>`     | Print numbered string n (SASM) or named string n (**ArgSfx only**)      |
| `%%`        | Literal percent                                                         |
| `%<xx>`     | ANSI escape sequence (e.g., `%31` = red text)                           |
| `%b`        | Backspace                                                               |
| `%c`        | Second nested macro name                                                |
| `%d`        | Error category ("ERROR" or "WARNING")                                   |
| `%e`        | Error message                                                           |
| `%f`        | Current filename                                                        |
| `%h`        | Converts a 2 digit ASCII hex number to a real hex number and inserts it |
| `i<N>`      | Extended command where `<N>` is the command (see below)                 |
| `%k`        | Free memory in bytes                                                    |
| `%l`        | Line number                                                             |
| `%m`        | Current macro name                                                      |
| `%n`        | Newline (CR+LF)                                                         |
| `%p`        | Parent label                                                            |
| `%q`        | Prints a quote (")                                                      |
| `%s`        | Enable listing for one line                                             |
| `%t`        | Tab                                                                     |
| `%u`        | Unknown symbol (forward ref)                                            |
| `%x<expr> ` | Evaluate and print an expression (whitespace after `<expr>` required)   |

### A.8 Extended `PRINTF` Commands - `%i<N>`

| Code  | Meaning                                                                      |
| ----- | ---------------------------------------------------------------------------- |
| `%ib` | Print total number of bytes (End message only, see Appendix A.1, "`DEFEND`") |
| `%ic` | Print processor type                                                         |
| `%ie` | Print number of errors                                                       |
| `%if` | Print number of files                                                        |
| `%il` | Print number of lines                                                        |
| `%is` | Print number of symbols                                                      |
| `%iw` | Print number of warnings                                                     |

Refer to Chapter 5 for full formatting examples.

---

### A.9 Linker CLI Options

| Option         | Description                                                                                                       |
| -------------- | ----------------------------------------------------------------------------------------------------------------- |
| `-a1`          | Upload to ADS SuperChild1 hardware (**ArgLink only**)                                                             |
| `-a2`          | Upload to ADS SuperChild2 hardware (**ArgLink only**)                                                             |
| `-b<size>`     | Set file input/output buffers (0-31), default = 10K                                                               |
| `-c`           | Duplicate public warnings                                                                                         |
| `-d`           | Upload to RAMboy development cartridge                                                                            |
| `-e<ext>`      | Change default file extension, default = `.SOB`                                                                   |
| `-f<addr>`     | Set Fabcard port address (in hex), default = 290                                                                  |
| `-h<size>`     | String hash size, default = 256                                                                                   |
| `-i`           | Display file information while loading.                                                                           |
| `-l<size>`     | Display used ROM layout (size is in K)                                                                            |
| `-m<size>`     | Memory size (in megabytes), default = 2                                                                           |
| `-n`           | Upload to Nintendo emulation system                                                                               |
| `-o<ROM name>` | Output a ROM image                                                                                                |
| `-p[<addr>]`   | Set Printer port address (in hex), default = 378                                                                  |
| `-r`           | Display ROM block information                                                                                     |
| `-s`           | Display all public symbols                                                                                        |
| `-t[<type>]`   | Set ROM type (in hex), default = 7D                                                                               |
| `-w [prefix]`  | Set prefix (Working directory) for object files                                                                   |
| `-y`           | Use secondary ADS backplane CIC (**ArgLink only**)                                                                |
| `-z`           | Generate a `.MAP` symbol map file for use with the ArgBug debugger.<br>Includes ROM addresses. (**ArgLink only**) |
| `@[<file>]`    | Include a list of object files to link                                                                            |

---

### A.10 ArgBug `.MAP` File Format

The ArgBug `.MAP` File format consists of 2 segments:

- The `SIZE` segment, listing all ROM addresses where a processor mode directive (e.g. `LONGA`, `LONGI`, `SHORTA`, `SHORTI`) was invoked in the orignal assembly,

- and the `SM32` symbol map segment, listing symbol addresses/values and their names.

#### `SIZE` Segment Format

- Segment begins with "SIZE" magic number

- Each SIZE entry has:

  - 3 bytes in little endian containing a SNES address (`lo:hi:bank` LE, `bank:hi:lo` BE)
  
  - 1 byte denoting Type ID (1 - 4)
 
### Type IDs:

- `01` - `MAP_SHORTA` - Accumulator 8-bit

- `02` - `MAP_SHORTI` - Index registers X/Y 8-bit

- `03` - `MAP_LONGA` - Accumulator 16-bit

- `04` - `MAP_LONGI` - Index registers X/Y 16-bit

#### Symbol Map Segment Format

- Segment begins with ASCII "`SM32`" magic number, followed by 2 bytes indicating the total number of symbols in little-endian.

- Each symbol entry has:
  
  - 4 bytes in little-endian denoting the value of the symbol; (`00:lo:hi:bank`) if it is a SNES ROM address, a 32-bit value for any other symbol (e.g equates, constants, variables).
  
  - 1 byte denoting the length of the symbol name in bytes.
  
  - Symbol name (ASCII)
 
---

End of the ArgSfx assembler manual
