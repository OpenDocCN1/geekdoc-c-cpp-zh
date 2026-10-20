```
Employee 0 is a SalariedEmployee
Employee 1 is a HourlyEmployee
Employee 2 is a CommissionEmployee
Employee 3 is a BasePlusCommissionEmployee
```

Fig. 10.9 | Employee hierarchy test program. (Part 4 of 4.)

# Creating the Array of Employees

Line 33 declares employees and assigns it an array of four Employee variables. Line 36 assigns the reference to a SalariedEmployee object to employees[0]. Line 37 assigns the reference to an HourlyEmployee object to employees[1]. Line 38 assigns the reference to a CommissionEmployee object to employees[2]. Line 39 assigns the reference to a BasePlusCommissionEmployee object to employee[3]. These assignments are allowed, because a SalariedEmployee is an Employee, an HourlyEmployee is an Employee, a CommissionEmployee is an Employee and a BasePlusCommissionEmployee is an Employee. Therefore, we can assign the references of SalariedEmployee, HourlyEmployee, CommissionEmployee and BasePlusCommissionEmployee objects to superclass Employee variables, even though Employee is an abstract class.

# Polymorphically Processing Employees

Lines 44–65 iterate through array employees and invoke methods toString and earnings with Employee variable currentEmployee, which is assigned the reference to a different Employee in the array on each iteration. The output illustrates that the appropriate methods for each class are indeed invoked. All calls to method toString and earnings are resolved at execution time, based on the type of the object to which currentEmployee refers. This process is known as dynamic binding or late binding. For example, line 46 implicitly invokes method toString of the object to which currentEmployee refers. As a result of dynamic binding, Java decides which class’s toString method to call at execution time rather than at compile time. Only the methods of class Employee can be called via an Employee variable (and Employee, of course, includes the methods of class Object). A superclass reference can be used to invoke only methods of the superclass—the subclass method implementations are invoked polymorphically.

# Performing Type-Specific Operations on BasePlusCommissionEmployees

We perform special processing on BasePlusCommissionEmployee objects—as we encounter these objects at execution time, we increase their base salary by 10%. When processing objects polymorphically, we typically do not need to worry about the “specifics,” but to adjust the base salary, we do have to determine the specific type of Employee object at execution time. Line 49 uses the instanceof operator to determine whether a particular Employee object’s type is BasePlusCommissionEmployee. The condition in line 49 is true if the object referenced by currentEmployee is a BasePlusCommissionEmployee. This would also be true for any object of a BasePlusCommissionEmployee subclass because of the is-a relationship a subclass has with its superclass. Lines 53–54 downcast currentEmployee from type Employee to type BasePlusCommissionEmployee—this cast is allowed only if the object has an is-a relationship with BasePlusCommissionEmployee. The condition at line 49 ensures that this is the case. This cast is required if we’re to invoke subclass BasePlusCommissionEmployee methods getBaseSalary and setBaseSalary on the cur-