
```text
45 66.45 44.754 11.12 51 176 176 47 79.15 47.273 10.60 47 162 164
54 83.12 51.855 10.33 50 166 170 49 81.42 49.156 8.95 44 180 185
51 69.63 40.836 10.95 57 168 172 51 77.91 46.672 10.00 48 162 168
48 91.63 46.774 10.25 48 162 164 49 73.37 50.388 10.08 67 168 168
57 73.37 39.407 12.63 58 174 176 54 79.38 46.080 11.17 62 156 165
52 76.32 45.441 9.63 48 164 166 50 70.87 54.625 8.92 48 146 155
51 67.25 45.118 11.08 48 172 172 54 91.63 39.203 12.88 44 168 172
51 73.71 45.790 10.47 59 186 188 57 59.08 50.545 9.93 49 148 155
49 76.32 48.673 9.40 56 186 188 48 61.24 47.920 11.50 52 170 176
52 82.78 47.467 10.50 53 170 172
```

- a. 创建一个包含这些数据的文本文件。
- b. 使用 `INFILE` 语句将数据输入 SAS。有关此任务的更多信息，请参阅第 2 章。
- c. 使用 `PROC UNIVARIATE` 为每个变量生成汇总统计量。有关此任务的更多信息，请参阅第 3 章。
- d. 使用 `PROC SGPLOT` 生成以静息脉搏为函数的跑 1.5 英里时间图。有关此任务的更多信息，请参阅第 6 章。

4. 从具有四个组且均值分别为 (15, 15, 18, 15) 的等重复单因素方差分析模型中生成数据，标准差为 1.5。假设每个组重复五次。提示：SAS 帮助可以建议语法。记住如果 `Z ~ N(0,1)`，则 `μ+σ*Z ~ N(μ, σ²)`。通过使用 `PROC GLM` 拟合方差分析模型来检验四个组的均值相等性。报告结果。提示：你需要使用一个标识生成组的变量，并且需要从指定的分布中生成随机响应。此组变量是与 `PROC GLM` 一起使用的 `CLASS` 语句的一部分。有关线性模型的更多信息，请参阅第 5 章。

5. 生成观测对 (`X`,`Y`)，其中 `Y ~ N(3 + X - 0.5*X², σ=2)`，且 `X` 从 0 到 10 按 0.05 的增量变化。绘制数据的散点图，并叠加回归线和 LOESS 拟合。你是否有证据表明线性回归模型在这里是不充分的？提示：`X²` 项可以使用 `X*X` 或 `X**2` 编码。提示：`DO` 循环可以用非整数增量指定。（参见 SAS 帮助关于 `DO` 循环。）有关生成统计图形的更多信息，请参阅第 6 章和第 7 章。

## 读取、合并和管理数据以供后续分析

![](img/26474180ee55914c13fb9156a7678157_38_0.png)

- 2.1 数据集的临时与永久状态 ................................... 24
- 2.2 将数据读入 SAS 数据集 ..................................................... 27
- 2.3 写出文件或制作简单报告 ........................................... 39
- 2.4 连接数据集并添加观测 ..................................... 46
- 2.5 合并数据集并添加变量 ................................................ 50
- 2.6 使用 `PROC SQL` 进行数据库处理 ..................................................... 58
- 2.7 摘要 ............................................................................... 70
- 2.8 参考文献 ............................................................................ 71
- 2.9 练习 ............................................................................. 71
- 2.10 自学实验室探索 ..................................................... 73

第 1 章的重点是帮助你开始编写 SAS 程序，并为使你的程序易于阅读和清晰提供建议。（当你需要使用一年前编写的程序时，你会感谢我的，因为它现在与你的当前项目相关。）除了模拟数据你所分析的数据集，你总是需要为统计分析读取一个数据集。坦率地说，你在为分析设置和塑造数据集上花费的时间，可能比做统计描述和分析所花费的时间还要多。本章讨论这项工作。关于用标签增强变量名或用格式增强变量值的其他细节，则推迟到第3章和第8章。在你开始探索将数据读入SAS的方法之前，让我们先对SAS中的函数以及函数如何用于向数据集中添加变量这一主题做一个简短的 digression。

在第1章中，`LOG10`函数在Display 1.1中被介绍，用来生成包含某些变量常用对数值的新变量。在Display 1.2中，你看到了在`DATA`步中使用`RAND`函数生成伪随机数的用法。与`RAND`相关的许多与统计分布有关的函数将在第8章中介绍。虽然本章的重点是创建分析数据集，但你应该牢记，在数据集创建之后，可以从数据集中的变量创建新变量。在Base SAS Help中可以看到SAS函数功能和多样性的一个很好的概览。（按类别查看函数和`CALL`例程。）你会看到描述性统计函数（例如，`MIN`（最小值）、`CV`（变异系数）、`GEOMEAN`（几何平均值）和`STD`（标准差））。你会看到数学函数（例如，`ABS`（绝对值）、`EXP`（指数函数）、`LOG`（以e为底的对数）、`LOG10`（以10为底的对数）、`LOG2`（以2为底的对数）和`SQRT`（平方根））。其他可能对统计程序员感兴趣的函数类别包括三角函数、截断函数、州和邮政编码、变量、日期和时间、组合、数组和字符函数。

### 2.1 数据集的临时与永久状态

SAS中的数据集具有两部分名称。然而，如果你希望它们仅在SAS的特定会话期间存在，那么它们可以具有单部分名称（有点像巴西足球的巨星）。如第1.4节“什么是SAS数据集”中所讨论的，SAS数据集是矩形对象，其中行是不同的观测值，列是不同的变量。将永久SAS数据集视为驻留在称为SAS库的集合中。两部分名称包括库名和数据集名，以句点分隔。例如，`myfiles.nitrofen`具有指向包含我的SAS数据集的子目录的库名`myfiles`。第二部分名称是`nitrofen`，即特定的数据集。`nitrofen`数据集可能包括图形和格式的目录。提示：最好为图形、格式等有单独的位置。（为提供一点背景，`nitrofen`是一种除草剂。该数据集包含水蚤Ceriodaphnia dubia暴露于不同浓度的`nitrofen`的`nitrofen`浓度-生殖反应数据。¹）

¹ Nitrofen数据集来自Bailer, A. John., and James T. Oris. 1994. “Assessing Toxicity of Pollutants in Aquatic Systems.” Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.

假设你有一个名为`nitrofen.sas7bdat`的SAS数据集。（记住，`.sas7bdat`是Windows中SAS数据集的常见扩展名。）`nitrofen.sas7bdat`数据集存储在一个指向服务器上位置的路径规范的文件夹中。例如：

`C:\Users\baileraj.IT\BAILERAJ\Classes\Web-CLASSES\sta402\data`

#### Display 2.1 定义一个库并引用该库中的数据集

```
libname myfiles "C:\Users\baileraj.IT\BAILERAJ\Classes\Web-CLASSES\sta402\data";
ods rtf file="C:\Users\baileraj.IT\Desktop\Display-2.1.rtf";
proc means data=myfiles.nitrofen maxdec=1 min q1 median q3 max;
  class conc;
  var total brood1 brood2 brood3;
run;
ods rtf close;
```

确认代码正确，只需快速查看SAS日志：

```
1 libname myfiles "C:\Users\baileraj.IT\BAILERAJ\Classes\Web-CLASSES\sta402\data";
NOTE: Libref MYFILES was successfully assigned as follows:
  Engine:        V9
  Physical Name: C:\Users\baileraj.IT\BAILERAJ\Classes\Web-CLASSES\sta402\data
2
3 ods rtf file="C:\Users\baileraj.IT\Desktop\Display-2.1.rtf";
NOTE: Writing RTF Body file: C:\Users\baileraj.IT\Desktop\Display-2.1.rtf
4 proc means data=myfiles.nitrofen maxdec=1 min q1 median q3 max;
5  class conc;
6  var total brood1 brood2 brood3;
7 run;
NOTE: There were 50 observations read from the data set MYFILES.NITROFEN.
```

SAS日志总结了包含SAS数据集的文件夹已正确分配给库名，并且在`PROC MEANS`中处理了50个观测值（五个浓度中每个浓度10个生物）。

#### Display 2.2 产仔数浓度的五数概括

| Conc | N Obs | Variable | Minimum | Lower Quartile | Median | Upper Quartile | Maximum |

|------|-------|----------|---------|----------------|--------|----------------|---------|

| 0 | 10 | total | 24.0 | 30.0 | 32.5 | 34.0 | 36.0 |

|  |  | brood1 | 3.0 | 5.0 | 5.5 | 6.0 | 6.0 |

|  |  | brood2 | 10.0 | 11.0 | 12.0 | 14.0 | 15.0 |

|  |  | brood3 | 10.0 | 12.0 | 15.0 | 15.0 | 17.0 |

| 80 | 10 | total | 26.0 | 29.0 | 32.5 | 33.0 | 36.0 |

|  |  | brood1 | 3.0 | 5.0 | 5.0 | 6.0 | 8.0 |

|  |  | brood2 | 9.0 | 11.0 | 12.0 | 12.0 | 13.0 |

|  |  | brood3 | 12.0 | 14.0 | 14.5 | 16.0 | 18.0 |

| 160 | 10 | total | 23.0 | 27.0 | 29.0 | 30.0 | 31.0 |

|  |  | brood1 | 2.0 | 6.0 | 6.0 | 6.0 | 6.0 |

|  |  | brood2 | 8.0 | 10.0 | 12.0 | 12.0 | 13.0 |

|  |  | brood3 | 10.0 | 11.0 | 11.0 | 12.0 | 13.0 |

| 235 | 10 | total | 7.0 | 13.0 | 16.5 | 21.0 | 27.0 |

|  |  | brood1 | 2.0 | 4.0 | 6.0 | 6.0 | 7.0 |

|  |  | brood2 | 0.0 | 0.0 | 3.5 | 10.0 | 13.0 |

|  |  | brood3 | 0.0 | 6.0 | 6.5 | 9.0 | 10.0 |

| 310 | 10 | total | 0.0 | 5.0 | 6.0 | 6.0 | 15.0 |

|  |  | brood1 | 0.0 | 5.0 | 5.5 | 6.0 | 7.0 |

|  |  | brood2 | 0.0 | 0.0 | 0.0 | 0.0 | 10.0 |

|  |  | brood3 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |

如果不想永久保存数据集，而只想在当前SAS会话中使用它怎么办？其他章节中有大量临时文件存储的示例。例如，Display 1.2中模拟简单线性回归数据集的代码（在Display 2.3中以最小修改重现）生成一个名为`WORK.lin_reg_data`的数据集（其两部分名称），或更简单地`lin_reg_data`（其单部分名称）。

#### Display 2.3 生成临时数据集的示例代码

```
data lin_reg_data;
  call streaminit(32123);
  do x = 0 to 10 by 1;
    y = 3 + 2*x + 2*RAND('NORMAL');
    output;
  end;
run;

ods rtf bodytitle file='C:\Users\baileraj.IT\Desktop\ch2-fig2.3.rtf';
proc sgplot data=lin_reg_data;   * or equivalently, data=work.lin_reg_data;
  scatter y=y x=x;
run;

proc reg data=lin_reg_data;
  model y=x;
run;
ods rtf close;
```

Display 2.3代码中生成的数据集包含11个观测值和两个变量（`X`，`Y`）。SAS日志的一瞥证实了这一点，并显示以下消息：

```
NOTE: The data set WORK.LIN_REG_DATA has 11 observations and 2 variables.
```

`WORK`库是SAS在SAS会话执行期间分配的临时存储。`lin_reg_data`是在本次SAS会话期间存储在此临时库中的数据集。关闭SAS后，`lin_reg_data`数据集就会消失到虚拟蒸汽中，或者如果你愿意的话，消失到电子以太中。

### 2.2 将数据读入SAS数据集

统计合作者或顾问的常见起点是与需要帮助探索变量间关系、检验处理差异或其他同样有趣的事情的同事或客户会面。此时一个重要问题是：“你的数据是否以电子格式存在？”这个问题在不同学科中的答案各不相同。生物医学科学和商业的同事通常使用Microsoft Excel电子表格进行数据录入和分析。社会科学的同事更可能使用SPSS或其他统计应用程序来设置数据并对其进行操作。如果是小数据集，则可能位于以空格、制表符或其他分隔符分隔变量字段的文本文件中。导入不同原始数据类型的文件在后面的章节中讨论。可以直接将数据输入SAS数据表，或在使用不同系统时将数据保存为SAS数据格式。因为我很少，如果有的话，直接将数据输入SAS数据表，并且reading SAS permanent data sets is covered by the first section of this chapter, I won’t spend any more time discussing these topics here.
