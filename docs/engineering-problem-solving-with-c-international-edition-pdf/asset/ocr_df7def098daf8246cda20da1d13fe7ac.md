# Program Output

Problems 11-13 refer to the following statements:

```
string strng1 = "abc", strng2 = "ABC", strng3 = "123";
```

+   11. What is the output of the following statement?

```
cout << strng3.size() << endl;
```

+   12. What is the output of the following statement?

```
cout << ((strng1==strng2)?strng1:strng2) << endl;
```

+   13. What is the output of the following statements?

```
strng1 += strng2;
cout << strng1 << endl;
```

# Programming Exercises

**Linear Interpolation.** The following problems refer to the wind-tunnel test data stored in the file tunnel.dat. The file contains the set of data which consists of a flight-path angle (in degrees) and its corresponding coefficient of lift on each line in the file. The flight-path angles will be in ascending order.

+   14. Write a program that reads the wind-tunnel test data and then allows the user to enter a flight-path angle. If the angle is within the bounds of the data set, the program should then use linear interpolation to compute the corresponding coefficient of lift. (You may need to refer to the section on linear interpolation in Section 2.5.)

+   15. Modify the program in Problem 14 so that it prints a message to the user giving the range of angles that are covered in the data file after reading the values.

+   16. Write a function that could be used to verify that the flight-path angles are in ascending order. The function should return a zero if the angles are not in order and a 1 if they are in order. Assume that the corresponding function prototype is

```
int ordered(double x[], int num_pts);
```

+   17. Write a function that receives two one-dimensional array that correspond to the flight-path angles and the corresponding coefficients of lift. The function should sort the flight-path angles into ascending order while maintaining the correspondence between the flight-path angles and the corresponding coefficients of lift. Assume that the corresponding function prototype is

```
void reorder(double& x, double& y);
```

+   18. Modify the program developed in Problem 14 such that it uses the function developed in Problem 16 to determine whether the data are in the desired order. If they are not in the desired order, use the function developed in Problem 17 to reorder them.