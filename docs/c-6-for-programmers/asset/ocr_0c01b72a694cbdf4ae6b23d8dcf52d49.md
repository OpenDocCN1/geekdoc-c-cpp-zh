# 11.4.1 Creating and Using a CommissionEmployee Class

We begin with class CommissionEmployee (Fig. 11.4). The colon (:) followed by class name object in line 5 indicates that class CommissionEmployee extends (i.e., inherits from) class object (an alias for class Object in namespace System). You use inheritance to create classes from existing classes. Every class (except object) extends an existing class. Because class CommissionEmployee extends object, class CommissionEmployee inherits object's methods—or object has no fields. (Section 11.7 summarizes object's methods.) Every C# class directly or indirectly inherits object's methods. If a class does not specify that it inherits from another class, the new class implicitly inherits from object. For this reason, you typically do not include ':' object' in your code—we do so in this example, then not again in the book.

```
```csharp
// Fig. 11.4: CommissionEmployee.cs
// CommissionEmployee class represents a commission employee.
using System;

public class CommissionEmployee : object
{
    public string FirstName { get; }
    public string LastName { get; }
    public string SocialSecurityNumber { get; }
    private decimal grossSales; // gross weekly sales
    private decimal commissionRate; // commission percentage

    // five-parameter constructor
    public CommissionEmployee(string firstName, string lastName,
        string socialSecurityNumber, decimal grossSales,
        decimal commissionRate)
    {
        // implicit call to object constructor occurs here
        FirstName = firstName;
        LastName = lastName;
        SocialSecurityNumber = socialSecurityNumber;
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
        }
    }
```
```