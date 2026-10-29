Following is a sample run of Program 7.2:

```
Enter a grade: 85
Enter a grade: 90
Enter a grade: 78
Enter a grade: 75
Enter a grade: 92

The total of the grades 85 90 78 75 92 is 420
```

Note that in Program 7.2, unlike Program 7.1, only the values stored in each array element are displayed. Although the second for loop is used to accumulate the total of each element, the accumulation could also have been accomplished in the first for loop by placing the statement total = total + grade[i]; after the cin statement used to enter a value. Also, the cout statement used to display the total is placed outside the second for loop so that the total is displayed only once, after all values have been added to the total. If this cout statement were placed inside the for loop, five totals would be displayed, with only the last displayed total containing the sum of all array values.

# EXERCISES 7.1

+   1. **(Practice)** Write array declarations for the following:
+      a. A list of 100 integer grades
+      b. A list of 50 double-precision temperatures
+      c. A list of 30 characters, each representing a code
+      d. A list of 100 integer years
+      e. A list of 32 double-precision velocities
+      f. A list of 1000 double-precision distances
+      g. A list of 6 integer code numbers

+   2. **(Practice)** Write correct notation for the first, third, and seventh elements of the following arrays:
+      a. `int grades[20]`
+      b. `double prices[10]`
+      c. `double amounts[16]`
+      d. `int dist[15]`
+      e. `double velocity[25]`
+      f. `double time[100]`

+   3. **(Practice)**
+      a. Write input statements using `cin` that can be used to enter values in the first, third, and seventh elements of each array declared in Exercise 2.
+      b. Write a `for` loop that can be used to enter values for each array declared in Exercise 2.