

要在安装中查看自动宏变量，请在 %PUT 语句中使用 _AUTOMATIC_ 选项。

## Code

```
%PUT _AUTOMATIC_;
```

## SAS Log Results

```
%PUT _AUTOMATIC_;
AUTOMATIC AFDSID 0
AUTOMATIC AFDSNAME
AUTOMATIC AFLIB
AUTOMATIC AFSTR1
AUTOMATIC AFSTR2
AUTOMATIC FSPBDV
AUTOMATIC SYSBUFFR
AUTOMATIC SYSCC 0
AUTOMATIC SYSCHARWIDTH 1
AUTOMATIC SYSCMD
AUTOMATIC SYSDATE 10JUN04
AUTOMATIC SYSDATE9 10JUN2004
AUTOMATIC SYSDAY Thursday
AUTOMATIC SYSDEVIC
AUTOMATIC SYSDMG 0
AUTOMATIC SYSDSN WORK    INVENTORY
AUTOMATIC SYSENDIAN LITTLE
AUTOMATIC SYSENV FORE
AUTOMATIC SYSERR 0
AUTOMATIC SYSFILRC 0
AUTOMATIC SYSINDEX 3
AUTOMATIC SYSINFO 0
AUTOMATIC SYSJOBID 3580
AUTOMATIC SYSLAST WORK.INVENTORY
AUTOMATIC SYSLOCKRC 0
AUTOMATIC SYSLIBRC 0
AUTOMATIC SYSMACRONAME
AUTOMATIC SYSMAXLONG 2147483647
AUTOMATIC SYSMENV S
AUTOMATIC SYSMSG
AUTOMATIC SYSNCPU 1
AUTOMATIC SYSPARM
AUTOMATIC SYSPBUFF
AUTOMATIC SYSPROCESSID 41D4E614295031274020000000000000
AUTOMATIC SYSPROCESSNAME DMS Process
AUTOMATIC SYSPROCNAME
AUTOMATIC SYSRC 0
AUTOMATIC SYSSCP WIN
AUTOMATIC SYSSCPL XP_HOME
AUTOMATIC SYSSITE 0045254001
AUTOMATIC SYSSIZEOFLONG 4
AUTOMATIC SYSSIZEOFUNICODE 2
AUTOMATIC SYSSTARTID
AUTOMATIC SYSSTARTNAME
AUTOMATIC SYSTIME 12:50
AUTOMATIC SYSUSERID Valued Sony Customer
AUTOMATIC SYSVER 9.1
AUTOMATIC SYSVLONG 9.01.01M0P111803
AUTOMATIC SYSVLONG4 9.01.01M0P11182003
```

## Building Macro Tools and Applications

宏设施结合 SQL 过程的能力，使得能够创建多功能宏工具和通用应用程序。在开发用户编写的宏时，一个主要的设计目标应该是它们有用且易于使用。最好避免使用不符合您需求的宏，或者名称复杂难以记住的宏。

作为工具，宏应设计为满足尽可能多用户的需求。它们不应存在歧义，应包含独特的宏变量名，避免宏变量与数据集变量之间的命名冲突，并且不要试图做太多事情。这种实用主义的宏设计方法有助于获得用户的广泛认可和接受。

## Creating Simple Macro Tools

宏工具可以构建来执行各种有用的任务。最有效的宏是那些简单且执行常见任务的宏。在着手构建一个或多个宏工具之前，先探索当前正在执行的流程，然后通过与受影响的人员沟通来确定用户的常见需求并找出空白。一旦完成此项工作，您将处于更有利的位置来构建简单且有用的宏工具，以便用户接受。

假设在非正式的需求分析阶段，您识别出一些用户在工作中使用各种方法和方法来创建数据集和变量交叉引用列表。为了防止不必要的重复劳动，您决定构建一个简单的宏工具，可供所有用户使用，以检索一个或多个 SAS 数据集中的列信息。

## Cross-Referencing Columns

列交叉引用列表在您需要快速识别列定义所在的 SAS 库数据集时很有用。使用 COLUMNS 字典表（有关更多信息，请参阅第 2 章“在 PROC SQL 中使用数据”），可以创建一个宏来捕获列级信息，包括列名、类型、长度、位置、标签、格式、 informat、索引，以及包含列在指定 SAS 库中位置的交叉引用列表。在下一个示例中，COLUMNS 宏由一个 PROC SQL 查询组成，可访问 SAS 库中的任何单个列。如果宏被用户请求

```
%COLUMNS(WORK, CUSTNUM);
```

调用，则宏将为用户库 WORK 中的列 CUSTNUM 在所有 DATA 类型中生成交叉引用列表。

## SQL Code

```
%MACRO COLUMNS(LIB, COLNAME);
    PROC SQL;
        SELECT LIBNAME, MEMNAME, NAME, TYPE, LENGTH
        FROM DICTIONARY.COLUMNS
            WHERE LIBNAME="&LIB" AND
                UPCASE(NAME)="&COLNAME" AND
                MEMTYPE="DATA";
    QUIT;
%MEND COLUMNS;
%COLUMNS(WORK,CUSTNUM);
```

值得注意的是，在包含区分大小写名称的数据库中可能会找到多个匹配项。这将允许同时显示“employee”和“EMPLOYEE”作为匹配项。这在实践中不太可能经常发生，但确实是一种可能性。

## Results

| Library Name | Member Name | Column Name | Column Type | Column Length |
| WORK | CUSTOMERS | custnum | num | 3 |
| WORK | CUSTOMERS2 | custnum | num | 3 |
| WORK | CUSTOMERS_BACKUP | custnum | num | 8 |
| WORK | INVOICE | custnum | num | 3 |
| WORK | PURCHASES | custnum | num | 4 |
| WORK | PURCHASES2 | Custnum | num | 8 |

## Determining the Number of Rows in a Table

有时在不先读取所有行之前了解表中的观测值（或行）数量很有用。虽然真正的 SAS 表的行数可用，但使用 libname 引擎的 DBMS 表的行数不可用。在下一个示例中，用户定义的宏 NOBS 访问 TABLES 字典表（有关更多信息，请参阅第 2 章）。宏 NOBS 设计为接受并处理两个用户提供的值：库引用和表名。一旦提供这些值，结果将在输出窗口中显示。

## SQL Code

```
%MACRO NOBS(LIB, TABLE);
    PROC SQL;
        SELECT LIBNAME, MEMNAME, NOBS
            FROM DICTIONARY.TABLES
                WHERE UPCASE(LIBNAME)="&LIB" AND
                      UPCASE(MEMNAME)="&TABLE" AND
                      UPCASE(MEMTYPE)="DATA";
    QUIT;
%MEND NOBS;

%NOBS(WORK,PRODUCTS);
```

## Results

| Library Name | Member Name | Number of Physical Observations |
|--------------|-------------|---------------------------------|
| WORK         | PRODUCTS    | 10                              |

## Identifying Duplicate Rows in a Table

有时能够识别表中的重复行很有用。在下一个示例中，使用 COUNT 汇总函数和 HAVING 子句的 SELECT 语句用于用户定义的宏 DUPS。宏 DUPS 设计为接受并处理三个用户提供的值：库引用、表名和 GROUP BY 列表中的列。一旦通过提交宏 DUPS 提供这些值，宏将被执行，结果将在输出窗口中显示。

## SQL Code

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
%MEND DUPS;

%DUPS(WORK,PRODUCTS,PRODTYPE);
```

## Results

| Product Type | Duplicate_Rows |
|---|---:|
| Phone | 3 |
| Software | 4 |
| Workstation | 2 |

## Summary

- 1. CASE 表达式是 PROC SQL 中的一种结构，用于评估是否满足特定条件（请参阅“CASE 表达式”部分）。
- 2. CASE 表达式可用于有条件地处理表的行（请参阅“CASE 表达式”部分）。
- 3. 从对表中每一行的求值中返回单个值（请参阅“CASE 表达式”部分）。
- 4. 逻辑条件可以使用 AND 和 OR 逻辑运算符组合（请参阅“逻辑和空值”部分）。
- 5. 当未指定 ELSE 表达式且每个 WHEN 条件均为“false”时，返回缺失或 NULL 值（请参阅“逻辑和空值”部分）。
- 6. 缺失值与 0（零）值或空白字符不同，因为它代表唯一值或缺乏值（请参阅“逻辑和空值”部分）。
- 7. PROC SQL 可与 SAS 宏设施一起使用来执行常见和重复性任务（请参阅“将 PROC SQL 与宏语言接口”部分）。
- 8. 可以为所有用户创建简单但有效的用户定义宏，结合 SQL 过程（请参阅“构建宏工具和应用程序”部分）。
- 9. 可以使用 INTO 子句定义单值宏变量（请参阅“使用聚合函数创建宏变量”部分）。
- 10. 可以使用 INTO 子句和 SEPARATED BY 关键字定义值列表宏变量（请参阅“使用 WHERE 子句控制宏变量的选择和填充”部分）。

