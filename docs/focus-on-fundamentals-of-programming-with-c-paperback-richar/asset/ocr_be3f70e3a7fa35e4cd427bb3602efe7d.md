The string:

```
"abcBLANKdef"
```

will be left unchanged. But:

```
"abc"BLANK"def"
```

is expanded to:

```
"abc""def"
```

# Macros With Arguments: #define identifier(arg1, arg2, ...) string

Note that there can be no space between the identifier and the left parenthesis of the argument:

```
// macro2.c
#define SQ(x) ((x) * (x))
```

So:

```
SQ(7 + w)
```

expands to:

```
((7+w) * (7+w))
```