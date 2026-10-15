```
```csharp
class Program
{
    static void Main(string[] args)
    {
        int monthlyWage = 1234;
        int months = 12, bonus = 1000;

        bool isActive = true;
        double rating = 99.25;

        double ratePerHour = 12.34;
        int numberOfHoursWorked = 165;

        long veryLongMonth = numberOfHoursWorked;

        double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

        //Console.WriteLine(currentMonthWage);

        ratePerHour += 3;//ratePerHour = ratePerHour + 3;

        if (currentMonthWage > 2000)
        {
            //Console.WriteLine("Top paid employee");
        }
    }
}
```
```

Say that I create a long variable. Variables of the long type can contain a much larger value than integers can, so I can actually say that I'm going to create a variable, veryLongMonth, and I'm going to assign to that the numberOfHoursWorked. So I'm now converting the numberOfHoursWorked into a long.