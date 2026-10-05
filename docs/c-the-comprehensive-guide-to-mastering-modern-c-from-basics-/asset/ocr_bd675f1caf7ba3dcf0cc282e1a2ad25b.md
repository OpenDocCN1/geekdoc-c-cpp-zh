look the same.

# 23.3.1 Values for a “Function” Parameter

The procedure thus complete. But what do you use as the third parameter for calculate? Try a function—of course, with the appropriate signature.

```
// https://godbolt.org/g719|41ler
#include <functional> // function
#include <iostream> // cout
int calculate(int a, int b, std::function<int(int,int)> binop) {
    return binop(a,b);
}
int plus(int a, int b) { return a+b; }
int times(int a, int b) { return a*b; }
int main() {
    std::cout << calculate(3, 4) << "\n"; // Output: 7
    std::cout << calculate(3, 4) << "\n"; // Output: 12
}
```

**Listing 23.13** Use the name of a suitable function as a function parameter.

That's all. The plus and times functions, instances of function<int(int, int)>, are passed to the function calculate() as parameters.

It is important that the signatures of the functions match. For example, you cannot use the negate function. The compiler complains with an error:

```
int negate(int a) { return -a; }
//
...
std::cout << calculate(3, 4, negate) << "\n"; // wrong signature
```