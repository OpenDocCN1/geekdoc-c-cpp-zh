268 Learning SAS as Example: A Programmer's Guide, Second Edition

# Program 16.7: Outputting More Than One Statistic with PROC MEANS

```
proc means data=Learn.Blood noprint;
  var RBC WBC;
  output out = Many_Stats
    mean = M_RBC M_WBC
    n = N_RBC N_WBC
    nmiss = Miss_RBC Miss_WBC
    median = Med_RBC Med_WBC;
run;
```

So, you get it. You can output as many statistics as you want and name anything you want. A listing of this data set, using PROC PRINT, is shown here:

**Figure 16.7: Listing of Data Set Many_Stats**

| TYPE | FREQ | RBC | WBC | N_RBC | N_WBC | Miss_RBC | Miss_WBC | Med_RBC | Med_WBC |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1000 | 5.48335 | 70.427 | 916 | 908 | 84 | 92 | 5.52 | 70.40 |

The two variables M_RBC and M_WBC represent the means of RBC and WBC, respectively. The two variables Med_RBC and Med_WBC are the medians of the variables. N_RBC and N_WBC represent the number of nonmissing values; Miss_RBC and Miss_WBC represent the number of missing values for these variables. As a check, notice that N_RBC plus Miss_WBC equals 1,000, the total number of observations in data set Blood.

# 16.9 Asking SAS to Name the Variables in the Output Data Set

You can ask SAS to create variable names for any of the summary statistics produced by PROC MEANS. The OUTPUT AUTONAME causes PROC MEANS to create variable names for the selected statistics using the variable names in the VAR statement and an underscore character followed by the name of the statistic. The best way to see this is to look at a program and a listing of the output data set:

# **Program 16.8: Demonstrating the OUTPUT Option AUTONAME**

```
proc means data=Learn.Blood noprint;
  var RBC WBC;
  output out = Many_Stats
    mean =
    n =
    nmiss =
    median = / autoname;
run;
```

Because AUTONAME is a statement option, it follows a slash in the OUTPUT statement. Take a look at a listing of this data set to see how SAS named these variables: