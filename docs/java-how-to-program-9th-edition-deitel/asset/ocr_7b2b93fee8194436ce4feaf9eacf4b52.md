abstract, we indicate that each concrete subclass must provide an appropriate earnings implementation and that a program will be able to use superclass Employee variables to invoke method earnings polymorphically for any type of Employee.

# 10.5.2 Concrete Subclass SalariedEmployee

Class SalariedEmployee (Fig. 10.5) extends class Employee (line 4) and overrides abstract method earnings (lines 33–37), which makes SalariedEmployee a concrete class. The class includes a constructor (lines 9–14) that takes a first name, a last name, a social security number and a weekly salary as arguments; a set method to assign a new nonnegative value to instance variable weeklySalary (lines 17–24); a get method to return weeklySalary’s value (lines 27–30); a method earnings (lines 33–37) to calculate a SalariedEmployee’s earnings; and a method toString (lines 40–45), which returns a String including the employee’s type, namely, "salaried employee: " followed by employee-specific information produced by superclass Employee’s toString method and SalariedEmployee’s getWeeklySalary method. Class SalariedEmployee’s constructor passes the first name, last name and social security number to the Employee constructor (line 12) to initialize the private instance variables not inherited from the superclass. Method earnings overrides Employee’s abstract method earnings to provide a concrete implementation that returns the SalariedEmployee’s weekly salary. If we do not implement earnings, class SalariedEmployee must be declared abstract—otherwise, class SalariedEmployee will not compile. Of course, we want SalariedEmployee to be a concrete class in this example.

```
1  // Fig. 10.5: SalariedEmployee.java
2  // SalariedEmployee concrete class extends abstract class Employee.
3  
4  public class SalariedEmployee extends Employee
5  {
6      private double weeklySalary;
7  
8      // four-argument constructor
9      public SalariedEmployee( String first, String last, String ssn,
10      double salary )
11  {
12      super( first, last, ssn ); // pass to Employee constructor
13      setWeeklySalary( salary ); // validate and store salary
14  } // end four-argument SalariedEmployee constructor
15  
16  // set salary
17  public void setWeeklySalary( double salary )
18  {
19      if ( salary >= 0.0 )
20          baseSalary = salary;
21      else
22          throw new IllegalArgumentException(
23          "Weekly salary must be >= 0.0" );
24  } // end method setWeeklySalary
25
```