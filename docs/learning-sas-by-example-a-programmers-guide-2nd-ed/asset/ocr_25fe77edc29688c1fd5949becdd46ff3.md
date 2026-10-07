An OUTPUT statement tells PROC MEANS that you want to create a summary SAS data set. In this example, you are going to name your output data set My_Summary. Next, you can specify what statistics you want in this data set. You can output most of the statistics listed earlier in this chapter. Following the keyword and an equal sign, provide a list of names that correspond to these values. In program, the variable MeanBC is the mean of all the RBC values, and MeanBC is the mean of all the WBC values. You can name these anything you want—they are arbitrary. The order of the variables here corresponds to the order of the variables in the VAR list. It is convenient to name these variables in a way that helps you remember what they stand for. Shortly, SAS will name these variables for you in a very convenient way. Finally, if you want to create a SAS data set but do not want any printed output from PROC MEANS, use the NOPRINT option. As we mentioned earlier, if you choose to use PROC SUMMARY instead of PROC MEANS, you do not need a NOPRINT option—it is the default for that procedure.

Program 16.6 includes a PROC PRINT statement so that you can see the contents of the output data set. Here is the listing of the summary data set My_Summary:

Figure 16.6: Output from Program 16.6

| _TYPE | FREQ | MeanRBC | MeanWBC |
|---|---|---|---|n| 0 | 1000 | 5.48353 | 7042.97 |

This data set has only one observation. It includes the two means plus additional variables created by PROC MEANS. We will discuss these two variables later when we run the procedure with a CLASS statement.

When you are outputting only a single statistic (such as a mean in the previous example), you can omit the variable list following the keyword MEAN= if you want. If you do SAS gives these summary variables the same names as the variables listed in the VAR statement. **It is strongly recommended that you do not do this.** It is easy to make a mistake when you have the same variable name in two data sets, with one representing individual values and the other representing a summary statistic.

# 16.6 Outputting Other Descriptive Statistics with PROC MEANS

As we mentioned earlier, you can output more than one statistic in your output data set. For an example, let's output the mean, the number of nonmissing observations, the number of missing observations, and the median. Here is the program: