# Software Engineering Observation 9.3

With inheritance, the common instance variables and methods of all the classes in the hierarchy are declared in a superclass. When changes are made for these common features in the superclass—subclasses then inherit the changes. Without inheritance, changes would need to be made to all the source-code files that contain a copy of the code in question.

# 9.4.3 Creating a CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy

Now we redeclare class BasePlusCommissionEmployee (Fig. 9.8) to extend class CommissionEmployee (Fig. 9.4). A BasePlusCommissionEmployee object is a CommissionEmployee, because inheritance passes on class CommissionEmployee’s capabilities. Class BasePlusCommissionEmployee also has instance variable baseSalary (Fig. 9.8, line 6). Keyword extends (line 4) indicates inheritance. BasePlusCommissionEmployee inherits CommissionEmployee’s instance variables and methods, but only the superclass’s public and protected members are directly accessible in the subclass. The CommissionEmployee constructor is not inherited. So, the public BasePlusCommissionEmployee services include its constructor (lines 9–16), public methods inherited from CommissionEmployee, and methods setBaseSalary (lines 19–26), getBaseSalary (lines 29–32), earnings (lines 35–40) and toString (lines 43–53). Methods earnings and toString override the corresponding methods in class CommissionEmployee because their superclass versions do not properly calculate a BasePlusCommissionEmployee’s earnings or return an appropriate String representation.

```
// Fig. 9.8: BasePlusCommissionEmployee.java
// private superclass members cannot be accessed in a subclass.
public class BasePlusCommissionEmployee extends CommissionEmployee
{
    private double baseSalary; // base salary per week

    // six-argument constructor
    public BasePlusCommissionEmployee( String first, String last,
        String ssn, double sales, double rate, double salary )
    {
        // explicit call to superclass CommissionEmployee constructor
        super( first, last, ssn, sales, rate );

        setBaseSalary( salary ); // validate and store base salary
    } // end six-argument BasePlusCommissionEmployee constructor

    // set base salary
    public void setBaseSalary( double salary )
    {
        if ( salary >= 0.0 )
            baseSalary = salary;
        else
            throw new IllegalArgumentException(
                "Base salary must be >= 0.0" );
    } // end method setBaseSalary
```