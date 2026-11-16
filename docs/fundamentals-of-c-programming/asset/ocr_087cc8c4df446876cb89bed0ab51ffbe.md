```
#include <iostream>
/*
 * prompt requests an integer from the user and
 * keeps track of the cumulative number of entries.
 *
 * Returns the value entered by the user.
 */
int prompt() {
    static int count = 0;
    int value;
    std::cout << "Please enter integer #" << ++count << ": ";
    std::cin >> value;
    return value;
}

int main() {
    int value1, value2, sum;
    std::cout << "This program adds together two integers.\n";
    value1 = prompt(); // Call the function
    value2 = prompt(); // Call the function again
    sum = value1 + value2;
    std::cout << value1 << " + " << value2 << " = " << sum << "\n";
}
```

Listing 10.4 (promptwithstatic.cpp) behaves just like Listing 9.7 (evenbetterprompt.cpp) but in the new version main does not have to keep track of the number of user entries.

Local static variables were inherited from the C programming language, but their need has diminished with the introduction of objects in C++ (see Chapter 14). Functions with static variables provide a way to implement executable code with persistent state. Objects provide a more natural and more flexible way to achieve the same effect.

# 10.3 Overloaded Functions

In C++, a program can have multiple functions with the same name. When two or more functions within a program have the same name, the function is said to be overloaded. The functions must be different somehow, or else the compiler would not know how to associate a call with a particular function definition. The compiler identifies a function by more than its name; a function is uniquely identified by its signature. A function signature consists of the function's name and its parameter list. In the parameter list, only the types of the formal parameters are important, not their names. If the parameter types do not match exactly, both in number and position, then the function signatures are different. Consider the following overloaded functions:

+   1. void f() { /* ... */ }

This version has no parameters, so its signature differs from all the others which each have at least one parameter.

+   2. void f(int x) { /* ... */ }