11. (Numerical) A useful function with no parameters can be constructed to return a value for $\pi$ that's accurate to the maximum number of decimal places your computer allows. This value is obtained by taking the arcsine of 1.0, which is $\pi/2$, and multiplying the result by 2. In C++, the required expression is $2.0 * asin(1.0)$; the $asin()$ function is provided in the standard C++ mathematics library.(Remember to include cmath in your preprocessor directives). Using this expression, a C++ function named $pi()$ that calculates and displays the value of $\pi$. (In the next section, you will see how to return this value to the calling function.)

12. (Practice) a. Write a function template $display()$ that returns the value of the single argument passed to it when the function is called.

+   - Include the function template created in Exercise 12a in a complete C++ program that calls the function three times: once with a character argument, once with an integer argument, and once with a double-precision argument

13. (Numerical) a. Write a function template named $hole()$ that returns the value of any argument passed to it when the function is called.

+   - Include the function template created in Exercise 13a in a complete C++ program that calls the function three times: once with a character argument, once with an integer argument, and once with a double-precision argument

14. (Numerical) a. Write a function template named $maximum()$ that returns the maximum value of three arguments passed to the function when it is called. Assume that all three arguments are the same data type.

+   - Include the function template created in Exercise 14a in a complete C++ program that calls the function with three integers and then with double-precision numbers

15. (Numerical) a. Write a function template named $square()$ that computes and returns the square of the single argument passed to the function when it's called.

+   - Include the function template created for Exercise 15a in a complete C++ program.

# 6.2 Returning a Single Value

Using the method of passing data to a function explained in the previous section, the called function receives only copies of the values contained in arguments at the time of the call.(Review Figure 6.3 if it's unclear to you.) When a value is passed to a called function the passed is referred to as **passed by value** and is a distinct advantage of C++.The calling function does not have direct access to the variables used by arguments calling the function, it cannot inadvertently alter the value stored in one of these variables.

The function receiving the passed by value arguments can send the values it wants to in its fashion and return one, and only one, "legitimate" value directly to the calling function (see Figure 6.6). In this section, you will see how this value is returned to the calling function. As you