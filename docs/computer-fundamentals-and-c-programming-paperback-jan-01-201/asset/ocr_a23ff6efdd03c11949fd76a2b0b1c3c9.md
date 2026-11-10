For instance, the compiler, which otherwise sees 3 as an int, treats 3L as a long. There are no constants of type short. Next time you see the constants 540U or 450L, remember to treat them as unsigned int and signed long, respectively.

**Floating Point Constants** C treats a real constant as a double which takes up 8 bytes on most systems. Constants like 3.142 and 1789.456 have the type double even though a float (4 bytes) is wide enough for them. However, unlike integer constants which can only be promoted to long and long long, real constants can be both promoted and demoted:

+   - The F or f suffix denotes a real constant to float. The constants 3.142f and 1789.456F have the type float.
+   - The L or l (el) suffix promotes a real constant to long double, which may take up to 16 bytes.

These suffixes work with the exponential form also (like 3E4F). Demoting a constant to float often makes sense because it leads to savings in memory space and computation time.

**Character Constants** Any character or escape sequence enclosed in single quotes represents a character constant. The characters 'A', '\t' and '\7' are character constants having the ASCII values 65, 11 and 7, respectively. Strangely enough, C treats character constants as type int rather than char. This means the constant 'A' is stored in a space of 4 bytes (size of int).

**Takeaway:** The default type for an integer constant is `int`. For a real number, the default is `double`. A character constant is stored as an `int`. C doesn’t support a constant of type short.

# 5.13.2 Variables as Constants: The const Qualifier

A constant that is used multiple times in a program is often stored as a variable. If the value is changed later, then the code needs to be modified at a single location, thus making maintenance easier. The constant itself should be stored as a variable using the **const** qualifier:

```
const float euro_dollar = 1.325;
```

The **const** qualifier protects a variable from being rewritten by marking it read-only. You’ll often see this qualifier in the syntax of many C string-handling functions.

# 5.13.3 Symbolic Constants: Constants with Names

Storing a constant in a variable has a drawback. Every time a variable is encountered, the program has to access its memory location. Memory access takes time, so C offers **symbolic constants** to avoid this access. We have used PI as a symbolic constant in a **#define** directive of the preprocessor (4.4). The euro-dollar conversion problem has a better solution in the following **#define** directive:

```
#define euro_dollar 1.325f

*No semicolon — not a C statement*
```

The preprocessor replaces euro_dollar with 1.325 everywhere in the program. The compiler thus never gets to see euro_dollar but sees 1.325 instead. (The f suffix ensures that the default double