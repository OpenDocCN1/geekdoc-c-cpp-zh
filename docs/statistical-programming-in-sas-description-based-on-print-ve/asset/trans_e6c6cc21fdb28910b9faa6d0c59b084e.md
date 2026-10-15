

class.) 最后，我很幸运获得了迈阿密大学的 Barney 奖学金，该奖学金提供了一些支持，让我有时间从事本书材料的编写。

任何致谢部分都不能缺少对家人的认可。我很幸运拥有一个耐心且支持的家庭，即使我在周末下午本可以做其他事情的时候，却分心并对着电脑发牢骚。他们仍然支持我。我要向我的孩子们——Sara、Jacob、Chris 和 Emily——致以衷心的感谢，感谢他们带给我的爱、支持和快乐。最后，我要感谢并致敬我的妻子 Jenny。她是我最好的朋友、体贴而建设性的批评者、热情的支持者，她的爱与支持为我尝试新项目提供了美好的基础。第三次了，我发誓这是我写的最后一本书。

## Part 1
## The Basics—Including Some Nuts and Bolts

+ Chapter 1 Let's Get Started—Preliminaries and a SAS Quick Start...... 3
+ Chapter 2 Reading, Combining, and Managing Data for Later Analysis ........................................ 23
+ Chapter 3 Using SAS Procedures ........................................................ 85
+ Chapter 4 Complex Table Construction and Output Control ........... 121
+ Chapter 5 Basic Models in SAS ..................................................... 155
+ Chapter 6 Producing Statistical Graphics in SAS ........................... 197
+ Chapter 7 Traditional SAS Graphics ............................................... 237

![](img/26474180ee55914c13fb9156a7678157_16_0.png)

## Let’s Get Started—
Preliminaries and a SAS Quick Start

1.1 Statistical Computing versus Programming versus Managing Data ......................................................... 4

1.2 Good Programming Practice ......................................................... 4

1.3 SAS Program Structure ......................................................... 9

1.4 What Is a SAS Data Set? ......................................................... 16

1.5 Internally Documenting SAS Programs ......................................................... 18

1.6 Summary ......................................................... 19

1.7 References ......................................................... 19

1.8 Exercises ......................................................... 19

让我们先给出统计编程的工作定义，然后再介绍一个好的统计程序的结构和外观。DATA 步和过程的简要概述将通过简单但真实的示例呈现。这为快速上手 SAS 编程提供了快速入门。

![](img/26474180ee55914c13fb9156a7678157_18_0.png)

### 1.1 Statistical Computing versus Programming versus Managing Data

计算机是数据分析师和统计学家的分析仪器和实验工具。类似于化学家需要掌握质谱仪的熟练程度，遗传学家需要掌握基因和蛋白质表达技术的熟练程度，统计学家需要具备使用计算机作为工具来构建数据集、进行分析、拟合模型和模拟随机系统的技能。在接下来的章节中，我希望你能对统计编程可以回答的一些问题以及如何使用 SAS 回答这些问题有所了解。本书的重点是统计编程。有些内容涉及数据管理，而统计计算则涉及较少。统计编程可以被视为进行感兴趣的分析所需的编码，这可能包括使用现有过程或自定义现有过程中无法实现的分析。相比之下，统计计算可以被视为统计过程的高效编码（例如，数值方法、随机数生成等）。数据管理可以被概念化为数据文件的结构、存储和操作。本书旨在作为一个介绍，可以引导你阅读更具计算性的书籍，例如 Givens and Hoeting (2005)。这些统计编程思想是使用 SAS 引入的。有许多书籍提供了对 SAS 的优秀介绍（例如，Cody and Pass 1995, Delwiche and Slaughter 2008）。我希望本书能通过强调使用 SAS 解决统计编程问题来补充这些其他书籍。

### 1.2 Good Programming Practice

我认为良好的编程实践可以超越“我知道它是什么”的范畴。在本节中，建议了一些良好实践的指导方针。这些指导方针受到我多年来在许多编程课程中收到的建议的影响，也受到我多年后查看自己记录不充分的代码时产生的遗憾的影响。最后声明一下，我通常会遵循这些指导方针。然而，在我为简单、一次性应用生成快速程序的情况下，我可能不会那么严格地遵循这些指导方针。所以，让我们开始吧。

### Display 1.1 A SAS program that fits a multiple regression

```
/*      mreg-country-20may09.sas

Directory:  C:\baileraj\Classes\Spring09\programs\regression-examples
           [Laptop]
Author:     John Bailer
Purpose:    multiple regression example where average life expectancy
            of women is modeled as a function of country characteristics

Input data file - -------------------------------
            country.data

Directories:
            \\Casnov5\MST\MSTLab\Baileraj
            C:\Users\baileraj\BAILERAJ\Classes\Web-Classes\sta402\data

Input variables -------------------------------
Name = country name (Character variable)
Area = country area
Popsize = population size
Pcturban = % residents in urban setting
Lang = primary language
Liter = % literate
Lifemen = average life expectancy men
Lifewom = average life expectancy women
PcGNP = per capita gross national product

Created Variables -----------------------------
logarea = log10(area);
logpopn = log10(popsize);
loggnp = log10(pcGNP);
ienglish = (lang="English");

Data Source: Extracted from World Almanac
*/
* setting up macro variables for directories;
%let DIR1 = C:\Users\baileraj\BAILERAJ\Classes\Web-Classes\sta402\data;
%let DIR2 = \\Casnov5\MST\MSTLab\Baileraj;

data country;
title "country data analysis";
infile "&DIR1\country.data";

input name $ area popsize pcturban lang $ liter lifemen
      lifewom pcGNP;
logarea = log10(area);
logpopn = log10(popsize);
loggnp = log10(pcGNP);
ienglish = (lang="English");
drop area popsize pcgnp;
run;

proc print data=country;
run;

proc reg data=country;
    title "LITER and LOGGNP as predictors of Life expectancy of women";
    model lifewom = liter loggnp/ tol vif collinoint;
    output out=new p=yhat r=resid;
run;
```

### Display 1.1 *(continued)*

```
/* plot life expectancy of women vs. log(GNP) with a linear regression
   fit and LOESS fit superimposed
*/
ods rtf bodytitle
       title="C:\Users\bailera\Desktop\ch1-display-1_1-fig.rtf";
title "";
proc sgplot data=country;
  reg y=lifewom x=loggnp;
  loess y=lifewom x=loggnp;
run;
ods rtf close;
```

在示例中，程序开头有一个注释块（/* 和 */ 符号之间的所有文本）。程序名称是注释块的第一行。我使用了一种约定，即将日期作为文件名的一部分构建在其中。这是我发现很有用的习惯。目录和作者信息在接下来的几行中给出。我经常使用多台机器，在这里标识这些信息很有帮助。接下来，解释了程序的目的。之后，提供输入数据文件的名称。外部数据文件的目录和它们包含的输入变量接下来被标识。块中最后两个部分描述了创建的其他变量以及数据的原始来源。实际程序语句随后给出。在此示例中，注释块比程序更长。虽然有些人可能会认为这是过度，但我从未后悔注释太多，但我后悔过注释太少。顺便说一下，在此代码中还使用了第二种注释风格——以星号开头并以分号结尾的语句是注释（在代码中，见 * setting up macro variables for directories;）。一个更有用的代码版本可能会为数据集中的变量分配标签。例如，以下语句将增强许多统计过程的输出：

```
label lenglish = "Indicator that English is primary language";
```

此外，标签附加到 SAS 数据集中的变量。这将在即将到来的章节中更详细地讨论。

### 1.2.2 Use meaningful variable names

我的第一次编程经历是使用一种 FORTRAN 版本，该版本对变量名有上限。你可以使用包含最多四个字符的任何变量名。像 B1 和 X27 这样的变量名很常见。即使是 SAS，在其演变早期，变量名的最大长度也为八个字符。现在，变量名最长可达 32 个字符，可以包含大小写字母和下划线的混合。（这使得程序更易读，尽管 SAS 不区分大小写。）变量名可以以字母（a–z, A–Z）或下划线（_ ）开头，后面

