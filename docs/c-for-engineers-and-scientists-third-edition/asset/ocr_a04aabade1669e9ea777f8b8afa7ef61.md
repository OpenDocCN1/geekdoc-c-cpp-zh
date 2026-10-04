# Modularity Functions

parameters and accomplish nothing with main()'s variables. A function as swap () can be written only by using a reference or some other means that provides access to main()'s variables. (This other means with pointers, the topic of Chapter 12.)

In using reference, two cautions need to be mentioned. First, reference parameters must be by reference (that is, they can't be used to change constants). For example, calling swap () with two literals, in the call swap(20.5, 6.5), passes two constants to the function. However swap () can execute, it doesn't change the values of these constants.

Second, a function call gives an indication that the return value will be by reference. In C++ this is done by reference rather than passes by reference, specifically limited to a called function(). This calling procedure should be adhered to whenever possible, which means reference parameters should be used only in restricted situations that require multiple return values, as in the swap () function in Program 6.10. The calc () function included in Program 6.9, although useful for illustration purposes, could be written as two separate functions, each returning a single value.

![](bbox=[0.105, 0.383, 0.163, 0.445])

# EXERCISES 6.3

+   1. (Practice) Write parameter declarations for the following:
   a. A parameter named *slope* that will be a reference to a double-precision value
   b. A parameter named *energy* that will be a reference to a double-precision number
   c. A parameter named *minutes* that will be a reference to an integer number
   d. A parameter named *key* that will be a reference to a character
   e. A parameter named *yield* that will be a reference to a double-precision number

+   2. (Practice) Three integer arguments are to be used in a call to a function named time()., assuming that time () accepts these variables as the reference parameters sec, min, and hours and returns value to its calling function.

+   3. (Modify) Rewrite the findMax() function in Program 6.5 so that the variable max, declared in main(), is used to store the maximum value of the two passed numbers. The value of max should be set from within findMax(Hint: A reference to max to be accepted by findMax().

+   4. (Practice) Write a function named *change* that has an integer parameter and integer reference parameters named *hundreds*, *ifties*, *twenties*, *tens*, *fives*, and *ones*. The function is to consider the passed integer value as a dollar amount and return the value into the fewest number of equivalent bills. Using the reference parameters, the function should alter the arguments in the calling function.

+   5. (Practice) Write a function named *time* that has an integer parameter seconds and three integer reference parameters hours, mins, and secs. The

> ¹³Most compilers catch this error.