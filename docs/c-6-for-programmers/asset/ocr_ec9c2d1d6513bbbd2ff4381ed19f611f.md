# 11.4 Relationship between Base Classes and Derived Classes

In this section, we use an inheritance hierarchy containing types of employees in a company's payroll app to discuss the relationship between a base class and a derived class. In this company:

+   - *commission employees*—who will be represented as objects of a base class—are paid a percentage of their sales, while
+   - *base-salaried commission employees*—who will be represented as objects of a derived class—receive a base salary *plus* a percentage of their sales.

We divide our discussion of the relationship between these employee types into an evolutionary set of five examples that was carefully designed to teach key capabilities for good software engineering with inheritance:

+   1. The first example creates class `CommissionEmployee`, which directly inherits from class `object`. The class declares `public` auto-implemented properties for the first name, last name and social security number, and private instance variables for the commission rate and gross (i.e., total) sales amount.
+   2. The second example declares class `BasePlusCommissionEmployee`, which also directly inherits from `object`. The class declares `public` auto-implemented properties for the first name, last name and social security number, and private instance variables for the commission rate, gross sales amount *and* base salary. We create the class by writing *every* line of code the class requires—we'll soon see that it's more efficient to create this class by inheriting from `CommissionEmployee`.
+   3. The third example declares a separate `BasePlusCommissionEmployee` class that extends class `CommissionEmployee`—that is, a `BasePlusCommissionEmployee` *is* a `CommissionEmployee` who also has a base salary. `BasePlusCommissionEmployee` attempts to access class `CommissionEmployee`'s private members, but this results in compilation errors because a derived class *cannot* access its base class's private instance variables.
+   4. The fourth example shows that if base class `CommissionEmployee`'s instance variables are declared as `protected`, a `BasePlusCommissionEmployee` class that inherits from `CommissionEmployee` can access that data directly.
+   5. The fifth and final example demonstrates *best practice* by setting the `CommissionEmployee` instance variables back to `private` in class `CommissionEmployee` to enforce good software engineering. Then we show how a separate `BasePlusCommissionEmployee` class that inherits from class `CommissionEmployee` can use `CommissionEmployee`'s public methods and properties to manipulate `CommissionEmployee`'s private instance variables in a controlled manner.

In the first four examples, we'll directly access instance variables in several cases where properties should be used. In the fifth example, we'll apply effective software engineering techniques that we've presented up to this point in the book to create classes that are easy to maintain, modify and debug.