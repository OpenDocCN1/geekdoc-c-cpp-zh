that is to replace the letter b in the data file, and so on. Assume that all punctuation is to be replaced by spaces. Check to be sure that the key does not map two different characters to the same one during the encoding.

+   36. Write a program that decodes the file that is the output of Problem 35. Assume that the same integer key is read from the keyboard by this program, and is used in the decoding steps. Note that you will not be able to restore the punctuation characters.

# Temperature Distribution.

The temperature distribution in a thin metal plate with constant (or isothermal) temperatures on each side can be modeled using a two-dimensional grid, as shown in Figure 5.10. Typically, the number of points in the grid are specified, as are the constant temperatures on the four sides. The temperatures of the interior points are usually initialized to zero, but they change according to the temperatures around them. Assume that the temperature of an interior point can be computed as the average of the four adjacent temperatures; the points shaded in Figure 5.10 represent the average temperatures for the point labeled x in the grid. Each time that the temperature of an interior point changes, the temperatures of the points adjacent to it change. These changes continue until a thermal equilibrium is achieved and all temperatures become constant.

+   37. Write a program to model this temperature distribution for a grid with six rows and eight columns. Allow the user to enter the temperatures for the four sides. Use one array to store the temperatures. Thus, when a point is updated, its new value is used to update the next point. Continue updating the points, moving across the rows until the temperature differences for all entries are less than a user-entered tolerance value.

+   38. Modify the program generated in Problem 37 so that the updates are performed down the columns. Compare the equilibrium values for the two programs using different tolerance values. The equilibrium values should be very close for small tolerance values.

+   39. Modify the program in Problem 37 so that two arrays are used and so that the program can perform the updates as if they all happen at the same time. Thus, all temperatures are updated using one set of array values. The two arrays are needed so that all the old temperatures are available to compute each new temperature.

# Gauss Elimination.

The accuracy of the Gauss elimination technique can be improved using a process called pivoting. To perform row pivoting, we first reorder the equations so that the equation with the largest absolute value for the first coefficient is the first equation. We then eliminate the first variable from the equations that follow the first equation. Then, starting with the second equation, we reorder the equations such that the second equation has the largest coefficient (in absolute value) for the second variable. We then eliminate the second

![](bbox=[0.45, 0.72, 0.7, 0.86])

Figure 5.10 Temperature grid in a metal plate.