```
18  // set base salary
19  public void setBaseSalary( double salary )
20  {
21      if ( salary >= 0.0 )
22          baseSalary = salary;
23      else
24          throw new IllegalArgumentException(
25              "Base salary must be >= 0.0" );
26  } // end method setBaseSalary
27
28  // return base salary
29  public double getBaseSalary()
30  {
31      return baseSalary;
32  } // end method getBaseSalary
33
34  // calculate earnings
35  @Override // indicates that this method overrides a superclass method
36  public double earnings()
37  {
38      return getBaseSalary() + super.earnings();
39  } // end method earnings
40
41  // return String representation of BasePlusCommissionEmployee
42  @Override // indicates that this method overrides a superclass method
43  public String toString()
44  {
45      return String.format( "%s %s\n%s: %.2f", "base-salaried",
46          super.toString(), "base salary", getBaseSalary() );
47  } // end method toString
48 } // end class BasePlusCommissionEmployee
```

Fig. 9.11 | BasePlusCommissionEmployee class inherits from CommissionEmployee and accesses the superclass’s private data via inherited public methods. (Part 2 of 2.)

# Class BasePlusCommissionEmployee’s earnings Method

Method earnings (lines 35–39) overrides class CommissionEmployee’s earnings method (Fig. 9.10, lines 93–96) to calculate a base-salaried commission employee’s earnings. The new version obtains the portion of the earnings based on commission alone by calling CommissionEmployee’s earnings method with super.earnings() (line 34), then adds the base salary to this value to calculate the total earnings. Note the syntax used to invoke an overridden superclass method from a subclass—place the keyword super and a dot (.) separator before the superclass method name. This method invocation is a good software engineering practice—if a method performs all or some of the actions needed by another method, call that method rather than duplicate its code. By having BasePlusCommissionEmployee’s earnings method invoke CommissionEmployee’s earnings method to calculate part of a BasePlusCommissionEmployee object’s earnings, we avoid duplicating the code and reduce code-maintenance problems. If we did not use “super.” then BasePlusCommissionEmployee’s earnings method would call itself rather than the superclass version. This would result in a phenomenon we study in Chapter 18 called infinite recursion, which would eventually cause the method-call stack to overflow—a fatal runtime error.