```
```cpp
65 // set gross sales amount
66 void CommissionEmployee::setGrossSales( double sales )
67 {
68     grossSales = ( sales < 0.0 ) ? 0.0 : sales;
69 } // end function setGrossSales
70
71 // return gross sales amount
72 double CommissionEmployee::getGrossSales() const
73 {
74     return grossSales;
75 } // end function getGrossSales
76
77 // set commission rate
78 void CommissionEmployee::setCommissionRate( double rate )
79 {
80     commissionRate = ( rate > 0.0 && rate < 1.0 ) ? rate : 0.0;
81 } // end function setCommissionRate
82
83 // return commission rate
84 double CommissionEmployee::getCommissionRate() const
85 {
86     return commissionRate;
87 } // end function getCommissionRate
88
89 // calculate earnings
90 double CommissionEmployee::earnings() const
91 {
92     return getCommissionRate() * getGrossSales();
93 } // end function earnings
94
95 // print CommissionEmployee object
96 void CommissionEmployee::print() const
97 {
98     cout << "commission employee: "
99          << getFirstName() << ' ' << getLastName()
100         << "\nsocial security number: " << getSocialSecurityNumber()
101         << "\ngross sales: " << getGrossSales()
102         << "\ncommission rate: " << getCommissionRate();
103 } // end function print
```
```

Fig. 12.23 | CommissionEmployee's constructor and destructor output text. (Part 3 of 3.)

```
```cpp
1 // Fig. 12.24: BasePlusCommissionEmployee.h
2 // BasePlusCommissionEmployee class derived from class
3 // CommissionEmployee.
4 #ifndef BASEPLUS_H
5 #define BASEPLUS_H
6
7 #include <string> // C++ standard string class
8 #include "CommissionEmployee.h" // CommissionEmployee class declaration
9 using namespace std;
10
```
```

Fig. 12.24 | BasePlusCommissionEmployee class header file. (Part 1 of 2.)