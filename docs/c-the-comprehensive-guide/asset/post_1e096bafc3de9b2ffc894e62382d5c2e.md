
Now, of course, the line with `n = 8` is gone, because otherwise you would be breaking your promise. The compiler would now find fault with this line, because you cannot assign anything to a `const int&`, which `n` now is. However, you can use a variable when calling `print_cref8(x)` or a literal `print_cref8(42)`. This means that the following two function declarations can be used equally broadly as far as the arguments are concerned:

```cpp
void print_val8(int n);        // Parameter as value
void print_cref8(const int& n); // Parameter as constant reference
```

### 7.5.4 Call as Value, Reference, or Constant Reference?

All these variants of declaring a parameter have their justification, and you have to decide which one to use on a case-by-case basis:

- When called *as a value*, a copy is created. This can be a time- and memory-consuming process at program runtime. On the other hand, you can be sure that you will not accidentally change any external values.
- When called *as a reference*, no copy is created, but the compiler transfers the address of the parameter into the function. This is quick and saves space. But do you really want to change externally defined variables? Sometimes, yes, but not always.
- Use a `const` reference if you decide for a reference but do not want to have the variable changed.
- If you use a *non-const reference*, you simply cannot pass some parameters, just as the literal `42` cannot be passed to an `int&`, for example. There are also constant values and objects, all of which you exclude with an & only parameter.

A disadvantage when using references (and pointers) can arise due to *aliasing*. There are cases in which a reference in a function refers to a variable (via an alias) that no longer exists; it has already become invalid outside. Program crashes are the result. As the parameter is copied specifically for the function call when it is called as a value, this cannot happen here.

One way to avoid these program crashes is to forego references. Because a typical application is the output parameter, I recommend that you use a return value instead:

```cpp
// https://godbolt.org/z/oh91YvaqT
#include <iostream>
void twice(double &num) {      // output parameter as modifiable reference
    num *= 2.0;
}

int main() {
    double num = 7.25;
    twice(num);
    std::cout << num << "\n";  // now 14.5
}
```

It may look silly in this simple example, but if you have larger objects, you'll be tempted to do this all the time. Write instead:

```cpp
// https://godbolt.org/z/q4ov41cny
#include <iostream>
double twice(double num) {      // value parameter and return value
    return num * 2.0;
}
int main() {
    double num = 7.25;
    num = twice(num);            // change expressed by return value
    std::cout << num << "\n";    // also 14.5
}
```

Here, the parameter number is copied when twice is called, but this makes the program safer and also clearer. The good news is that copying has improved since C++11, especially for data types from the standard library: values are now often moved instead of copied, which is always beneficial for performance.

> **When in Doubt, Use Value**
>
> If in doubt, opt for a value parameter. This must be copied when called; for large objects, you can consider whether a constant reference is more suitable.

## 7.6 Function Body

The really exciting thing about a function is, of course, what it does—because that's what a program is all about. I'm not telling you anything new here. You've already become familiar with main() as a function, and other functions are not much different.

Take a look at the functions in Listing 7.6. We will need them later, so let's examine how their function bodies are structured now.

```cpp
std::vector<int> primes = {};      // global variable
bool isPrime(int n) {              // own function
    for(int factor : primes) {     // access to global variable
        if(factor*factor > n)      // access to parameter
            return true;
        if(n%factor==0)
            return false;
    }
    return true;
}

void calculatePrimesUpTo(int limit) { // another custom function
    for(int n=3; n<limit; n=n+2) {
        if(isPrime(n)) {                 // use custom function
            primes.push_back(n);
        }
    }
}
```

**Listing 7.6** Various definitions of functions.

First comes the definition of the *isPrime* function. The function receives a parameter of type `int`, which is used within the function under the name *n*. However, variables other than the *n* parameter are used in the function body.

With `for(int factor=...)`, I introduce a new `int` variable for the for loop—a *local variable*. You already know that it is only visible within the `for` loop. You cannot access factor from another function.

I also use *primes* in the `for`—a *global variable*: this was declared outside the function and is “visible” within the function. You can access all global variables that were previously declared within this module. This is the case with *primes*.

The same applies to other functions: you can use other functions if they have been declared beforehand. This happens, for example, in `calculatePrimesUpTo` in the `if`: I call `isPrime`, and the compiler already knows the function because I defined it earlier (higher up in this module)—and a definition is even better than a declaration in this regard.

If for some reason I had written the function `isPrime` later in the program code, the compiler would not yet know it and would complain. However, I could remedy this by at least declaring the required function beforehand.

```cpp
// ... extract ...
bool isPrime(int n);                 // Declaration of function defined later
void calculatePrimesUpTo(int limit) {
    for(int n=3; n<limit; n=n+2) {
        if(isPrime(n)) {              // Use of function defined later
            primes.push_back(n);
        }
    }
}
bool isPrime(int n) {                 // Definition after usage
    // ... as before ...
}
```

**Listing 7.7** A forward declaration without a function body.

This is sometimes called a *forward declaration*.

When you combine a program from multiple modules (`*.cpp` files), you can also use functions from another module. In principle, you use exactly the forward declaration mechanism just explained: if you have defined a function f() in module A that you want to use in module B, then simply declare f identical at the beginning of module B, and the parts will come together when the entire program is linked.

However, this is only the first step toward the correct procedure. For the `*.cpp` file of module A, you also maintain a corresponding header file `*.h` that contains all function declarations that are potentially to be used elsewhere. Then, in module B, use an `#include` of this header file and effectively achieve the same result as with the manual forward declaration.

I will demonstrate this cleaner solution in [Chapter 12](#).

## 7.7 Converting Parameters

When a function receives a parameter with a certain type, there are several possibilities for this parameter when it is called. Let's assume you have declared the `func` function as follows:

```cpp
void func(double param);
```

Then the following can happen when you call it up:

- `func(5.3)` — **the type matches**  
  5.3 is a double literal and therefore exactly matches the parameter type double. The call works.
- `func("Text")` — **the type does not match**  
  Here, the call is attempted with a `const char[]`, which does not match double. This is an error that the compiler will inform you about.
- `func(7)` — **the type can be converted**  
  Although 7 is an int, it can be converted into a double by the compiler. The call works, but the compiler first converts 7 to 7.0.

For the built-in types, the compiler has some rules about which conversions it can perform. Here is a very brief overview:

- `int` to `long` or `short` to `int` is not a problem during conversion.
- `long` to `int` is also done by the compiler, but a dangerous overflow can occur here.
- `short`, `int`, or `long` can be converted to `float` or `double`, although large long numbers can lose a few digits of precision when converted to `float`.
- `float` or `double` can be converted to `short`, `int`, or `long`. However, the fractional parts are lost here, and an overflow can occur again if the numbers are too large.
