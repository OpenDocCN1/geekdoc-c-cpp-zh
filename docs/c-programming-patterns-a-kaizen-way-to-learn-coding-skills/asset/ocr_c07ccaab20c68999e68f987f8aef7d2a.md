For the upper_limit of variable **space** at **row = 0**, the value will be (2*0 – 1) or -1. The lower_limit value of variable **space** at **row = 0** is also 0, so the loop-condition (0 < -1) will fail and no space will get printed. This holds true even for loop-condition (1 < -1).

Hence, we are in a position to get generalised expression for lower_limit and upper_limit.

| loop-condition | lower_limit <= space <= upper_limit |
|---|---|
| **Mathematical expression** | 1 <= space <= (2* row -1) |
| Syntax | `for ( space = 1 ; space <= ( 2* row – 1 ) ; space++)` |

This time somehow we are able to generalise the expressions otherwise we need to follow if-else condition as we did for the variable **numDec** using temporary variable **ul_numDec**.

# *Alternate solution*

| **Row level Repetitive Action** |||||
|---|---|---|---|---|
| row | **Column level Repetitive Action** ||||
| | **Variable :col** | **Variable :col** | **Variable :col** | **Output** |
| | **Output** | **spaces** | | **Output** |
| 1 | 1, 2, 3, 4 | Print 5 (no space) | 6, 7, 8, 9 | 4, 3, 2, 1 |
| 2 | 1, 2, 3, 4 | 5 | 6, 7, 8, 9 | 4, 3, 2, 1 |
| 3 | 1, 2, 3 | 4, 5, 6 | 7, 8, 9 | 3, 2, 1 |
| 4 | 1, 2 | 3, 4, 5, 6, 7 | 8, 9 | 2, 1 |
| 5 | 1 | 2, 3, 4, 5, 6, 7, 8 | 9 | 1 |

| **Row level Repetitive Action** |||||||
|---|---|---|---|---|---|---|---|
| row | **Column level Repetitive Action** (1 <= col <= 9) ||||||
| | **Print numbers** || **Print spaces** || **Print numbers** || **Output** |
| | lower_limit | upper_limit | lower_limit | upper_limit | lower_limit | upper_limit | |
| 1 | 1 | 4 | Print 5 | | 6 | 9 | 4, 3, 2, 1 |
| 2 | 1 | 4 | 5 | 5 | 6 | 9 | 4, 3, 2, 1 |
| 3 | 1 | 3 | 4 | 6 | 7 | 9 | 3, 2, 1 |
| 4 | 1 | 2 | 3 | 7 | 8 | 9 | 2, 1 |
| 5 | 1 | 1 | 2 | 8 | 9 | 9 | 1 |

For printing characters at the first row, means at row=1, this pattern doesn't required to print any space. So for the sake of initialization we can give it's upper_limit value as -1 and lower_limit value as 0. If we observe for printing spaces, the numeric pattern is such that the lower_limit value is less than upper_limit value for every row except the first row. This will help to allow condition to be fail and we will be not able to print space in the first row. This what we need.

Moreover it's one of the common practice to initialize variable with invalid data in order to verify validity of the programming logic whenever that programming logic gets executed. The values of variable acts like a check point whether the programming logic executes as per expected or not and this our purpose of doing exercises on programming patterns to be able to visualize the flow of data.