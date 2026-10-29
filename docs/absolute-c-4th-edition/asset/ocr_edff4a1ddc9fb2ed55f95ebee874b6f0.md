# Display 14.3 — Interface for the Derived Class HourlyEmployee

```
```cpp
//This is the header file hourlyemployee.h.
//This is the interface for the class HourlyEmployee.
#ifndef HOUR L YEMPLOYEE_H
#define HOURLYEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

    class HourlyEmployee : public Employee
    {
    public:
        HourlyEmployee( );
        HourlyEmployee(string theName, string theSsn,
                       double theWageRate, double theHours);
        void setRate(double newWageRate);
        double getRate( ) const;
        void setHours(double hoursWorked);
        double getHours( ) const;
        void printCheck( );
    private:
        double wageRate;
        double hours;
    };

}//SavitchEmployees

#endif //HOURLYEMPLOYEE_H
```
```

> Note that the definition of a derived class begins like any other class definition but adds a colon, the reserved word public, and the name of the base class to the first line of the class definition, as in the following (from Display 14.3):

```
```cpp
class HourlyEmployee : public Employee
{
```
```

The derived class (such as HourlyEmployee) automatically receives all the member variables and member functions of the base class (such as Employee) and can add additional member variables and member functions.