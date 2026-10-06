# FIGURE A-7

A two-dimensional array

| | 0 | 1 | ... | 51 |
|---|---|---|---|---|n| 0 | | | | |
| 1 | | | | |
| ... | | | | |
| 6 | | | | |

# A.6.2 Multidimensional Arrays

You can use a one-dimensional array, which has one index, for a simple collection of data. For example, you can organize 52 temperatures linearly, one after another. A one-dimensional array of these temperatures can represent this organization.

You can also declare multidimensional arrays. Use more than one index to designate an element in a multidimensional array. Suppose that you wanted to represent the minimum temperature for each day during 52 weeks. The following statements declare a two-dimensional array, minTemps:

```
const int DAYS_PER_WEEK = 7;
const int WEEKS_PER_YEAR = 52;
double minTemps[DAYS_PER_WEEK][WEEKS_PER_YEAR];
```

These statements specify the ranges for two indices: the first index can range from 0 to 6, while the second index can range from 0 to 51. Most people picture a two-dimensional array as a rectangular arrangement, or matrix, of elements that form rows and columns. Figure A-7 indicates the first dimension given in the definition of Array is the number of rows. minTemps has 7 rows and 52 columns. Each column in this matrix represents the seven daily minimum temperatures for a particular week.

To reference an element in a two-dimensional array, you must indicate both the row and column index that contain the element. You make these indices of row and column by writing two indices, for example, minTemps[1][15] is the element in the 2nd row and the 5th column. In the context of the temperature example, this element contains the minimum temperature recorded for the 2nd day (Monday) of the 52nd week. The rules for a one-dimensional array also apply to the indices of multidimensional arrays.

As an example of how to use a two-dimensional array in a program, consider the following program segment, which determines the smallest value in the previously described array minTemps. We use enumerators to reference the days of the week.