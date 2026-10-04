You've used functions that take one parameter, more than one parameter, and even no parameters. You can specify each situation—one parameter, multiple parameters, or no parameters—in function header. You have already defined a function, word_count, that takes a single parameter, a string.

If you have multiple parameters, you just separate the parameters with commas. Each of the parameters is defined the same way an individual parameter would be. But note that each parameter needs both a type and a name.

To define a function that has no parameters, you put nothing between the parentheses.

Sometimes you don't need a function to return anything; it just to do something on its own and not return a type of any sort. In this case, you can specify a different return type, called void.

When a program is compiled, the function definition should occur in the program before the function is actually called. Typically, functions are defined near the beginning of the file. You write the function definitions, and later you can make calls to that function. When the compiler comes along and encounters it sees a function name, with some arguments of various types, and it matches up to the function with that name and parameters.

Actually, it's slightly more complicated; all the compiler needs to know at first is the function header. In fact, there are ways you can give just the function header information and put the body of the function elsewhere. You'll learn more about this in lecture 15.

# Exercise 1

> For each of the following situations, what would the return type be?

+   1 A function that tells you whether a certain set of measurements indicates danger or not.
2 A function that prints out a warning message if there is danger.
3 A function that computes the recommended dosage of a medicine given a person's age and weight.
4 A function that will get a person's address by reading it from a file.

![](bbox=[0.547, 0.506, 0.735, 0.532])

# Exercise 2

> Imagine that you want a function to calculate how many days is it until the next leap year day, February 29. How you write the function header for such a function?

![](bbox=[0.547, 0.786, 0.735, 0.812])