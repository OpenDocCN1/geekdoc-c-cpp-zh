
![](img/1341ce50369ce8fcfb8dc3539d51c52f_101_0.png)

| 执行轨迹 | 计数器 | #500 | #501 | #502 | ... | #999 |
|---|---:|---|---|---|---|---|
| 计数器和变量的初始值 | 500 | 旧值 | 旧值 | 旧值 | 旧值 | 旧值 |
| 执行第I次循环后的值 | 501 | 空 | 旧值 | 旧值 | 旧值 | 旧值 |
| 执行第II次循环后的值 | 502 | 空 | 空 | 旧值 | 旧值 | 旧值 |
| 执行第III次循环后的值 | 503 | 空 | 空 | 空 | 旧值 | 旧值 |
| 执行第499次循环后的值 | 999 | 空 | 空 | 空 | 空 | 旧值 |
| 执行第500次循环后的值 | 1000 | 空 | 空 | 空 | 空 | 空 |

**图 5.2** 清除所有永久公共变量的算法的流程图和执行轨迹。

```
N10 #1 = #1 + 1;                         (COUNTER incremented by 1, for selecting the next variable)
IF [#1 LE 999] GOTO 10;                  (Branches to 10 if #1 is less than or equal to 999, i.e., if all variables up to #999 are not cleared)

M30;
```

一个更复杂的例子是计算例如 10 个给定数字的样本标准差（$\sigma_{n-1}$），这些数字存储在 #1 到 #10 中。数学公式为

$$\bar{x}=\frac{\sum x_i}{n}$$

$$\sigma_{n-1}=\sqrt{\frac{\sum(x_i-\bar{x})^2}{n-1}}$$

其中
- $x_i$ = 各个数据
- $n$ = 数据总数
- $\bar{x}$ = 给定数据的平均值

计算 $\sigma_{n-1}$ 的算法流程图见图 5.3。程序号 8002 基于该算法。虽然可以将任意值存储到变量 #1 至 #10 中，但本示例中选择的值分别为 1、2、3、...、10。得到的答案将是 3.0276503。该程序可用于计算最多 33 个数字（存储在 #1 至 #33 中）的 $\sigma_{n-1}$。

![](img/1341ce50369ce8fcfb8dc3539d51c52f_102_0.png)

**图 5.3** 计算样本标准差的算法的流程图。

```
O8002 (STANDARD DEVIATION CALCULATION);
(#1 THROUGH #10 @ DATA);
(STORE DESIRED VALUES IN #1...#10);
(#100 = NUMBER OF GIVEN DATA);
(SET #100 TO THE NUMBER OF DATA);
(#101 @ COUNTER);
(#102 @ SUM OF GIVEN DATA);
(#103 @ AVERAGE OF GIVEN DATA);
(#104 @ SUM OF SQUARE DEVIATION);
(#105 @ MEAN SQUARE DEVIATION);
(#501 @ STANDARD DEVIATION);
;

#1 = 1;                        (First data)
#2 = 2;                        (Second data)
#3 = 3;                        (Third data)
#4 = 4;                        (Fourth data)
#5 = 5;                        (Fifth data)
#6 = 6;                        (Sixth data)
#7 = 7;                        (Seventh data)
#8 = 8;                        (Eighth data)
#9 = 9;                        (Ninth data)
#10 = 10;                      (Tenth data. Note that the data-entry
                                step is not shown in the flowchart)
#100 = 10;                     (NUMBER of data)
#101 = 1;                      (Initial value of COUNTER)
#102 = #1;                     (Initial SUM set to the first data)
N10 #101 = #101 + 1;           (COUNTER incremented by 1)
#102 = #102 + #[#101];         (Next data added to SUM)
IF [#101 LT #100] GOTO 10;     (Branching to N10 if all data are not
                                added to SUM)
#103 = #102 / #100;            (AVERAGE calculated)
#101 = 1;                      (COUNTER initialized to 1)
#104 = [#103 - #1] * [#103 - #1];
                                (Initial SUM OF SQUARE DEVIA-
                                TION set to the square deviation for
                                the first data)
N20 #101 = #101 + 1;           (COUNTER incremented by 1)
#104 = #104 + [#103 - #[#101]] * [#103 - #[#101]];
                                (Square deviation for the next
                                data added to SUM OF SQUARE
                                DEVIATION)
IF [#101 LT #100] GOTO 20;     (Branching to N20 if square devia-
                                tions for all data are not added to
                                SUM OF SQUARE DEVIATION)
#105 = #104 / [#100 - 1];      (MEAN SQUARE DEVIATION
                                calculated)
#501 = SQRT[#105];             (STANDARD DEVIATION calcu-
                                lated and stored in the permanent
                                common variable #501)
M30;
```

注意，在 7.2 英寸 LCD 屏幕上，使用 MDI 键无法在一个程序段中连续输入超过 34 个字符。在复杂的数学计算中，确实会出现一个程序段中超过 34 个字符的情况。例如，在标准差程序中，有一个程序段（紧邻 N20 程序段的那个）包含 40 个字符。要在程序中拥有这样的程序段，唯一的方法是先在 PC 上输入程序，然后通过 RS-232C 端口将其下载到 CNC。这样，程序段中实际上可以使用任意数量的字符。然而，如果仅使用 MDI 键输入程序，则长程序段（超过 34 个字符）需要拆分为更小的程序段。例如，

```
#104 = #104 + [#103 - #[#101]] * [#103 - #[#101]];
```

可以按以下方式拆分为更小的程序段，其效果相同：

```
#111 = #103 - #[#101];

#111 = #111 * #111;
#104 = #104 + #111;
```

（引入一个新变量 #111 用于中间计算）

下一个例子求以下形式的一元二次方程的根

$$ax^2 + bx + c = 0$$

两个根的公式为

$$x_1 = \frac{-b + \sqrt{b^2 - 4ac}}{2a} \qquad\text{and}\qquad x_2 = \frac{-b - \sqrt{b^2 - 4ac}}{2a}$$

求这两个根的算法流程图如图 5.4 所示。在基于该算法的程序号 8003 中，可以为对应于 a、b 和 c 的变量赋予任意值。这里取 1、1 和 −2，得到两个根的解为 1 和 −2。

![](img/1341ce50369ce8fcfb8dc3539d51c52f_105_0.png)

**图 5.4** 求一元二次方程根的算法的流程图。

```
O8003 (QUADRATIC EQUATION SOLUTION);
(FORM @ A * X * X + B * X + C = 0);
(#1 @ A);
(#2 @ B);
(#3 @ C);
(ASSIGN DESIRED VALUES TO A,B,C);
(#100 @ DISCRIMINANT);
(#502 @ ROOT1);
(#503 @ ROOT2);
;
#1 = 1;                         (a, i.e. coefficient of x²)
#2 = 1;                         (b, i.e., coefficient of x)
#3 = -2;                        (c, i.e., constant term)
#100 = #2 * #2 - 4 * #1 * #3;   (Determinant calculated)

IF [ABS[#100] LT 0.000001] GOTO 10;          (Branching to N10 if determinant
                                               is 0)

IF [#100 LT 0] THEN #3000 = 1 (IMAG ROOTS);  ("3001 IMAG ROOTS" displayed
                                               and execution terminated, for a
                                               negative determinant. IF_THEN
                                               statement is described in detail in
                                               Sec. 5.3)

#502 = [-#2 + SQRT[#100]] / [2 * #1];         (First root calculated and stored
                                               in the permanent common variable #502)
#503 = [-#2 - SQRT[#100]] / [2 * #1];         (Second root calculated and stored
                                               in another permanent common variable #503)
GOTO 20;                                      (Branching to N20)
N10 #502 = -#2 / [2 * #1];                    (First root calculated, when the determinant is 0)
#503 = #502;                                  (The two roots are equal)
N20 M30;
```

回想一下，每次宏计算通常都会涉及 $10^{-6}$ 的误差。因此，即使判别式实际上为 0，计算结果也可能不*恰好为 0*。正是由于这个原因，本程序中将判别式的绝对值与一个很小的值进行比较。

注意，即使判别式为负并产生报警，永久公共变量 #502 和 #503 中仍可能存储有旧值（如果有的话）。如果这很可能引起混淆，则在判别式为负时将 #502 和 #503 设置为空（#0）。事实上，如前所述，良好的编程实践是在程序一开始就*无条件地*将这些变量设置为空。这适用于所有使用永久公共变量且不需要其旧值的程序。

作为额外练习，读者可以尝试开发程序来求

- 给定数据集中的最大值和最小值
- $\sum_i^n$ 型有限级数的和（一个以索引 i 表示的表达式）
- 无限但收敛级数的和（当发现某个级数项非常小，例如小于 0.000001 时，需要终止计算）
- 给定数字的阶乘计算等

只要有可能，就应使用*递推关系*来提高计算效率。例如，给定数字的阶乘可以用其前一个数字的阶乘来定义：$i! = (i - 1)! \times i$。这种技术在级数求和中尤其有利。下面给出一个例子：

$$\mathrm{sum} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots + (-1)^{n-1}\frac{x^{2n-1}}{(2n-1)!}$$

观察可知

第 $i$ 项 = $(-1)^{i-1}\frac{x^{2i-1}}{(2i-1)!}$ 和第 $(i+1)$ 项 = $(-1)^i\frac{x^{2i+1}}{(2i+1)!}$

