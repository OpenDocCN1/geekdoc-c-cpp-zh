```
```cpp
cout << setw(5) << miles << setw(5) << speed
     << setw(6) << hours
     << setw(7) << error << endl << endl;            //Line 14

cout << setw(5) << speed << setw(5) << miles
     << setw(4) << hours
     << setw(7) << error << endl << endl;            //Line 15

cout << setw(2) << miles << setw(6) << hours
     << setw(7) << error << endl << endl;            //Line 16

cout << setw(2) << miles
     << setw(7) << "error"
     << error << endl;                              //Line 17
return 0;                                           //Line 18
}                                                   //Line 19
```
```

# Sample Run:

```
```text
123456789012345678901234567890
  245
  245   55 35.45   3.76

   55  24535.45   3.76

245 35.45   3.76

245  error3.76
```
```

The statements in Lines 6, 7, 8, and 9 declare the variables miles, speed, hours, and error, and initialize these variables to 245, 55, 35.45, and 3.7564, respectively. The statement in Line 10 sets the output of floating-point numbers in a fixed decimal format with a decimal point and trailing zeros. The output of the statement in Line 11 shows the column positions when the specific values are printed; it is the first line of output.

The statement in Line 12 outputs the value of miles in five columns. Because miles has only three digits, only three columns are needed to output its value. Therefore, the first two columns are left blank in the second line of output.

The statement in Line 13 sets the output of floating-point numbers to two decimal places. The statement in Line 14 outputs the value of miles in the first five columns, the value of speed in the next five columns, the value of hours in the next six columns, and the value of error in the next seven columns. Because hours contains four digits and a decimal point, five columns are required to output the value of hours. Also, because the setw function sets the output of hours in six columns, the first column is left blank. Similarly, the value of error is output in seven columns leaving the first three columns blank. The fourth line of output is blank because the manipulator endl appears twice in the statement in Line 14.

The statement in Line 15 outputs the values of speed in the first five columns, miles in the next five columns, the value of hours in the next four columns, and error in