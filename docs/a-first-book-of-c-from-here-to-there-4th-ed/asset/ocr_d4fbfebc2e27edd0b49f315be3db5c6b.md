```
// set output formats for floating-point numbers only
cout << setiosflags(ios::showpoint) << setiosflags(ios::fixed)
    << setprecision(2);

while (celsius <= MAXCELSIUS)
{
    fahren = (9.0/5.0) * celsius + 32.0;
    cout << setw(4) << celsius
         << setw(13) << fahren << endl;
    celsius = celsius + STEPSIZE;
}

return 0;
}
```

This is the display produced when Program 5.4 runs:

| DEGREES | DEGREES |
| CELSIUS | FAHRENHEIT |
| ----- | ----- |
| 5 | 41.00 |
| 10 | 50.00 |
| 15 | 59.00 |
| 20 | 68.00 |
| 25 | 77.00 |
| 30 | 86.00 |
| 35 | 95.00 |
| 40 | 104.00 |
| 45 | 113.00 |
| 50 | 122.00 |

# EXERCISES 5.1

+   1. (Modify) Rewrite Program 5.1 to print the numbers 2 to 10 in increments of 2. The output of your program should be the following:
+      2 4 6 8 10
+   2. (Modify) Rewrite Program 5.4 to produce a table starting at a Celsius value of -10 and ending with a Celsius value of 60, in increments of 10 degrees.
+   3. (Desk check) a. For the following program, determine the total number of items displayed as well as the first and last numbers printed:
+      #include <iostream>
+      using namespace std;