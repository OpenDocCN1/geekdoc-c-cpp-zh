Listing 9.10 (primefunc.cpp) illustrates several important points about well-organized programs:

+   - The complete work of the program is no longer limited to the main function. The effort to test for primality is delegated to a separate function. main is focused on a simpler task: generating all the numbers to be considered and using another function (is_prime) to do the hard work of determining if a given number is prime. main is now simpler and more logically coherent. A function is coherent when it is focused on a single task. Coherence is a desirable property of functions. If a function becomes too complex by trying to do too many different things, it can be more difficult to write correctly and debug when problems are detected. A complex function should be decomposed into several, smaller, more coherent functions. The original function would then call these new simpler functions to accomplish its task. Here, main is not concerned about how to determine if a given number is prime; main simply delegates the work to is_prime and makes use of the is_prime function's findings.

+   - Each function is preceded by a thorough comment that describes the nature of the function. It explains the meaning of each parameter, and it indicates what the function should return. The comment for main may not be as thorough as for other functions; this is because main usually has no parameters, and it always returns a code to the operating system upon the program's termination.

+   - While the exterior comment indicates what the function is to do, comments within each function explain in more detail how the function accomplishes its task.

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

```
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