# # Chapter 6

# # Iteration

Iteration repeats the execution of a sequence of code. Iteration is useful for solving many programming problems. Iteration and conditional execution are key components of algorithm construction.

# ## 6.1 The while Statement

Listing 6.1: countoftive.cpp counts to five by printing a number on each output line.

Listing 6.1: countoftive.cpp
```cpp
#include <iostream>
using namespace std;

int main() {
  cout << 1 << endl;
  cout << 2 << endl;
  cout << 3 << endl;
  cout << 4 << endl;
  cout << 5 << endl;
}
```

When compiled and run, this program displays

![](bbox=[0.202, 0.737, 0.848, 0.853])

How would you write the code to count to 10,000? Would you copy, paste, and modify 10,000 printing statements? You could, but that would be impractical! Counting is such a common activity, and computers