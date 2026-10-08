# 11.4 Relationship between Base Classes and Derived Classes 493

that a derived-class method overrides a virtual or abstract base-class method. This modifier implicitly declares the derived-class method virtual and allows it to be overridden in derived classes further down the inheritance hierarchy. Adding the keyword to method Earnings declaration: In 11.4, as

```
public virtual decimal Earnings()
```

eliminates the first compilation error for line 11 of Fig. 11.8.
The compiler generates additional errors for line 42 of Fig. 11.8, because base class CommissionEmployee's instance variables commissionRate and grossSales are derived-class basePlusCommissionEmployee's methods are not allowed to access the base class members. The compiler also issues errors at lines 49-50 to ToString in BasePlusCommissionEmployee could have been prevented by using the public properties inherited from class CommissionEmployee. For example, line 42, 49 and 50 could have invoked the getters of properties commissionRate and grossSales to access CommissionEmployee's private instance variables commissionRate and grossSales, respectively.

# 11.4 CommissionEmployeeBasePlusCommissionEmployee Inheritance Using Protected Instances

To enable BasePlusCommissionEmployee to directly access base-class instance variables grossSales and commissionRate, we can declare those as protected in the base class. As discussed in Section 11.3, a base's protected members are accessible to all derived classes of that class. CommissionEmployee in this example is a modification of the version from Fig. 11.4 that declares its instance variables Sales and commissionRate

```
protected decimal grossSales; // gross sales
protected decimal commissionRate; // commission percentage
```

rather than. We also declare the Earnings method virtual so that BasePlusCommissionEmployee can override the method. The rest of class CommissionEmployee in this example is identical to Fig. 11.4. The complete source code for CommissionEmployee is included in this project's.

Class BasePlusCommissionEmployee
Class CommissionEmployee (Fig. 11.9) in this example extends the version of CommissionEmployee with protected instance variables grossSales and commissionRate. Each BasePlusCommissionEmployee object contains these CommissionEmployee instance variables, which are inherited into BasePlusCommissionEmployee as protected members. As a result, accessing instance variables grossSales and commissionRate no longer generates compilation errors in methods Earnings and ToString. Another class BasePlusCommissionEmployee, the new derived class also inherits grossSales and commissionRate as protected members.

Class BasePlusCommissionEmployee does not inherit CommissionEmployee's constructor. However, basePlusCommissionEmployee's constructor (lines 12–19) calls CommissionEmployee's constructor with a constructor initializer. Again, BasePlusCommissionEmployee's constructor must explicitly call CommissionEmployee's con-