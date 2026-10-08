A function may return more than one value. When a function returns more than one value, they are returned through the parameters rather than the return statement. Any time a function returns more than one value through the parameters, the addresses of the variables receiving the values must be specified in the argument list of the calling function.

The communication between the calling function and the called function is through the arguments and parameters and through the return statement. Values can be passed between functions in two different ways:

+   - By value—in this case the arguments are copied into temporary locations and the function parameters access copies.
- By pointer—in this case the memory addresses of the arguments are passed to the function parameters and the function parameters access the values by dereferencing the addresses or using the addresses to store values.
- An input function normally receives memory addresses from the calling function so that the function can return the input values to the calling function by storing them directly into the argument addresses.
- An output function normally receives the data from the calling function by value. The data is passed by value so that the data is protected and cannot be altered.
- A function may receive some arguments by value and others by pointer.
- A return statement passes a value.

Recursive functions can be written in C. A recursive function is a function that calls itself. A recursive function is called by a parent function the first time, after which the function calls itself. A recursive function ultimately must return the control to the parent function under a specific condition. The specific condition is called a base condition. Several recursive functions are presented in this chapter and in later chapters.

# Exercises

+   1. Write a main function and the subfunctions that computes the tip speed of a propeller whose shaft speed S varies from 1000 to 10,000 rpm in increments of 1000. Pass the diameter D of the propeller to the function from the main.