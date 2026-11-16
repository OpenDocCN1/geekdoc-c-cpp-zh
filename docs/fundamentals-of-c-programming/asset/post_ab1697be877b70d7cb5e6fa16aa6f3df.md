
```cpp
#include <iostream>

/*
 * increment(x)
 * Illustrates pass by value protocol.
 */
void increment(int x) {
    std::cout << "Beginning execution of increment, x = "
              << x << " \n";
    x++; // Increment x
    std::cout << "Ending execution of increment, x = "
              << x << " \n";
}

int main() {
    int x = 5;
    std::cout << "Before increment, x = " << x << " \n";
    increment(x);
    std::cout << "After increment, x = " << x << " \n";
}
```

For additional drama we chose to name the actual parameter the same as the formal parameter. Since the actual parameter and formal parameter are declared and used in different contexts and represent completely different memory locations, their names can be the same without any problems.

Listing 9.9 (passbyvalue.cpp) produces

```
Before increment, x = 5
Beginning execution of increment, x = 5
Ending execution of increment, x = 6
After increment, x = 5
```

The memory for the variable x in main is unaffected since increment works on a copy of the actual parameter.

C++ supports another way of passing parameters called pass by reference. Pass by reference is introduced in Section 10.9.

A function communicates its return value to the caller in the same way that the caller might pass a parameter by value. In the prompt function we saw earlier:

```cpp
int prompt(int n) {
    int result;
    std::cout << "Please enter integer # " << n << ": ";
    std::cin >> result;
    return result;
}
```

the return statement is

```
return result;
```

The variable result is local to prompt. We informally may say we are returning the result variable, but, in fact, we really are returning only the value of the result variable. The caller has no access to the local variables declared within any function it calls. In fact, the local variables for a function exist only when the function is active (that is, executing). When the function returns to its caller all of its local variables disappear from memory. During subsequent invocations, the function's local variables reappear when the function becomes active and disappear again when it finishes.

## 9.4 Function Examples

This section contains a number of examples of how we can use functions to organize a program's code.

### 9.4.1 Better Organized Prime Generator

Listing 9.10 (primefunc.cpp) is a simple enhancement of Listing 8.5 (moreefficientprimes.cpp). It uses the square root optimization and adds a separate is_prime function.

```cpp
Listing 9.10: primefunc.cpp

#include <iostream>
#include <cmath>

/*
 * is_prime(n)
 *  Determines the primality of a given value
 *  n an integer to test for primality
 *  Returns true if n is prime; otherwise, returns false
 */
bool is_prime(int n) {
    bool result = true;   // Provisionally, n is prime
    double root_n = sqrt(n);
    // Try all possible factors from 2 to the square
    // root of
    for (int trial_factor = 2;
         result && trial_factor <= root_n; trial_factor++)
        result = (n % trial_factor != 0);
    return result;
}

/*
 * main
 *  Tests for primality each integer from 2
 *  up to a value provided by the user.
 *  If an integer is prime, it prints it;
 *  otherwise, the number is not printed.
 */
int main() {
    int max_value;
    std::cout << "Display primes up to what value? ";
    std::cin >> max_value;
    for (int value = 2; value <= max_value; value++)
        if (is_prime(value)) // See if value is prime
            std::cout << value << " "; // Display the prime number
    std::cout << "\n"; // Move cursor down to next line
}
```

Listing 9.10 (primefunc.cpp) illustrates several important points about well-organized programs:

- The complete work of the program is no longer limited to the main function. The effort to test for primality is delegated to a separate function. main is focused on a simpler task: generating all the numbers to be considered and using another function (is_prime) to do the hard work of determining if a given number is prime. main is now simpler and more logically coherent. A function is coherent when it is focused on a single task. Coherence is a desirable property of functions. If a function becomes too complex by trying to do too many different things, it can be more difficult to write correctly and debug when problems are detected. A complex function should be decomposed into several, smaller, more coherent functions. The original function would then call these new simpler functions to accomplish its task. Here, main is not concerned about how to determine if a given number is prime; main simply delegates the work to is_prime and makes use of the is_prime function's findings.

- Each function is preceded by a thorough comment that describes the nature of the function. It explains the meaning of each parameter, and it indicates what the function should return. The comment for main may not be as thorough as for other functions; this is because main usually has no parameters, and it always returns a code to the operating system upon the program's termination.

- While the exterior comment indicates what the function is to do, comments within each function explain in more detail how the function accomplishes its task.

The call to is_prime returns true or false depending on the value passed to it. This means we can express a condition like

```
if (is_prime(value) == true) . . .
```

more compactly as

```
if (is_prime(value)) . . .
```

because if is_prime(value) is true, true == true is true, and if is_prime(value) is false, false == true is false. The expression is_prime(value) suffices.

Just as it is better for a loop to have exactly one entry point and exactly one exit point, preferably a function will have a single return statement. Simple functions with a small number of returns are generally tolerable, however. Consider the following version of is_prime:

```cpp
bool is_prime(int n) {
    for (int trialFactor = 2;
         trialFactor <= sqrt(static_cast<double>(n));
         trialFactor++)
        if (n % trialFactor == 0) // Is trialFactor a factor?
            return false; // Yes, return right away
    return true; // Tried them all, must be prime
}
```

This version uses two return statements, but eliminates the need for a local variable (result). Because a return statement exits the function immediately, no break statement is necessary. The two return statements are close enough textually in source code that the logic is fairly transparent.

### 9.4.2 Command Interpreter

Some functions are useful even if they accept no information from the caller and return no result. Listing 9.11 (calculator.cpp) uses such a function.

```cpp
Listing 9.11: calculator.cpp
#include <iostream>
#include <cmath>

/*
 * help_screen
 * Displays information about how the program works
 * Accepts no parameters
 * Returns nothing
 */
void help_screen() {
    std::cout << "Add: Adds two numbers\n";
    std::cout << "Example: a 2.5 8.0\n";
    std::cout << "Subtract: Subtracts two numbers\n";
    std::cout << "Example: s 10.5 8.0\n";
    std::cout << "Print: Displays the result of the latest operation\n";
    std::cout << "Example: p\n";
    std::cout << "Help: Displays this help screen\n";
    std::cout << "Example: h\n";
    std::cout << "Quit: Exits the program\n";
    std::cout << "Example: q\n";
}

/*
 * menu
 * Display a menu
 * Accepts no parameters
 * Returns the character entered by the user.
 */
char menu() {
    // Display a menu
    std::cout << "=== A)dd S)ubtract P)rint H)elp Q)uit ===\n";
    // Return the char entered by user
    char ch;
    std::cin >> ch;
    return ch;
}

/*
 * main
 * Runs a command loop that allows users to
 * perform simple arithmetic.
 */
int main() {
    double result = 0.0, arg1, arg2;
    bool done = false; // Initially not done
    do {
        switch (menu()) {
        case 'A': // Addition
case 'a':
    std::cin >> arg1 >> arg2;
    result = arg1 + arg2;
    std::cout << result << '\n';
    break;
case 'S': // Subtraction
case 's':
    std::cin >> arg1 >> arg2;
    result = arg1 - arg2;
    // Fall through, so it prints the result
case 'P': // Print result
case 'p':
    std::cout << result << '\n';
    break;
case 'H': // Display help screen
case 'h':
    help_screen();
    break;
case 'Q': // Quit the program
case 'q':
    done = true;
    break;
}
} while (!done);
}
```

The help_screen function needs no information from main, nor does it return a result. It behaves exactly the same way each time it is called. The menu function returns the character entered by the user.

### 9.4.3 Restricted Input

Listing 7.3 (betterinputonly.cpp) forces the user to enter a value within a specified range. We now can easily adapt that concept to a function. Listing 9.12 (betterinputfunc.cpp) uses a function named get_int_range that does not return until the user supplies a proper value.

```cpp
Listing 9.12: betterinputfunc.cpp

#include <iostream>

/*
 * get_int_range(first, last)
 *
 * Forces the user to enter an integer within a
 * specified range
 *
 * first is either a minimum or maximum acceptable value
 * last is the corresponding other end of the range,
 * either a maximum or minimum value
 * Returns an acceptable value from the user
 */
int get_int_range(int first, int last) {
    // If the larger number provided first,
    // switch the parameters
    if (first > last) {
        int temp = first;
```
