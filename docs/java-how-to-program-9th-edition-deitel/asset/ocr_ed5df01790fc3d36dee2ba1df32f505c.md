```
// calculate earnings; override abstract method earnings in Employee
@Override
public double earnings()
{
    if ( getHours() <= 40 ) // no overtime
        return getWage() * getHours();
    else
        return 40 * getWage() + ( getHours() - 40 ) * getWage() * 1.5;
} // end method earnings
```

```
// return String representation of HourlyEmployee object
@Override
public String toString()
{
    return String.format( "hourly employee: %s\n%s: $%,.2f; %s: %,.2f", super.toString(), "hourly wage", getWage(), "hours worked", getHours() );
} // end method toString
} // end class HourlyEmployee
```

Fig. 10.6 | HourlyEmployee class extends Employee. (Part 2 of 2.)

# 10.5.4 Concrete Subclass CommissionEmployee

Class CommissionEmployee (Fig. 10.7) extends class Employee (line 4). The class includes a constructor (lines 10–16) that takes a first name, a last name, a social security number, a sales amount and a commission rate; set methods (lines 19–26 and 35–42) to assign new values to instance variables commissionRate and grossSales, respectively; get methods (lines 29–32 and 45–48) that retrieve the values of these instance variables; method earnings (lines 51–55) to calculate a CommissionEmployee’s earnings; and method toString (lines 58–65), which returns the employee’s type, namely, "commission employee: " and employee-specific information. The constructor also passes the first name, last name and social security number to Employee’s constructor (line 13) to initialize Employee’s private instance variables. Method toString calls superclass method toString (line 62) to obtain the Employee-specific information (i.e., first name, last name and social security number).

```
// Fig. 10.7: CommissionEmployee.java
// CommissionEmployee class extends Employee.
public class CommissionEmployee extends Employee
{
    private double grossSales; // gross weekly sales
    private double commissionRate; // commission percentage

    // five-argument constructor
    public CommissionEmployee( String first, String last, String ssn, double sales, double rate )
    {
        super( first, last, ssn );
```

Fig. 10.7 | CommissionEmployee class extends Employee. (Part 1 of 2.)