```
13        super( first, last, ssn, sales, rate );
14        setBaseSalary( salary ); // validate and store base salary
15    } // end six-argument BasePlusCommissionEmployee constructor
16
17    // set base salary
18    public void setBaseSalary( double salary )
19    {
20        if ( salary >= 0.0 )
21            baseSalary = salary;
22        else
23            throw new IllegalArgumentException(
24                "Base salary must be >= 0.0" );
25    } // end method setBaseSalary
26
27    // return base salary
28    public double getBaseSalary()
29    {
30        return baseSalary;
31    } // end method getBaseSalary
32
33    // calculate earnings
34    @Override // indicates that this method overrides a superclass method
35    public double earnings()
36    {
37        return baseSalary + ( commissionRate * grossSales );
38    } // end method earnings
39
40    // return String representation of BasePlusCommissionEmployee
41    @Override // indicates that this method overrides a superclass method
42    public String toString()
43    {
44        return String.format(
45            "%s: %s %s\n%s: %s\n%s: %.2f\n%s: %.2f\n%s: %.2f",
46            "base-salaried commission employee", firstName, lastName,
47            "social security number", socialSecurityNumber,
48            "gross sales", grossSales, "commission rate", commissionRate,
49            "base salary", baseSalary );
50    } // end method toString
51 } // end class BasePlusCommissionEmployee
```

Fig. 9.9 | BasePlusCommissionEmployee inherits protected instance variables from CommissionEmployee. (Part 2 of 2.)

# Testing Class BasePlusCommissionEmployee

The BasePlusCommissionEmployeeTest class for this example is identical to that of Fig. 9.7 and produces the same output, so we do not show it here. Although the version of class BasePlusCommissionEmployee in Fig. 9.6 does not use inheritance and the version in Fig. 9.9 does, both classes provide the same functionality. The source code in Fig. 9.9 (47 lines) is considerably shorter than that in Fig. 9.6 (116 lines), because most of BasePlusCommissionEmployee’s functionality is now inherited from CommissionEmployee—there’s now only one copy of the CommissionEmployee functionality. This makes the code easier to maintain, modify and debug, because the code related to a commission employee exists only in class CommissionEmployee.