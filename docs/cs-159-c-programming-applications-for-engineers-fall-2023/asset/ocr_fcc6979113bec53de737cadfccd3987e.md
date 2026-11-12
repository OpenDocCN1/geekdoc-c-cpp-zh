Note: Calling a function is different than an iteration of a loop where the same code inside of the loop is being executed repeatedly. Each function call is independent of other function calls with local variables occupying unique memory locations.

# Review of Repetition Constructs and Techniques

# Limitations of Recursion

In the factorial example we saw that calculating 4! required four function calls, in each function call a unique set of variables is created and the status of each function needs to be "remembered" in order to continue after the called function terminates. A large number of function calls can require more memory than the computer is capable of providing.

# When should you NOT use recursion?

+   - When the number of recursive function calls has the potential to be large (counter-controlled) or unpredictable (event-controlled).