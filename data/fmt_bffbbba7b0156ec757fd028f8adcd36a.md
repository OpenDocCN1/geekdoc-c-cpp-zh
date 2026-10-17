
There are times when you are interested in the complete Cartesian product of the observations in two data sets (i.e., all rows from one data set paired with all rows from another data set). Consider a toy example in which you want to enumerate the sample

#### Display 2.40 Data set constructed from joining all rows from two tables

| `Obs` | `toss` | `face` |
|---|---|---|
| 1 | Heads | 1 |
| 2 | Heads | 2 |
| 3 | Heads | 3 |
| 4 | Heads | 4 |
| 5 | Heads | 5 |
| 6 | Heads | 6 |
| 7 | Tails | 1 |
| 8 | Tails | 2 |
| 9 | Tails | 3 |
| 10 | Tails | 4 |
| 11 | Tails | 5 |
| 12 | Tails | 6 |

### 2.7 Summary

The chapter started with an emphasis on reading data into SAS from various sources. It then moved into strategies for modifying data sets to add observations or variables. The SQL procedure was introduced for manipulating tables using a structured query language. Consistent with the title of this book (the “Statistical Programming” part), the goal of these manipulations is to produce a data set for analysis. Believe it or not, there are a few more topics associated with processing data in SAS that you might need to master. (This observation is similar to the captain of the Titanic observing, “Gee, I bet there is even more ice below the surface associated with that berg.”)

Remember how the special variable `FIRST.CONC` was used in `PUT` statements? There are many other special internal variables, such as those associated with sorting—`FIRST` and `LAST`—and variables associated with observations being in a data set—`IN`. There are many other procedures for updating (`PROC UPDATE`), managing data sets efficiently (`PROC COPY`, `PROC DATASETS`), or reshaping data sets (`PROC TRANSPOSE`). You are encouraged to explore all of these. The transporting of data sets between systems and applications is facilitated by `PROC IMPORT` and `PROC EXPORT`, while moving SAS catalogs between systems is facilitated by `PROC CPORT` and `PROC CIMPORT`. You are encouraged to see the Help pages and other SAS resources and skim the overview and descriptions of these topics. A collection of `PUT`, `SET`, `MERGE`, and `SQL` self-study laboratory exercises are included after the exercises. Working through all of these exercises should help you develop intuition about data set manipulation in SAS.

### 2.8 References

Kuehl, Robert O. 1994. Statistical Principles of Research Design and Analysis. 1st Ed. Belmont, CA: Duxbury Press, a division of Cengage Learning, Inc.

Lange, Nicholas, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. 1994. Case Studies in Biometry. New Jersey: John Wiley & Sons, Inc.

### 2.9 Exercises

**1.** Generate a customized printout of the meat⁴ data from Chapter 5. (Use `PUT` statements in a SAS data set.) The report should look like the following:

```
Packaging Condition = Plastic

Data        Mean    Std. Dev.

---------------  ------  --------

7.66  6.98  7.80    x.xx    x.xx

Packaging Condition = Vacuum

Data        Mean    Std. Dev.

---------------  ------  --------

5.26  5.44  5.80    x.xx    x.xx

etc.
```

⁴ Meat data set usage based on the “Bacteria growth in meat” data set from Kuehl, R. O. Statistical Principles of Research Design and Analysis. 1st Ed. © 1994. Brooks/Cole, a part of Cengage Learning, Inc. ISBN: 9780534188047(0534188044).

```
raw data . . .
logcount condition
7.66 Plastic
6.98 Plastic
7.80 Plastic
5.26 Vacuum
5.44 Vacuum
5.80 Vacuum
7.41 Mixed
7.33 Mixed
7.04 Mixed
3.51 Co2
2.91 Co2
3.66 Co2
```

**Hints:** You can use `@` as part of a `PUT` statement to put the values of multiple observations on the same line in the text file. You can use functions such as `MEAN` and `VAR` in `DATA` step programming to find summary statistics. Alternatively, you can use `PROC MEANS` with a `CLASS` statement to set a condition and create an output data set with the summary statistics. This output summary statistics data set could be merged with the original raw data set.

**2.** Fifty animals were exposed to one of five concentration levels of nitrogen (10 animals per group, but some observations might be missing in the data). The data was recorded separately for three broods produced by each of the 50 animals. Thus, each animal can have data in each of the three brood data sets. A particular animal is uniquely identified by the `ID` variable. Produce a combined data set containing observations (animals and `ID`s) that has data on all three broods. In addition, construct an additional variable for the total number of young produced in all three broods. Compare the different joins for this data. In particular, construct the following:

- a. `Brood1 [inner join] Brood2 [inner join] Brood3`
- b. `(Brood1 [left join] Brood2) [left join] Brood3`
- c. `(Brood1 [right join] Brood2) [right join] Brood3`
- d. `Brood1 [full join] Brood2 [full join] Brood3`

Print the results for the different combined data sets. Multiple observations are given on each line.

#### Brood=1 数据

变量：`ID` `conc` `number of young`

| `ID` | `conc` | `number of young` |
|---|---|---|
| 3 | 0 | 6 |
| 4 | 0 | 6 |
| 5 | 0 | 6 |
| 6 | 0 | 5 |
| 7 | 0 | 6 |
| 8 | 0 | 5 |
| 9 | 0 | 3 |
| 10 | 0 | 6 |
| 12 | 80 | 5 |
| 13 | 80 | 6 |
| 14 | 80 | 5 |
| 15 | 80 | 8 |
| 16 | 80 | 3 |
| 17 | 80 | 5 |
| 18 | 80 | 7 |
| 19 | 80 | 5 |
| 20 | 80 | 3 |
| 21 | 160 | 6 |
| 22 | 160 | 6 |
| 23 | 160 | 2 |
| 24 | 160 | 6 |
| 25 | 160 | 6 |
| 26 | 160 | 6 |
| 27 | 160 | 6 |
| 28 | 160 | 5 |
| 30 | 160 | 6 |
| 31 | 235 | 4 |
| 32 | 235 | 6 |
| 34 | 235 | 6 |
| 35 | 235 | 6 |
| 36 | 235 | 6 |
| 37 | 235 | 7 |
| 38 | 235 | 4 |
| 39 | 235 | 6 |
| 40 | 235 | 7 |
| 41 | 310 | 6 |
| 42 | 310 | 6 |
| 43 | 310 | 7 |
| 44 | 310 | 0 |
| 45 | 310 | 5 |
| 47 | 310 | 6 |
| 48 | 310 | 4 |
| 49 | 310 | 6 |
| 50 | 310 | 5 |

#### Brood=2 数据

变量：`ID` `conc` `number of young`

| `ID` | `conc` | `number of young` |
|---|---|---|
| 1 | 0 | 14 |
| 2 | 0 | 12 |
| 3 | 0 | 11 |
| 4 | 0 | 12 |
| 6 | 0 | 14 |
| 7 | 0 | 12 |
| 8 | 0 | 13 |
| 9 | 0 | 10 |
| 10 | 0 | 11 |
| 11 | 80 | 11 |
| 13 | 80 | 11 |
| 14 | 80 | 12 |
| 15 | 80 | 13 |
| 16 | 80 | 9 |
| 17 | 80 | 9 |
| 18 | 80 | 12 |
| 19 | 80 | 13 |
| 20 | 80 | 12 |
| 21 | 160 | 12 |
| 22 | 160 | 12 |
| 23 | 160 | 8 |
| 24 | 160 | 10 |
| 25 | 160 | 11 |
| 26 | 160 | 13 |
| 27 | 160 | 12 |
| 29 | 160 | 13 |
| 30 | 160 | 12 |
| 31 | 235 | 13 |
| 32 | 235 | 10 |
| 33 | 235 | 5 |
| 34 | 235 | 0 |
| 35 | 235 | 13 |
| 36 | 235 | 0 |
| 37 | 235 | 0 |
| 38 | 235 | 2 |
| 39 | 235 | 8 |
| 40 | 235 | 0 |
| 41 | 310 | 0 |
| 42 | 310 | 0 |
| 43 | 310 | 0 |
| 45 | 310 | 10 |
| 46 | 310 | 0 |
| 47 | 310 | 0 |
| 48 | 310 | 0 |
| 49 | 310 | 0 |
| 50 | 310 | 0 |

#### Brood=3 数据

变量：`ID` `conc` `number of young`

| `ID` | `conc` | `number of young` |
|---|---|---|
| 1 | 0 | 10 |
| 2 | 0 | 15 |
| 3 | 0 | 17 |
| 4 | 0 | 15 |
| 5 | 0 | 15 |
| 6 | 0 | 15 |
| 7 | 0 | 15 |
| 8 | 0 | 12 |
| 10 | 0 | 14 |
| 11 | 80 | 16 |
| 12 | 80 | 16 |
| 13 | 80 | 18 |
| 14 | 80 | 16 |
| 15 | 80 | 15 |
| 16 | 80 | 14 |
| 17 | 80 | 13 |
| 18 | 80 | 12 |
| 19 | 80 | 14 |
| 20 | 80 | 14 |
| 21 | 160 | 11 |
| 22 | 160 | 11 |
| 23 | 160 | 13 |
| 24 | 160 | 11 |
| 25 | 160 | 13 |
| 26 | 160 | 12 |
| 27 | 160 | 12 |
| 28 | 160 | 11 |
| 29 | 160 | 10 |
| 30 | 160 | 11 |
| 31 | 235 | 6 |
| 32 | 235 | 5 |
| 33 | 235 | 0 |
| 34 | 235 | 6 |
| 35 | 235 | 8 |
| 36 | 235 | 10 |
| 38 | 235 | 9 |
| 39 | 235 | 7 |
| 40 | 235 | 10 |
| 41 | 310 | 0 |
| 42 | 310 | 0 |
| 43 | 310 | 0 |
| 44 | 310 | 0 |
| 45 | 310 | 0 |
| 46 | 310 | 0 |
| 48 | 310 | 0 |
| 49 | 310 | 0 |
| 50 | 310 | 0 |

### 2.10 自学实验室探索

以下代码示例提供了一系列更高级的 `PUT`、`SET`、`MERGE` 和 `SQL` 操作。建议按顺序完成每个 `DATA` 步和 `PROC SQL` 查询，以深入了解 `DATA` 步操作和数据集构建。
