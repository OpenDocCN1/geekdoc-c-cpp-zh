```
// set output formats
cout << setw(10)
    << setiosflags(ios::fixed)
    << setiosflags(ios::showpoint)
    << setprecision(2);

cout << "The net pay for employee " << emp.idNum
    << " is $" << netPay << endl;

return 0;
}

double calcNet(Employee temp)  // temp is of data type Employee
{
    return (temp.payRate * temp.hours);
}
```

The output produced by Program 16.4 is as follows:

The net pay for employee 6782 is $361.66

In reviewing Program 16.4, observe that both main() and calcNet() use the same data type to define their structure variables. The structure variable defined in main() and the structure variable defined in calcNet() are two different structures. Any changes made to the local temp variable in calcNet() aren’t reflected in the emp variable of main(). In fact, because both structure variables are local to their functions, the same structure variable name could have been used in both functions with no ambiguity.

When calcNet() is called by main(), copies of emp’s structure values are passed to the temp structure. calcNet() then uses two of the passed member values to calculate a number, which is returned to main(). An alternative to the pass-by-value function call in Program 16.4, in which the called function receives a copy of a structure, is a pass by reference that passes a reference to a structure. Doing so allows the called function to access and alter values directly in the calling function’s structure variable. For example, in Program 16.4, the prototype of calcNet() can be modified to the following:

double calcNet(Employee &);

If this function prototype is used and the calcNet() function is rewritten to conform to it, the main() function in Program 16.4 can be used as is. Program 16.4a shows these changes in the context of a complete program, with the two changed statements shaded.