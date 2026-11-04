
// three-parameter constructor
public Employee(string firstName, string lastName,
    string socialSecurityNumber)
{
    FirstName = firstName;
    LastName = lastName;
    SocialSecurityNumber = socialSecurityNumber;
}

// return string representation of Employee object, using properties
public override string ToString() => $"{FirstName} {LastName}\n" +
    $"social security number: {SocialSecurityNumber}";

// abstract method overridden by derived classes
public abstract decimal Earnings(); // no implementation here

Fig. 12.4 | Employee abstract base class. (Part 2 of 2.)

Why did we declare Earnings as an abstract method? As explained earlier, it simply does not make sense to provide an implementation of this method in class Employee. We cannot calculate the earnings for a general Employee—we first must know the specific Employee type to determine the appropriate earnings calculation. By declaring this method abstract, we indicate that each concrete derived class must provide an appropriate Earnings implementation and that an app will be able to use base-class Employee variables to invoke method Earnings polymorphically for any type of Employee.

## 12.5.2 Creating Concrete Derived Class SalariedEmployee

Class SalariedEmployee (Fig. 12.5) extends class Employee (line 5) and overrides Earnings (line 37), which makes SalariedEmployee a concrete class. The class includes a constructor (lines 10–15) that takes a first name, a last name, a social security number and a weekly salary as arguments; property WeeklySalary (lines 18–34) to manipulate instance variable weeklySalary, including a set accessor that ensures we assign only nonnegative values to weeklySalary; method Earnings (line 37) to calculate a SalariedEmployee’s earnings; and method ToString (lines 40–42), which returns a string including the employee’s type, namely, "salaried employee: ", followed by employee-specific information produced by base class Employee’s ToString method and SalariedEmployee’s weeklySalary property. Class SalariedEmployee’s constructor passes the first name, last name and social security number to the Employee constructor (line 12) via a constructor initializer to initialize the base class’s data. Method Earnings overrides Employee’s abstract method Earnings to provide a concrete implementation that returns the SalariedEmployee’s weekly salary. If we do not implement Earnings, class SalariedEmployee must be declared abstract—otherwise, a compilation error occurs (and, of course, we want SalariedEmployee to be a concrete class).

```csharp
if (value < 0) // validation
{
    throw new ArgumentOutOfRangeException(nameof(value),
        value, $"{nameof(Wage)} must be >= 0");
}

    wage = value;
}

// property that gets and sets hourly employee's hours
public decimal Hours
{
    get
    {
        return hours;
    }
    set
    {
        if (value < 0 || value > 168) // validation
        {
            throw new ArgumentOutOfRangeException(nameof(value),
                value, $"{nameof(Hours)} must be >= 0 and <= 168");
        }

        hours = value;
    }
}

// calculate earnings; override Employee's abstract method Earnings
public override decimal Earnings()
{
    if (Hours <= 40) // no overtime
    {
        return Wage * Hours;
    }
    else
    {
        return (40 * Wage) + ((Hours - 40) * Wage * 1.5M);
    }
}

// return string representation of HourlyEmployee object
public override string ToString() =>
    $"hourly employee: {base.ToString()}\n" +
    $"hourly wage: {Wage:C}\nhours worked: {Hours:F2}";
```

Fig. 12.6 | HourlyEmployee class that extends Employee. (Part 2 of 2.)

## 12.5.4 Creating Concrete Derived Class CommissionEmployee

Class CommissionEmployee (Fig. 12.7) extends class Employee (line 5). The class includes a constructor (lines 11–18) that takes a first name, a last name, a social security number, a sales amount and a commission rate; properties GrossSales and CommissionRate (lines 21–37 and 40–56) to manipulate instance variables grossSales and commissionRate, respectively; overridden method Earnings (line 59) to calculate a CommissionEmployee's earnings; and overridden method ToString (lines 62–65), which returns a CommissionEmployee's Employee's string representation. The constructor also passes the first name, last name and social security number to the Employee constructor (line 14) to initialize Employee's data. Method ToString calls base-class method ToString (line 63) to get the string representation of the Employee-specific information (i.e., first name, last name and social security number).

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
        decimal commissionRate) : base(firstName, lastName, socialSecurityNumber)
    {
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
    get
    {
        return commissionRate;
    }
    set
    {
        if (value <= 0 || value >= 1) // validation
        {
            throw new ArgumentOutOfRangeException(nameof(value),
                value, $"{nameof(CommissionRate)} must be > 0 and < 1");
        }

        commissionRate = value;
    }
    }

    // calculate earnings; override abstract method Earnings in Employee
    public override decimal Earnings() => CommissionRate * GrossSales;

    // return string representation of CommissionEmployee object
    public override string ToString() =>
        $"commission employee: {base.ToString()}\n" +
        $"gross sales: {GrossSales:C}\n" +
        $"commission rate: {CommissionRate:F2}";
}
```

Fig. 12.7 | CommissionEmployee class that extends Employee. (Part 2 of 2.)

## 12.5.5 Creating Indirect Concrete Derived Class BasePlusCommissionEmployee

Class BasePlusCommissionEmployee (Fig. 12.8) extends class CommissionEmployee (line 5) and therefore is an indirect derived class of class Employee. BasePlusCommissionEmployee has a constructor (lines 10–17) that takes as arguments a first name, a last name, a social security number, a sales amount, a commission rate and a base salary. It then passes the first name, last name, social security number, sales amount and commission rate to the CommissionEmployee constructor (lines 13–14) to initialize the base class’s data. BasePlusCommissionEmployee also contains property BaseSalary (lines 21–37) to manipulate instance variable baseSalary. Overridden method Earnings (line 40) calculates a BasePlusCommissionEmployee’s earnings, calling base class CommissionEmployee’s Earnings to calculate the commission-based portion of the BasePlusCommissionEmployee’s earnings. Again, this shows the benefits of code reuse. The overridden ToString method (lines 43–44) creates a string representation of a BasePlusCommissionEmployee that contains "base-salaried", followed by the string returned by base class CommissionEmployee’s ToString method (another example of code reuse), then the base salary. The result is a string beginning with "base-salaried commission employee", followed by the rest of the BasePlusCommissionEmployee’s information. Recall that CommissionEmployee’s ToString method obtains the employee’s first name, last name and social security number by invoking the ToString method of its base class (i.e., Employee)—a further demonstration of code reuse. BasePlusCommissionEmployee’s ToString initiates a chain of method calls that spans all three levels of the Employee hierarchy.
