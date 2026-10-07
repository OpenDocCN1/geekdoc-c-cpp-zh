Default arguments look a lot like function overloading since you can use the same name and different arguments to call the function. However, there is no overloading when default arguments are used. The compiler is performing argument substitution and calling the same function.

You can use function overloading and default arguments together as long as no ambiguities are created:

```
void foo();           // ambiguous
void foo(int a = 10); // ambiguous
```