
```cpp
cin.get(ch);
cin.ignore(50, '\n');
cin >> x;
cin.ignore(50, 'E');
cin >> y;
```

### 5. 给定输入：

```text
46 A 49
```

以及以下 C++ 代码：

```cpp
int x = 10, y = 18;
char z = '*';
cin >> x >> y >> z;
cout << x << " " << y << " " << z << endl;
```

输出是什么？

### 6. 假设 x 和 y 是 int 变量，z 是 double 变量，ch 是 char 变量。假设输入语句为：

```cpp
cin >> x >> y >> ch >> z;
```

如果输入如下，x、y、z 和 ch 中分别存储了什么值（如果有）？

- a. 35 62.78
- b. 86 32A 92.6
- c. 12 .45A 32

### 7. 使用函数 `setprecision` 必须包含哪个头文件？

### 8. 使用函数 `pow` 必须包含哪个头文件？

### 9. 假设 name 是 string 类型的变量。编写输入语句，读取输入 Brenda Clinton 并将其存储到 name 中。（假设输入来自标准输入设备。）

### 10. 编写一条 C++ 语句，使用操纵符 `setfill` 输出一行包含 35 个星号的内容，如下行所示：

```text
***********************************
```

### 11. 假设 age 是 int 变量，name 是 string 变量。执行以下输入语句后，age 和 name 的值分别是什么：

```cpp
cin >> age;
getline(cin, name);
```

如果输入为：

- a. 23 Lance Grant
- b. `23`  
  `Lance Grant`

### 12. 假设 age 是 int 变量，ch 是 char 变量，name 是 string 变量。执行以下输入语句后，age 和 name 的值分别是什么：

第一行中的数字分别表示一个矩形的长和宽。第二行中的数字表示一个圆的半径。第三行包含一个人的名、姓和年龄。第四行中的第一个数字是月初的储蓄账户余额，第二个数字是年利率。（假设 π = 3.1416。）第五行包含一个大写字母，其范围在 A 到 Y 之间（含 A 和 Y）。编写语句，使程序执行后，文件 `outData.txt` 的内容如下所示。如有必要，请声明额外的变量。你的语句应具有足够的通用性，以便当输入文件的内容发生变化并再次运行程序时（无需编辑和重新编译），它能输出相应的结果。

```text
Rectangle:
Length = 10.20, width = 5.35, area = 54.57, perimeter = 31.10

Circle:
Radius = 15.60, area = 764.54, circumference = 98.02

Name: Randy Gill, age: 31
Beginning balance = $18500.00, interest rate = 3.50
Balance at the end of the month = $18553.96

The character that comes after A in the ASCII set is B
```

- e. 编写关闭输入文件和输出文件的语句。
- f. 编写一个 C++ 程序，测试 a 到 e 部分中的语句。

### 2. 考虑以下程序，其中语句的顺序不正确。重新排列这些语句，使程序提示用户输入圆柱体的高度和底面半径，并输出圆柱体的体积和表面积。将输出格式化为两位小数。

```cpp
#include <iostream>
#include <cmath>

int main()
{}

double height;

cout << "Volume of the cylinder = "
     << PI * pow(radius, 2.0) * height << endl;

cout << "Enter the height of the cylinder: ";
cin >> radius;
cout << endl;

return 0;

double radius;

cout << "Surface area: "
     << 2 * PI * radius * height + 2 * PI * pow(radius, 2.0) << endl;
cout << fixed << showpoint << setprecision(2);

cout << "Enter the radius of the base of the cylinder: ";
cin >> height;
cout << endl;

#include <iostream>
const double PI = 3.14159;

using namespace std;
```

### 3. 编写一个程序，提示用户输入一个人的体重（以千克为单位），并输出等效的体重（以磅为单位）。输出两个体重值，并四舍五入到两位小数。（注意：1 千克 = 2.2 磅。）将输出格式化为两位小数。

### 4. 每年夏天，John 和 Jessica 都会在后院种植蔬菜，并从当地苗圃购买种子和肥料。该苗圃提供不同袋装规格的各种蔬菜肥料。购买某种肥料时，他们想知道该肥料每磅的价格以及每平方英尺的施肥成本。以下程序提示用户输入肥料袋的重量（以磅为单位）、该袋肥料的成本，以及该袋肥料可覆盖的面积（以平方英尺为单位）。程序应输出所需结果。然而，该程序包含逻辑错误。请找出并改正逻辑错误，使程序正常工作。

```cpp
//Logic errors.

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    double cost;
    double area;

    double bagSize;

    cout << fixed << showpoint << setprecision(2);

    cout << "Enter the amount of fertilizer, in pounds, "
         << "in one bag: ";
    cin >> bagSize;
    cout << endl;

    cout << "Enter the cost of the " << bagSize
         << " pound fertilizer bag: ";
    cin >> cost;
    cout << endl;

    cout << "Enter the area, in square feet, that can be "
         << "fertilized by one bag: ";
    cin >> area;
    cout << endl;

    cout << "The cost of the fertilizer per pound is: $"
         << bagSize / cost << endl;
    cout << "The cost of fertilizing per square foot is: $"
         << area / cost << endl;

    return 0;
}
```

### 5. 一座足球场的经理希望你编写一个程序，计算每场比赛后的门票销售总额。门票有四种类型——包厢票、边线票、高级票和普通入场票。每场比赛后，数据按以下形式存储在文件中：

```text
ticketPrice   numberOfTicketsSold
...
```

示例数据如下所示：

| 票价 | 售出票数 |
| --- | --- |
| 250 | 5750 |
| 100 | 28000 |
| 50 | 35750 |
| 25 | 18750 |

第一行表示票价为 $250，并且以该价格售出了 5750 张票。输出售出的票数和销售总额。将输出格式化为两位小数。

### 6. 编写一个程序，计算并打印员工的月薪。净工资是在扣除以下项目后计算得出的：

- 联邦所得税：15%
- 州税：3.5%
- 社会保障税：5.75%
- 医疗保险/医疗补助税：2.75%
- 养老金计划：5%
- 健康保险：$75.00

你的程序应提示用户输入总金额和员工姓名。输出将存储在文件中。将输出格式化为两位小数。示例输出如下：

```text
Bill Robinson
Gross Amount: ............ $3575.00
Federal Tax: ............ $ 536.25
State Tax: ............ $ 125.13
Social Security Tax: ..... $ 205.56
Medicare/Medicaid Tax: ... $ 98.31
Pension Plan: ............... $ 178.75
Health Insurance: ........... $ 75.00
Net Pay: .................... $2356.00
```

注意，第一列左对齐，右列右对齐。

### 7. 重做第 2 章中的编程练习 21，使每个字符串都能存储一行文本。

### 8. 公司中有三名员工将获得一次特别加薪。给定一个文件，例如 `Ch3_Ex8Data.txt`，其中包含以下数据：

| 姓 | 名 | 当前薪资 | 加薪百分比 |
| --- | --- | --- | --- |
| Miller | Andrew | 65789.87 | 5 |
| Green | Sheila | 75892.56 | 6 |
| Sethi | Amit | 74900.50 | 6.1 |

每个输入行由员工的姓、名、当前薪资和加薪百分比组成。例如，在第一个输入行中，员工的姓是 Miller，名是 Andrew，当前薪资是 65789.87，加薪为 5%。编写一个程序，从指定文件读取数据，并将输出存储到文件 `Ch3_Ex8Output.dat` 中。对于每位员工，数据必须按以下形式输出：firstName lastName updatedSalary。将十进制数的输出格式化为两位小数。

### 9. 编写一个程序，接受质量（以克为单位）和密度（以克每立方厘米为单位）作为输入，并使用公式 density = mass / volume 输出物体的体积。将输出格式化为两位小数。

### 10. 信用卡未付余额的利息使用平均每日余额计算。假设 netBalance 是账单中显示的余额，payment 是已支付的款项，d1 是账单周期中的天数，d2 是在账单周期前付款的天数。那么，平均每日余额为：

```text
averageDailyBalance = (netBalance * d1 - payment * d2)/d1
```

如果每月利率为，例如 0.0152，则未付余额的利息为：

```text
interest = averageDailyBalance * 0.0152
```

编写一个程序，接受 netBalance、payment、d1、d2 和每月利率作为输入。程序输出利息。将输出格式化为两位小数。
