```
39     lastName = last; // should validate
40   } // end method setLastName
41
42   // return last name
43   public String getLastName()
44   {
45       return lastName;
46   } // end method getLastName
47
48   // set social security number
49   public void setSocialSecurityNumber( String ssn )
50   {
51       socialSecurityNumber = ssn; // should validate
52   } // end method setSocialSecurityNumber
53
54   // return social security number
55   public String getSocialSecurityNumber()
56   {
57       return socialSecurityNumber;
58   } // end method getSocialSecurityNumber
59
60   // set gross sales amount
61   public void setGrossSales( double sales )
62   {
63       if ( sales >= 0.0 )
64           grossSales = sales;
65       else
66           throw new IllegalArgumentException(
67               "Gross sales must be >= 0.0" );
68   } // end method setGrossSales
69
70   // return gross sales amount
71   public double getGrossSales()
72   {
73       return grossSales;
74   } // end method getGrossSales
75
76   // set commission rate
77   public void setCommissionRate( double rate )
78   {
79       if ( rate > 0.0 && rate < 1.0 )
80           commissionRate = rate;
81       else
82           throw new IllegalArgumentException(
83               "Commission rate must be > 0.0 and < 1.0" );
84   } // end method setCommissionRate
85
86   // return commission rate
87   public double getCommissionRate()
88   {
89       return commissionRate;
90   } // end method getCommissionRate
```

Fig. 9.10 | CommissionEmployee class uses methods to manipulate its private instance variables. (Part 2 of 3.)