

(例如，通过正式的计算机科学或管理信息系统培训) 可能会发现 SQL 对数据集的操作比老式的 SAS 程序员更自然。 (是的，这是一个坦白。我的前学生之一 Matt Wheeler，使用 PROC SQL 做了相当多的项目工作，这让我意识到我应该学习更多关于这个过程的知识。) 本节提供了该过程的概述，重点介绍使用 PROC SQL 拼接和合并数据集。可能有趣的背景参考包括 SAS 高级认证的文档。

大体思路是 PROC SQL 将数据集视为可使用命令查询进行操作、处理和显示的表。以下是基本语法，摘自 SAS Help：

```sas
PROC SQL;
    CREATE TABLE name;
    SELECT variables FROM list-of-tables/dataset
        GROUP BY  /* optional */
        HAVING    /* optional */
    ;
```

### Display 2.30 Running a simple query on a SAS data set containing the highest nitrofen concentration data

```sas
data conc_310;
    input total @@;
    conc = 310;  * define a variable containing the value of the nitrofen conc.;
    datalines;
6 6 7 0 15 5 6 4 6 5
;
run;

ods rtf bodytitle file='C:\Users\baileraj.IT\Desktop\ch2-fig2.30.rtf';
proc sql;
    select conc,total from conc_310;
quit;
ods rtf close;
```

此查询从 conc_310 SAS 数据集（或表）中选择两个变量（或列）。此查询产生的视图显示在 Display 2.31 中。仅使用 SELECT（无 CREATE）仅打印所选表的感兴趣条目。

### Display 2.31 Result of the simple query with the total number of young produced in the highest nitrofen concentration

| conc | total |
|------|-------|
| 310 | 6 |
| 310 | 6 |
| 310 | 7 |
| 310 | 0 |
| 310 | 15 |
| 310 | 5 |
| 310 | 6 |
| 310 | 4 |
| 310 | 6 |
| 310 | 5 |

PROC SQL 的真正威力体现在你操作表关系时显现。例如，五 个硝基酚浓度数据集使用 UNION 在 Display 2.32 中进行拼接。在 PROC SQL 中，SAS 数据集 all_sql 是以下命令的结果：

```
create table all_sql as
```

所有变量都从每个数据集中选择，这是以下命令的结果：

```
select * from conc_0
```

* 是一个通配符，表示选择所有变量。UNION 将表堆叠成最终表。然后，所有值按 CONC 内的 ID 进行排序，这是以下命令的结果：

```
order by conc, id;
```

### Display 2.32 Concatenating data sets using UNION in PROC SQL

```sas
data conc_0;
    input total @@;
    conc = 0;   * define a variable containing the value of the nitrofen conc.;
    id=_n_;     * define an animal ID corresponding the observation number;
    datalines;
27 32 34 33 36 34 33 30 24 31
;
run;

data conc_80;
    input total @@;
    conc = 80;  * define a variable containing the value of the nitrofen conc.;
    id=_n_;     * define an animal ID corresponding the observation number;
    datalines;
33 33 35 33 36 26 27 31 32 29
;
run;

data conc_160;
    input total @@;
    conc = 160; * define a variable containing the value of the nitrofen conc.;
    id=_n_;     * define an animal ID corresponding the observation number;
    datalines;
29 29 23 27 30 31 30 26 29 29
;
run;

data conc_235;
    input total @@;
    conc = 235; * define a variable containing the value of the nitrofen conc.;
    id=_n_;     * define an animal ID corresponding the observation number;
    datalines;
23 21 7 12 27 16 13 15 21 17
;
run;

data conc_310;
    input total @@;
    conc = 310; * define a variable containing the value of the nitrofen conc.;
    id=_n_;     * define an animal ID corresponding the observation number;
    datalines;
6 6 7 0 15 5 6 4 6 5
;
run;
```

### Display 2.32 (continued)

```sas
proc sql;
    create table all_sql as
    select * from conc_0
    union
    select * from conc_80
    union
    select * from conc_160
    union
    select * from conc_235
    union
    select * from conc_310
    order by conc,id;
quit;  * RUN has no effect on SQL because statements are immediately executed;
       * QUIT ends SQL;
ods rtf bodytitle file='C:\Users\baileraj.IT\Desktop\ch2-fig2.32.rtf';
proc print data=all_sql;
run;
ods rtf close;
```

这五个表（或数据集）的并集产生一个名为 all_sql 的新表，然后将其打印。该表的内容显示在 Display 2.33 中。

### Display 2.33 Result of combining five nitrofen concentration tables into a single table using PROC SQL

| Obs | total | conc | id |
| --- | ----- | ---- | -- |
| 1 | 27 | 0 | 1 |
| 2 | 32 | 0 | 2 |
| ... | ... | ... | ... |
| 48 | 4 | 310 | 8 |
| 49 | 6 | 310 | 9 |
| 50 | 5 | 310 | 10 |

除了拼接表之外，PROC SQL 还使用连接命令合并表。特别是，PROC SQL 中的内连接相当于 DATA 步编程中的合并。Display 2.34 包含合并 SMSA 子集数据集的 PROC SQL 代码（即与 Display 2.26 中的合并类似的操作）。

### Display 2.34 An inner join of the three SMSA subset data sets using PROC SQL

```sas
data SMSA_subset_weather;
    length city $ 27;
    input city & JanTemp JulyTemp    RelHum Rain;
datalines;
Akron, OH  27 71 59 36
Albany-Schenectady-Troy, NY  23 72 57 35
Baltimore, MD  35 77 55 43
Allentown, Bethlehem, PA-NJ  29 74 54 44
Atlanta, GA  45 79 56 47
;
run;

data SMSA_subset_demog;
    length city $ 27;
    input city & Mortality Education PopDensity
        pct_NonWhite pct_WC pop pop_per_house income;
datalines;
Akron, OH  921.87 11.4 3243 8.8 42.6 660328 3.34 29560
Albany-Schenectady-Troy, NY  997.87 11.0 4281 3.5 50.7 358880 3.14 31458
Baltimore, MD  1071.29 9.6 6441 24.4 43.7 2199531 3.44 32368
Allentown, Bethlehem, PA-NJ  962.35 9.8 4260 0.8 39.4 635481 3.21 31856
Atlanta, GA  982.29 11.1 3125 27.1 50.2 2138321 3.41 32452
;
run;

data SMSA_subset_pollution;
    length city $ 27;
    input city & HCpot NOxPot SO2Pot NOx;
datalines;
Akron, OH  21 15 59 15
Albany-Schenectady-Troy, NY  8 10 39 10
Baltimore, MD  43 38 206 38
Allentown, Bethlehem, PA-NJ  6 6 33 6
Atlanta, GA  18 8 24 8
;
run;

proc sql;
    create table SMSA_subset_sql as
    select * from
        SMSA_subset_weather w, SMSA_subset_demog d, SMSA_subset_pollution p
    where w.city=d.city and d.city=p.city;

ods rtf bodytitle file='C:\Users\baileraj.IT\Desktop\ch2-fig2.34.rtf';
proc print data=SMSA_subset_sql;
    var city JulyTemp education SO2Pot;
run;
ods rtf close;
```

PROC SQL 命令包括为每个数据集定义别名。例如：

```
select * from
    SMSA_subset_weather w, SMSA_subset_demog d,
        SMSA_subset_pollution p
```

此代码允许 w.city 引用 SMSA_subset_weather 数据集中的 CITY 变量。此外，还声明了一个连接条件，当三个数据集中的 CITY 相同 时，合并数据集的行相匹配。例如：

```
where w.city=d.city and d.city=p.city;
```

PROC SQL 内连接产生的数据集显示在 Display 2.35 中。

### Display 2.35 Data set produced by the inner join of the three SMSA subset data sets

| Obs | City | JulyTemp | Education | SO2Pot |
|---|---|---|---|---|
| 1 | Akron, OH | 71 | 11.4 | 59 |
| 2 | Albany-Schenectady-Troy, NY | 72 | 11.0 | 39 |
| 3 | Baltimore, MD | 77 | 9.6 | 206 |
| 4 | Allentown, Bethlehem, PA-NJ | 74 | 9.8 | 33 |
| 5 | Atlanta, GA | 79 | 11.1 | 24 |

使用 DATA 步编程与使用 PROC SQL 合并数据集之间的一个区别是，在使用 DATA 步编程合并之前，输入数据集需要按某个键变量排序。PROC SQL 中不需要排序。

一个有趣的问题是，“如果正在组合的数据集中没有完全匹配会发生什么？” 在接下来的系列显示中，这个问题得到了解答。在 Display 2.36 中，显示了具有五个城市中的三个城市的两个 SMSA 子集数据集。在 Display 2.37 中，第一个表显示了包含三个共同城市的内连接的结果。第二个和第三个表显示了外连接的结果和连接中第一个数据集的元素（左连接）。第四个表显示了外连接的结果和连接中第二个数据集的元素（右连接）。第五个表显示了外连接的结果和来自两个数据集的元素并集（全连接）。SAS 文档用阴影 Venn 图说明这些连接，这是一个概念化这些操作的良好模型。在本书中，经验显示在 Display 2.36 中显示。输出显示在 Display 2.37 中。

3 外连接是内连接的内容（两个表的交集）加上来自连接中表的额外观测。

