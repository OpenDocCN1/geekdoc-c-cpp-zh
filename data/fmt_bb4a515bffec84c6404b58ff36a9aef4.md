
# SAS® 编程 2：数据处理技术：课程笔记

![](img/d3bde6e6ab06b1fc622215d982111742_0_0.png)

![](img/d3bde6e6ab06b1fc622215d982111742_0_1.png)

课程笔记

## 多数据数据集

`DATA <sas-data-set-1 ... sas-data-set-n>;`

## SET 语句选项

`SET <sas-data-set-end=variable>;`

### 显式输出

`OUTPUT <sas-data-set-1 ... sas-data-set-n>;`

## 拼接函数

`CAT(<string-1>, ..., <string-n>);`

`CATT(<string-1>, ..., <string-n>);`

`CATX(<separator, <string-1>, ..., <string-n>);`

## 条件处理

`SELECT <select-expression>;`

`WHEN-1 (value-1 < ..., <value-n> statement;);`

`<...WHEN-n (value-1 < ..., <value-n> statement;);`

`<OTHERWISE statement>;`

`END;`

## 拼接运算符

`string1 !! string2`

## 字符函数

`CHAR(<string,position>)`

`COMPBL(<source, <chars>);`

`FIND(<string,substring, <modifiers,startpos>);`

`LEFT(<string>)`

`LENGTH(<argument>)`

`LOWCASE(<string>)`

`PROPCASE(<argument, <delimiter>s);`

`RIGHT(<string, <charlist>);`

`SUBSTR(<string,<length>);`

`STRIP(<string>)`

`TRANWRD(<source,target,replacement>);`

`TRIM(<string>)`

`UPCASE(<string>)`

## SAS 数据集选项

`SAS-data-set(KEEP=variable-1 <variable-2 ... variable-n>)`

`SAS-data-set(DROP=variable-1 <variable-2 ... variable-n>)`

`SAS-data-set(OBS=n)`

`SAS-data-set(FIRSTOBS=n)`

`SAS-data-set(RENAME=<old-variable=new-variable ...>)`

### 截断函数

`RETAIN variable-name <initial-value>; ...;`

### 创建累加变量

`variable + expression;`

`ROUND(<argument, <round-off-unit>);`

`CEIL(<argument>)`

`FLOOR(<argument>)`

`INT(<argument>)`

## DATA 步中的 BY 处理

```
DATA output=sas-data-set;
SET <sas-data-set>;
BY <variable- ..., <additional SAS statements>;
RUN;
```

## 转换函数

`INPUT(<source,informat>)`

`PUT(<source,format>);`

## 描述性统计函数

`MAX(<argument-1, <argument-2>, ..., <argument-n>)`

`MEAN(<argument-1, <argument-2>, ..., <argument-n>)`

`MIN(<argument-1, <argument-2>, ..., <argument-n>)`

`N(<argument-1, <argument-2>, ..., <argument-n>)`

`NMISS(<argument-1, <argument-2>, ..., <argument-n>)`

## 指定 First. 和 Last. 变量

`FIRST.by-variable`

`Last.by-variable`

## INPUT 的格式化样式

`INPUT pointer-control variable format ...;`

`SUM(<argument-1, <argument-2>, ..., <argument-n>)`

## 数组函数

## 单个结尾 @ INPUT 规范

`INPUT specifications ... @;`

![](img/d3bde6e6ab06b1fc622215d982111742_1_0.png)

SAS 以及所有其他 SAS Inc. 产品或服务名称均为 SAS Institute Inc. 在美国及其他国家的注册商标或商标。* 美国注册。其他品牌和产品名称为各自公司的商标。版权所有 © 2014 SAS Inc. Cary, NC, USA。保留所有权利。

课程笔记

《SAS® 编程 2：数据处理技术》课程笔记由 Davetta Dunlap、Susan Farmer、Karen Feldman 和 Johnny Johnson 开发。Mark Jordan、Marjorie Lampton、Rob McAfee、Linda Mitterling 和 Kathy Passarella 提供了额外贡献。课程开发与支持部门提供了编辑和制作支持。

SAS 以及所有其他 SAS Institute Inc. 产品或服务名称均为 SAS Institute Inc. 在美国及其他国家的注册商标或商标。® 表示 SAS 注册。其他品牌和产品名称为各自公司的商标。

# 第 4 章 读取原始数据文件................................................4-1

# 第 5 章 数据转换.....................................................5-1

# 第 6 章 调试技术 ................................................................. 6-1

演示：确定逻辑错误 ................................................. 6-8

# 第 7 章 迭代处理数据.................................................. 7-1

7.3 SAS 数组处理...................................................................... 7-30

7.5 答案 ................................................................................ 7-61

# 第 8 章 重构数据集............................................................... 8-1

# 第 9 章 合并 SAS® 数据集 ................................................................ 9-1

# 第 10 章 创建和维护永久格式 ................................ 10-1

# 第 11 章 其他 SAS® 语言 ................................................ 11-1

## 课程描述

本课程适用于需要学习使用 SAS DATA 和过程步进行数据处理技术，以访问、转换和总结 SAS 数据集的读者。本课程基于 SAS® Programming 1: Essentials 课程中介绍的概念，不建议 SAS 软件初学者参加。

## 了解更多...

![](img/d3bde6e6ab06b1fc622215d982111742_9_0.png)

有关课程大纲中其他课程的信息，请拨打 1-800-333-7660 联系 SAS 教育部门，或发送电子邮件至 training@sas.com。您也可以在网站 http://support.sas.com/training/ 以及培训课程目录中找到这些信息。

![](img/d3bde6e6ab06b1fc622215d982111742_9_1.png)

有关与本课程笔记主题相关的其他 SAS 书籍列表，美国客户可以拨打 1-800-727-3228 联系 SAS出版部门或发送电子邮件至 sasbook@sas.com。美国以外的客户请联系当地 SAS 办公室。

此外，请访问网站 http://support.sas.com/publishing/ 查看书籍列表。

## 先决条件

在参加本课程之前，您应该具有至少六月的 SAS 程序编写经验，或者完成了 SAS Programming 1: Essentials 课程并使用 SAS 一个月。具体而言，您应该能够：

- 提交 SAS 程序

- 诊断并修正语法错误

- 检查 SAS 数据集的描述和数据部分

- 访问 SAS库

- 读取并创建 SAS数据集

- 读取 Excel 表格

- 读取分隔符原始数据

- 在读取原始数据时检查数据错误

- 使用 SAS 过程验证数据

- 清理无效数据

- 创建变量

- 合并 SAS数据集

- 使用全局语句

- 使用标签和格式（包括自定义格式）

- 筛选观测

- 使用 FREQ 和 MEANS 过程生成摘要报告。

### 第 1 章 引言

#### 1.1 SAS 基础概述

##### 目标

- 描述 SAS软件

- 描述 Base SAS 和 SAS Foundation 工具的功能

##### 什么是 SAS?

SAS 是一套业务解决方案和技术，帮助组织解决业务问题。

![](img/d3bde6e6ab06b1fc622215d982111742_14_0.png)

##### 你可以用 SAS 做什么？

SAS 允许你执行以下操作：

- 跨多个源访问数据

- 管理数据

- 执行复杂的分析

- 在整个组织范围内传递信息

![](img/d3bde6e6ab06b1fc622215d982111742_15_0.png)

##### 什么是 Base SAS？

Base SAS 是所有 SAS 软件的核心。

Base SAS 是 SAS Foundation 产品集中的产品，它提供了：

- 一种高度灵活、高度扩展的第四代编程语言

- 丰富的封装编程过程库

- 一个用于管理 SAS 任务的图形化用户界面

##### 关于本课程

本课程侧重于使用 DATA Step（数据步）处理数据，包括：

- 创建多个 SAS 数据集

- 累加总和并汇总数据

- 读取固定列原始数据文件

- 使用函数处理变量值

- 执行 DO 循环和 SAS 数组处理

- 旋转数据集

- 合并数据集

![](img/d3bde6e6ab06b1fc622215d982111742_16_0.png)

# 1.01 投票

你用过 DATA Step 吗？

- a. 是的，仅负责维护程序

- b. 没有，完全没用

#### 1.2 课程安排

##### 目标

- 描述课程中使用的数据。

- 设计工作坊可用的编辑器和处理模式。

- 指定用于文件的命名规范。

- 定义三个级别的练习。

- 讨论如何访问帮助帮助（Help）。

本课程专注于一家拥有传统实体店、在线商店和大型目录的零售商。

![](img/d3bde6e6ab06b1fc622215d982111742_17_0.png)

##### Orion 数据

大量数据以各种格式存储在事务系统中。

![](img/d3bde6e6ab06b1fc622215d982111742_18_0.png)

##### 编写和运行 SAS 程序

在本课程中，你将使用编辑器编写并处理访问 Orion 数据以及创建报告的 SAS 程序。

![](img/d3bde6e6ab06b1fc622215d982111742_18_1.png)

##### SAS Enterprise Guide 程序编辑器 SAS 窗口环境

# 第1章 引言

| SAS Enterprise Guide | SAS 窗口环境 |
| :--- | :--- |
| 编辑器 | 增强编辑器或程序编辑器 |
| 格式 | 自动或手动 |
| 语法帮助 | 上文敏感或基于菜单键 |
| 输出 | SAS 报告或 HTML |
| 项目 | 是或否 |
| 自动完成 | 是或否 |

##### 什么是 SAS Enterprise Guide？

SAS Enterprise Guide 是一个强大的 Windows 客户端应用程序，提供了一个用于透明访问 SAS 功能的图形用户界面 (GUI)。

它提供了：

- 带有向导的点击界面，允许用户定义任务

- 根据用户选择生成并执行 SAS 代码

- 一个完整的编程接口，用于编写、编辑和提交 SAS 代码

本课程将使用该编程接口。

##### 什么是 SAS 窗口环境？

![](img/d3bde6e6ab06b1fc622215d982111742_20_0.png)

SAS 窗口环境由一系列窗口组成，你可以使用这些窗口编辑和提交程序并查看结果。SAS 窗口环境包含以下窗口：

- 用于准备和提交程序的增强编辑器和程序编辑器窗口

- 用于查看注释（Notes）、警告消息和错误信息的日志窗口

- 输出窗口，包含大多数 SAS 过程生成的输出

# 1.02 多项选择投票

你将使用哪个编辑器来编写 SAS 程序？

- a. SAS Enterprise Guide 程序编辑器

- b. SAS 窗口环境中的程序编辑器

- c. 其他编辑器

- d. 我不知道。

##### 程序命名规范

在本课程中，你将以下结构检索并保存 SAS 程序：

- 1 课程 ID

- 2 章节

- 3 类型 (na=活动, d=演示, e=练习, s=答案)

- 4 项目

- 5 占位符

![](img/d3bde6e6ab06b1fc622215d982111742_21_0.png)

##### 编程 2，第4章，演示 1

##### 定位数据文件

在本课程中，使用宏变量引用来提供更灵活的文件定位方法。

示例：

```
%let path=s:\workshop;
```

```
infile "&path\sales.csv";
```

```
infile "&path\payroll.dat";
```

##### 三个练习级别

课程的设计是让你只完成**一组**练习。请选择最适合你技能的级别。

| 级别 | 描述 |
| :--- | :--- |
| 等级 1 | 提供逐步说明。 |
| 等级 2 | 提供较少的信息和指导。 |
| 挑战 | 提供最少的信息和指导。学生可能需要使用帮助功能。 |

##### 获取帮助

在课堂上，你可以根据使用的编辑器通过以下几种方式获取产品帮助：

- 入门教程

- 软件包含的帮助功能

- 如果可以访问网络，可以使用基于网络的帮助

![](img/d3bde6e6ab06b1fc622215d982111742_22_0.png)

##### 扩展你的学习

课后，你将可以访问本课程创建的扩展学习页面。该页面包括：

- 课程数据和程序文件

- 课程笔记的 PDF 文件

- 其他课程特定的资源。

![](img/d3bde6e6ab06b1fc622215d982111742_23_0.png)

此页面在课程期间可能可用。

#### 1.3 课程数据文件

##### 目标

- 运行 SAS 程序创建课程数据文件。

- 运行 SAS 程序定义数据位置。

##### 业务场景

识别课程数据文件的位置并创建数据文件。

![](img/d3bde6e6ab06b1fc622215d982111742_24_0.png)

##### 创建课程文件

creata 程序创建课程数据文件。该程序必须在课程开始时运行。

- 打开 libname 程序。LIBNAME 语句以星号开头。这意味着它被注释掉了，SAS 不执行。此时，你只想让 SAS 执行 %LET 语句来告诉它数据所在。

- 注意默认值。如果你的文件要创建在 s:\workshop，则不需要更改。

- 按 F3 提交程序。

- 查看结果并确认输出包含文件列表。

##### 定义数据位置

libname 程序告诉 SAS 寻找课程数据。每次启动新会话时必须运行此程序。

- 1. 注意 %LET 语句的默认值。

- 2. 如果你的文件不在 S:\workshop，请更改 PATH= %LET 语句的值以反映你的数据位置。

```
/* Windows/UNIX */

/* STEP 1: 注意 %LET 语句的默认值。 */
/* STEP 2: 如果你的文件不在 S:\workshop */
/* 修改 PATH= %LET 语句的值以反映 */
/* 你的数据位置。 */
```

##### 必练习

- 1. 创建课程数据

  a. 所有课程数据的默认位置是 s:\workshop。如果你的数据文件要创建在 s:\workshop 以外，你必须为你的课程数据识别一个位置。

      在此处创建文件：C:\Workshop\PR2

  b. 选择 文件 -> 程序。

  c. 导航到数据文件夹，选择 credata 并点击打开。程序显示在编辑器中。

观察 %LET 语句的默认值。

- 如果你的文件要创建在 s:\workshop，则不需要更改。
