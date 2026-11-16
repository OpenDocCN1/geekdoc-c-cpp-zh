```
Listing 4.6: dividedanger.cpp

// File dividedanger.cpp
#include <iostream>
int main() {
   int dividend, divisor;
   // Get two integers from the user
   std::cout << "Please enter two integers to divide:";
   std::cin >> dividend >> divisor;
   // Divide them and report the result
   std::cout << dividend << " / " << divisor << " = "
      << dividend/divisor << '\n';
}
```

The expression dividend/divisor is potentially dangerous. If the user enters, for example, 32 and 4, the program works nicely

```
Please enter two integers to divide: 32 4
32/4 = 8
```

and displays the answer of 8. If the user instead types the numbers 32 and 0, the program reports an error and terminates. Division by zero is undefined in mathematics, and integer division by zero in C++ is illegal. When the program attempts the division at run time, the system detects the attempt and terminates the program.

This particular program can fail in other ways as well; for example, outside of the C++ world, 32.0 looks like a respectable integer. If the user types in 32.0 and 8, however, the program crashes because 32.0 is not a valid way to represent an integer in C++. When the compiler compiles the source line std::cin >> dividend >> divisor;

given that dividend has been declared to be an int, it generates slightly different machine language code than it would if dividend has been declared to be a double instead. The compiled code expects the text entered by the user to be digits with no extra decoration. Any deviation from this expectation results in a run-time error. Similar results occur if the user enters text that does not represent an integer, like fred.

Observe that in either case—entry of a valid but inappropriate integer (zero) or entry of a non-integer (32.0 or fred)—it is impossible for the compiler to check for these problems at compile time. The compiler cannot predict what the user will enter when the program is run. This means it is up to the programmer to write code that can handle bad input that the user may provide. As we continue our exploration of programming in C++, we will discover ways to make our programs more robust against user input (see Listing 5.3 (betterdivision.cpp) in Chapter 5, for example). The solution involves changing the way the program runs depending on the actual input provided by the user.

# 4.6.3 Logic Errors

Consider the effects of replacing the expression