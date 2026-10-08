# APPENDIX F

# Classes and Objects

calc method that contains two double parameters and then assign the return value to the program's gross variable. In the GrossPay class, the calcGross method that contains two double parameters calculates and returns the gross pay amount for an hourly worker. Before the program ends, it displays the contents of its gross variable on the computer screen. Sample runs of the gross pay program are shown in Figures F-17 and F-18.

714

```
1 // GrossPay.cpp
2 //Displays the gross pay for salaried and
3 //hourly employees
4 //Created/revised by <your name> on <current date>
5
6 #include <iostream>
7 #include <iomanip>
8 #include "GrossPay.h"
9 using namespace std;
10
11 int main()
12 {
13 //createGrossPay object
14 GrossPay employee;
15 //declare variables
16 int employeeType = 0;
17 double salary = 0.0;
18 double hours = 0.0;
19 double hrlyPay = 0.0;
20 double gross = 0.0;
21
22 cout << fixed << setprecision(2);
23
24 //determine employee's type
25 cout << "Salaried" (1) or Hourly (2): ";
26 cin >> employeeType;
27
28 if (employeeType == 1)
29 {
30 cout << "Annual salary: ";
31 cin >> salary;
32 gross = employee.calcGross(salary);
33 }
34 else
35 if (employeeType == 2)
36 {
37 cout << "Hours worked: ";
38 cin >> hours;
39 cout << "Hourly pay: ";
40 cin >> hrlyPay;
41 gross =
42 employee.calcGross(hours, hrlyPay);
43 }
44 else
45 cout << "Incorrect employee type.";
46 c++ << endl;
47 //end if
48 //end if
```

Figure F-16 Gross pay program (continues)