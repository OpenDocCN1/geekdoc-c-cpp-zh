In this approach, the return type was simply allowed to default to int. In C99 (and in C++) this default no longer occurs, and the int must be explicitly specified, as it is for all of the programs in this book.

Here is another example. In the past a function such as

```
int isEven(int val)
{
    return !(val%2);
}
```

would often have been written like this:

```
/* use integer default */
isEven (int val)
{
    return !(val%2);
}
```

In the first instance, the return type of int is explicitly specified. In the second, it is assumed by default. The implicit int rule does not apply only to function return values (although that was its most common use).

For example, for C89 and earlier, the isEven() function could also be written like this:

```
isEven(const val)
{
    return ! (val%2);
}
```

Here, the parameter val also defaults to int—in this case, const int. Again, this default to int is not supported by C99.

> Note Technically, a C99-compatible compiler can accept code containing implied ints after reporting a warning error. This allows old code to be compiled. However, there is no requirement that a C99-compatible compiler accept such code.

# Implicit Function Declarations Have Been Removed

In C89, if a function is called without a prior explicit declaration, then an implicit declaration of that function is created. This implicit declaration has the following form:

```
extern int name();
```

Implicit function declarations are no longer supported by C99.

> Note Technically, a C99-compatible compiler can accept code containing implied function declarations after reporting a warning error. This allows old code to be compiled. However, there is no requirement that a C99-compatible compiler accept such code.