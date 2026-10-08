# 12.5 Case Study: Payroll System Using Polymorphism 529

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: $16.75
hours worked: 40.00
erned: $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: $10,000.00
commission rate: 0.06
erned: $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: $5,000.00
commission rate: 0.04
base salary: $300.00
 base salary with 10% increase is: $330.00
erned: $530.00

+   Employee 0 is a SalariedEmployee
Employee 1 is a HourlyEmployee
Employee 2 is a CommissionEmployee
Employee 3 is a BasePlusCommissionEmployee

Fig. 12.9 | Employee hierarchy tree app.(Part 3 of 3).

Assigned-Derived Objects to Base-Class References
Lines 33–46 iterate the List<Employee> named employees and initialize it with the SalariedEmployee, HourlyEmployee, CommissionEmployee and BasePlusCommissionEmployee created in lines. Each element of the List is an Employee variable. The derived-class objects can be assigned to an element of employees because a SalariedEmployee is an employee, an HourlyEmployee is an employee, a CommissionEmployee is an employee and a BasePlusCommissionEmployee is an employee. This is allowed even though Employee is an abstract class.

Polymorphic Processing of Employees
Lines 39–56 iterate through ToString and Earnings with Employee variable currentEmployee, which assigned the reference of a different Employee during iteration. The output illustrates that the appropriate methods for each class are invoked. Virtual methods ToString and Earnings are resolved at execution time, based on the type of the object which currentEmployee refers. This process is known as dynamic binding or late binding. For example, line 41 implicitly invokes ToString of the object to which currentEmployee refers. Only methods of subclass can be called via an Employee variable—and includes object's methods, such as ToString. (Section 11.7 describes the methods that all classes inherit from class.) A base-class reference can be used to invoke only methods that were originally declared in the base class or in the class hierarchy.

Giving BasePlusCommissionEmployees 10% Raises
We perform special processing on BasePlusCommissionEmployee objects—as we encounter them, we increase their base salary by 10%. When processing polymorphically,