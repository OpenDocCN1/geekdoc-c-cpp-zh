Table 11-1 uses the term thrown, which is explained later in this chapter.

Most exceptions you will use derive from three classes:

+   * The predefined Common Language Runtime exception classes derived from SystemException
* The user-defined application exception classes you derive from ApplicationException
* The Exception class, which is the parent of SystemException and ApplicationException

> Microsoft previously advised that you should create your own custom exceptions from the ApplicationException class. The company has revised its thinking and now advise that you should use the Exception class as a base in practice, it has not found the previous approach to be of value. For updates, visit http://msdn.microsoft.com.

# # Purposefully Generating a SystemException

You can deliberately generate a SystemException by forcing a program to contain an error. As an example, in every programming language, it is illegal to divide an integer by zero because the operation is mathematically undefined. Consider the MilesPerGallon program in Figure 11-1, which prompts a user for two values and divides the first by the second. If the user enters nonzero integers, the program runs correctly and without incident. However, if the user enters 0 when prompted to enter gallons, division by 0 takes place, and an error is generated. Figure 11-2 shows two executions of the program.

> When you divide a floating-point value by 0 in C#, no exception occurs. Instead, C assigns the special Infinity to the result. Because floats and doubles are imprecise, dividing them by 0.000000... to an infinite number of decimal places approaches infinity mathematically.