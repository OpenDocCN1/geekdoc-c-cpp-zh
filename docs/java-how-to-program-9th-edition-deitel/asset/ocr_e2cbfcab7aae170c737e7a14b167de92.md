rent Employee object—as you’ll see momentarily, attempting to invoke a subclass-only method directly on a superclass reference is a compilation error.

# Common Programming Error 10.3

Assigning a superclass variable to a subclass variable (without an explicit cast) is a compilation error.

# Software Engineering Observation 10.4

If a subclass object’s reference has been assigned to a variable of one of its direct or indirect superclasses at execution time, it’s acceptable to downcast the reference stored in that superclass variable back to a subclass-type reference. Before performing such a cast, use the instanceof operator to ensure that the object is indeed an object of an appropriate subclass.

# Common Programming Error 10.4

When downcasting a reference, a ClassCastException occurs if the referenced object at execution time does not have an is-a relationship with the type specified in the cast operator.

If the instanceof expression in line 49 is true, lines 53–60 perform the special processing required for the BasePlusCommissionEmployee object. Using BasePlusCommissionEmployee variable employee, line 56 invokes subclass-only methods getBaseSalary and setBaseSalary to retrieve and update the employee’s base salary with the 10% raise.

# Calling earnings Polymorphically

Lines 63–64 invoke method earnings on currentEmployee, which polymorphically calls the appropriate subclass object’s earnings method. Obtaining the earnings of the SalariedEmployee, HourlyEmployee and CommissionEmployee polymorphically in lines 63–64 produces the same results as obtaining these employees’ earnings individually in lines 22–27. The earnings amount obtained for the BasePlusCommissionEmployee in lines 63–64 is higher than that obtained in lines 28–30, due to the 10% increase in its base salary.

# Using Reflection to Get Each Employee’s Class Name

Lines 68–70 display each employee’s type as a String, using basic features of Java’s so-called reflection capabilities. Every object knows its own class and can access this information through the getClass method, which all classes inherit from class Object. Method getClass returns an object of type Class (from package java.lang), which contains information about the object’s type, including its class name. Line 70 invokes getClass on the current object to get its runtime class. The result of the getClass call is used to invoke getName to get the object’s class name.

# Avoiding Compilation Errors with Downcasting

In the previous example, we avoided several compilation errors by downcasting an Employee variable to a BasePlusCommissionEmployee variable in lines 53–54. If you remove the cast operator (BasePlusCommissionEmployee) from line 54 and attempt to assign Employee variable currentEmployee directly to BasePlusCommissionEmployee variable employee, you’ll receive an “incompatible types” compilation error. This error indicates that the attempt to assign the reference of superclass object currentEmployee to subclass variable employee is not allowed. The compiler prevents this assignment because a CommissionEmployee is not a BasePlusCommissionEmployee—the is-a relationship applies only between the subclass and its superclasses, not vice versa.