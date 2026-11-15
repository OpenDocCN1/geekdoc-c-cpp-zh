```
```cpp
// Determine sums for the direction categories.
for (r=0; r<=4; +++)
   for (c=0; c<=4; c++)
   {
      k = grid[r][c];
      category[k]++;
   }

// Determine category with maximum sum.
for (k=0; k<=7; k++)
   if (category[k] > category[maxk])
      maxk = k;

// Print report.
cout.setf(ios::fixed);
cout.precision(1);
perc = (double)category[maxk]/25*100;
cout << "The wind is blowing from the "
     << direction[maxk-1]
     << perc << "% of the time." << endl;

// Close file.
winds.close();
}

// Exit program.
return 0;
}
//-----------------------------------------------
```
```

# 5. TESTING

Using the data from the hand example, the output from the program should appear as follows:

The wind is blowing from the SE 76 % of the time.

# MODIFY!

These problems relate to the program developed in this section for determining primary wind direction.

+   1. Modify the program to print the number of values in each category, using direction notation (such as SE).
+   2. Modify the program to print more than one output line if there is more than one direction with the same number of maximum values.
+   3. Modify the program to print the message "Possible cyclone or hurricane" if there are winds in all four quadrants of the compass.
+   4. Modify the program so that it prints a grid to demonstrate the direction of the winds. For example, it could print the character '>' if the wind is from the W, and '<' if the wind is from the E. Choose characters for all eight wind directions.
+   5. Modify the program so that it reads the grid size (number of rows and number of columns) from the first row of the data file. Assume a maximum of 100 rows by 100 columns.