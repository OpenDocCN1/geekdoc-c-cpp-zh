```
static void Main(string[] args)
{
    int monthlyWage = 1234;
    int months = 12, bonus = 1000;

    bool isActive = true;
    double rating = 99.25;

    double ratePerHour = 12.34;
    int numberOfHoursWorked = 165;

    double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

    Console.WriteLine(currentMonthWage);

    ratePerHour += 3;//ratePerHour = ratePerHour + 3;

    if (currentMonthWage > 2000)
    {
        Console.WriteLine("Top paid employee");
    }

    int numberOfEmployees = 15;
    numberOfEmployees--;

    bool a;
    int b;

    Console.ReadLine();
}
```

Automatically, each type has its default value, and for a Boolean that will be false and for an integer that will be 0. Each of these primitive types comes with the default value built in and it's assigned if we do not assign a value. We've now seen how we can perform very simple operations, but there's so much more we can do with data types.

```
int intMaxValue = int.MaxValue;

int intMinValue = int.MinValue;

double doubleMaxValue = double.MaxValue;
```