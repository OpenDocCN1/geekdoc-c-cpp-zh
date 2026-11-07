outputs a series of random integers; the output of random can be “piped” directly to program sum using the UNIX command line

```
$ random | sum
```

This causes the sum of the integers produced by random to be calculated. Piping can be performed in UNIX, LINUX, Mac OS X and Windows.

Program output can be redirected to a file by using the **redirect output symbol (>)**. (The same symbol is used for UNIX, LINUX, Mac OS X and Windows.) For example, to redirect the output of program random to a new file called out, use

```
$ random > out
```

Finally, program output can be appended to the end of an existing file by using the **append output symbol (>>)**. (The same symbol is used for UNIX, LINUX, Mac OS X and Windows.) For example, to append the output from program random to file out created in the preceding command line, use the command line

```
$ random >> out
```

# F.3 Variable-Length Argument Lists

It is possible to create functions that receive an unspecified number of arguments. An ellipsis (…) in a function’s prototype indicates that the function receives a variable number of arguments of any type.¹ Note that the ellipsis must always be placed at the end of the parameter list, and there must be at least one argument before the ellipsis. The macros and definitions of the **variable arguments header <cstdarg>** (Fig. F.1) provide the capabilities necessary to build functions with variable-length argument lists.

| Identifier | Description |
|---|---|
| `va_list` | A type suitable for holding information needed by macros `va_start`, `va_arg` and `va_end`. To access the arguments in a variable-length argument list, an object of type `va_list` must be declared. |
| `va_start` | A macro that is invoked before the arguments of a variable-length argument list can be accessed. The macro initializes the object declared with `va_list` for use by the `va_arg` and `va_end` macros. |
| `va_arg` | A macro that expands to an expression of the value and type of the next argument in the variable-length argument list. Each invocation of `va_arg` modifies the object declared with `va_list` so that the object points to the next argument in the list. |
| `va_end` | A macro that performs termination housekeeping in a function whose variable-length argument list was referred to by the `va_start` macro. |

**Fig. F.1** | The type and the macros defined in header `<cstdarg>`.

+   1. In C++, programmers use function overloading to accomplish much of what C programmers accomplish with variable-length argument lists.