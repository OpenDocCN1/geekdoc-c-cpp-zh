```
// close file
file.close();
// Exit program.
return 0;
}
bool isPeak(const double grid[][N], int i, int j)
{
    if ((grid[i-1][j]<grid[i][j]) &&
        (grid[i+1][j]<grid[i][j]) &&
        (grid[i][j-1]<grid[i][j]) &&
        (grid[i][j+1]<grid[i][j]))
        return true;
    else
        return false;
}
/******************************/
```

# 5. TESTING

The following output was printed using a data file that corresponds to the hand example (recall that this file must contain a special first line that specifies the number of rows and columns in the elevation data):

```
Top Left point defined as row 0, column 0
Peak at row: 2 column: 1
Peak at row: 2 column: 5
Peak at row: 4 column: 3
```

# Modify!

Modify the peak-finding program as follows:

+   1. Print a count of the number of peaks in the grid.
+   2. Print the location of valleys instead of peaks. Assume that a valley is a point with an elevation lower than the four surrounding elevations. Write a boolean function named isValley to be called by your program.
+   3. Find and print the location and elevation of the highest point and the lowest point in the elevation data. Write a function named extremes to be called by your program.
+   4. Assuming that the distance between points in a vertical and horizontal direction is 100 feet, give the location of the peaks in feet from the lower left corner of the grid.
+   5. Modify the function isPeak() to use all eight neighboring points in determining a peak instead of only four neighboring points.
+   6. Add pre-conditions to the function isPeak().