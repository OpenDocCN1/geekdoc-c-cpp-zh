
# 函数

代码

```c
1: /*/Program Aim: Show two functions
2: ascertain minimum and maximum of 3 numbers*/
3: #include <stdio.h>
4: int main()
5: {
6:     int max(int no1, int no2, int no3);
7:     int min(int no1, int no2, int no3);
8:     int val1, val2, max_val, min_val;
9:     
10:    ///Read 3 Numbers
11:    printf("Program to find maximum of 3 numbers\n\n");
12:    printf("\n\nEnter number 1: \t", &val1);
13:    scanf("%d", &val1);
14:    printf("Enter number 2: \t",
15:    scanf("%d", &val2);
16:    printf("Enter number 3: \t",
17:    scanf("%d", &val3);
18:
19:
20:    //find max
21:    max_val = max(val1, val2, val3);
22:    printf("maximum of %d, %d and %d is: %d\n",
23:    val1, val2, val3, max_val);
24:
25:    //find min
26:    min_val = min(val1, val2, val3);
27:    printf("minimum of %d, %d and %d is: %d\n",
28:    val1, val2, val3, min_val);
29:    getch();
30: }
31:
32:   //Function to compute maximum
33:   int max(int no1, int no2, int no3)
34:   {
35:     if ((no1 > no2) && (no1 > no3))
36:        return (no1);
37:
38:     else if ((no2 > no1) && (no2 > no3))
39:        return (no2);
40:     else return (no3);
41:   }
42:
43:   //Function to compute minimum
44:   int min(int no1, int no2, int no3)
45:   {
46:     if ((no1 < no2) && (no1 < no3))
47:        return (no1);
48:
49:     else if ((no2 < no1) && (no2 < no3))
50:        return (no2);
51:
52:     else return (no3);
53:   }
```

# 代码

```c
1: //程序目标 - 使用函数计算圆的属性/
2: #include <stdio.h>
3: 
4:
5: main()
6: {
7: getRadius();
8: 
9: printf("\nProgram End\n");
10: getch();
11: }
12:
13: getRadius()
14: {
15:     int radius;
16:     float pi = 3.1412;
17:     printf("Enter a radius: \t");
18:     scanf("%d", &radius);
19:
20: //函数的调用与执行
21:     printf("Radius of %d. Diameter is %d cm\n",
22:     radius, diameter(radius));
23:
24:     printf("Radius of %d. Circumference is %d cm\n",
25:     radius, circumference(radius));
26: }
27:
28: // 直径函数
29: int diameter(int radius)
30: {
31: return (2 * radius);
32: }
33:
34: // 周函数
35: int circumference(int radius)
36: {
37:     float pi = 3.142;
38:     return (2 * pi * radius);
39: }
40:
41: // 函数结束
42:
```

## 注释

存在两个函数，一个用于计算圆直径，另一个用于计算周 - 第 28 到 39 行。直径和周的整数变量在每个函数内部声明（第 29 和 35 行）。整数半径在第 15 行声明并在第 18 行扫描到内存。函数在第 13 到 26 行被调用，并从第 28 到 39 行返回。

Q7.2. 扩展上述程序，创建一个计算圆面积的函数。

# 结语

如果读者从第一书中获得了乐趣或获益，他们可能想考虑《商务 C 语言编程》系列中的第二或第三本书。

# 第二册

第二册侧重于将大部分内容应用于业务问题。但读者应该熟悉一些商务数学、统计学和财务。编程应用的领域包括预测、财务管理、人力资源管理、简单的损益表和比率、折旧方法、概率论和游戏。第一书中关于循环、数据类型和处理的知识是至关重要的。

其中一个章节展示了如何使用 `for` 循环计算和比较直线折旧、余额余额折旧和数字数字和折旧。用户输入资产成本和预期寿命（年）。结果是 C 程序通过各种折旧方法计算每年的折旧额。

一个专门预测的章节包含了循环和嵌套循环。首先从 `while` 开始，然后进展到使用 `for` 来保护数据输入。例如，`for` 循环确保输入的数据项数量符合预期，`while` 循环确保数据值在相关范围内。直线图（例如 y = mx + c 或 y = a + bx）和多项式（例如 a = bx²）公式应用于业务场景。更复杂的公式用于计算预测所需的 b、a 和 r 值 - 这些值是业务顾问使用和理解的。需要一些相关性和回归的知识。

一个章节采用了表格循环，并进一步开发这些以计算折扣值和年金价值。在此，一个章节专门介绍资本投资评估。循环用于根据用户输入的指定的折扣因子（一个百分比）计算折扣值。折扣值与相应的估计现金流相乘，然后得出用于决策的净现值。程序开始于用户输入所有值（年份、估计现金流和来自他们提供的纸质表格的折扣值）。然后进展到用户编写自己的折扣表程序。将这些值输入到相应年份的现金流中。程序进一步开发为在 `for` 循环内自动计算折扣值，允许仅输入现金流。用户输入折扣值 - 一个百分比 - 然后是现金流。程序计算其他所有内容，包括内部收益率。`while` 循环允许用户更改折扣因子以插值得到更准确的内部收益率。还研究了售后回租和预期值的计算。这需要预先具备现金流折现模型的知识。

一个关于自动售卖机的案例研究展示了如何计算硬币数量。循环允许处理硬币投入和找零发放。提供了管理报告，管理层可以访问这些信息，例如各种硬币的库存、咖啡库存、重新订单数量等。程序将循环与字母数字密码保护相结合，引入了 `Strcmp`。

设计了存储在永久内存和临时内存中的数据库。研究了存储在临时内存中的人力资源数据库中的结构，使用了密码保护并结合了多种数据类型：`char`、`int`、`DATE`，用于根据裁员法根据 1967-2003 年《裁员付款法案》的计算计算裁员金。存储在永久内存中的电子电话簿将循环与 `switch` 语句相结合，向读者介绍了指针和文件创建。

正态分布和泊松分布以及学习曲线理论应用数据类型、处理和循环的知识。工资单通过所得税类型和税率的组合进行处理。

著名的火柴游戏从工厂食堂带到了电脑。玩家可以在一个涉及 17 根数字火柴的游戏中与电脑斗智。玩家和电脑轮流挑选 1 到 3 根火柴，从而减少可用火柴的数量。挑选最后一根火柴的人输。

# 第三册

第三册致力于业务中的数组以及第一、二书中未涵盖的问题，读者应该熟悉第一书的所有内容以及商务财务中的热门话题。研究了仅靠循环不足以解决的领域，例如评估投资风险。需要第一书中引入的数组、资本投资评估和标准差知识。第三册将第一、二册中的循环和数组结合到现金流中，其中可以使用表格格式打印汇总数据来评估一系列项目。预期值被写为一系列现金流，并查看相关的的结果，其中计算了标准差、变异和变异系数。这对业务顾问来说是无价的数据。

讨论了变动成本法。用户可以指定产品线的数量，输入每个产品的销售值和变动成本。然后是固定成本。程序设计用于计算每个产品范围的盈亏平衡点、贡献率和安全边际。读者必须熟悉数组、`for` 循环、变动成本法和盈亏平衡分析。

工资单的准备扩展到包括字符数组和一组循环，用于生成用户确定数量的工资单，包含名、姓和各种税率范围。结合了第一、二书中讨论的示例。结果是，工资单准备包含了用于员工姓名的字符数组、用于数据输入准确性以及针对特定人数员工的 `while` 循环。

一个章节将数组应用于图形内容，在屏幕上打印水平条形图以视觉化方式呈现数据。编写了使用二项分布解决问题的程序。

猜数字游戏得到了扩展。一个案例研究详细查看了早期不完善彩票设计的陷阱、随机数是如何生成的以及如何避免重复。循环和数组与 C 语言的一些高级领域相结合，以实现正确的程序设计。为了对玩家公平，该章节扩展涵盖了使用循环、数组和概率论计算中奖的概率。出于本性，程序员通过程序设计中内置的安全措施来防止过度利用赌者的弱点，允许赌徒进行有限次数的游戏并设有最大投注限制。彩票游戏从整体上进行了研究，这在编程历史上任何语言中都是未包含过的。

# 附录一 – 答案

A2.1. 第 25 行错误。它应该是 `z` 而不是 `&x`。向屏幕输出数据时不应有 `&` 符号。

A2.2. 第 22 行错误。它应该是 `%f` 而不是 `%d`。`%f` 用于浮点数，`%d` 用于整数，w 在第 6 行中已声明为浮点型。

A2.3. 第 16 行应该是 `z` 而不是 `&x`。由于设计不当导致。

# 附录一 - 答案

## A3.1. density1.c

```c
1 程序目标 - 计算密度密度、质量和体积
2 #include <stdio.h>
3 main() {
4
5     float mass, volume, density = 0;
6
7     printf("Enter mass <grams>: ");
8     scanf("%f", &mass);
9
10    printf("Enter volume <cubic cm>: ");
11    scanf("%f", &volume);
12
13    density = mass / volume;
14
15    printf("\nDensity is %0.2f gram per cubic cm", density);
16
17    printf("\nProgram End\n");
18}
19
20 getch();
```

# 附录一 - 答案

## A3.2 incomeTaxAW/DRKS21082017c

```c
1 /*显示计算个人所得税的程序
2 for 针对个体工商户*/
3 #include <stdio.h>
4 main(){
5 
6
7 // 声明变量
8 float profitBeforeTax, incomeTaxRate,
9 incomeTaxAmount = 0, profitAfterTax = 0;
10
11 // 输入
12 printf("Enter profit before tax: %f");
13 scanf("%f", &profitBeforeTax);
14
15 printf("Enter income tax rate percent: %f");
16 scanf("%f", &incomeTaxRate);
17
18 // 计算个人所得税
19 incomeTaxAmount = profitBeforeTax * incomeTaxRate / 100;
20
21 // 计算税后利润
22 profitAfterTax = profitBeforeTax - incomeTaxAmount;
23
24 // 输出
25 printf("\nProfit before tax: %0.2f", profitBeforeTax);
26 printf("\nIncome tax is: %0.2f", incomeTaxAmount);
27 printf("\nProfit after tax is: %0.2f", profitAfterTax);
28 printf("\nProgram End\n");
29
30 get();
31 }
```

# 代码

```c
1: /*显示计算个人所得税的程序
2: for 针对个体工商户*/
3: #include <stdio.h>
4: main(){
5:
6: // 声明变量
7: float profitBeforeTax, incomeTaxRate,
8: incomeTaxAmount = 0, profitAfterTax = 0;
9:
10: // 输入
11: printf("Enter profit before tax: %f");
12: scanf("%f", &profitBeforeTax);
13:
14: printf("Enter income tax rate percent: %f");
15: scanf("%f", &incomeTaxRate);
16:
17: // 计算个人所得税
18: incomeTaxAmount = profitBeforeTax * incomeTaxRate/100;
19:
20: // 计算税后利润
21: profitAfterTax = profitBeforeTax - incomeTaxAmount;
22:
23: printf("\nScreen Output");
24: printf("\nProfit before tax: \t%0.2f", profitBeforeTax);
25: printf("\nIncome tax is: \t%0.2f", incomeTaxAmount);
26:
27: printf("\nProfit after tax is: \t%0.2f", profitAfterTax);
28:
29: printf("\n\nProgram End!");
30: getch();
31:
32: }
```

# 附录一 - 答案

## Q3.3. 屏幕输入输出程序

```c
#include <stdio.h>
int main() {
```
