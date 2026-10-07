

# 第 2 章：DS2 语言简介 23

```
/* Section 3 */
method term();
put '*********';
put 'Ending';
put '*********';
enddata;
run;
```

## 2.4 关键概念回顾

- 所有的 DS2 程序都由块组成：data（数据）、package（包）和 thread（线程）。
- DS2 程序块有三种类型：data、package 和 thread。
- 程序块以适当的 `DATA`、`PACKAGE` 或 `THREAD` 语句开始，并以相应的 `ENDDATA`、`ENDPACKAGE` 或 `ENDTHREAD` 语句结束。程序的其余部分由全局声明语句和方法定义组成。所有可执行语句必须是方法定义的一部分。
- 有三个系统方法：`IN`、`RUN` 和 `TERM`。每个 data 和 thread 程序必须包含其中一个方法的显式编码。系统方法自动执行且不接受参数。
- 你可以编写用户定义方法，但注意以下几点：
    - 用户定义方法不会自动执行；它们只在调用时执行。
    - 用户定义方法可以接受参数，值可以通过传值或引用传递（`IN_OUT` 参数）。
    - 没有 `IN_OUT` 参数的方法可以返回值，类似于 SAS 函数。
    - 方法的 `IN_OUT` 参数值可以在本地修改，类似于 SAS CALL 过程。
    - 用户定义方法可以存储在 DS2 package 中供重用。
- 在 DS2 程序中创建的变量应使用 `DECLARE (DCL)` 语句进行声明。声明的位置决定了变量的作用域。
- 通过 `SET` 语句引入 DS2 程序的变量、在全局程序空间（方法定义开始之前）声明的变量或在程序代码中出现未声明的变量具有全局作用域。全局变量可以在 DS2 程序内部任何地方引用，它们是 PDV 的一部分，并且默认包含在程序集中。
- 在 `METHOD` 块内部声明的变量和方法参数变量的作用域是局部的，且只能在该方法内部引用。局部变量永远不会包含在 PDV 中，也无法成为程序结果的一部分。

# 第 3 章：DS2 数据程序详情

- 3.1 引言 ................................................................................................................ 25
- 3.2 DS2 数据程序与 Base SAS DATA Step 的对比........................................... 25
- 3.2.1 通用注意事项 ..................................................................................... 25
- 3.2.2 “六个微妙差异” ........................................................ 26
- 3.2.3 DS2 “缺失”功能 ................................................................................ 33
- 3.3 DS2 中的数据类型 ............................................................................................ 38
- 3.3.1 DS2 与 ANSI 数据类型 .......................................................................... 38
- 3.3.2 自动数据类型转换 ....................................................... 40
- 3.3.3 非数据类型 ................................................................................ 42
- 3.3.4 处理 SAS 缺失和 ANSI 空值 ................................... 45
- 3.4 关键概念回顾 ................................................................................ 49

# 3.1 引言

在本章中，我们将关注 DS2 数据程序的基础，首先通过将传统的 DATA Step 与 DS2 数据程序进行进一步对比，并深入研究 DS2 中的一些新特性。在此过程中，我们将更复杂的 Base DATA Step 转换为 DS2 数据程序，并引入几个 DS2 特有的概念和技术。具体而言，我们将涵盖以下几点：

- 更多 DS2 数据程序语法和结构
- 使用 FedSQL 查询直接为 DS2 数据程序的 `SET` 语句提供输入
- DS2 中可以处理的各种 ANSI 数据类型
- DS2 自动数据类型转换规则
- 独特的 DS2 程序语句
- 独特的 DS2 表达式
- 选定的 DS2 函数

## 3.2 DS2 数据程序与 Base SAS DATA Steps 的对比

### 3.2.1 通用注意事项

DS2 数据程序语法与 Base SAS DATA Step 语法的相似性对于丰富的 SAS 程序员来说是一个优势。这种相似性明显体现在 Base SAS DATA Step 和 DS2 数据程序共享的语句语法上。例如，这些语句在两种语言中的工作方式基本相同：

- `SET`
- BY 组处理，包括 `First.variable` 和 `Last.variable`
- DO 组和 DO 循环
    - `DO i= start TO STOP BY interval`
    - `DO WHILE ()`
    - `DO UNTIL ()`
    - 循环控制语句 `CONTINUE`、`LEAVE` 和 `END`
- 程序流控制语句
    - `RETURN`
    - `OUTPUT`
    - `GOTO`
    - `STOP`
- 声明语句
    - `KEEP` 和 `DROP`
    - `RETAIN`

记住，在任何 DS2 程序中，全局声明语句必须出现在全局程序空间中——即在 `DATA`、`THREAD` 或 `PACKAGE` 语句之后，第一个方法定义之前。

## 3.2.2 “六个微妙差异”

尽管传统的 DATA Step 和 DS2 数据程序中的许多工作工作完全相同，但存在一些非常微妙的差异，在 DS2 中编程时需要记住。让我们回顾一下主要的区别，我称之为“六个微妙差异”。

### 3.2.2.1 所有可执行语句必须是方法的一部分

在全局程序空间中的可执行语句会导致语法错误：

```
proc ds2;
data _null_;
set crs.one_day;
put _all_;
enddata;
run;
```

SAS 日志：

```
ERROR: Compilation error.
ERROR: Parse encountered end of input.
```

将可执行语句封装在方法中可以解决这个问题：

```
proc ds2;
data _null_;
  method()
    set crs.one_day;
    put _all_;
  end;
enddata;
run;
```

SAS 日志：

```
NOTE: Execution succeeded.
```

## 2.2 DS2 程序默认不覆盖写

如果你提交此程序，它会正常运行。如果你再次提交完全相同的程序，将导致语法错误：

```
proc ds2;
data test1 test2;
  method()
    set crs.one_day;
  end;
enddata;
run;

proc ds2;
data test1 test2;
  method()
    set crs.one_day;
  end;
enddata;
run;
```

SAS 日志：

```
683 proc ds2;
684 data test1 test2;
685 method();
686 set crs.one_day;
687 end;
688 enddata;
689 run;
690 NOTE: Execution succeeded. 12 rows affected.
691 quit;
692 NOTE: PROCEDURE DS2 used (Total process time):

| Metric | Value |
| :--- | :--- |
| real time | 0.05 seconds |
| cpu time | 0.04 seconds |

```
691
692 proc ds2;
693 data test1 run;
694 method();
695
696 set crs.one_day;
697 end;
698 enddata;
699 run;
ERROR: Compilation error.
ERROR: Base table or view already exists TEST1
ERROR: Unable to CREATE TABLE statement for table
work.test1.
```

你可以使用 `DATA` 语句中的 `OVERWRITE=YES` 选项来控制这种行为，或者 `OVER=YES` 选项仅允许覆盖指定选项的数据集。`DATA` 语句允许覆盖其中列出的所有输出表。例如，这解决了 `test1` 数据集的问题，但由于不允许覆盖 `test2`，我们仍然会编译错误：

```
proc ds2;
data test1(overwrite=yes) test2;
method();
set crs.one_day;
end;
enddata;
run;
quit;
```

SAS 日志：

```
ERROR: Compilation error.
ERROR: Base table or view already exists TEST2
ERROR: Unable to execute CREATE TABLE statement for table
work.test2.
```

使用 `DATA` 语句的 `OVERWRITE=YES` 选项允许覆盖两个表：

```
proc ds2;
data test1 test2 /overwrite=yes;
method();
set crs.one_day;
end;
enddata;
run;
quit;
```

SAS 日志：

NOTE: Execution succeeded. 12 rows affected.

