That functions with different names or arity are distinct goes without saying. The presence of a reference symbol turns the argument type into another argument type (thus, f(int) and f(int&) can coexist). The following three overloads have different signatures:

Click here to view code image

```
void f(int x) {}       // #1
void f(int& x) {}      // #2
void f(const int& x) {} // #3
```

This code snippet compiles. Problems will arise, however, when we call f:

Click here to view code image

```
int i = 3;
const int ci = 4;

f(i);
f(ci);
f(3);
```

All three function calls are ambiguous: for the first call #1 and #2 are equal matches, and for the other calls #1 and #3. Mixing overloads of reference and value arguments almost always fails. Thus, when one overload has a reference qualified argument, the corresponding argument of the other overloads should be reference qualified as well. We can achieve this in our toy example by omitting the value-argument overload. Then f(3) and f(ci) will resolve to the overload with the constant reference and f(i) to that with the mutable one.

# ## 1.5.5 main Function

The main function is not fundamentally different from any other function. There are two signatures allowed in the standard:

```
int main()
```

or:

```
int main(int argc, char* argv[])
```

The latter is equivalent to:

```
int main(int argc, char** argv)
```