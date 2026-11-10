# # 9 Terminal Input/Output Functions

# **WHAT TO LEARN**

+   - How *end-of-file (EOF)* and *buffering* issues affect the behavior of input/output functions.
+   - Fetching and writing a character with the **getchar** and **putchar** functions.
+   - Performing the same tasks with the **getc/fgetc** and **putc/fputc** functions.
+   - Converting text files between UNIX and MSDOS systems.
+   - How the special files—**stdin**, **stdout** and **stderr**—are used with programs.
+   - Reading and formatting character data with **scanf**.
+   - Printing individual data items as a character string with **printf**.

# ## 9.1 I/O FUNCTION BASICS

Unlike other languages, C depends on functions for carrying out even the most trivial tasks. C supports no keywords for taking input from the keyboard or for displaying output on the terminal. Functions that carry out input/output operations consider data as a stream of *characters* irrespective of the data type they actually represent. Thus, some of the I/O functions discussed in this chapter have to perform type conversion of data before they reach the destination.

Most I/O functions have to contend with two issues—EOF and buffering of data. Input functions often need to check for an *end-of-file (EOF)* condition. The term “file” is misleading because EOF actually indicates the end of data. There's no character named EOF in the ASCII character set (Appendix B). For keyboard input, UNIX/Linux systems use [*Ctrl-d*] and MSDOS/Windows systems use [*Ctrl-z*] to indicate EOF to a program.

Functions like **getchar** and **scanf** are often used in a loop which is terminated on EOF, i.e., when no further input is forthcoming or no error is encountered:

```
    while ((c = getchar()) != EOF)
    while (scanf("%d", &day) != EOF)
```