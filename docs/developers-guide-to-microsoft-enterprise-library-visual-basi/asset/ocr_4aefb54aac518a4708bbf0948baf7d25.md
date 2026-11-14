# EDITING THE APPLICATION CODE TO USE THE NEW POLICY

Now you can update your exception handling code to use the new policy. You have two choices. If the configured exception policy does everything you need to do, you can actually remove the Try...Catch block completely from the method that may cause an error, and—instead—use the **Process** method of the **ExceptionManager** to execute the code within the method, as shown here.

```
Public Function GetWeeklySalary(ByVal employeeId As String, _
    ByVal weeks As Integer) As Decimal

    Dim employeeName As String = String.Empty
    Dim salary As Decimal = 0
    Dim weeklySalary As Decimal = 0

exManager.Process(Function() _
    Dim connString As String = ConfigurationManager.ConnectionStrings( _
        "EmployeeDatabase").ConnectionString _
    employeeName = "John Smith" _
    salary = 1000000 _
    weeklySalary = salary / weeks _
    End Function, _
    "ExceptionShielding")

    Return weeklySalary
End Function
```

The approach used above is only valid in Visual Basic if you are using version 10 and Visual Studio 2010. It is not valid in Visual Basic version 9 in Visual Studio 2008.

The body of your logic is placed inside a lambda function and passed to the **Process** method. If an exception occurs during the execution of the expression, it is caught and handled according to the configured policy. The name of the policy to execute is specified in the second parameter of the **Process** method.

Alternatively, you can use the **Process** method in your main code to call the method of your class. This is a useful approach if you want to perform exception shielding at the boundary of other classes or objects. If you do not need to return a value from the function or routine you execute, you can create any instance you need and work with it inside the lambda expression, as shown here.

```
exManager.Process(Function() _
    Dim calc As New SalaryCalculator() _
    Console.WriteLine("Result is: {0}", calc.GetWeeklySalary("jsmith", 0)) _
    End Function, _
    "ExceptionShielding")
```

The approach used above is only valid in Visual Basic if you are using Visual Studio 2010. It is not valid in Visual Basic in Visual Studio 2008.