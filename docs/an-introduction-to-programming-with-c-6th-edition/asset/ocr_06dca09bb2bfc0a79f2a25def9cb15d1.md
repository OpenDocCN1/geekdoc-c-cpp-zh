# CHAPTER 9 Value-Returning Functions

+   25. Desk-check the program using the same data used to desk-check the algorithm.

+   d. If necessary, create a new project named Advanced24 Project. Enter your C++ instructions into a source file named Advanced24.cpp. Also enter appropriate comments and additional instructions required by the compiler.

+   e. Save and then run the program. Test the program using the same data used to desk-check the program.

+   25. In this exercise, learn about using a default value for a formal parameter.

+   a. You can define a default value for one or more of the formal parameters. If a formal parameter has a default value, then you do not need to provide an argument for it when you call the function. Follow the instructions for starting C++ and opening the Advanced25.cpp file. The file is contained in either the Cpp6\Chap09 Project folder or Chap09 folder. The program uses a value-returning function to calculate a bonus amount. The bonus rate is based on the salesperson's code: either A or B. The user enters the bonus rate only for salespeople with an "A" code. Salespeople with a "B" code always receive 5%.

+   b. Define a default value for a formal parameter prototype, using the syntax formalParameterDataType=default. If the prototype also contains the parameter's name, use the syntax formalParameterDataType formalParameterName=default. Keep in mind that all parameters having a default value must be placed after those that do not have a default value in the function prototype. Change the function prototype so that it uses the number 05 as the default value for the bonus rate.

+   c. Save and run the program. Test the program appropriately.

+   26. Follow the instructions for starting C++ and opening SwatBugs26.cpp file. The file is contained in either the Cpp6\SwatBugs26 Project folder or the Cpp6\Chap09 folder. Debug the program.

# Answers to TRY THIS Exercises

# Pencil and Paper

+   1. double divideByTwo(int wholeNumber)

```
{
    return wholeNumber / 2;
} //end of divideByTwo function
```

+   2. double divideByTwo(int); or divideByTwo(int wholeNumber);