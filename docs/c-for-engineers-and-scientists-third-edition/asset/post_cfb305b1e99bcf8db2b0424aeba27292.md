
# 716 Structures

# Program 13.3

```cpp
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

const int NUMRECS = 5;    // maximum number of records

struct PayRec // this is a global declaration
{
    int id;
    string name;
    double rate;
};

int main() {
    int i;
    PayRec employee[NUMRECS] = {
        { 32479, "Abrams, B.", 6.72 },
        { 36623, "Bohm, P.", 7.54 },
        { 34145, "Donaldson, S.", 5.56 },
        { 35987, "Ernst, T.", 5.43 },
        { 36203, "Gwodz, K.", 8.72 }
    };

    cout << endl;    // start on a new line
    cout << setw(ios::left); // left-justify the output
    for ( i = 0; i < NUMRECS; i++) {
        cout << setw(7) << employee[i].id;
        cout << setw(15) << employee[i].name;
        cout << setw(6) << employee[i].rate << endl;
    }

    return 0;
}
```

Program 13.3 displays the following output:

| 32479 | Abrams, B. | 6.72 |
| 36623 | Bohm, P. | 7.54 |
| 34145 | Donaldson, S. | 5.56 |
| 35987 | Ernst, T. | 5.43 |
| 36203 | Gwodz, K. | 8.72 |

# Chapter 13
## 717

In reviewing Program 13.3, notice the initialization of the array of structures. Although the initializers for each structure have been enclosed in inner braces, they aren't strictly necessary because all members have been initialized. With all external and static variables, in the absence of explicit initializers, the numeric elements of static and external arrays or structures are initialized to 0 and their character elements are initialized to NULLS. The iosflags(ios::left) manipulator included in the cout stream forces each name to be left-justified in its designated field width.

![](img/e2a849fc7bc04aa2e6669ad865e0c2b_736_0.png)

# EXERCISES 13.2 Define arrays of structures for each of the data types described in

- 1. (Practice) Exercise 1 of Section 13.1.
- 2. (Practice) a. Using the data type
```cpp
struct MonthDays
{
    string name;
    int days;
};
```
define an array of 12 structures of type MonthDays. Make the array initialize the array with the names of 12 months in a year and the number of days in each month.
b. Include the array created in Exercise 2a in a program that displays the names and days in each month.
- 3. (Modify) Using the data type declared in Exercise 2a, write a C++ program that accepts a month in numerical format and displays the names and the number of days in the month. For example, in response to input of 3, the program would display 31 days.
- 4. (Data Processing) a. Declare a single structure data type suitable for employee in the following chart:

| Number | Name | Rate | Hours |
| :--- | :--- | :--- | :--- |
| 3462 | Jones | 4.62 | 40 |
| 6793 | Robbins | 5.83 | 38 |
| 6985 | Smith | 5.22 | 45 |
| 7834 | Swain | 6.89 | 40 |
| 8867 | Timmins | 6.43 | 35 |
| 9002 | Williams | 4.75 | 42 |

b. Using the data type declared in Exercise 4a, write a C++ program that interactively accepts the chart's data in an array of six structures. After the data has entered, the program should create a payroll report listing employee's name, number, and gross pay. Include the total gross pay of all employees at the end of the report.
- 5. (Data Processing) a. Declare a single structure data type suitable for car in the following chart:

| Car Number | Miles Driven | Gallons Used |
| :--- | :--- | :--- |
| 25 | 1450 | 62 |
| 36 | 3240 | 136 |
| 44 | 1792 | 76 |
| 52 | 2360 | 105 |
| 68 | 2114 | 67 |

b. Using the data type declared for Exercise 5a, write a C++ program that interactively accepts the chart's data in an array of five structures. After the data has entered, the program should create a report listing each car number and the car's miles per gallon. At the end of the report, include the average miles per gallon for the entire fleet of cars.

# 13.3 Structures as Function Arguments

Structure members can be passed to a function in the same manner as any scalar variable. For example, given the structure definition

```cpp
struct {
  int idNum;
  double payRate;
  double hours;
}
```
the following statement passes a copy of the structure member emp.idNum to a function named display():

```cpp
display(emp.idNum);
```

Similarly, the statement

```cpp
calcPay(emp.payRate, emp.hours);
```

passes copies of the values stored in structure members emp.payRate and emp.hours to values stored in structure members emp.payRate and emp.hours to the calcPay() function. Both functions, display() and calcPay(), must declare the correct data types for their arguments.

Copies of all structure members can also be passed to a function by including the structure as an argument to the called function. For example, this function passes a copy of the emp structure to calcNet():

```cpp
calcNet(emp);
```

# Chapter 13 Structures as Function Arguments

Inside calcNet(), a declaration must be made to receive the structure. Program 13.4 declares a global data type for an employee structure. The main() and calcNet() functions use this data type to define structures with the names emp and temp.

# Program 13.4

The output produced by Program 13.4 is as follows:

The net pay for employee 6782 is $361.66

# Structures

In reviewing Program 13.4, observe that both main() and calcNet() use the same data type to define their structure variables. The structure variable defined in main() and the structure variable defined in calcNet() are different structures. Any changes made to the local variable in calcNet() aren't reflected in the emp variable of main(). In fact, because both structure variables are local to their functions, the same variable name could have been used in both functions with ambiguity.

When calcNet() is called by main(), copies of emp's structure values are passed to the temp structure, which is then returned to main(). Because calcNet() returns a non-integer, the data type of the returned value must be included in all declarations for calcNet().

An alternative to the pass-by-value call in Program 13.4, which the function receives a copy of the structure, is a pass by reference that passes a reference to a structure. Doing so permits the function to access and alter values directly in the calling function's structure. For example, referring to Program 13.4, the prototype of calcNet() can be modified to the following:

```cpp
double calcNet(Employee&);
```

If this function prototype is used and the calcNet() function is rewritten to conform to it, the main() function in Program 13.4 can be used as is. Program 13.4a shows changes in the context of a complete program.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_739_0.png)

# Program 13.4a

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

struct Employee    // declare a global data type
{
    int idNum;
    double payRate;
    double hours;
};

double calcNet(Employee&);    // function prototype

int main()
{
    Employee emp = {6782, 8.93, 40.5};
    double netPay;
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_739_1.png)

# Chapter 13
## 721
Structures as Function Arguments

```cpp
netPay = calcNet(emp); // pass a reference
// set output formats
cout << setw(10)
 << setiosflags(ios::fixed)
 << setiosflags(ios::showpoint)
<< setprecision(2);
```

```cpp
cout << "The net pay for employee " << emp.idNum
     << is $" << netPay << endl;

return 0;
}

double calcNet(Employee& temp) // temp is a reference variable
{
    return temp.payRate * temp.hours;
}
```

Program 13.4a produces the same output as Program 13.4, except the calcNet() function in 13.4a receives direct access to emp instead of a copy. This means the variable name temp in calcNet() is an alternate for the variable emp in main(), and any changes to emp are direct changes to emp.
