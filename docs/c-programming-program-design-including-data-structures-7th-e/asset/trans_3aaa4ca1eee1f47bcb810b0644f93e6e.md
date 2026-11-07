
- **18.** 假设 age 是 `int` 变量，ch 是 `char` 变量，name 是字符串变量。执行以下输入语句后，age 和 name 的值分别是什么：(8)

```cpp
cin >> age;
cin.get(ch);
getline(cin, name);
```

如果输入为：

  - a. `23 Lance Grant`
  - b.

    ```
    23
    Lance Grant
    ```

- **19.** 以下程序本应从名为 `input.dat` 的文件中读取两个数字，并将这两个数字的和写入名为 `output.dat` 的文件。然而，它未能做到。重写该程序，使其完成预期功能。（另外，请包含关闭文件的语句。）(10)

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
    int num1, num2;
    ifstream infile;

    outfile.open("output.dat");
    infile >> num1 >> num2;
    outfile << "Sum = " << num1 + num2 << endl;
    return 0;
}
```

- **20.** 什么可能导致输入流进入失败状态？当输入流进入失败状态时会发生什么？(5)

- **21.** 使用 `ifstream` 和 `ofstream` 数据类型的程序需要包含哪个头文件？(10)

- **22.** 假设 `infile` 是 `ifstream` 变量，`employee.dat` 是包含员工信息的文件。编写使用变量 `infile` 打开此文件的 C++ 语句。(10)

- **23.** 程序从名为 `inputFile.dat` 的文件读取数据，并在进行一些计算后，将结果写入名为 `outFile.dat` 的文件。回答以下问题：(10)

  - a. 程序执行后，文件 `inputFile.dat` 的内容是什么？
  - b. 如果文件 `outFile.dat` 在程序执行前为空，程序执行后其内容是什么？
  - c. 如果文件 `outFile.dat` 在程序执行前包含 100 个数字，程序执行后其内容是什么？
  - d. 如果文件 `outFile.dat` 在程序执行前不存在，会发生什么？

- **24.** 假设 `infile` 是 `ifstream` 变量，并且它与包含以下数据的文件关联：`27306 Savings 7503.35`。编写 C++ 语句，将第一个输入读入并存储到 `int` 变量 `acctNumber`，第二个输入读入并存储到 `string` 变量 `accountType`，第三个输入读入并存储到 `double` 变量 `balance`。(10)

- **25.** 假设有以下语句：(10)

```cpp
ofstream outfile;
double distance = 375;
double speed = 58;
double travelTime;
```

编写 C++ 语句完成以下操作：

  - a. 使用变量 `outfile` 打开文件 `travel.dat`。
  - b. 编写语句，将输出格式化为固定形式的两位小数。
  - c. 将变量 `day`、`distance` 和 `speed` 的值写入文件 `travel.dat`。
  - d. 计算 `travelTime` 并将其写入文件 `travel.dat`。
  - e. 处理 (a) 到 (d) 中的信息需要哪些头文件？

# 编程练习

- **1.** 考虑以下不完整的 C++ 程序：

```cpp
#include <iostream>

int main()
{
    ...
}
```

  - a. 编写一条语句，在该程序中包含头文件 `fstream`、`string` 和 `iomanip`。
  - b. 编写语句，声明 `inFile` 为 `ifstream` 变量，`outFile` 为 `ofstream` 变量。
  - c. 程序将从文件 `inData.txt` 读取数据，并将输出写入文件 `outData.txt`。编写语句打开这两个文件，将 `inFile` 与 `inData.txt` 关联，并将 `outFile` 与 `outData.txt` 关联。
  - d. 假设文件 inData.txt 包含以下数据：

    ```
    Giselle Robinson Accounting
    5600 5 30
    450 9
    75 1.5
    ```

    第一行包含一个人的名、姓以及此人工作的部门。第二行中，第一个数字表示月总工资，奖金（百分比）和税款（百分比）。第三行包含行驶距离和行驶时间。第四行包含售出的咖啡杯数和每杯咖啡的价格。编写语句，使程序执行后，文件 outData.txt 的内容如下所示。如有必要，请声明额外的变量。你的语句应足够通用，以便如果输入文件的内容发生变化并再次运行程序（无需编辑和重新编译），它也能输出相应结果。

    ```
    Name: Giselle Robinson, Department: Accounting
    Monthly Gross Salary: $5600.00, Monthly Bonus: 5.00%, Taxes: 30.00%
    Paycheck: $4116.00

    Distance Traveled: 450.00 miles, Traveling Time: 9.00 hours
    Average Speed: 50.00 miles per hour

    Number of Coffee Cups Sold: 75, Cost: $1.50 per cup
    Sales Amount = $112.50
    ```

  - e. 编写语句关闭输入文件和输出文件。
  - f. 编写一个 C++ 程序，测试 a 到 e 部分中的语句。

- **2.** 考虑以下程序，其中语句的顺序不正确。重新排列这些语句，使程序提示用户输入圆柱体的高度和底面半径，并输出圆柱体的体积和表面积。将输出格式化为两位小数。

```cpp
#include <iomanip>
#include <cmath>

int main()
{
    double height;

    cout << "Volume of the cylinder = "
         << PI * pow(radius, 2.0)* height << endl;

    cout << "Enter the height of the cylinder: ";
    cin >> radius;
    cout << endl;

    return 0;
}

double radius;

cout << "Surface area: "
     << 2 * PI * radius * height + 2 * PI * pow(radius, 2.0)
     << endl;
cout << fixed << showpoint << setprecision(2);

cout << "Enter the radius of the base of the cylinder: ";
cin >> height;
cout << endl;

#include <iostream>
const double PI = 3.14159;

using namespace std;
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_231_0.png)

- **3.** 编写一个程序，提示用户输入一个人的体重（以千克为单位），并输出等效的体重（以磅为单位）。输出两种体重，并四舍五入到两位小数。（注意 1 千克 = 2.2 磅。）将输出格式化为两位小数。

- **4.** 每年夏天，John 和 Jessica 都会在后院种植蔬菜，并从当地苗圃购买种子和肥料。该苗圃提供不同袋装规格的多种蔬菜肥料。购买某种肥料时，他们想知道每磅肥料的价格以及每平方英尺的施肥成本。以下程序提示用户输入肥料袋的重量（以磅为单位）、袋子的成本，以及该袋肥料可覆盖的面积（以平方英尺为单位）。程序应输出所需结果。然而，该程序包含逻辑错误。找出并修正逻辑错误，使程序正常工作。

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

- **5.** 某足球场经理希望你编写一个程序，计算每场比赛后的门票销售总额。门票有四种类型——包厢票、边线票、优等票和普通票。每场比赛后，数据以以下形式存储在文件中：

| 票价 | 售出票数 |
| --- | --- |
| ... | ... |

示例数据如下：

| 票价 | 售出票数 |
| --- | --- |
| 250 | 5750 |
| 100 | 28000 |
| 50 | 35750 |
| 25 | 18750 |

第一行表示票价为 $250，并且以该价格售出了 5750 张票。输出售出的票数和总销售额。将输出格式化为两位小数。

- **6.** 某公司有三名员工将获得一次特殊加薪。给定一个文件，例如 Ch3_Ex6Data.txt，其中包含以下数据：

| 姓 | 名 | 当前工资 | 加薪百分比 |
| --- | --- | --- | --- |
| Miller | Andrew | 65789.87 | 5 |
| Green | Sheila | 75892.56 | 6 |
| Sethi | Amit | 74900.50 | 6.1 |

每个输入行由员工的姓、名、当前工资和加薪百分比组成。例如，在第一个输入行中，员工的姓是 Miller，名是 Andrew，当前工资是 65789.87，加薪是 5%。编写一个程序，从指定文件读取数据，并将输出存储到文件 Ch3_Ex6Output.dat 中。对于每位员工，必须按以下形式输出数据：名 姓 更新后的工资。将十进制数字的输出格式化为两位小数。

