```
Call BasePlusCommissionEmployee's toString with subclass reference to subclass object:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Call BasePlusCommissionEmployee's toString with superclass reference to subclass object:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00
```

Fig. 10.1 | Assigning superclass and subclass references to superclass and subclass variables. (Part 2 of 2.)

In Fig. 10.1, lines 10–11 create a CommissionEmployee object and assign its reference to a CommissionEmployee variable. Lines 14–16 create a BasePlusCommissionEmployee object and assign its reference to a BasePlusCommissionEmployee variable. These assignments are natural—for example, a CommissionEmployee variable's primary purpose is to hold a reference to a CommissionEmployee object. Lines 19–21 use commissionEmployee to invoke toString explicitly. Because commissionEmployee refers to a CommissionEmployee object, superclass CommissionEmployee's version of toString is called. Similarly, lines 24–27 use basePlusCommissionEmployee to invoke toString explicitly on the BasePlusCommissionEmployee object. This invokes subclass BasePlusCommissionEmployee's version of toString.

Lines 30–31 then assign the reference of subclass object basePlusCommissionEmployee to a superclass CommissionEmployee variable, which lines 32–34 use to invoke method toString. When a superclass variable contains a reference to a subclass object, and that reference is used to call a method, the subclass version of the method is called. Hence, commissionEmployee2.toString() in line 34 actually calls class BasePlusCommissionEmployee's toString method. The Java compiler allows this “crossover” because an object of a subclass is an object of its superclass (but not vice versa). When the compiler encounters a method call made through a variable, the compiler determines if the method can be called by checking the variable's class type. If that class contains the proper method declaration (or inherits one), the call is compiled. At execution time, the type of the object to which the variable refers determines the actual method to use. This process, called dynamic binding, is discussed in detail in Section 10.5.

# 10.4 Abstract Classes and Methods

When we think of a class, we assume that programs will create objects of that type. Sometimes it's useful to declare classes—called abstract classes—for which you never intend to create objects. Because they're used only as superclasses in inheritance hierarchies, we refer