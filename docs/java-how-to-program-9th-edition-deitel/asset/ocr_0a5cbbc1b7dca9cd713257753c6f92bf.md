```
protected String firstName;
protected String lastName;
protected String socialSecurityNumber;
protected double grossSales; // gross weekly sales
protected double commissionRate; // commission percentage
```

The rest of the class declaration (which is not shown here) is identical to that of Fig. 9.4.

We could have declared CommissionEmployee’s instance variables public to enable subclass BasePlusCommissionEmployee to access them. However, declaring public instance variables is poor software engineering because it allows unrestricted access to the these variables, greatly increasing the chance of errors. With protected instance variables, the subclass gets access to the instance variables, but classes that are not subclasses and classes that are not in the same package cannot access these variables directly—recall that protected class members are also visible to other classes in the same package.

# Class BasePlusCommissionEmployee

Class BasePlusCommissionEmployee (Fig. 9.9) extends the new version of class CommissionEmployee with protected instance variables. BasePlusCommissionEmployee objects inherit CommissionEmployee’s protected instance variables firstName, lastName, socialSecurityNumber, grossSales and commissionRate—all these variables are now protected members of BasePlusCommissionEmployee. As a result, the compiler does not generate errors when compiling line 37 of method earnings and lines 46–48 of method toString. If another class extends this version of class BasePlusCommissionEmployee, the new subclass also can access the protected members.

When you create a BasePlusCommissionEmployee object, it contains all instance variables declared in the class hierarchy to that point—i.e., those from classes Object, CommissionEmployee and BasePlusCommissionEmployee. Class BasePlusCommissionEmployee does not inherit class CommissionEmployee’s constructor. However, class BasePlusCommissionEmployee’s six-argument constructor (lines 10–15) calls class CommissionEmployee’s five-argument constructor explicitly to initialize the instance variables that BasePlusCommissionEmployee inherited from class CommissionEmployee. Similarly, class CommissionEmployee’s constructor implicitly calls class Object’s constructor. BasePlusCommissionEmployee’s constructor must do this explicitly because CommissionEmployee does not provide a no-argument constructor that could be invoked implicitly.

```
1  // Fig. 9.9: BasePlusCommissionEmployee.java
2  // BasePlusCommissionEmployee inherits protected instance
3  // variables from CommissionEmployee.
4
5  public class BasePlusCommissionEmployee extends CommissionEmployee
6  {
7      private double baseSalary; // base salary per week
8
9      // six-argument constructor
10     public BasePlusCommissionEmployee( String first, String last,
11         String ssn, double sales, double rate, double salary )
12     {
```

Fig. 9.9 | BasePlusCommissionEmployee inherits protected instance variables from CommissionEmployee. (Part 1 of 2.)