# C.6 Macros with Variable-Length Argument Lists

Macros may have variable-length argument lists. This allows for macro wrappers around functions like printf. For example, to automatically add the name of the current file to a debug statement, you can define a macro as follows:

```
```c
#define DEBUG(...) printf(__FILE__ ": " __VA_ARGS__)
```
```

This DEBUG macro takes a variable number of arguments, as indicated by the ... in the argument list. As with functions, the ... must be the last argument. Unlike functions, the ... can be the macro's only argument. The identifier __VA_ARGS__, which begins and ends with two underscores, is a placeholder for the variable-length argument list. Assuming this macro appears in the file file.c, the preprocessor replaces the following macro call

```
```c
DEBUG("x = %d, y = %d\n", x, y);
```
```

with

```
```c
printf("file.c" ": " "x = %d, y = %d\n", x, y);
```
```

Recall that strings separated by whitespace are concatenated during preprocessing, so the three string literals will be combined to form printf's first argument.

# C.7 Other C99 Features

Here we provide brief overviews of some additional C99 features. These include keywords, language capabilities and standard-library additions.

# C.7.1 Compiler Minimum Resource Limits

[This section can be read after Section 15.4.]

Before C99, the standard required C implementations to support identifiers of

+   - no less than 31 characters for identifiers with internal linkage, and
+   - no less than six characters for identifiers with external linkage (Section 15.4).

C99 increased these limits to 63 characters for identifiers with internal linkage and 31 characters for identifiers with external linkage. These are just lower limits. Compilers are free to support identifiers with more characters than these limits. For more information, see the C18 standard's Section 5.2.4.1.

C also sets minimum limits on many language features. For example, compilers must support at least 1,023 members in a struct, enum or union, and at least 127 parameters to a function. For more information on other limits, see the C18 Standard Section 5.2.4.1.

# C.7.2 The restrict Keyword

[This section can be read after Section 7.5.]

The keyword restrict declares a restricted pointer that should have exclusive access to a region of memory. Objects accessed through a restricted pointer cannot be