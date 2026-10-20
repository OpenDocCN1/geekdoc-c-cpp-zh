```
91
92   // calculate earnings
93   public double earnings()
94   {
95     return getCommissionRate() * getGrossSales();
96   } // end method earnings
97
98   // return String representation of CommissionEmployee object
99   @Override // indicates that this method overrides a superclass method
100  public String toString()
101  {
102    return String.format( "%s: %s %s\n%s: %s\n%s: %.2f\n%s: %.2F",
103      "commission employee", getFirstName(), getLastName(),
104      "social security number", getSocialSecurityNumber(),
105      "gross sales", getGrossSales(),
106      "commission rate", getCommissionRate() );
107  } // end method toString
108 } // end class CommissionEmployee
```

Fig. 9.10 | CommissionEmployee class uses methods to manipulate its private instance variables. (Part 3 of 3.)

Subclass BasePlusCommissionEmployee (Fig. 9.11) inherits CommissionEmployee’s non-private methods and can access the private superclass members via those methods. Class BasePlusCommissionEmployee has several changes that distinguish it from Fig. 9.9. Methods earnings (lines 35–39) and toString (lines 42–47) each invoke method getBaseSalary to obtain the base salary value, rather than accessing baseSalary directly. If we decide to rename instance variable baseSalary, only the bodies of method setBaseSalary and getBaseSalary will need to change.

```
1  // Fig. 9.11: BasePlusCommissionEmployee.java
2  // BasePlusCommissionEmployee class inherits from CommissionEmployee
3  // and accesses the superclass’s private data via inherited
4  // public methods.
5
6  public class BasePlusCommissionEmployee extends CommissionEmployee
7  {
8    private double baseSalary; // base salary per week
9
10   // six-argument constructor
11   public BasePlusCommissionEmployee( String first, String last,
12     String ssn, double sales, double rate, double salary )
13   {
14     super( first, last, ssn, sales, rate );
15     setBaseSalary( salary ); // validate and store base salary
16   } // end six-argument BasePlusCommissionEmployee constructor
17
```

Fig. 9.11 | BasePlusCommissionEmployee class inherits from CommissionEmployee and accesses the superclass’s private data via inherited public methods. (Part 1 of 2.)