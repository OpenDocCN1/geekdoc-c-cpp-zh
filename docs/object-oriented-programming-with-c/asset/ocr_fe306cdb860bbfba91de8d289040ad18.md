```
cout.width(10);  
cout << 275.5 << "\n";
```

will produce the following output:

`+ | | 2 7 5 . | 5 0 0`

The flags such as **showpoint** and **showpos** do not have any bit fields and therefore are used as single arguments in **setf()**. This is possible because the **setf()** has been declared as an overloaded function in the class **ios**. Table 10.5 lists the flags that do not possess a named bit field. These flags are not mutually exclusive and therefore can be set or cleared independently.

# Table 10.5 — *Flags that do not have bit fields*

| Flag | Meaning |
|---|---|
| `ios :: showbase` | Use base indicator on output |
| `ios :: showpos` | Print + before positive numbers |
| `ios :: showpoint` | Show trailing decimal point and zeroes |
| `ios :: uppercase` | Use uppercase letters for hex output |
| `ios :: skipws` | Skip white space on input |
| `ios :: unitbuf` | Flush all streams after insertion |
| `ios :: stdio` | Flush **stdout** and **stderr** after insertion |

Program 10.9 demonstrates the setting of various formatting flags using the overloaded **setf()** function.

# Program 10.9 — Formatting with Flags in setf()