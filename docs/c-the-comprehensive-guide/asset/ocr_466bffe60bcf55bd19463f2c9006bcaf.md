But what happens if several operators of the same precedence are next to each other? In expressions such as 10-5-2, the left - is evaluated first because - is *left-associative* — as if the expression ((10-5)-3) were in parentheses. The result is therefore 2. All binary arithmetic, Boolean, and comparative operators are left-associative, so you can intuitively calculate with them. Sometimes this is also called *left-to-right associative* or *LR-associative*.

The group of assignment operators, in turn, is consistently *right-associative*, which is why the compiler for `x += y += z += 1` executes `(x += (y += (z += 1)))` as expected and first increments `z` by 1 in order to then deal with the other variables one after the other. If the expression were evaluated as `(((x += y) += z) += 1)`, then `x` would receive a new value several times because `x += y` also returns `x`, and then `+= z` would be executed; `y` would not be changed. And `x` would be returned once again, and `+= 1` would increment it by 1 instead of increasing `z`.

Most of the time, precedence and associativity work intuitively and as expected. If in doubt, it is better to bracket as later readers will probably ask themselves the same questions as you.

# ## 4.4 Built-In Data Types

So far you have only learned about types in a flyover—and around them, just as much fundamental C++ as was necessary to understand them.

This section builds on these basics. You now know enough about the language to understand the comprehensive explanations of all the built-in types.

In this section, you will learn which data types are available to you in C++ if you do not use `#include` in your program or do not use the *standard library*. What are the *built-in data types*, and what can you do with them?

Pay attention to the types of variables and function parameters in the following example.

```
```cpp
// https://godbolt.org/z/MPPsbdq9c
#include <iostream> // cin, cout for input and output

void input(unsigned &birthDay_,
           unsigned &birthMonth_,
           unsigned &birthYear_,
           unsigned long long &taxnumber_,
           double &bodyheight_)
{
    /* Inputs still without good error handling... */
    std::cout << "Date of birth: "; std::cin >> birthDay_;
    std::cout << "Month of birth: "; std::cin >> birthMonth_;
```
```