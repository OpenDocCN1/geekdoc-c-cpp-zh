# 9.4. FUNCTION EXAMPLES

```
/*
 * main
 * Tests for primality each integer from 2
 * up to a value provided by the user.
 * If an integer is prime, it prints it;
 * otherwise, the number is not printed.
 */
int main(
    int max_value;
    cout << "Display primes up to what value? ";
    cin >> max_value;
    for (int value = 2; value <= max_value; value++)
        if (is_prime(value)) // See if value is prime
            cout << value << " "; // Display the prime number
    cout << endl; // Move down to next line
}
```

Listing 9.9 (prime.cpp) illustrates several important points about well-organized programs:
The test for primality is delegated to a separate function: **main** is focused on a simpler task: generating all the numbers to be considered and using another function (**is_prime**) to do the work of determining if a given number is prime. **main** is now simpler and more logically coherent. A function is coherent when it focuses on a single task. Coherence is a desirable property of functions. A function becomes complex by trying to do many things, it is more difficult to write correctly and debug when problems are detected. A complex function should be decomposed into several, more coherent functions. The original function would then call these simpler functions to accomplish its task. **Main** is not concerned about how to determine if a given number is prime; it simply delegates the work to **is_prime** and makes use of the **is_prime** function's findings.

Each function is preceded by a comment that describes the nature of the function. It explains the meaning of each parameter, and it indicates what the function should return. The comment for **main** may not be as thorough as for others functions; because **main** usually has no parameters, and it always returns a code to the operating system upon the program's termination.

While the exterior comment indicates what the function is to do, comments within each function explain in detail how the function accomplishes its task.

The call to **is_prime** return true or false depending on the value passed to it. The means a condition like

```
if (is_prime(value) == true) . . .
```

can be expressed more compactly as

```
if (is_prime(value)) . . .
```

because **is_prime(value)** is true, true ~ == true is true, and if **is_prime(value)** is false, false ~ == true is false. The expression **is_prime(value)** suffices.

Just as it is better for a loop to have exactly one entry and exactly one exit, preferably a function will have a small **return** statement. Simple functions with a small number of **returns** are generally tolerable, however. Consider the following version of **is_prime**: