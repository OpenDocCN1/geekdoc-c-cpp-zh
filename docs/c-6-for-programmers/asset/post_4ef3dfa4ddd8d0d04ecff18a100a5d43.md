
```
49   $"gross sales: {grossSales:C}\n" +
50   $"commission rate: {commissionRate:F2}\n" +
51   $"base salary: {baseSalary}";
52 }
```

Fig. 11.9 | BasePlusCommissionEmployee inherits from CommissionEmployee and has access to CommissionEmployee's protected members. (Part 2 of 2.)

## Testing Class BasePlusCommissionEmployee

The BasePlusCommissionEmployeeTest class in this example's project is identical to that of Fig. 11.7 and produces the same output, so we do not show the code here. Although the version of class BasePlusCommissionEmployee in Fig. 11.6 does not use inheritance and the version in Fig. 11.9 does, both classes provide the same functionality. The source code in Fig. 11.9 (52 lines) is considerably shorter than that in Fig. 11.6 (97 lines), because a large portion of the class's functionality is now inherited from CommissionEmployee—there's now only one copy of the CommissionEmployee functionality. This makes the code easier to maintain, modify and debug, because the code related to a CommissionEmployee exists only in that class.

## public vs. protected Data

We could have declared base class CommissionEmployee's instance variables grossSales and commissionRate as public to enable derived class BasePlusCommissionEmployee to access the base-class instance variables. However, declaring public instance variables is poor software engineering, because it allows unrestricted access to the instance variables by any of the class's clients, greatly increasing the chance of errors and inconsistencies. With protected instance variables, the derived class gets access to the instance variables, but classes that are not derived from the base class cannot access its variables directly.

## Problems with protected Instance Variables

In this example, we declared base-class instance variables as protected so that derived classes could access them. Inheriting protected instance variables enables you to directly access the variables in the derived class without invoking the set or get accessors of the corresponding property, thus violating encapsulation. In most cases, it's better to use private instance variables and access them via properties to encourage proper software engineering. Your code will be easier to maintain, modify and debug.

Using protected instance variables creates several potential problems. First, since the derived-class object can set an inherited variable's value directly without using a property's set accessor, a derived-class object can assign an invalid value to the variable. For example, if we were to declare CommissionEmployee's instance variable grossSales as protected, a derived-class object (e.g., BasePlusCommissionEmployee) could then directly assign a negative value to grossSales, making it invalid.

The second problem with protected instance variables is that derived-class methods are more likely to be written to depend on the base class's data implementation. In practice, derived classes should depend only on the base-class services (i.e., non-private methods and properties) and not on the base-class data implementation. With protected instance variables in the base class, we may need to modify all the derived classes of the base class if the base-class implementation changes. For example, if for some reason we were to change
the names of instance variables grossSales and commissionRate, then we'd have to do so for all occurrences in which a derived class directly references base-class instance variables grossSales and commissionRate. In such a case, the software is said to be fragile or brittle, because a small change in the base class can "break" derived-class implementation. You should be able to change the base class implementation while still providing the same services to the derived classes. Of course, if the base-class services change, we must reimplement our derived classes.

> **Software Engineering Observation 11.4**
> Declaring base-class instance variables private (as opposed to protected) enables the base-class implementation of these instance variables to change without affecting derived-class implementations.

## 11.4.5 CommissionEmployee–BasePlusCommissionEmployee Inheritance Hierarchy Using private Instance Variables

We now reexamine our hierarchy, this time using the best software engineering practices.

## Base Class CommissionEmployee

Class CommissionEmployee (Fig. 11.10) once again declares instance variables grossSales and commissionRate as private (lines 10–11). Methods Earnings (line 65) and ToString (lines 68–72) no longer directly access these instance variables—rather they use properties GrossSales and CommissionRate to access the data. If we decide to change the instance-variable names, the Earnings and ToString declarations will not require modification—only the bodies of the properties GrossSales and CommissionRate that directly manipulate the instance variables will need to change. These changes occur solely within the base class—no changes to the derived class are needed. Localizing the effects of changes like this is a good software engineering practice. Derived class BasePlusCommissionEmployee (Fig. 11.11) inherits from CommissionEmployee’s and can access the private base-class members via the inherited public properties.

// Fig. 11.10: CommissionEmployee.cs
// CommissionEmployee class represents a commission employee.
using System;

public class CommissionEmployee
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

Fig. 11.10 | CommissionEmployee class represents a commission employee. (Part I of 3.)

```csharp
71        $"gross sales: {GrossSales:C}\n" +
72        $"commission rate: {CommissionRate:F2}";
73    }
```

Fig. 11.10 | CommissionEmployee class represents a commission employee. (Part 3 of 3.)

## Derived Class BasePlusCommissionEmployee

Class BasePlusCommissionEmployee (Fig. 11.11) has several changes to its method implementations that distinguish it from the version in Fig. 11.9. Methods Earnings (Fig. 11.11, line 43) and ToString (lines 46–47) each invoke property BaseSalary’s get accessor to obtain the base-salary value, rather than accessing baseSalary directly. If we decide to rename instance variable baseSalary, only the body of property BaseSalary will need to change.

```csharp
 1   // Fig. 11.11: BasePlusCommissionEmployee.cs
 2   // BasePlusCommissionEmployee inherits from CommissionEmployee and has
 3   // controlled access to CommissionEmployee's private data via
 4   // its public properties.
 5   using System;
 6
 7   public class BasePlusCommissionEmployee : CommissionEmployee
 8   {
 9       private decimal baseSalary; // base salary per week
10
11       // six-parameter derived-class constructor
12       // with call to base class CommissionEmployee constructor
13       public BasePlusCommissionEmployee(string firstName, string lastName,
14           string socialSecurityNumber, decimal grossSales,
15           decimal commissionRate, decimal baseSalary)
16           : base(firstName, lastName, socialSecurityNumber,
17               grossSales, commissionRate)
18       {
19           BaseSalary = baseSalary; // validates base salary
20       }
21
22       // property that gets and sets
23       // BasePlusCommissionEmployee's base salary
24       public decimal BaseSalary
25       {
26           get
27           {
28               return baseSalary;
29           }
30           set
31           {
32               if (value < 0) // validation
```

Fig. 11.11 | BasePlusCommissionEmployee inherits from CommissionEmployee and has access to CommissionEmployee's private data via its public properties. (Part 1 of 2.)
