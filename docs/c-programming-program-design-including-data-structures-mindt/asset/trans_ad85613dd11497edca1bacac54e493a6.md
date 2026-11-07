

20. 哪些情况可能导致输入流进入失败状态？输入流进入失败状态后会发生什么？（5）

21. 在使用数据类型 `ifstream` 和 `ofstream` 的程序中，需要包含哪个头文件？（10）

22. 假设 `infile` 是一个 `ifstream` 变量，而 `employee.dat` 是一个包含员工信息的文件。请写出使用变量 `infile` 打开该文件的 C++ 语句。（10）

23. 某程序从名为 `inputFile.dat` 的文件中读取数据，经过一些计算后，将结果写入名为 `outFile.dat` 的文件。回答以下问题：（10）

- a. 程序执行后，文件 `inputFile.dat` 的内容是什么？
- b. 如果程序执行前文件 `outFile.dat` 为空，程序执行后该文件的内容是什么？
- c. 如果程序执行前文件 `outFile.dat` 包含 100 个数字，程序执行后该文件的内容是什么？
- d. 如果程序执行前文件 `outFile.dat` 不存在，会发生什么？

24. 假设 `infile` 是一个 `ifstream` 变量，并且它与包含以下数据的文件相关联：`27306 savings 7503.35`。请写出读取并存储数据的 C++ 语句：将第一个输入存储到 `int` 变量 `acctNumber` 中，将第二个输入存储到 `string` 变量 `accountType` 中，将第三个输入存储到 `double` 变量 `balance` 中。（10）

25. 假设有以下语句：（10）

```cpp
ofstream outfile;
int numOfJuiceBottlesSold = 35;
double costOfaJuiceBottle = 0.75;
double revenue;
```

利用这些信息，编写 C++ 语句完成以下操作：

- a. 使用变量 `outfile` 打开文件 `sales.dat`。
- b. 编写语句，将 `outfile` 中的输出格式设置为定点格式，并保留两位小数。
- c. 计算销售果汁瓶所得的收入，并将其存储在变量 `revenue` 中。
- d. 将变量 `numOfJuiceBottlesSold`、`costOfaJuiceBottle` 和 `revenue` 的值写入文件 `sales.dat`。
- e. 编写语句关闭文件 `sales.dat`。

## 编程练习

### 1. 考虑以下不完整的 C++ 程序：

```cpp
#include <iostream>

int main()
{
    ...
}
```

- a. 编写一条语句，将头文件 `fstream`、`string` 和 `iomanip` 包含到该程序中。

- b. 编写语句，将 `inFile` 声明为 `ifstream` 变量，将 `outFile` 声明为 `ofstream` 变量。

- c. 程序将从文件 `inData.txt` 中读取数据，并将输出写入文件 `outData.txt`。编写语句打开这两个文件，将 `inFile` 与 `inData.txt` 关联，并将 `outFile` 与 `outData.txt` 关联。

- d. 假设文件 `inData.txt` 包含以下数据：

```text
Giselle Robinson Accounting
5600 5 30
450 9
75 1.5
```

第一行包含某人的名字、姓氏以及其工作的部门。第二行中，第一个数字表示月度总工资，后面依次是奖金百分比和税率百分比。第三行包含旅行距离和旅行时间。第四行包含售出的咖啡杯数量以及每杯咖啡的成本。编写语句，使程序执行后，文件 `outData.txt` 的内容如下所示。如有必要，可以声明其他变量。所编写的语句应具有足够的通用性：如果输入文件的内容发生变化，并且无需编辑和重新编译程序即可再次运行，那么程序应输出相应的结果。

```text
Name: Giselle Robinson, Department: Accounting
Monthly Gross Salary: $5600.00, Monthly Bonus: 5.00%, Taxes: 30.00%
Paycheck: $4116.00

Distance Traveled: 450.00 miles, Traveling Time: 9.00 hours
Average Speed: 50.00 miles per hour

Number of Coffee Cups Sold: 75, Cost: $1.50 per cup
Sales Amount = $112.50
```

- e. 编写语句关闭输入文件和输出文件。

- f. 编写一个 C++ 程序，测试 a 至 e 部分中的语句。

### 2. 考虑以下程序，其中语句的顺序不正确。重新排列这些语句，使程序提示用户输入圆柱体的高度和底面半径，并输出圆柱体的体积和表面积。将输出格式设置为保留两位小数。

```cpp
#include <iomanip>
#include <cmath>

int main()
{
    double height;

    cout << "Volume of the cylinder = "
         << PI * pow(radius, 2.0) * height << endl;

    cout << "Enter the height of the cylinder: ";
    cin >> radius;
    cout << endl;

    return 0;

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

### 3. 编写一个程序，提示用户输入某人的体重（单位：千克），并输出相应的体重（单位：磅）。将两个体重都四舍五入到小数点后两位输出。（注意：1 千克 = 2.2 磅。）将输出格式设置为保留两位小数。

### 4. 每年夏天，John 和 Jessica 都会在后院种植蔬菜，并从当地苗圃购买种子和肥料。该苗圃出售各种类型、不同袋装规格的蔬菜肥料。购买某种肥料时，他们希望知道每磅肥料的价格，以及每平方英尺的施肥成本。

下面的程序提示用户输入肥料袋的重量（单位：磅）、肥料袋的价格，以及一袋肥料可以覆盖的面积（单位：平方英尺）。程序应输出所需的结果。但是，该程序包含逻辑错误。请找出并修正这些逻辑错误，使程序能够正确运行。

```cpp
// Logic errors.

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

### 5. 某公司有三名员工有资格获得特别加薪。现有一个文件，例如 **Ch3_Ex5Data.txt**，其中包含以下数据：

| 姓名 | 工资 | 加薪比例 |
|---|---:|---:|
| Miller Andrew | 65789.87 | 5 |
| Green Sheila | 75892.56 | 6 |
| Sethi Amit | 74900.50 | 6.1 |

每个输入行包含员工的姓氏、名字、当前工资和加薪百分比。例如，在第一行输入中，员工的姓氏是 **Miller**，名字是 **Andrew**，当前工资是 **65789.87**，加薪比例为 **5%**。编写一个程序，从指定文件中读取数据，并将输出存储到文件 `Ch3_Ex5Output.dat` 中。对于每名员工，必须按照以下格式输出数据：`firstName lastName updatedSalary`。将十进制数的输出格式设置为保留两位小数。

### 6. 编写一个程序，输入物体的质量（单位：克）和密度（单位：克/立方厘米），并使用以下公式输出物体的体积：*体积 = 质量 / 密度*。将输出格式设置为保留两位小数。

### 7. 信用卡未偿余额的利息根据每日平均余额计算。假设 *netBalance* 是账单上显示的余额，*payment* 是支付金额，*d1* 是计费周期中的天数，*d2* 是付款日距离计费周期结束的天数。那么，每日平均余额为：

*averageDailyBalance = (netBalance × d1 − payment × d2) / d1*

如果月利率为 0.0152，那么未偿余额的利息为：

*interest = averageDailyBalance × 0.0152*

编写一个程序，输入 *netBalance*、*payment*、*d1*、*d2* 和月利率。程序输出利息。将输出格式设置为保留两位小数。

### 8. Linda 正在创办一家新的化妆品和服装企业。她希望在支付所有费用后获得约 10% 的净利润，这些费用包括商品成本、店铺租金、员工工资以及店铺的电费。她想知道商品应加价多少，才能在年底支付所有费用后，获得约为商品成本 10% 的净利润。请注意，商品加价后，她还希望将商品以 15% 的折扣价出售。编写一个程序，提示 Linda 输入商品总成本、员工工资（包括她自己的工资）、年租金以及预计电费。然后，程序输出商品应加价的金额，使 Linda 能够获得期望的利润。

### 9. Dairy Farm 决定使用立方体形状的容器，而不是圆柱体形状的容器来运输牛奶。编写一个程序，提示用户输入

