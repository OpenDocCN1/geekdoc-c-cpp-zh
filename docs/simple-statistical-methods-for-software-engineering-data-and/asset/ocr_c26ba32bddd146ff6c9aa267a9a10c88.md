# Data 16.1 Pareto Distribution of Usage

# Parameters

+   m = 1
+   - 1.2

# Statistics

+   Mean = 6
+   Median = 1.8

| No. of Features | Probability Density Function (PDF) of Usage | Cumulative Distribution Function (CDF) of Usage |
| --- | --- | --- |
| 1 | 0.600 | 0.000 |
| 2 | 0.364 | 0.565 |
| 3 | 0.253 | 0.732 |
| 4 | 0.191 | 0.811 |
| 5 | 0.152 | 0.855 |
| 6 | 0.125 | 0.884 |
| 7 | 0.106 | 0.903 |
| 8 | 0.091 | 0.918 |
| 9 | 0.080 | 0.928 |
| 10 | 0.071 | 0.937 |
| 11 | 0.064 | 0.944 |
| 12 | 0.058 | 0.949 |
| 13 | 0.053 | 0.954 |
| 14 | 0.049 | 0.958 |
| 15 | 0.045 | 0.961 |
| 16 | 0.042 | 0.964 |
| 17 | 0.039 | 0.967 |
| 18 | 0.036 | 0.969 |
| 19 | 0.034 | 0.971 |
| 20 | 0.032 | 0.973 |

Illes-Seifert and Paech set up four Pareto hypotheses and prove each is right.

+   1. Pareto distribution of defects in files: a small number of files accounts for the majority of defects
+   2. Pareto distribution of defects in files across releases
+   3. Pareto distribution of defects in code: a small part of the system’s code size accounts for the majority of defects
+   4. Pareto distribution of defects in code across releases

In another example, Ostrand and Weyuker [2] have studied the distribution of defects over different files in 13 releases of a large industrial inventory tracking system. For each release, the faults were always heavily concentrated in a relatively small number of files. For example, they find that in a certain release, 10% of files account for 68% of the faults. Interestingly, they find that in a certain release, a small number of files contain more code; a small number of files contain more code.

In yet another example, Murgia et al. [3] studied the defects in two open source Java projects, both developed following agile practices, and find, “There are few Compilation Units hosting most bugs, and most other Compilation Units are with a very few bugs,”