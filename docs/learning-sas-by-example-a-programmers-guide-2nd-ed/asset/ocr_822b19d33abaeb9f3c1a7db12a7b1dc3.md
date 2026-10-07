# 14 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 2.5: Output from Program 2.1

| Gender | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|---|---|---|---|---||
| F | 2 | 40.00 | 2 | 40.00 |
| M | 3 | 60.00 | 5 | 100.00 |

Summary Statistics

| Variable | N | Std Dev | Minimum | Maximum |
|---|---|---|---|---||
| Age | 5 | 37.6000000 | 20.2188031 | 15.0000000 | 65.0000000 |
| Height | 5 | 67.2000000 | 4.8622646 | 60.0000000 | 72.0000000 |
| Weight | 5 | 155.0000000 | 44.0056815 | 101.0000000 | 220.0000000 |

What you see is the Output window.(The exact appearance of these windows will vary, depending on how you set up SAS.) The top part of the output (produced by PROC FREQ) shows that there were two females and three males in the data set (the numbers listed under Frequency). The column labeled shows the frequencies as a percent of all the non-missing listed values in the data set. The last two columns display Cumulative Frequency and Cumulative Percentages. There were two females (representing 40% of the subjects) and two plus three five males females, which are referred to as a cumulative frequency,(representing 100% of the subjects). The Cumulative Percent show the cumulative counts as percentages. You will see later how to eliminate these last two columns because they are seldom used.

Below the frequency display see Summary Statistics for the three numeric variables (produced by PROC MEANS). N is the number of non-missing values, Mean is the arithmetic mean, Std Dev is the standard deviation, Minimum and Maximum are the smallest non-missing value and the largest value, respectively.

Notice the two titles correspond to the text you placed in the TITLE statement.

> Note: By default, SAS centers all output. For most of the output in this book, a system called NOCENTER was used so that the output is left-justified. The statement (not shown here) Options NOCENTER was included at the beginning of every program.

You can switch among the three windows by clicking the appropriate tab at the bottom of the screen. These tabs will be located in other places if you are using Enterprise Guide or SAS Studio, but you will have no trouble finding them. The tabs for the windowing environment are in Figure 2.6.