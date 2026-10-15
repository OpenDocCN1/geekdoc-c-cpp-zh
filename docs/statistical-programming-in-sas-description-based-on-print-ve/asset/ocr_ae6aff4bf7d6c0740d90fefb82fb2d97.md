# Display 9.4 Expanding a single record into multiple records

```
data D6;
    input name $ sex $ t1 t2 t3 t4 t5 time6 time_7;

ARRAY num_array{*} _NUMERIC_;
DO inum = 1 to dim(num_array);
    time = inum;
    ADL = num_array{inum};
    output;
END;
keep name sex time ADL;

datalines;
Smith M 6 6 5 5 5 4 3
Jones F 7 5 4 4 3 2 1
Fisher M 5 5 5 3 2 2 1
;
run;
```

The array statement collects all of the numeric variables. The dim function returns the length of this array (=7 in this example). The time variable is defined in the loop, and the ADL variable is defined in terms of each array element. The results of this iterative assignment are output to the data set. (The data set is cleverly named D6 because this is the sixth data set defined in this chapter. Perhaps rereading Chapter 1 about naming data sets would be helpful.) Only four of the variables are preserved in the data set by the keep statement. Try this at home: See what happens if you run this code without the keep statement.

As a final remark about arrays, an array can be defined in more than one dimension, although you might prefer to use matrices in PROC IML before resorting to higher dimensional data arrays.

# 9.2 Case Study 1: Monte Carlo p-Value for Test of Spatial Randomness

A p-value, the probability of observing a test statistic at least as extreme as the observed value of the test statistic when the null hypothesis is true, is commonly reported in statistical inference. When the sampling distribution of a test statistic has a familiar form, standard statistical distributions (e.g., t or F) can be used to calculate the p-value. In other cases, it might be very difficult to calculate a p-value if the test statistic does not have a familiar form. In the following example, arrays are used in a Monte Carlo calculation of a p-value based on an average nearest-neighbor test statistic.