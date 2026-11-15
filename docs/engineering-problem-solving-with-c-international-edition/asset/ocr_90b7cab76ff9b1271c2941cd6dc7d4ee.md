```
10. int r, c, x[4][5];
...
for (r=0; r<=3; r++)
for (c=0; c<=4; c++)
x[r][c] = r + c;
```

# Program Output

Problems 11 and 12 refer to the following statements:
int sum, k, i, j;
int x[4][4]={{1,2,3,4},{5,6,7,8},{9,8,7,3},{2,1,7,1}};

+   11. Give the value in sum after the following statements are executed:
+   sum = x[0][0];
+   for (k=1; k<3; k++)
+   sum += x[k][k];

+   12. Give the value in sum after the following statements are executed:
+   sum = 0;
+   for (i=1; i<3; i++)
+   for (j=0; j<=3; j++)
+   if (x[i][j] > x[i-1][j])
+   sum++;

# PROGRAMMING PROBLEMS

Linear Interpolation. The following problems refer to wind-tunnel test data available on the companion website. The file contains a flight-path angle (in degrees) and its corresponding coefficient of lift on each line in the file. The flight-path angles will be in ascending order.

+   13. Write a program that reads the wind-tunnel test data, and then allows the user to enter a flight-path angle. If the angle is within the bounds of the data set, the program should use linear interpolation to compute the corresponding coefficient of lift. (You may need to refer to the section on linear interpolation in Section 2.5.)

+   14. Modify the program in Problem 13 so that it prints a message to the user. The message should give the range of angles that are covered in the data file after reading the values.

+   15. Write a function that could be used to verify that the flight-path angles are in ascending order. The function should return a 0 if the angles are not in order and a 1 if they are in order. Assume that the corresponding function prototype is

```
int ordered(double x[], int num_pts);
```

+   16. Write a function that receives two one-dimensional arrays that correspond to the flight-path angles and their coefficients of lift. The function should sort the flight-path angles into ascending order while maintaining the correspondence between the flight-path angles and their coefficients of lift. Assume that the corresponding function prototype is

```
void reorder(double x[], double y[], int num_pts);
```

+   17. Modify the program developed in Problem 14 such that it uses the function developed in Problem 15 to determine whether or not the data are in the desired order. If they are not in the desired order, use the function developed in Problem 16 to reorder them.

Noise Signals. In engineering simulations, we often want to generate a floating-point sequence of values with a specified mean and variance. The function developed in Chapter 4 allows us to generate numbers between limits a and b, but it does not allow us to specify the mean and