## Chapter 6: Output Control and Linking

### Controlling Object Output

By default, ArgSfx writes all assembled object code to the output file, if one is specified. You can fine-tune what gets written using the `WRITE` directive.

```asm6502
    WRITE OFF
; this block will be skipped
    WRITE ON
; this block will be included
```

Blocks are defined implicitly when any of the following occur:

- An `ORG` directive is encountered
- A file is included with `INCBIN` or `INCCOL`
- A block size exceeds \~15–16KB (one EMS page)

Only blocks within `WRITE ON` will be output. This is useful for selective compilation or temporary exclusion of data.

---

### Generating Output Binaries

In SASM, use the `OUTPUT` directive to specify the final binary file:

```asm6502
    OUTPUT "game.bin"
```

You can also use the `-o` CLI flag:

```batch
sasmx main.asm -oout/game.bin
```

Note that these features do nothing in ArgSfx. As a workaround, do the following:

```asm6502
; start of your asm file
    org    0,0    ; there must be an ORG to some PC/ROM position at the start for assembly to succeed
    [your code follows...]
```

Then pass the following to ArgSfx and ArgLink:

```batch
argsfx main.asm -vgame.sob
arglink main.sob -ogame.bin
```

in both assemblers, If no output file is specified, no output file will be written.

---

### Listing and Symbols

- `LIST ON` / `OFF` - enables or disables source listings.
- `SYMBOLS ON` - emits defined symbols to screen or to a file specified with `-x`.
- `-xsymbols.txt` - writes symbol list to `symbols.txt`.

Each symbol is listed as:

```asm6502
symbol_name    $value
```

---

### Linkable Object Files (.SOB)

To generate a linkable file, use the `-v` option:

```batch
argsfx bank0.asm -vbank0.sob
```

Use `PUBLIC` to export symbols:

```asm6502
    PUBLIC start
start
    jmp main
```

Use `EXTERN` to reference symbols defined in other SOB files:

```asm6502
    EXTERN external_routine
    jsr external_routine
```

Expressions using externs are valid and preserved for evaluation at link time:

```asm6502
    EXTERN kris,dyl,giles
value = kris/dyl+giles
```

Note that you cannot perform a relative branch to an `EXTERN` symbol.

---

### The SL.EXE and ArgLink SFX Linkers

SASM pairs with **SL.EXE** and ArgSfx with **ARGLINK.EXE**, the integrated linker that combines `.SOB` files into a final ROM image.

To use the linker:

```batch
arglink <[opts] obj1 [opts] obj2....>
```

The most commonly used set of parameters to generate a SNES ROM image are:

```batch
arglink -b30 -h1024 -t7d -z -o[name].sfc @[filelist]
```

Below are the most commonly used CLI options for the linker:

| Option         | Description                                                                                                       |
| -------------- | ----------------------------------------------------------------------------------------------------------------- |
| `-b<size>`     | Set file input/output buffers (0-31), default = 10K                                                               |
| `-h<size>`     | String hash size, default = 256                                                                                   |
| `-o<ROM name>` | Output a ROM image                                                                                                |
| `-t[<type>]`   | Set ROM type (in hex), default = 7D                                                                               |
| `-z`           | Generate a `.MAP` symbol map file for use with the ArgBug debugger.<br>Includes ROM addresses. (**ArgLink only**) |
| `@[<file>]`    | Include a list of `.SOB` object files to link                                                                     |

Full CLI options are covered in the Appendix.

---

### Environment-Sensitive Output

Suppress or enable categories of output using `SUPPRESS` and `RELEASE`:

```asm6502
    SUPPRESS <option>
    RELEASE <option>
```

Valid categories:

- `WARN` - warnings
- `ERROR` - errors
- `PRTF` - `PRINTF` output
- `EXPR` - expressions
- `ANSI` - ANSI control codes

---

Next: Special notes, best practices, and quirks.
