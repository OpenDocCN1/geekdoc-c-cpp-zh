# 12.4.1 Creating and Using a CommissionEmployee Class

Let’s examine CommissionEmployee’s class definition (Figs. 12.4–12.5). The CommissionEmployee header (Fig. 12.4) specifies class CommissionEmployee’s public services, which include a constructor (lines 12–13) and member functions earning (line 30) and print (line 31). Lines 15–28 declare public get and set functions that manipulate the class’s data members (declared in lines 33–37)—firstName, lastName, socialSecurityNumber, grossSales and commissionRate. Member functions setGrossSales (defined in lines 56–62 of Fig. 12.5) and setCommissionRate (defined in lines 71–77 of Fig. 12.5), for example, validate their arguments before assigning the values to data members grossSales and commissionRate, respectively.

```
```cpp
// Fig. 12.4: CommissionEmployee.h
// CommissionEmployee class definition represents a commission employee.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class
using namespace std;

class CommissionEmployee
{
public:
   CommissionEmployee( const string &, const string &, const string &,
      double = 0.0, double = 0.0 );

   void setFirstName( const string & ); // set first name
   string getFirstName() const; // return first name

   void setLastName( const string & ); // set last name
   string getLastName() const; // return last name

   void setSocialSecurityNumber( const string & ); // set SSN
   string getSocialSecurityNumber() const; // return SSN

   void setGrossSales( double ); // set gross sales amount
   double getGrossSales() const; // return gross sales amount

   void setCommissionRate( double ); // set commission rate (percentage)
   double getCommissionRate() const; // return commission rate

   double earnings() const; // calculate earnings
   void print() const; // print CommissionEmployee object
private:
   string firstName;
   string lastName;
   string socialSecurityNumber;
   double grossSales; // gross weekly sales
   double commissionRate; // commission percentage
}; // end class CommissionEmployee

#endif
```
```

**Fig. 12.4** | *CommissionEmployee class header.*