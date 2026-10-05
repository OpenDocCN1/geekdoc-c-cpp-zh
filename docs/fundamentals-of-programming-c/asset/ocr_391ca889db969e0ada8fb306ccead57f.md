# # Chapter 7

# Other Conditional and Iterative Statements

The if/else and while statements are sufficient to implement algorithms that involve conditional execution and looping. The break and continue statements are convenient but are not necessary. C++ provides some additional conditional and iterative statements that are more convenient to use in some circumstances. These additional statements include

+   - switch: an alternative to multi-way if/else statements
- the conditional operator: an expression that exhibits the behavior of an if/else
- do/while: a loop that checks its condition after its body is executed
- for: a loop convenient for counting

These alternate contain certain parts of algorithms to expressed more clearly and succinctly. This chapter explores these others of expressing conditional execution and iteration.

# ## 7.1 The Switch Statement

The switch provides a convenient alternative for multi-way if/else statements like the one in Listing 5.15(restlydigittow.cpp). Listing 7.1 (switchdigittow.cpp) is uses a switch statement instead of a multi-way if/else statement.

### Listing 7.1: switchdigittow.cpp
```cpp
#include <iostream>

using namespace std;

int main() {
    int value;
    cout << "Please enter an integer in the range 0...5: ";
```