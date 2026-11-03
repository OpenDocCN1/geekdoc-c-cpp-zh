When HELLO(John) appears in a program file, it's expanded to

```
```c
puts("Hello, " "John");
```
```

The string "John" replaces #x in the replacement-text. Strings separated by whitespace are concatenated during preprocessing, so the preceding statement is equivalent to

```
```c
puts( "Hello, " "John" );
```
```

The # operator must be used in a macro with arguments because the operand of # refers to an argument of the macro.

The ## operator concatenates two tokens. Consider the following macro definition:

```
```c
#define TOKENCONCAT(x, y) x ## y
```
```

When TOKENCONCAT appears in the program, its arguments are concatenated and used to replace the macro. For example, TOKENCONCAT(O, K) is replaced by OK in the program. The ## operator must have two operands.

# ## 13.8 Line Numbers

The #line preprocessor directive causes the subsequent source-code lines to be renumbered starting with the specified constant integer value. The directive

```
```c
#line 100
```
```

starts line numbering from 100 beginning with the next source-code line. A filename can be included in the #line directive. The directive

```
```c
#line 100 "file1.c"
```
```

indicates that lines are numbered from 100 beginning with the next source-code line and that the name of the file for the purpose of any compiler messages is "file1.c". The directive normally is used to help make the messages produced by syntax errors and compiler warnings more meaningful. The line numbers do not appear in the source file.

# ## 13.9 Predefined Symbolic Constants

Standard C provides predefined symbolic constants, several of which are shown in Fig. 13.1—the rest are in Section 6.10.8 of the C standard document. These identifiers begin and end with two underscores and often are useful to include additional information in error messages. These identifiers and the defined identifier (used in Section 13.5) cannot be used in #define or #undef directives.

| Symbolic constant | Explanation |
| --- | --- |
| `__LINE__` | The line number of the current source-code line (an integer constant). |
| `__FILE__` | The name of the source file (a string). |
| `__DATE__` | The date the source file was compiled (a string of the form "Mmm dd yyyy" such as "Jan 19 2002"). |

Fig. 13.1 | Some predefined symbolic constants. (Part 1 of 2.)