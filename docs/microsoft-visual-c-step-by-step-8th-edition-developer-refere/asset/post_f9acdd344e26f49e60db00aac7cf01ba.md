
```
private double calculateFee(double dailyRate = 500.0, int noOfDays = 1)
{
    Console.WriteLine("calculateFee using two optional parameters");
    return dailyRate * noOfDays;
}
```

4. Add another implementation of the calculateFee method to the Program class, as shown in the code below. This version takes one optional parameter, called dailyRate, of type double. The body of the method calculates and returns the fee for a single day only.

Click here to view code image

```
private double calculateFee(double dailyRate = 500.0)
{
    Console.WriteLine("calculateFee using one optional parameter");
    
    int defaultNoOfDays = 1;
    return dailyRate * defaultNoOfDays;
}
```

5. Add a third implementation of the calculateFee method to the Program class. This version takes no parameters and uses hardcoded values for the daily rate and number of days.

Click here to view code image

```
private double calculateFee()
{
    Console.WriteLine("calculateFee using hardcoded values");
    double defaultDailyRate = 400.0;
    int defaultNoOfDays = 1;
    return defaultDailyRate * defaultNoOfDays;
}
```

6. In the run method, add the following statements in bold that call calculateFee and display the results:

Click here to view code image

```
public void run()
{
    double fee = calculateFee();
    Console.WriteLine($"Fee is {fee}");
}
```

## Tip

You can quickly view the definition of a method from the statement that invokes it. To do so, right-click the method call and then click Peek Definition. The following image shows the Peek Definition window for the calculateFee method.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_125_0.png)

This feature is extremely useful if your code is split across multiple files, or even if it is in the same file but the file is very long.

7. On the Debug menu, click Start Without Debugging to build and run the program.

The program runs in a console window and displays the following messages:

Click here to view code image

```
calculateFee using hardcoded values
Fee is 400
```

The run method called the version of calculateFee that takes no parameters rather than either of the implementations that take optional parameters because that version most closely matches the method call.

Press any key to close the console window and return to Visual Studio.

8. In the run method, modify the statement that calls calculateFee to match the code shown in bold here:

Click here to view code image

```
public void run()
{
    double fee = calculateFee(650.0);
    Console.WriteLine($"Fee is {fee}");
}
```

9. On the Debug menu, click Start Without Debugging to build and run the program.

The program displays the following messages:

Click here to view code image

```
calculateFee using one optional parameter
Fee is 650
```

This time, the run method called the version of calculateFee that takes one optional parameter. As before, this is the version that most closely matches the method call.

Press any key to close the console window and return to Visual Studio.

10. In the run method, modify the statement that calls calculateFee again:

Click here to view code image

```
public void run()
{
    double fee = calculateFee(500.0, 3);
    Console.WriteLine($"Fee is {fee}");
}
```

11. On the Debug menu, click Start Without Debugging to build and run the program.

The program displays the following messages:

Click here to view code image

```
calculateFee using two optional parameters
Fee is 1500
```

As you might expect from the previous two cases, the run method called the version of calculateFee that takes two optional parameters.

Press any key to close the console window and return to Visual Studio.

12. In the run method, modify the statement that calls calculateFee and specify the dailyRate parameter by name:

Click here to view code image

```
public void run()
{
    double fee = calculateFee(dailyRate : 375.0);
    Console.WriteLine($"Fee is {fee}");
}
```

13. On the Debug menu, click Start Without Debugging to build and run the program.
The program displays the following messages:

Click here to view code image

```
calculateFee using one optional parameter
Fee is 375
```

As earlier, the run method calls the version of calculateFee that takes one optional parameter. Changing the code to use a named argument does not change the way in which the compiler resolves the method call in this example.
Press any key to close the console window and return to Visual Studio.

14. In the run method, modify the statement that calls calculateFee and specify the noOfDays parameter by name.

Click here to view code image

```
public void run()
{
    double fee = calculateFee(noOfDays : 4);
    Console.WriteLine($"Fee is {fee}");
}
```

15. On the Debug menu, click Start Without Debugging to build and run the program.
The program displays the following messages:

Click here to view code image

```
calculateFee using two optional parameters
Fee is 2000
```

This time, the run method called the version of calculateFee that takes two optional parameters. The method call has omitted the first parameter (dailyRate) and specified the second parameter by name. The version of the calculateFee method that takes two optional parameters is the only one that matches the call.
Press any key to close the console window and return to Visual Studio.

16. Modify the implementation of the calculateFee method that takes two optional parameters. Change the name of the first parameter to theDailyRate and update the return statement to match that shown in bold in the following code:

Click here to view code image

```
private double calculateFee(double theDailyRate = 500.0, int noOfDays = 1)
{
```

```
Console.WriteLine("calculateFee using two optional parameters");
    return theDailyRate * noOfDays;
}
```

17. In the run method, modify the statement that calls calculateFee and specify the theDailyRate parameter by name.

Click here to view code image

```
public void run()
{
    double fee = calculateFee(theDailyRate : 375.0);
    Console.WriteLine("Fee is {fee}");
}
```

18. On the Debug menu, click Start Without Debugging to build and run the program.

The program displays the following messages:

Click here to view code image

```
calculateFee using two optional parameters
Fee is 375
```

The previous time that you specified the fee but not the daily rate (step 12), the run method called the version of calculateFee that takes one optional parameter. This time, the run method called the version of calculateFee that takes two optional parameters. In this case, using a named argument has changed the way in which the compiler resolves the method call. If you specify a named argument, the compiler compares the argument name to the names of the parameters specified in the method declarations and selects the method that has a parameter with a matching name. If you had specified the argument as aDailyRate: 375.0 in the call to the calculateFee method, the program would have failed to compile because no version of the method has a parameter that matches this name.

Press any key to close the console window and return to Visual Studio.

## Summary

In this chapter, you learned how to define methods to implement a named block of code. You saw how to pass parameters into methods and how to return data from methods. You also saw how to call a method, pass arguments, and obtain a return value. You learned how to define overloaded methods with different parameter lists, and you saw how the scope of a variable determines where it can be accessed. Then, you used the Visual Studio 2015 debugger to step through code as it runs. Finally, you learned how to write methods that take optional parameters and how to call methods by using named parameters.

- If you want to continue to the next chapter, keep Visual Studio 2015 running
and turn to Chapter 4, “Using decision statements.”

- If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Declare a method | Write the method within a class. Specify the method name, parameter list, and return type, followed by the body of the method between braces. For example:
```
int addValues(int leftHandSide, int rightHandSide)
{
...
}
``` |
| Return a value from within a method | Write a return statement within the method. For example:
```
return leftHandSide + rightHandSide;
``` |
| Return from a method before the end of the method | Write a return statement within the method. For example:
```
return;
``` |
| Define an expression-bodied method | Use the => sequence followed by the expression that defines the body of the method and a closing semicolon. For example:
```
double calculateFee(double dailyRate, int noOfDays)
=> dailyRate * noOfDays;
``` |
| Call a method | Write the name of the method followed by any arguments between parentheses. For example:
```
addValues(39, 3);
``` |
| Use the Generate Method Stub Wizard | Right-click a call to the method, and then click Generate Method Stub. |
| Display the Debug toolbar | On the View menu, point to Toolbars, and then click Debug. |
| Step into a method | On the Debug toolbar, click Step Into.
or
On the Debug menu, click Step Into. |
| Step out of a method | On the Debug toolbar, click Step Out.
or
On the Debug menu, click Step Out. |
| Specify an optional parameter to a method | Provide a default value for the parameter in the method declaration. For example:
```
void optMethod(int first, double second = 0.0,
    string third = "Hello")
{
...
}
``` |
| Pass a method argument as a named parameter | Specify the name of the parameter in the method call. For example:
```
optMethod(first : 100, third : "World");
``` |
