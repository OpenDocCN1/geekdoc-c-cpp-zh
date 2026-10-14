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