# Constants of the Global Kind

Constants are useful in functions because they let you change a value in only one spot and have the change reflected throughout the function. Like any function’s variables, however, the const type of constant is valid in only one function at a time. Rather than re-create a constant for each function, you can use the #define preprocessor directive to create a global constant, available to all functions in the source code file.

+   » Use the const keyword to create a constant for use within a function.
+   » Refer to Chapter 6 for more details on constants and the const keyword.

# Introducing defined constants

A defined constant is a shortcut — specifically, something used in a source code file to substitute for something else. This constant operates at the compiler level and affects the entire source code file. It’s created by using the #define directive, in this format:

```
#define SHORTCUT text
```

SHORTCUT is a keyword, usually written in all caps. It’s created by the compiler to represent the text part. The line doesn’t end with a semicolon, because it’s a compiler directive, not a C language statement. The defined constant you create can be used elsewhere in the code, in any function: The keyword SHORTCUT being replaced by the text.

The following line creates the defined constant OCTO, equal to the value 8:

```
#define OCTO 8
```

After its definition, you can use the defined constant OCTO anywhere in your code to represent the value 8. For example:

```
printf("Mr. Octopus has %d legs.",OCTO);
```

The preceding statement outputs this text:

```
Mr. Octopus has 8 legs.
```