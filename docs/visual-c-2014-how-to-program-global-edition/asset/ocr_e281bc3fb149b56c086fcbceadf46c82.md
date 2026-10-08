# 11.4 Relationship between Base Classes and Derived Classes 497

```
// implicit call to object constructor occurs here
FirstName = firstName;
LastName = lastName;
SocialSecurityNumber = socialSecurityNumber;
GrossSales = grossSales; // validates gross sales
CommissionRate = commissionRate; // validates commission rate
}
```

// property that gets and sets employee's gross sales

// property that gets and sets employee's commission rate

// calculate employee's pay

```
public virtual decimal Earnings() => CommissionRate * GrossSales;
```

![](bbox=[0.125, 0.936, 0.834, 0.95])