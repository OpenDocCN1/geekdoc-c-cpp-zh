# 11.4 Relationship between Base Classes and Derived Classes 489

```
// display BasePlusCommissionEmployee's data
Console.WriteLine("nEmployee information obtained by properties and methods: \n");
Console.WriteLine($"First name is {employee.FirstName}");
Console.WriteLine($"Last name is {employee.LastName}");
Console.WriteLine(");
Console.WriteLine($"Social security number is {employee.SocialSecurityNumber}");
Console.WriteLine($"Gross sales are {employee.GrossSales:C}");
Console.WriteLine(");
Console.WriteLine($"Commission rate is {employee.CommissionRate:F2}");
Console.WriteLine($"Earnings are {employee.Earnings:C}");
Console.WriteLine($"Base salary is {employee.BaseSalary:C}");

employee.BaseSalary = 1000.00M; // set base salary

Console.WriteLine("\nUpdated employee information obtained by ToString:\n");
Console.WriteLine(employee);
Console.WriteLine($"earnings: {employee.Earnings:C}");

})
```

Employee information obtained by properties and methods:

First name is Bob
Last name is Lewis
Social security number is 33-33-3333
Gross sales are $5,000.00
Commission rate is 0.04
Earnings are $500.00
Base salary is $300.00

Updated employee information obtained by ToString:

base-serialized commission employee: Bob Lewis
social security number: 33-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $1,000.00
earnings: $1,200.00

> Fig. 11.7 Testing class BasePlusCommissionEmployee.(Part 2 of 2.)

Code Duplication
Much of the code for class BasePlusCommissionEmployee (Fig. 11.6) is similar, or identical,
to that of class CommissionEmployee (Fig. 11.4). For example, in class BaseCommissionEmployee, FirstName, LastName and SocialSecurityNumber are identical
to those of class CommissionEmployee. Classes CommissionEmployee and BaseCommissionEmployee also contain private instance variables commissionRate and grossSales, as well as properties to manipulate these variables. In addition, the BasePlusCommissionEmployee constructor is almost identical to that of class CommissionEmployee, except that BasePlusCommissionEmployee's constructor also sets the BaseSalary.