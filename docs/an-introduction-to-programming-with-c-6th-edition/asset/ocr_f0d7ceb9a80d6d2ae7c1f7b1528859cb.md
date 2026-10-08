# The Salary Program

the getNewPayInfo: the value of the current salary, the value of the raise rate, the address of the variable where the raise can be stored after it is calculated, and the address of the variable where the new salary can be stored after it is calculated. In other words, the main function passes its currentSalary and raiseRate variables by value, and it passes its raise newSalary variables by reference.

385

# Problem specification
Create a program that allows the user to enter an employee's current salary and raise rate. The program should calculate and display the employee's raise and new salary.

# main function
IPO chart information
Input

C++ instructions

+   current salary
raise rate

double currentSalary = 0.0;
double raiseRate = 0.0;

# Processing
none

# Output
raise
new salary

double raise = 0.0;
double newSalary = 0.0;

+   Algorithm
1. enter the current salary
and raise rate

```
cout << "Current salary": ";
cin >> currentSalary;
out << "raise rate (in decimal format): ";
cin >> raiseRate;
```

+   2. call the getNewPayInfo
function to calculate the raise
and new salary; pass the
function the current salary
and raise rate, as well as the
addresses of variables in which
to store the raise and new salary

```
getNewPayInfo(currentSalary,
raiseRate, raise, newSalary);
```

+   3. display the raise and new salary

```
cout << "Raise: $$" << endl;
cout << "New salary: $$" << newSalary
cout << endl;
```

# getNewPayInfo function
IPO chart information
Input

C++ instructions

+   current salary (formal parameter)
raise rate (formal parameter)
addresses of variables to store:
raise (formal parameter)
new salary (formal parameter)

double current
double rate
double &pay

Figure 10-18 Problem specification, IPO chart information, and C++ instructions for the
salary program (continues)