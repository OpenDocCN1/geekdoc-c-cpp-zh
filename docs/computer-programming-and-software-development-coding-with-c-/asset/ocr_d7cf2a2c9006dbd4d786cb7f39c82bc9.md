```
```csharp
public double ReceiveWage()
{
    double wageBeforeTax = NumberOfHoursWorked * HourlyRate.Value;
    double taxAmount = wageBeforeTax * taxRate;

    Wage = wageBeforeTax - taxAmount;

    Console.WriteLine($"The wage for {NumberOfHoursWorked} hours of work is {Wage}.");
    NumberOfHoursWorked = 0;

    return Wage;
}

public void DisplayEmployeeDetails()
{
    Console.WriteLine($"\nFirst name: {FirstName}\nLast name: {LastName}\nEmail: {Email}\nBirthday: {BirthDay.ToShortDateString()}\n");
}
```
```

This method is now available. It's now known, let's say, on the Manager class as well. And in a very similar way, we can also ask to perform work. We can also invoke the ReceiveWage method. And if you run this, we will see that Bethany has performed some work, and we see the details for Mary. Mary has done some work, and now Mary receives a wage. You may be thinking at this point, well, that's fine, but what is the added value? Mary can do the exact same things as Bethany, our employee, so the manager is not really different from the employee at this point. Correct, but I can now extend my Manager type. I can add things here on the Manager class that are not available on the employee. What does a manager do? Well, for example, an added functionality wrapped inside of a method, that is, is attending a management meeting. So it could be that our manager needs to perform an action that is not available for an employee such as attending a management meeting. Management meetings tend to run very long, so I'm going to increase the number of hours worked with 10. By doing that, I've introduced something that you may not have noticed yet. The