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

# Summary

In this chapter, you learned how to define methods to implement a named block of code. You saw how to pass parameters into methods and how to return data from methods. You also saw how to call a method, pass arguments, and obtain a return value. You learned how to define overloaded methods with different parameter lists, and you saw how the scope of a variable determines where it can be accessed. Then, you used the Visual Studio 2015 debugger to step through code as it runs. Finally, you learned how to write methods that take optional parameters and how to call methods by using named parameters.

+   If you want to continue to the next chapter, keep Visual Studio 2015 running