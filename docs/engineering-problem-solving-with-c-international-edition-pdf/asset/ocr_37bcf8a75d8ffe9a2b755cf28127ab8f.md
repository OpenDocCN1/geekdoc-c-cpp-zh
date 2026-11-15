```
Point x9:  Short-time power = (1 + 1)/2 = 1
Long-time power = (1 + 1 + 4 + 16 + 25 )/5 = 9.4
Ratio = 1/9.4 = 0.11
1 2 1 1 1 5 4 2 1 1 1
short window
long window
Point x10:  Short-time power = (1 + 1)/2 = 1
Long-time power = (1 + 1 + 1 + 4 + 16 )/5 = 4.6
Ratio = 1/4.6 = 0.22
```

By using the previous ratios computed, possible seismic events occurred at points x5 and x6. Because the time interval between points is 0.01 second, the times that correspond to the seismic events are 0.05 and 0.06 second. (We assume that the first point in the file occurred at 0.0 second.)

# 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it divides the solution into a series of sequential steps.

# Decomposition Outline

+   1. Read data header and allocate memory.
+   2. Read seismic data from the data file and read numbers of measurement for power from the keyboard.
+   3. Compute power ratios and print possible seismic event times.

Step 3 involves computing power ratios and comparing them to the threshold to determine whether a possible event occurred. Because we need to compute two power measurements for each possible event location, we implement the power measurement as a function. The refinement in pseudocode for the main function and the power function can now be developed:

# Refinement in Pseudocode

```
main: set threshold to 1.5
   read npts and time-interval
   allocate memory for sensor array
```