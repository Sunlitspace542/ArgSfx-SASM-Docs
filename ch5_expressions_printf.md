## Chapter 5: Expressions and the `PRINTF` System

### Expression Evaluation

ArgSfx includes a 32-bit expression evaluator for use in equates, conditionals, and many directives. Expressions follow typical operator precedence, and evaluation is left-to-right for operators of equal precedence.

Numbers can be represented in several different bases:

- `$` prefix or `h` suffix for hexadecimal (base 16)
- `%` prefix or `b` suffix for binary (base 2)
- no prefix or suffix for decimal (base 10)

You can also insert the current ROM position of a source code line into an expression with the `@` operator:

```asm6502
    IFGT @-$200000
    PRINTF "More than 16 megabits of ROM used!"
    ENDC
```

A `*` at the beginning of an expression also seems to be used for the same purpose as `@`:

```asm6502
ramstart    incfile    ASM\ramstuff.asm
xoffset    equ    *-ramstart
```

#### Operators and Precedence

| Operator | Description                      | Precedence |
| -------- | -------------------------------- | ---------- |
| `>`      | Hi-byte                          | 10         |
| `<`      | Lo-byte                          | 10         |
| `+`      | Unary plus                       | 9          |
| `-`      | Unary minus                      | 9          |
| `~`      | Unary NOT                        | 9          |
| `$`      | Gets a sine value (undocumented) | 8          |
| `<<`     | Shift left                       | 8          |
| `>>`     | Shift right                      | 8          |
| `>`      | Greater than                     | 7          |
| `<`      | Less than                        | 7          |
| `=`      | Equal                            | 6          |
| `&`      | Logical AND                      | 5          |
| `^`      | Logical XOR                      | 4          |
| `!`      | Logical OR                       | 3          |
| `\|`     | MOD (remainder)                  | 2          |
| `/`      | Divide                           | 2          |
| `*`      | Multiply                         | 2          |
| `+`      | Addition                         | 1          |
| `-`      | Subtraction                      | 1          |

> **Warning:** The `|` MOD operator is broken and may not evaluate correctly. Avoid using it.

Expressions may contain parentheses to override default precedence:

```asm6502
value = (10 + 3) * 2 ; result = 26
```

You may use assembler variables like `LONGA`, `NARG`, or date fields (`_YEAR`, `_MONTH`, etc.) in expressions.

---

### The `PRINTF` Directive

`PRINTF` allows formatted text output during assembly. It supports text, variables, expressions, strings, and ANSI control codes.

```asm6502
    PRINTF "Current label is: %f, line %l"
```

`PRINTF` can also take an expression as its only parameter:

```asm6502
    PRINTF myvar
```

#### `PRINTF` Commands

| Code        | Meaning                                                                 |
| ----------- | ----------------------------------------------------------------------- |
| `%$<n>`     | Print numbered string n (SASM) or named string n (**ArgSfx only**)      |
| `%%`        | Literal percent                                                         |
| `%<xx>`     | ANSI escape sequence (e.g., `%31` = red text)                           |
| `%b`        | Backspace                                                               |
| `%c`        | Second nested macro name                                                |
| `%d`        | Error category ("Error" or "Warning")                                   |
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

#### Extended `PRINTF` Commands - `%i<N>`

| Code  | Meaning                                                                      |
| ----- | ---------------------------------------------------------------------------- |
| `%ib` | Print total number of bytes (end message only, see Appendix A.1, "`DEFEND`") |
| `%ic` | Print processor type                                                         |
| `%ie` | Print number of errors                                                       |
| `%if` | Print number of files                                                        |
| `%il` | Print number of lines                                                        |
| `%is` | Print number of symbols                                                      |
| `%iw` | Print number of warnings                                                     |

#### Field Formatting

You can align expressions or variables with a field definition, such as:

```asm6502
    PRINTF "Memory: %[5,.]m  Label: %[6,0]myvar"
```

or alternatively, escape the fields with commas:

```asm6502
    PRINTF "Memory: ",[5,.]m,"  Label: ",[6,0]myvar
```

- `[width,fillchar]` before the code pads the output.
- Prefix with `:$` to display values in 32-bit hexadecimal. The fields must be escaped by commas to do so.

---

### Redirecting Output

Use `FOPEN` to write `PRINTF` output to a file, and `FCLOSE` to return output to the console:

```asm6502
    FOPEN +log.txt     ; '+' = Append mode
    PRINTF "Building segment %$1"
    FCLOSE log.txt
```

To force file closure and allow reuse (e.g. for `INCLUDE`), do:

```asm6502
    FCLOSE !
```

Use `RUN` to include the result of a `PRINTF` string as source code:

```asm6502
    STRING mystring[64]="text"
    RUN ' DB "%$mystring"'
```

Note that spaces are used in place of tabs in the `RUN` string, and that the `PRINTF` string parameter is wrapped in single quotes.

---

### Defining and Using Strings

SASM allows for defining up to five user strings using `DEFS`:

```asm6502
    DEFS 1,"Level loaded:"
    PRINTF "%$1 mylabel=%xmylabel "
```

ArgSfx also allows for defining unlimited named user strings using `STRING`:

```asm6502
    STRING mystring[150]="text" or label
```

Numbered strings can also be operated upon using `STRING` in ArgSfx:

```asm6502
    STRING 5[64]="text" or label
```

`DEFS` can also operate upon named strings after they have been defined:

```asm6502
    DEFS mystring,"text" or label
```

Strings can have a maximum length of 150 characters.

You can manipulate strings with:

- `STRLEN (label),<str>` – stores string length in label/expression (use in expressions by omitting the label parameter)
- `ROLS str,offset` – rotates string left (replaced by `SUBSTR` in ArgSfx, see Chapter 7)
- `SUBSTR start,end,str` - gets a substring
- `UPPER str`, `LOWER str` – change string case

---

Next: File I/O, output control, writing object code, and using the linker.
