preceded by # in the substitution string, the argument is converted into a quoted string when the macro is expanded. Thus, if you define a macro as

```
#define OUT(x) printf ("#x)
```

and you invoke it with the statement

```
OUT(Hello Mom);
```

it expands to this statement:

```
printf("Hello Mom\"");
```

The conversion performed by the stringizing operator takes special characters into account. Thus, if a character in the argument normally requires an escape character, the # operator inserts a backslash before the character. Continuing with the example, the

invocation

```
OUT("Hello Mom\"");
```

expands to

```
printf("\Hello Mom\\\"");
```

The # operator is demonstrated in Listing 22.4. First, you need to look at one other operator used in macros, the concatenation operator (##).This operator concatenates, and joins, two strings in the macro expansion. It doesn't include quotation marks or special treatment of escape characters. Its main use is to create sequences of C source code. For example, if you define and invoke a macro as

the macro invoked in the second line is expanded to

```
salad = func3(q, w);
```

You can see that, by using the ## operator, you determine which function is called. You have actually modified the C source code.

Listing 22.4 shows an example of one way to use the # operator.