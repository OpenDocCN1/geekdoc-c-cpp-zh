# Chapter 7

# Other Conditional and Iterative Statements

The if/else and while statements are sufficient to implement any algorithms that involve conditional execution and looping. The break and continue statements are convenient but are not necessary. C++ provides some additional conditional and iterative statements that are more convenient to use in some circumstances. These additional statements include

+   - switch: an alternative to some multi-way if/else statements
+   - the conditional operator: an expression that exhibits the behavior of an if/else statement
+   - do/while: a loop that checks its condition after its body is executed
+   - for: a loop convenient for counting

These alternate constructs allow certain parts of algorithms to expressed more clearly and succinctly. This chapter explores these other forms of expressing conditional execution and iteration.

# 7.1 The switch Statement

The switch statement provides a convenient alternative for some multi-way if/else statements like the one in Listing 5.16 (restyleddigititoword.cpp). Listing 7.1 (switchdigititoword.cpp) is a new implementation of Listing 5.16 (restyleddigititoword.cpp) that uses a switch statement instead of a multi-way if/else statement.

```
Listing 7.1: switchdigititoword.cpp
#include <iostream>
int main() {
    int value;
    std::cout << "Please enter an integer in the range 0..5: ";
    std::cin >> value;
    switch (value) {
```