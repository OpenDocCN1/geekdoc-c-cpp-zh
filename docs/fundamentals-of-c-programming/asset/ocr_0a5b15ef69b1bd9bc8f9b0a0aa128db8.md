| x | f(x) | h | Approx. f'(x) | Actual f'(x) |
|---|---|---|---|---|
| 5.000000 | 80.000000 | 0.000000 | 30.000000 | 30.000000 |
| 5.010000 | 80.300300 | 0.000000 | 30.060000 | 30.060000 |
| 5.020000 | 80.601200 | 0.000000 | 30.120000 | 30.120000 |
| 5.030000 | 80.902700 | 0.000000 | 30.180000 | 30.180000 |
| 5.040000 | 81.204800 | 0.000000 | 30.240000 | 30.240000 |
| 5.050000 | 81.507500 | 0.000000 | 30.300000 | 30.300000 |
| 5.060000 | 81.810800 | 0.000000 | 30.360000 | 30.360000 |
| 5.070000 | 82.114700 | 0.000000 | 30.420000 | 30.420000 |
| 5.080000 | 82.419200 | 0.000000 | 30.480000 | 30.480000 |
| 5.090000 | 82.724300 | 0.000000 | 30.540000 | 30.540000 |
| 5.100000 | 83.030000 | 0.000000 | 30.600000 | 30.600000 |

Even with h as large as 0.01, the results are not too bad:

| x | f(x) | h | Approx. f'(x) | Actual f'(x) |
|---|---|---|---|---|
| 5.000000 | 80.000000 | 0.010000 | 30.030000 | 30.000000 |
| 5.010000 | 80.300300 | 0.010000 | 30.090000 | 30.060000 |
| 5.020000 | 80.601200 | 0.010000 | 30.150000 | 30.120000 |
| 5.030000 | 80.902700 | 0.010000 | 30.210000 | 30.180000 |
| 5.040000 | 81.204800 | 0.010000 | 30.270000 | 30.240000 |
| 5.050000 | 81.507500 | 0.010000 | 30.330000 | 30.300000 |
| 5.060000 | 81.810800 | 0.010000 | 30.390000 | 30.360000 |
| 5.070000 | 82.114700 | 0.010000 | 30.450000 | 30.420000 |
| 5.080000 | 82.419200 | 0.010000 | 30.510000 | 30.480000 |
| 5.090000 | 82.724300 | 0.010000 | 30.570000 | 30.540000 |
| 5.100000 | 83.030000 | 0.010000 | 30.630000 | 30.600000 |

In Listing 20.17 (derivative.cpp), the statement
`auto der = derivative(fun, h);`
assigns der to the function returned by derivative; thus, der(x) returns the value of the derivative
of fun at x. In order for der to compute its answer, it must have access to function fun. It has this access
because der is a lambda function that captured fun and h during the call to derivative.

# 20.5 Algorithms in the Standard Library

CAUTION! SECTION UNDER CONSTRUCTION

The flexible design of the STL containers and their iterators make possible the STL’s generic algorithms.
The algorithms provided by the STL are powerful and flexible, but they also are somewhat arcane and can
be difficult to use for casual C++ programmers. The STL algorithms are best viewed as the building blocks
for more specific tasks required by applications.

In order to use the STL algorithms you must include the following preprocessor directive: