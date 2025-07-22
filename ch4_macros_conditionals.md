## Chapter 4: Macros and Conditional Assembly

### Macros

ArgSfx features a powerful macro system that supports either positional or named arguments. Macros are reusable blocks of code that can be parameterized and expanded multiple times during assembly.

#### Basic Macro Definition

```asm6502
my_macro    MACRO    [param1, param2]
    lda    #{param1}
    sta    {param2}
    ENDM
```

- Use square brackets to define named parameters (recommended).
- Parameters must be referenced using `{name}`. Keep in mind that the assembler internally maps these to positional arguments.
- Up to 36 total macro parameters can be specified.
- Use `ENDM` to close the macro definition.
- You may use the traditional `\1` - `\9` and `\A` - `\Z`, in place of named parameters.
- Conditional blocks can be used to direct macro logic.
- Use `MEXIT` to prematurely terminate expansion of a macro (e.g. if a certain condition is met)
- Variable assignments with `=` can be used for purposes such as iteration, e.g. `my_variable = my_variable + 1`

### Calling a Macro

```asm6502
    my_macro    $20,target_var
```

This expands to:

```asm6502
    lda    #$20
    sta    target_var
```

### Parameter `\0`

Parameter `\0` is a special parameter that is passed in a way similar to the `.b`, `.w`, or `.l` instruction suffixes.

(e.g. `my_macro.z` passes a suffix argument containing the character "z")

```asm6502
my_macro.z [parameters 1-36 are passed as usual...]
```

### Strings as Parameters

To pass strings to a macro, enclose them in angle brackets (`<` and `>`).

```asm6502
my_macro    <my string>,$20,variable
```

#### Escaping Reserved Characters

To include a literal `{` or `}` in a macro body, write `{{` or `}}` respectively.

To include a literal `\` in a macro body (e.g. to insert file paths), write `\\`.

#### Local Labels in Macros

To use local labels in macros repeatedly without symbol collision, use `\@` anywhere in their names.

---

### Macro Utilities

#### `NARG` - Number of Macro Arguments

This predefined variable holds the number of arguments passed to the current macro.

#### `LONGA` - Accumulator Width

This predefined variable holds the current accumulator width. Nonzero if 16 bit.

#### `LONGI` - Index Register Width

This predefined variable holds the current width of the index registers. Nonzero if 16 bit.

---

### Code Repetition and Iteration - `REPT`, `IRP`, and `IRS`

#### `REPT` - Repeat

Repeats a block of code a specified number of times.

```asm6502
    REPT 4
    nop
    ENDR
```

#### `IRP` - Iterate Repeat Parameter

Iterate over a list of values using a replacement symbol:

```asm6502
    REPT 3
    IRP index,10,20,30
    lda    #index
    ENDR
```

#### `IRS` - Iterate Repeat String Parameter

Like `IRP`, but uses named/numbered strings:

```asm6502
    REPT 3
    IRS mystring,"A","B","C"
    RUN ' db "%$mystring"'
    ENDR
```

---

### Conditional Assembly

ArgSfx allows complex conditional logic to include or exclude code based on constants, labels, strings, or environment variables.

```asm6502
    IFD SYMBOL
    ; do something if symbol is defined
    ENDC
```

```asm6502
    IFEQ symbol-10
    ; if symbol-10 is equal to zero, do something
    ELSEIF
    ; do something else
    ENDC
```

#### Condition Types

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

Use `ELSEIF` to invert the condition block to test for and handle the opposite condition, and `ENDC` to terminate the condition block.

---

Next: Expressions, evaluation, and the PRINTF system.
