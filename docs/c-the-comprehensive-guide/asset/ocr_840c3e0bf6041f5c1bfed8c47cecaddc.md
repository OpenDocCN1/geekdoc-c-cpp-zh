Now, of course, the line with `n = 8` is gone, because otherwise you would be breaking your promise. The compiler would now find fault with this line, because you cannot assign anything to a `const int&`, which `n` now is. However, you can use a variable when calling `print_cref8(x)` or a literal `print_cref8(42)`. This means that the following two function declarations can be used equally broadly as far as the arguments are concerned:

```
```cpp
void print_val8(int n);        // Parameter as value
void print_cref8(const int& n); // Parameter as constant reference
```
```

# 7.5.4 Call as Value, Reference, or Constant Reference?

All these variants of declaring a parameter have their justification, and you have to decide which one to use on a case-by-case basis:

+   - When called *as a value*, a copy is created. This can be a time- and memory-consuming process at program runtime. On the other hand, you can be sure that you will not accidentally change any external values.
+   - When called *as a reference*, no copy is created, but the compiler transfers the address of the parameter into the function. This is quick and saves space. But do you really want to change externally defined variables? Sometimes, yes, but not always.
+   - Use a `const` reference if you decide for a reference but do not want to have the variable changed.
+   - If you use a *non-const reference*, you simply cannot pass some parameters, just as the literal `42` cannot be passed to an `int&`, for example. There are also constant values and objects, all of which you exclude with an & only parameter.

A disadvantage when using references (and pointers) can arise due to *aliasing*. There are cases in which a reference in a function refers to a variable (via an alias) that no longer exists; it has already become invalid outside. Program crashes are the result. As the parameter is copied specifically for the function call when it is called as a value, this cannot happen here.

One way to avoid these program crashes is to forego references. Because a typical application is the output parameter, I recommend that you use a return value instead:

```
```cpp
// https://godbolt.org/z/oh91YvaqT
#include <iostream>
void twice(double &num) {      // output parameter as modifiable reference
    num *= 2.0;
}

int main() {
    double num = 7.25;
```
```