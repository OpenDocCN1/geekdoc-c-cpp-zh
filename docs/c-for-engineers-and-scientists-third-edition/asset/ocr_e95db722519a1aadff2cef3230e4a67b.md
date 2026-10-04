# 274 Repetition Statements

Program 5.16

```
#include <iostream>
#include <iomanip>
using namespace std;

// this program displays a table of numbers with their squares and cubes,
// starting from the number 1. The final number in the table is
// input by the user.

int main() {
    int num, final;

    cout << "Enter the final number for the table: ";
    cin >> final;

    cout << "NUMBER SQUARE CUBE\n";
    cout << "--------------------------------------\n";

    for (num = 1; num <= final; num++) {
        cout << setw(3) << num
             << setw(8) << num*num
             << setw(7) << num*num*num << endl;
    }

    return 0;
}
```

In Program 5.16, a variable is used in the for statement to control the condition (middle) expression. A cin has been placed before the loop to allow the user to decide what the final value should be. Notice that this arrangement permits the user to set the table's size at runtime, instead of having it set at compile time. This arrangement makes the program more general because it can be used to create a variety of tables without the need for reprogramming and recompiling.

# EXERCISES 5.5

+   1. (cin within a loop) Write and run a C++ program that accepts six Fahrenheit temperatures, one at a time, and converts each value entered to its Celsius equivalent before the next value is requested. Use a for loop in your program. The conversion required is Celsius = (5.0/9.0) x (Fahrenheit - 32).