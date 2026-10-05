18. On the **Debug** menu, select **Without Debugging** to build and run the program.

The program displays the following messages:

Click here to view code image

```
calculateFee using two optional parameters
Fee is 2000
```

This time, the **run** method called the version of `calculateFee` that takes two optional parameters. The method call has omitted first parameter `dailyRate` and specified the second parameter by name. The version of the `calculateFee` method that takes two optional parameters is the only one that matches the call.

19. Press any key to close the console window and return to Visual Studio.

20. Modify the `calculateFee` method that takes two optional parameters. Change the name of the first parameter to `theDailyRate` and update the `return` statement to match that shown in bold in the following code:

Click here to view code image

```
private double calculateFee(double theDailyRate = 500.0, int noOfDays = 1)
{
    Console.WriteLine("calculateFee using two optional parameters");
    return theDailyRate * noOfDays;
}
```

21. In the **run** method, modify the statement that `calculateFee` and specify the `theDailyRate` parameter by name.

Click here to view code image

```
public void run()
{
```