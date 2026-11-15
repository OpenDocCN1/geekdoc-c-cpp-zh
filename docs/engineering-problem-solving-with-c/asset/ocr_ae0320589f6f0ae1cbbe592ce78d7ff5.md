# 1. PROBLEM STATEMENT

Using the polynomials that represent the altitude and velocity for a weather balloon, print a table using units of meters and meters per second. Also find the maximum altitude (or height) and its corresponding time.

# 2. INPUT/OUTPUT DESCRIPTION

The following I/O diagram shows the user input that represents the starting time, time increment, and ending time for the table. The output is the table of altitude and velocity values and the maximum altitude and its corresponding time. We can use the built-in data type double for our input and output objects.

![](bbox=[0.225, 0.355, 0.785, 0.485])

# 3. HAND EXAMPLE

Assume that the starting time is 0 hours, the time increment is 1 hour, and the ending time is 5 hours. To obtain the correct units, we need to divide the velocity value in meters per hour by 3600 in order to get meters per second. Using our calculator, we can then compute the following values:

| Time | Altitude (m) | Velocity (m/s) |
|---|---|---|
| 0 | 220.00 | 1.14 |
| 1 | 3,951.88 | 0.94 |
| 2 | 6,994.08 | 0.76 |
| 3 | 9,414.28 | 0.59 |
| 4 | 11,277.28 | 0.45 |
| 5 | 12,645.00 | 0.32 |

We can also determine the maximum altitude for this table, which is 12,645.00 meters; it occurred at 5 hours.

# 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it breaks the solution into a series of sequential steps.