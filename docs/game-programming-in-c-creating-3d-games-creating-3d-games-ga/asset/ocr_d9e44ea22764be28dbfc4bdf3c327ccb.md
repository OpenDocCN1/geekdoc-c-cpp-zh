can't pass in temporary values for the parameters. For example, `Swap (50, 100)` is invalid because 50 and 100 are not declared variables.

**warning**

PASS-BY-VALUE IS DEFAULT: By default, all parameters in C++, even objects, pass by value. In contrast, languages like Java and C# default to passing objects by reference.

# Pointers

To understand pointers, it first helps to remember the way computers store variables in memory. During program execution, entering a function automatically allocates memory for local variables in a segment of memory called the **stack**. This means that all local variables in a function have memory addresses known to the C++ program.

Table A.1 shows code snippets and possible locations of their variables in memory. Notice that each variable has an associated memory address. The table shows the memory addresses in hexadecimal simply because that’s the typical notation for memory addresses.

# Table A.1 Variable Storage

| Code | Variable | Memory Address | Value |
|---|---|---|---|
| `int x = 50;` | x | 0xc230 | 50 |
| `int y = 100;` | y | 0xc234 | 100 |
| `int z = 200;` | z | 0xc238 | 200 |