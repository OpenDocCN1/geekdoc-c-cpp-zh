# 13.2.2 Higher-Dimensional Arrays

To illustrate the use of an array with more than two dimensions, consider again the collection of water temperatures recorded four times a day at each of three discharge outlets of the cooling system of a nuclear power plant.

| Time | Location | | |
| | Outlet-A | Outlet-B | Outlet-C |
| 12 A.M. | 65.5 | 68.7 | 62.0 |
| 6 A.M. | 68.8 | 68.9 | 64.5 |
| 12 P.M. | 70.4 | 69.4 | 66.3 |
| 6 P.M. | 68.5 | 69.1 | 65.8 |

Suppose now that these temperatures are recorded for 1 week, so that seven such tables are collected:

| Time | Location | | |
| | Outlet-A | Outlet-B | Outlet-C |
| 12 A.M. | 66.5 | 69.4 | 68.4 |
| 6 A.M. | 68.4 | 71.2 | 69.3 |
| 12 P.M. | 70.1 | 71.9 | 70.2 |
| 6 P.M. | 69.5 | 70.0 | 69.4 |
Saturday

| Time | Location | | |
| | Outlet-A | Outlet-B | Outlet-C |
| 12 A.M. | 63.7 | 66.2 | 64.3 |
| 6 A.M. | 64.0 | 66.8 | 64.9 |
| | | | 66.3 |
| | | | 65.8 |
Monday

| Time | Location | | |
| | Outlet-A | Outlet-B | Outlet-C |
| 12 A.M. | 65.5 | 68.7 | 62.0 |
| 6 A.M. | 68.8 | 68.9 | 64.5 |
| 12 P.M. | 70.4 | 69.4 | 66.3 |
| 6 P.M. | 68.5 | 69.1 | 65.8 |
Sunday

The collection of these tables can be modeled with a three-dimensional array object, declared by

```
const int NUM_DAYS = 7, NUM_TIMES = 4, NUM_OUTLETS = 3;

typedef double
    ThreeDimTemperatureArray[NUM_DAYS][NUM_TIMES][NUM_OUTLETS];

ThreeDimTemperatureArray temperature;
```

The object temperature can then be used to store these 84 temperature readings.
A single subscript is used to access elements in a one-dimensional array and two subscripts are used to access elements in a two-dimensional array, so it seems reasonable that three subscripts are needed to access an element in a three-dimensional array. The first