a sales amount and a commission rate; properties GrossSales and CommissionRate (lines 21–37 and 40–56) to manipulate instance variables grossSales and commissionRate, respectively; overridden method Earnings (line 59) to calculate a CommissionEmployee's earnings; and overridden method ToString (lines 62–65), which returns a CommissionEmployee's Employee's string representation. The constructor also passes the first name, last name and social security number to the Employee constructor (line 14) to initialize Employee's data. Method ToString calls base-class method ToString (line 63) to get the string representation of the Employee-specific information (i.e., first name, last name and social security number).

```
```csharp
// Fig. 12.7: CommissionEmployee.cs
// CommissionEmployee class that extends Employee.
using System;

public class CommissionEmployee : Employee
{
    private decimal grossSales; // gross weekly sales
    private decimal commissionRate; // commission percentage

    // five-parameter constructor
    public CommissionEmployee(string firstName, string lastName,
        string socialSecurityNumber, decimal grossSales,
        decimal commissionRate)
    {
        : base(firstName, lastName, socialSecurityNumber)

        GrossSales = grossSales; // validates gross sales
        CommissionRate = commissionRate; // validates commission rate
    }

    // property that gets and sets commission employee's gross sales
    public decimal GrossSales
    {
        get
        {
            return grossSales;
        }
        set
        {
            if (value < 0) // validation
            {
                throw new ArgumentOutOfRangeException(nameof(value),
                    value, $"{nameof(GrossSales)} must be >= 0");
            }

            grossSales = value;
        }
    }

    // property that gets and sets commission employee's commission rate
    public decimal CommissionRate
    {
```
```