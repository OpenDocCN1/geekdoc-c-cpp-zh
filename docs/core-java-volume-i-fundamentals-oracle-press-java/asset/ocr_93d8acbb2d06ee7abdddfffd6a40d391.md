is perfectly legal—\u005B and \u005D are the encodings for [ and ].

**Table 3.3** Escape Sequences for Special Characters

| Escape Sequence | Name | Unicode Value |
| --- | --- | --- |
| `\b` | Backspace | `\u0008` |
| `\t` | Tab | `\u0009` |
| `\n` | Line feed | `\u000a` |
| `\r` | Carriage return | `\u000d` |
| `\f` | Form feed | `\u000c` |
| `\"` | Double quote | `\u0022` |
| `\'` | Single quote | `\u0027` |
| `\\` | Backslash | `\u005c` |
| `\s` | Space. Used in text blocks to retain trailing white space. | `\u0020` |
| `\newline` | In text blocks only: Join this line with the next | — |

> > **CAUTION:**
> >
> > Unicode escape sequences are processed before the code is parsed. For example, "\u0022+\u0022" is *not* a string consisting of a plus sign surrounded by quotation marks (U+0022). Instead, the \u0022 are converted into " before parsing, yielding ""+"", or an empty string.

Even more insidiously, you must beware of \u inside comments. The comment