

# 练习

11. A-1 Appliances 商店需要一个程序，允许商店在月初输入库存的洗碗机数量、当月购买的数量以及当月售出的数量。该程序应计算并显示月末的洗碗机库存数量。

- a. 为该问题创建一个 IPO 图，然后对算法进行两次人工跟踪检查（desk-check）。在第一次跟踪检查中，使用 5000 作为月初的洗碗机数量，1000 为购买数量，3500 为销售数量。在第二次跟踪检查中，使用 45、20 和 125。

- b. 在类似于本章图 4-12 所示的表中列出输入、处理和输出项，以及算法。然后将算法编码为程序。

- c. 使用与算法跟踪检查时相同的数据对程序进行人工跟踪检查。

- d. 将 C++ 指令输入名为 `Introductory11.cpp` 的源文件中。同时输入适当的注释以及编译器所需的任何额外指令。

- e. 保存并运行程序。使用与程序跟踪检查时相同的数据对程序测试。

12. 一场音乐会有三个座位区域：管弦乐席（Orchestra）、主楼（Main floor）和阳台（Balcony）。管弦乐席为 $25。主楼席为 $30，阳台席为 $15。经理希望有一个程序，允许他输入每个座位区域售出的门票数量。该程序应计算并显示每个座位区域产生的收入，以及总收入。

- a. 为该问题创建一个 IPO 图，然后对算法进行两次人工跟踪检查。在第一次跟踪检查中，使用 50、100 和 75 分别作为管弦乐、主楼和阳台的数量。在第二次跟踪检查中，使用 30、25 和 99。

- b. 在类似于本章图 4-12 所示的表中列出输入、处理和输出项，以及算法。然后将算法编码为程序。

- c. 使用与算法跟踪检查时相同的数据对程序进行人工跟踪检查。

- d. 将 C++ 指令输入名为 `Introductory12.cpp` 的源文件中。同时输入适当的注释以及编译器所需的任何额外指令。

- e. 保存并运行程序。使用与程序跟踪检查时相同的数据对程序测试。

# 第 4 章

# 完成解决问题的过程

## 中级

-13. Mama Calari's Pizza 的经理想要一个程序，用于计算并显示一个圆形披萨可以切成多少片。经理将输入整个披萨的半径。对于本次练习，使用数字 14.13 作为一片披萨的面积，并使用 3.14 作为 pi 的值。

- a. 为该问题创建一个 IPO 图，然后对算法进行两次人工跟踪检查。在第一次跟踪检查中，使用 10 作为披萨的半径。在第二次跟踪检查中，使用 6。（提示：切片数应略大于 22）
- b. 在类似于本章图 4-12 所示的表中列出输入、处理和输出项，以及算法。然后将算法编码为程序。
- c. 使用与跟踪检查时相同的数据对程序进行跟踪检查。
- d. 将你的 C++ 指令输入名为 `Intermediate13.cpp` 的源文件中。同时输入适当的注释以及编译器所需的任何额外指令。
- e. 保存并运行程序。使用与程序跟踪检查时相同的数据对程序测试。

## 高级

-14. 完成入门级练习 12。将 `Introductory12.cpp` 中的指令输入（或复制）名为 `Advanced14.cpp` 的新源文件中。修改 `Advanced14.cpp` 中的代码，使其计算并显示每个座位区域对总收入的百分比。保存并运行程序。使用 50、100 和 75 分别作为管弦乐、主楼和阳台席的数量对程序测试。然后使用 30、25 和 99 进行测试。（不用担心答案中额外的的小位数。）

-15. 在本次练习中，你将探索在货币计算中使用整数。
- a. 按照启动 C++ 和打开 `Advanced15.cpp` 文件的说明操作。如有必要，将 `system("pause")` 作为一个语句，然后保存程序。当提示输入总薪时，输入 `45.13` 并按回车。屏幕上显示的净薪是错误的，因为这不是减去切片数后的结果。按任意键停止程序。
- b. 检查 `Advanced15.cpp` 文件包含的代码。`#include <iomanip>` 指令告诉 C++ 编译器在当前程序中包含 `iomanip` 文件的内容。`iomanip` 文件包含了 `setprecision` 流操纵符的定义，它出现在 `cout << setprecision(2) << endl;` 语句中。`fixed` 流操纵符定义在 `iostream` 文件，它强制实数显示特定的小数位数。在此程序中，输出值将以两位小数显示。你将在第 5 章学习该指令和两个流操纵符。
- c. 为什么净薪显示为 $33.85 而不是 $33.84？提示：将 `cout << fixed << setprecision(2) << endl;` 语句改为注释，保存并运行程序。输入 `45.13` 为总薪并按回车。研究输出，停止程序并将注释改回语句。
- d. 使用 `Advanced15.cpp` 文件中出现的注释来修改你的程序代码。为什么你需要在计算联邦税和州税的表达式中添加 `.5`？
- e. 保存、运行并测试程序以验证其运行正常，然后停止程序。

-16. 按照启动 C++ 和使用 `SwatBugs16.cpp` 文件的说明操作。程序声明并初始化了一个 `double` 变量。在显示变量值之前，该变量增加了 1.5。如有必要，将 `system("pause");` 语句改为注释，然后保存程序。运行并调试程序。

# TRY THIS 练习的答案

![](img/d64a28a68f49d61137bf2f3170ac40ad_135_0)-1. 见图 4-38。

| IPO 图信息 | C++ 指令 |
| --- | --- |
| 输入 | |
| sale1 | double sale1 = 0.0; |
| sale2 | double sale2 = 0.0; |
| commission rate | double commissionRate = 0.0; |
| 处理 | |
| totalSales | double totalSales = 0.0; |
| 输出 | |
| commission | double commission = 0.0; |
| 算法 | |
| 1. 输入 sale1, sale2 和佣金率 | cout << "First sale? "; cin >> sale1;
cout << "Second sale? "; cin >> sale2;
cout << "Commission rate in decimal format? "; cin >> commissionRate; |
| 2. 通过加 sale1 和 sale2 计算总销售 | totalSales = sale1 + sale2; |
| 3. 通过乘以率计算佣金 | commission = totalSales * commissionRate; |
| 4. 显示佣金 | cout << "Commission: $" << commission << endl; |

2. 见图 4-39。

| IPO 图信息 | C++ 指令 |
| --- | --- |
| 输入 | |
| cup price | double cupPrice = 0.0; |
| plate price | double platePrice = 0.0; |
| cups purchased | int cupsPurchased = 0; |
| plates purchased | int platesPurchased = 0; |
| sales tax rate (5.5%) | const double TAX_RATE = .055; |
| 处理 | |
| total cup cost | double totalCupCost = 0.0; |
| total plate cost | double totalPlateCost = 0.0; |
| subtotal | double subtotal = 0.0; |
| 输出 | |
| total cost | double totalCost = 0.0; |
| 算法 | |
| 1. 输入杯价、售价、杯子数量和盘子数量 | cout << "Cup price: "; cin >> cupPrice;
out << "Plate price: "; cin >> platePrice;
out << "Cups purchased: "; cin >> cupsPurchased;
out << "Plates purchased: "; cin >> platesPurchased; |
| 2. 通过杯子数量乘以杯价计算总杯成本 | totalCupCost = cupsPurchased * cupPrice; |
| 3. 通过盘子数量乘以售价计算总盘成本 | totalPlateCost = platesPurchased * platePrice; |
| 4. 通过加总杯成本和总盘子成本计算小计 | subtotal = totalCupCost + totalPlateCost; |
| 5. 通过小计乘以销售税率并加上结果计算总成本 | totalCost = subtotal * TAX_RATE + subtotal; |
| 6. 显示总成本 | cout << "Total cost: $";
cout << totalCost << endl; |

