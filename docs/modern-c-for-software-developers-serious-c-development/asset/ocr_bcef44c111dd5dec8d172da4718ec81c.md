compilation options. #elif is followed by a constant expression. If the expression is true, the block of code attached to the #elif is compiled and no other #elif expressions are tested. Otherwise, the next block in the #if chain is tested.

The general form for #elif is:

```
#if expression
statement sequence
#elif expression 1
statement sequence
#elif expression 2
statement sequence
#elif expression 3
statement sequence
#elif expression 4
.
#else
statement sequence
#endif
```

Example:

```
#define US 0
#define ENGLAND 1
#define FRANCE 2
```

```
#if ACTIVE_COUNTRY == US
char currency[] = "dollar";
#elif ACTIVE_COUNTRY == ENGLAND
char currency[] = "pound";n#else
char currency[] = "franc"
#endif
```

# #ifdef and #ifdef

There is another preprocessor for conditional compilation that uses the #ifdef and #ifdef directives. These directives mean "if defined" and "if not defined" respectively. The The