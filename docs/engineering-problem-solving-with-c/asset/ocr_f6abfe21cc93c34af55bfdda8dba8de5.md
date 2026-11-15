![](bbox=[0.15, 0.08, 0.9, 0.66])

Figure 6.1 Example structure chart.

library function
programmer-defined functions

must be defined in the file containing the main function or in another available file or library of files. (If the function is included in a system library file, such as the sqrt function, it is often called a library function; other functions are usually called programmer-written, or programmer-defined, functions.) After executing the statements in a function, the program execution continues with the statement that called the function.

Consider the simple task of converting from degrees Celsius to degrees Fahrenheit. We can write a programmer defined function to perform this calculation, and call the function from any program solution that requires this conversion. Our conversion function will have one input parameter, a temperature in degrees Celsius, and will return the equivalent temperature in degrees Fahrenheit. To illustrate, we will write a program solution that reads temperatures in degrees Celsius from an input file and writes the degrees Fahrenheit to an output file. The