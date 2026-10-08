Call BasePlusCommissionEmployee's ToString and Earnings methods with derived class reference to derived class object:

```
base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
nernings: $500.00
```

Call BasePlusCommissionEmployee's ToString and Earnings methods with derived class reference to derived class object:

```
base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
nernings: $500.00
```

**Fig. 12.1** Assigning base-class and derived-class references to base-class and derived-class variables. (Part 3 of 3)

In Fig. 12, lines 11–12 create a new CommissionEmployee object and assign its reference to CommissionEmployee variable and lines 15–16 create a new BasePlusCommissionEmployee object and assign its reference to a BasePlusCommissionEmployee variable. These assignments are natural—a CommissionEmployee variable's primary purpose is to hold a reference to a CommissionEmployee object. Lines 23–24 use the reference commissionemployee to invoke methods ToString and Earnings. Because commissionemployee refers to a CommissionEmployee object, base class CommissionEmployee's version of the methods are called. Similarly, lines 31–33 use the reference basePlusCommissionEmployee to invoke the methods ToString and Earnings on the BasePlusCommissionEmployee-object. This invokes derived class BasePlusCommissionEmployee's version of the methods.

Line 37 assigns the reference to derived-class object BasePlusCommissionEmployee to a base-class CommissionEmployee variable, which lines 41–43 use to invoke ToString and Earnings. Note that commissionEmployee2.ToString() in line 41 actually calls BasePlusCommissionEmployee's ToString method. The compiler allows this "crossover" because an object of a derived class is an object of its base class (but not versa). When the compiler encounters a virtual method call through a variable, the compiler checks the variable's type to determine if the method can be called. If that class contains the proper method declaration (or inherits it), the call compiles. At execution time, the type of object to which the variable refers determines the actual method used.

# Software Engineering Observation 12.3

A base-class variable that contains a reference to a derived-class object is used to call a virtual method actually calls the overriding derived-class version of the method.

![](bbox=[0.125, 0.865, 0.215, 0.945])