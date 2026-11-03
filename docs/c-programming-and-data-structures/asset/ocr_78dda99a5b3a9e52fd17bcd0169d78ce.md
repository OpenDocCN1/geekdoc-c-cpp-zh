If statement is included in the program at the beginning, then the preprocessor replaces every occurrence of the identifier in the source code by the string. The keyword #define is written just as shown (starting from the first column) followed by the identifier and a string, with at least one blank space between them. Note that the definition is not terminated by a semicolon. The string may be any text, while the identifier must be a valid C name.

There are different forms of macro substitution. The most common forms are:

+   1. Simple macro substitution.
+   2. Argumented macro substitution.
+   3. Nested macro substitution.

# Simple Macro Substitution

Simple string replacement is commonly used to define constants. Examples of definition of constants are:

```
#define COUNT 100
#define FALSE 0
#define SUBJECTS 6
#define PI 3.1415926
#define CAPITAL "DELHI"
```

Notice that we have written all macros in capitals. It is a convention to write all macros in capitals to identify them as symbolic constants. A definition, such as

```
#define M 5
```

will replace all occurrences of M with 5, starting from the line of definition to the end of the program. However, a macro inside a string does not get replaced. Consider the following two lines:

```
total = M * value;
printf("M = %d\n", M);
```

These two lines would be changed during preprocessing as follows:

```
total = 5 * value;
printf("M = %d\n", 5);
```

Notice that the string "M=%d\n" is left unchanged.

A macro definition can include expressions as well. Following are valid definitions:

```
#define AREA 5 * 12.46
#define SIZE sizeof(int) * 4
#define TWO-PI 2.0 * 3.1415926
```

# Argumented Macro Substitution

The preprocessor permits us to define more complex and more useful form of replacements. It takes the form:

```
#define identifier(f1, f2, ........, fn) string
```

Notice that there is no space between the macro identifier and the left parentheses. The identifiers f1, f2, ... ,fn are the formal macro arguments that are analogous to the formal arguments in a function definition. A basic difference between the simple replacement discussed above and the replacement of macros with arguments. Subsequent occurrence of a macro with arguments is known as a macro call (similar to a function call). When a macro is called, the preprocessor substitutes the string, replacing the formal parameters with the actual parameters. Hence, the string behaves like a template, replacing the formal parameters.