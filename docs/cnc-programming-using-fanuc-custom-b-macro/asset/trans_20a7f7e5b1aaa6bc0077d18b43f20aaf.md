
```
END 1;
```
（循环结束。执行跳转到循环开头，以检查 #1 是否仍然小于或等于 999）

```
M30;
```

使用 WHILE 语句计算标准差的流程图见图 5.9（算法开头的数据输入步骤未在流程图中显示）。程序号为 8006 的是相应程序。注意，该算法使用两个循环。

![](img/1341ce50369ce8fcfb8dc3539d51c52f_115_0.png)

**图 5.9** 使用 WHILE 语句计算样本标准差的算法流程图。

```text
O8006 (STD DEV CALCULATION USING WHILE);
(#1 THROUGH #10 @ DATA);
(STORE DESIRED VALUES IN #1...#10);
(#100 @ NUMBER OF GIVEN DATA);
(SET #100 TO THE NUMBER OF DATA);
(#101 @ COUNTER);
(#102 @ SUM OF GIVEN DATA);
(#103 @ AVERAGE OF GIVEN DATA);
(#104 @ SUM OF SQUARE DEVIATION);
(#105 @ MEAN SQUARE DEVIATION);
(#505 @ STANDARD DEVIATION);
;
#1 = 1;                      (First data)
#2 = 2;                      (Second data)
#3 = 3;                      (Third data)
#4 = 4;                      (Fourth data)
#5 = 5;                      (Fifth data)
#6 = 6;                      (Sixth data)
#7 = 7;                      (Seventh data)
#8 = 8;                      (Eighth data)
#9 = 9;                      (Ninth data)
#10 = 10;                    (Tenth data)
#100 = 10;                   (NUMBER of data)
#101 = 1;                    (Initial value of COUNTER)
#102 = #1;                   (Initial SUM set to the first data)
WHILE [#101 LT #100] DO 1;   (The first loop starts here. It ends at
                             the END 1 block. Note that END 1
                             appears twice in this program
                             because the same identification num-
                             ber, 1, has been used for both the
                             loops. The current loop is executed if
                             #101 is less than #100. If not, the loop
                             terminates, and the execution jumps
                             after the END 1 block of this loop)
#101 = #101 + 1;             (COUNTER incremented by 1)
#102 = #102 + #[#101];       (Next data added to SUM)
END 1;                       (The end of the first loop. The execu-
                             tion jumps to the start of the loop to
                             check if #101 is still less than #100)
#103 = #102 / #100;          (AVERAGE calculated)
#101 = 1;                    (COUNTER initialized to 1)
#104 = [#103 - #1] * [#103 - #1];
                             (Initial SUM OF SQUARE DEVIA-
                             TION set to the square deviation for
                             the first data)
WHILE [#101 LT #100] DO 1;   (The second loop starts here. It is
                             executed if #101 is less than #100. If
                             not, the loop terminates, and the exe-
                             cution jumps to the block after the
                             END 1 block of this loop, that is,
                             jumps after the second END 1 of this program)
#101 = #101 + 1;             (COUNTER incremented by 1)
#104 = #104 + [#103 - #[#101]] * [#103 - #[#101]];
                             (Square deviation for the next data
                             added to SUM OF SQUARE DEVIATION)
END 1;                       (The end of the second loop. The execu-
                             tion jumps to the start of the loop to
                             check if #101 is still less than #100)
#105 = #104 / [#100 − 1];    (MEAN SQUARE DEVIATION calculated)
#505 = SQRT[#105];           (STANDARD DEVIATION calculated and
                             stored in the permanent common variable #505)
M30;
```

图 5.5 所示的级数求和流程图是为与条件 GOTO 语句配合使用而设计的。同一算法如果希望用 WHILE 语句实现，其流程图将如图 5.10 所示。读者应尝试根据该流程图编写程序，此练习留作习题。只需为输入 x 和 n，以及计数器 i、项和总和定义变量。此后，编写程序就只是按照已定义的变量照搬流程图而已。

**图 5.10**  
使用 WHILE 语句的级数求和算法流程图。

![](img/1341ce50369ce8fcfb8dc3539d51c52f_117_0.png)

尽管 WHILE 语句用于循环执行，但如果指定条件为真，它也可以用于执行某些语句块一次：

```text
WHILE [<a conditional expression>] DO 1;
...
...
...
GOTO 10;
END 1;
N10 ...;
```

回想一下，IF_THEN_ 格式在满足指定条件时只能执行一条宏语句。此前已提出一种间接方法来执行多条语句。

### 5.5 宏变量编号的算术运算

如前所述，宏变量不能使用任意字母数字字符组合来定义。它们只能通过特定变量编号来定义。这有点不方便，因为程序员无法直观感受到程序中使用的不同变量所赋予的含义。

然而，宏变量的一个独特特性是允许对变量编号进行算术运算。这在某些情况下可以加以利用。例如，在 PASCAL 中，可以用五个变量（例如 MARKS1、MARKS2、MARKS3、MARKS4 和 MARKS5）存储一名学生在五门科目中的成绩。另一方面，在宏程序中，成绩可以存储在例如 #101、#102、#103、#104 和 #105 中。虽然 MARKS1、MARKS2、MARKS3、MARKS4 和 MARKS5 彼此完全独立，但 #101、#102、#103、#104 和 #105 遵循一种模式。某一科目的变量编号可以通过在前一科目的变量编号上加 1 来得到。这一事实可用于编写例如计算总成绩的程序。此类算法的流程图见图 5.11，相应程序号为 8007。该程序中使用 WHILE 语句创建循环，因为它比条件 GOTO 语句更可取。不过，读者应尝试使用 IF_GOTO_ 语句构造该循环，作为练习。

![](img/1341ce50369ce8fcfb8dc3539d51c52f_119_0.png)

**执行轨迹**  
*（假设成绩为 50、60、70、80 和 90）*

|  | 计数器 | 总和 |
|---|---:|---:|
| 计数器和总和的初始值 | 0 | 0 |
| 执行 I 循环后的值 | 1 | 50 |
| 执行 II 循环后的值 | 2 | 110 |
| 执行 III 循环后的值 | 3 | 180 |
| 执行 IV 循环后的值 | 4 | 260 |
| 执行 V 循环后的值 | 5 | 350 |
| 最终总和 |  | 350 |

**图 5.11** 计算总成绩的算法流程图及执行轨迹。

```text
O8007 (AGGREGATE MARKS CALCULATION);
(#1 @ COUNTER);
(#2 @ SUM);
(#3 @ TOTAL SUBJECTS);
(#506 @ FINAL SUM);

#101 = 50;
#102 = 60;
#103 = 70;
#104 = 80;
#105 = 90;
#1 = 0;
#2 = 0;
#3 = 5;                 (If the total number of subjects is differ-
                        ent from 5, define #3 accordingly)

WHILE [#1 LT #3] DO 1; (Start of the loop)
#1 = #1 + 1;           (COUNTER incremented by 1)
#2 = #2 + #[100 + #1]; (Marks obtained in the next subject
                        added to SUM)

END 1;                 (End of the loop)

#506 = #2;             (FINAL SUM stored in the permanent
                        common variable #506)

M30;
```

当然，这是一个简单的例子；五门科目的成绩可以直接相加。然而，如果数据数量太大（例如 100），这样的程序就会有用。此外，这里的目的是解释如何对变量和编号进行算术运算，以及在这种情况下如何绘制包含循环的流程图。

宏变量的这种特性还可以用于操作某些遵循确定模式的系统变量。例如，对于某一特定轴，各种工件偏置值的变量编号之间相差 20（见表 5.2(a) 的每一行，该表是表 3.12 的一部分）。类似地，对于某个特定工件坐标系，下一轴的变量编号增加 1（见表 5.2(a) 的每一列）。所识别出的模式可以用编号 5201 进行数学描述，如表 5.2(b) 所示，该表是表 5.2(a) 的一部分。因此，如果指定了轴和工件坐标系，就可以计算出相应的系统变量编号。外部 G54、G55、G56、G57、G58 和 G59 工件坐标系的乘数（20 的倍数）分别为 0、1、2、3、4、5 和 6，而 X 轴、Y 轴和 Z 轴的加数分别为 0、1 和 2（其余轴如果存在，则为 3、4、5 等）。因此，例如，G56 坐标系的 Y 轴偏置值存储在变量编号 5201 + 20 × 3 + 1 中，即 #5262 中。

| 轴 | 外部 | G54 | G55 | G56 | G57 | G58 | G59 |
|---|---|---|---|---|---|---|---|
| X | #5201 | #5221 | #5241 | #5261 | #5281 | #5301 | #5321 |
| Y | #5202 | #5222 | #5242 | #5262 | #5282 | #5302 | #5322 |
| Z | #5203 | #5223 | #5243 | #5263 | #5283 | #5303 | #5323 |

(a)

| 轴 | 外部 | G54 | G55 | G56 |
|---|---|---|---|---|
| X | #5201 + 20 × 0 + 0 | #5201 + 20 × 1 + 0 | #5201 + 20 × 2 + 0 | #5201 + 20 × 3 + 0 |
| Y | #5201 + 20 × 0 + 1 | #5201 + 20 × 1 + 1 | #5201 + 20 × 2 + 1 | #5201 + 20 × 3 + 1 |
| Z | #5201 + 20 × 0 + 2 | #5201 + 20 × 1 + 2 | #5201 + 20 × 2 + 2 | #5201 + 20 × 3 + 2 |

(b)

**表 5.2** 铣床上各种工件偏置值的系统变量编号规律

