```
char c;
auto *cp = &c, d = c; // OK
auto e = c, f = c+1; // ERROR: deduction mismatch char vs. int
```

Here, two pairs of variables are declared with a shared auto specifier. The declarations of cp and d deduce the same type char for auto, so this is valid code. The declarations of e and f, however, deduce char and int due to the promotion to int when computing c+1, and that inconsistency results in an error.

A somewhat parallel special situation can also occur with placeholders for deduced return types. Consider the following example: Click here to view code image

```
auto f(bool b) {
if (b) {
return 42.0; // deduces return type double
} else {
return 0; // ERROR: deduction conflict
}
}
```

In this case, each return statement is deduced independently, but if different types are deduced, the program is invalid. If the returned expression calls the function recursively, deduction cannot occur and the program is invalid unless a prior deduction already determined the return type. That means that the following code is invalid: Click here to view code image

```
auto f(int n)
{
if (n > 1) {
return n*f(n-1); // ERROR: type of f(n-1) unknown
} else {
return 1;
}
}
```

but the following otherwise equivalent code is fine:

Click here to view code image

```
auto f(int n)
{
if (n <= 1) {
return 1; // return type is deduced to be int
} else {
return n*f(n-1); // OK: type of f(n-1) is int and so is type of n*f(n-1)
}
}
```