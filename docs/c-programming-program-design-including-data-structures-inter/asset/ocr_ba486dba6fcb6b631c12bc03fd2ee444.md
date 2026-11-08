```
```cpp
cout << "Line 23: volume = "
     << PI * radius * radius * height << endl;    //Line 23
cout << "Line 24: PI = " << PI << endl;           //Line 24

cout << "Line 25: "
     << setprecision(3) << radius << ", "
     << setprecision(2) << height << ", "
     << setprecision(5) << PI << endl;             //Line 25

return 0;                                          //Line 26
}                                                  //Line 27
```
```

# Sample Run:

```
```text
Line 10: setprecision(2)
Line 11: radius = 12.67
Line 12: height = 12.00
Line 13: volume = 6051.80
Line 14: PI = 3.14

Line 15: setprecision(3)
Line 16: radius = 12.670
Line 17: height = 12.000
Line 18: volume = 6051.797
Line 19: PI = 3.142

Line 20: setprecision(4)
Line 21: radius = 12.6700
Line 22: height = 12.0000
Line 23: volume = 6051.7969
Line 24: PI = 3.1416

Line 25: 12.670, 12.00, 3.14159
```
```

In this program, the statement in Line 2 includes the header file iomanip, and the statement in Line 4 declares the named constant PI and sets the value to eight decimal places. The statements in Lines 7 and 8 declare and initialize the variables radius and height to store the radius of the base and the height of a cylinder. The statement in Line 10 sets the output of floating-point numbers in a fixed decimal format with a decimal point and trailing zeros.

The statements in Lines 11, 12, 13, and 14 output the values of radius, height, volume, and PI to two decimal places.

The statements in Lines 16, 17, 18, and 19 output the values of radius, height, volume, and PI to three decimal places.

The statements in Lines 21, 22, 23, and 24 output the values of radius, height, volume, and PI to four decimal places.

The statement in Line 25 outputs the value of radius to three decimal places, the value of height to two decimal places, and the value of PI to five decimal places.