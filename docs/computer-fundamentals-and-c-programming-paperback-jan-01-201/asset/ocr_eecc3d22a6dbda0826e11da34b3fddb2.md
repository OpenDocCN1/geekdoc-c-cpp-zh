# 13.4 HANDLING LINES AS STRINGS

We often deal with *text* files which are organized as a group of lines containing printable characters. Each line is separated from its adjacent one by the appropriate newline character specific to the operating system (CR-LF for MSDOS, LF for UNIX). We routinely sort lines, display those that contain a specific string and also modify them. C supports the following I/O functions that read and write lines:

+   - **gets/puts** (Discussed here but unsafe to use)
+   - **fgets/fputs**

These functions use a *buffer* (an array) as an argument to store a line of data. The two sets differ in handling of NUL and the newline character. We’ll first take up the **gets/puts** duo, understand the danger involved in using **gets** and then discuss the safer functions, **fgets** and **fputs**. We’ll also understand how the **fgets/sscanf** combination is often a better alternative to **scanf** for formatting input data.

# 13.4.1 Using gets/puts: The Unsafe Way

| Function | Details |
|---|---|
| `gets` | **Prototype:** `char *gets(char *s);`<br>**Header file:** `stdio.h`<br>**Return value:** (i) s on success, (ii) NULL on error or when EOF occurs before any characters are read. |
| `puts` | **Prototype:** `int puts(const char *s);`<br>**Header file:** `stdio.h`<br>**Return value:** A non-negative number on success or EOF on error. |

Both functions use a single argument, a pointer to char. For **gets**, this must be an implicit pointer to a buffer represented by an array of type char. **puts** simply writes the contents of the buffer to the terminal:

```
char stg[80];                 Can hold up to 80 characters including NUL
gets(stg);                    Reads a line from standard input into stg
puts(stg);                    Writes contents of stg to standard output
```

**gets** converts the trailing newline to NUL, while **puts** adds it back before writing to the terminal. `stg` must be large enough to hold an entire line of input even though **gets** doesn’t check this size. Thus, if the line is longer than the size of `stg`, **gets** will simply overflow this buffer.

> **Note:** The infamous Morris worm, which paralyzed (possibly) one-tenth of the Internet in 1988, originated from an overflow situation caused by **gets** in a self-replicating and self-propagating program.

# 13.4.2 gets_puts.c: A Program Using gets and puts

Program 13.2 changes the case of text from lower to upper in a line of text read by **gets**. **puts** writes the modified line to the standard output. A subsequent program will use the **toupper** library