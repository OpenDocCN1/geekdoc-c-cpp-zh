```
26    // return base salary
27    public double getBaseSalary()
28    {
29        return baseSalary;
30    } // end method getBaseSalary
31
32    // calculate earnings; override method earnings in CommissionEmployee
33    @Override
34    public double earnings()
35    {
36        return getBaseSalary() + super.earnings();
37    } // end method earnings
38
39    // return String representation of BasePlusCommissionEmployee object
40    @Override
41    public String toString()
42    {
43        return String.format( "%s %s; %s: $%,.2f",
44            "base-salaried", super.toString(),
45            "base salary", getBaseSalary() );
46    } // end method toString
47 } // end class BasePlusCommissionEmployee
```

Fig. 10.8 | BasePlusCommissionEmployee class extends CommissionEmployee. (Part 2 of 2.)

# 10.5.6 Polymorphic Processing, Operator instanceof and Downcasting

To test our Employee hierarchy, the application in Fig. 10.9 creates an object of each of the four concrete classes SalariedEmployee, HourlyEmployee, CommissionEmployee and BasePlusCommissionEmployee. The program manipulates these objects nonpolymorphically, via variables of each object’s own type, then polymorphically, using an array of Employee variables. While processing the objects polymorphically, the program increases the base salary of each BasePlusCommissionEmployee by 10%—this requires determining the object’s type at execution time. Finally, the program polymorphically determines and outputs the type of each object in the Employee array. Lines 9–18 create objects of each of the four concrete Employee subclasses. Lines 22–30 output the String representation and earnings of each of these objects nonpolymorphically. Each object’s toString method is called implicitly by printf when the object is output as a String with the %s format specifier.

```
1  // Fig. 10.9: PayrollSystemTest.java
2  // Employee hierarchy test program.
3
4  public class PayrollSystemTest
5  {
6      public static void main( String[] args )
7      {
8          // create subclass objects
9          SalariedEmployee salariedEmployee =
10             new SalariedEmployee( "John", "Smith", "111-11-1111", 800.00 );
```

Fig. 10.9 | Employee hierarchy test program. (Part 1 of 4.)