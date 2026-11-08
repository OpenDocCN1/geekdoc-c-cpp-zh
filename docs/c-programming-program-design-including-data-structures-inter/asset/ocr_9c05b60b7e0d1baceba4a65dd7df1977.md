```
```cpp
double calculatePay() const;
//Function to calculate and return the wages.
//Postcondition: Pay is calculated and returned

void setNameRateHours(string first, string last,
                      double rate, double hours);
//Function to set the first name, last name, payRate,
//and hoursWorked according to the parameters.
//Postcondition: firstName = first; lastName = last;
//              payRate = rate; hoursWorked = hours

partTimeEmployee(string first = "", string last = "",
                 double rate = 0, double hours = 0);
//Constructor with parameters
//Sets the first name, last name, payRate, and hoursWorked
//according to the parameters. If no value is specified,
//the default values are assumed.
//Postcondition: firstName = first; lastName = last;
//              payRate = rate; hoursWorked = hours

private:
    double payRate;       //variable to store the pay rate
    double hoursWorked;   //variable to store the hours worked
};
```
```

The definitions of the member functions can be placed in a separate file. Recall that to include a system-provided header file, such as iostream, in a user program, you enclose the header file between angle brackets; to include a user-defined header file in a program, you enclose the header file between double quotation marks.

# Multiple Inclusions of a Header File

The previous section discussed how to create the header file of a derived class. To include a header file in a program, you use the preprocessor command. Recall that before a program is compiled, the preprocessor first processes the program. Consider the following header file:

```
```cpp
//Header file test.h

const int ONE = 1;
const int TWO = 2;
```
```

Suppose that the header file testA.h includes the file test.h in order to use the identifiers ONE and TWO. To be specific, suppose that the header file testA.h looks like:

```
```cpp
//Header file testA.h

#include "test.h"
.
.
.
```
```