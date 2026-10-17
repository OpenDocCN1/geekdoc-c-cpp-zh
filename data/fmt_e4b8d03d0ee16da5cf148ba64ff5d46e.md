
```cpp
// 程序用于 General Crates, Inc. 根据
// 用户输入的尺寸计算体积、客户费用和利润。
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    // 成本和金额常量
    const double COST_PER_CUBIC_FOOT = 0.23;
    const double CHARGE_PER_CUBIC_FOOT = 0.5;

    // 变量
    double length; // 木箱的长度
    double width; // 木箱的宽度
    double height; // 木箱的高度
    double volume; // 木箱的体积
    double cost; // 制造木箱的成本
    double charge; // 向客户收取的费用
    double profit; // 木箱获得的利润

    // 设置数字的输出格式
    cout << setprecision(2) << fixed << showpoint;

    // 提示用户输入木箱的长度、宽、高。
    cout << "Enter the dimensions of the crate (in feet):\n";
    cout << "Length: ";
    cin >> length;
    cout << "Width: ";
    cin >> width;
    cout << "Height: ";
    cin >> height;

    // 计算木箱的体积、生产成本、
    // 客户费用和利润。
    volume = length * width * height;
    cost = volume * COST_PER_CUBIC_FOOT;
    charge = volume * CHARGE_PER_CUBIC_FOOT;
    profit = charge - cost;

    // 显示计算的数据。
    cout << "The volume of the crate is " << volume << " cubic feet." << endl;
    cout << "To build: $" << cost << endl;
    cout << "Charge to customer: $" << charge << endl;
    cout << "Profit: $" << profit << endl;

    return 0;
}
```

### 程序输出（示例输入已加粗显示）

输入木箱的尺寸（英尺）：

长度：**10**

宽度：**8**

高度：**4**

木箱的体积是 320.00 立方英尺。

制造费用：$73.60

客户费用：$160.00

利润：$86.40

### 程序输出（不同示例输入已加粗显示）

输入木箱的尺寸（英尺）：

长度：**12.5**

宽度：**10.5**

高度：**8**

木箱的体积是 1050.00 立方英尺。

制造费用：$241.50

客户费用：$525.00

利润：$283.50

## 复习题与练习

### 简答

1. 假设定义了以下变量：

```cpp
int age;
double pay;
char section;
```

编写一个 `cin` 语句将输入读入这些变量中。

2. 假设定义了一个字符串对象：

```cpp
string description;
```

- A) 写一个读取单单词字符串的 `cin` 语句。
- B) 写一个读取包含多个单词字符串的语句。

3. 下程序必须包含哪些头文件？

```cpp
int main()
{
  double amount = 89.7;
  cout << showpoint << fixed;
  cout << setw(8) << amount << endl;
  return 0;
}
```

4. 通过确定每个表达式的值来完成下表。

| 表达式 | 值 |
|---|---|
| 28 / 4 - 2 | |
| 6 + 12 * 2 - 8 | |
| 4 + 8 * 2 | |
| 6 + 17 % 3 - 2 | |
| 2 + 22 * (9 - 7) | |
| (8 + 7) * 2 | |
| (16 + 7) % 2 - 1 | |
| 12 / (10 - 6) | |
| (19 - 3) * (2 + 2) / 4 | |

5. 为以下代数表达式编写 C++ 表达式：

```cpp
a = 12*x
z = 5*x + 14*y + 6*k
y = pow(x,4)
g = (b+12)/(4*k)
c = pow(a,3)/pow(b,4)
```

6. 假设程序有以下变量定义：

```cpp
int units;
float mass;
double weight;
```

以及以下语句：

```cpp
weight = mass * units;
```

将发生哪种自动数据类型转换？

- A) `mass` 被降级为 `int`，`units` 保持为 `int`，`mass * units` 的结果为 `int`。
- B) `units` 被提升为 `float`，`mass` 保持为 `float`，`mass * units` 的结果为 `float`。
- C) `units` 被提升为 `float`，`mass` 保持为 `float`，`mass * units` 的结果为 `double`。

7. 假设程序有以下变量定义：

```cpp
int a, b = 2;
float c = 4.2;
```

以及以下语句：

```cpp
a = b * c;
```

`a` 中将存储什么值？

A) 8.4

B) 8

C) 0

D) 以上均非

8. 假设 `qty` 和 `salesReps` 都是整数。使用类型强制转换表达式重写以下语句，使其不再执行整数除法：

```cpp
unitsEach = qty / salesReps;
```

9. 重写以下变量定义，使该变量成为命名常量：

```cpp
int rate;
```

10. 完成以下右表，为左侧列提供使用复合赋值运算符的语句。这些语句应与左侧列的语句等效。

| 使用赋值运算符的语句 | 使用复合赋值运算符的语句 |
|---|---|
| x = x + 5; | |
| total = total + subtotal; | |
| dist = dist / rep; | |
| ppl = ppl * period; | |
| inv = inv - shrinkage; | |
| num = num % 2; | |

### 第 3 章 表达式与交互性

11. 编写一个多重赋值语句，用于替换以下分组赋值语句：

```cpp
east = 1; west = 1; north = 1; south = 1;
```

12. 编写一个 `cout` 语句，使变量 `divSales` 显示在一个宽度为 8 的字段中，使用固定点表示法，精度为 2 位小数。小数点应始终显示。

13. 编写一个 `cout` 语句，使变量 `totalAge` 显示在一个宽度为 12 的字段中，使用固定点表示法，精度为 4 位小数。

14. 编写一个 `cout` 语句，使变量 `population` 显示在一个宽度为 12 的字段中，左对齐，精度为 8 位小数。小数点应始终显示。

### 填空题

15. ________ 函数返回角度的余弦值。

16. ________ 函数返回角度的正弦值。

17. ________ 函数返回角度的正切值。

18. ________ 函数返回数的指数函数。

19. ________ 函数返回浮点数除法的余数。

20. ________ 函数返回数的自然对数。

21. ________ 函数返回以 10 为底的对数。

22. ________ 函数返回数的幂值。

23. ________ 函数返回数的平方根。

24. 使用数学函数的程序必须包含 ________ 文件。

### 算法工作台

25. 一家商店为其客户提供最高信用额度。每个客户的可用额度是其最高额度减去已使用的额度。为该程序编写伪代码算法，询问客户的最高信用额度和已使用的信用额度。程序应显示客户的可用额度。

在你编写伪代码算法后，将其转换为一个完整的 C++ 程序。

26. 为一个程序编写伪代码算法，计算零售销售的总额。程序应询问销售金额和销售税率。税率应以浮点数形式输入。例如，如果销售税为 6%，用户应输入 0.06。程序应显示销售税金额和销售总额。

在你编写伪代码算法后，将其转换为一个完整的 C++ 程序。

27. 为一个程序编写伪代码算法，要求用户输入高尔夫球手在三场比赛中的比分，然后显示这三个分数的平均值。

在你编写伪代码算法后，将其转换为一个完整的 C++ 程序。

### 找错误

以下程序均包含一些错误。请尽可能多地找出它们。

```cpp
28. using namespace std;
int main () {
  double number1,number2, sum;
  Cout << "Enter a number: ";
  Cin << number1;
  Cout << "Enter another number: ";
  Cin << number2;
  number1 +number2 = sum;
  Cout << "The sum of the two numbers is " << sum
  return 0;
}
```

```cpp
29. #include <iostream>
using namespace std;
int main() {
  int number1, number2;
  float quotient;
  cout << "Enter two numbers and I will divide\n";
  cout << "the first by the second for you.\n";
  cin >> number1, number2;
  quotient = static_cast<float>(number1) / number2;
  cout << quotient
  return 0;
}
```

```cpp
30. #include <iostream>
using namespace std;
int main() {
  int number1, number2, product;
  cout << "Enter two numbers and I will multiply\n";
  cout << "them for you.\n";
  cin >> number1 >> number2;
  product = number1 * number2;
  cout << product
  return 0;
}
```

```cpp
31. #include <iostream>
using namespace std;
main() {
    int number1, number2;
    cout << "Enter two numbers and I will multiply\n";
    cout << "them for you.\n";
    cin >> number1 >> number2;
    number1 *= 50;
    number2 *= 50;
    cout << number1 << " " << number2;
    return 0;
}
```

```cpp
32. #include <iostream>
main() {
    double number, half;
    cout << "Enter a number and I will divide\n";
    cout << "it for you.\n";
    cin >> number;
    half = number / 2;
    cout << fixed << setprecision(2) << half;
    return 0;
}
```

```cpp
33. #include <iostream>
using namespace std;
int main() {
    string name;
    cout << "What is your name? ";
    getline(cin, name);
    cout << "Hello " << name << endl;
    return 0;
}
```

```cpp
34. #include <iostream>
using namespace std;
int main() {
    double salary, monthly;
    cout << "What is your annual salary? ";
    cin >> salary;
    monthly = salary / 12;
    cout << fixed << setprecision(2) << monthly << endl;
    return 0;
}
```

```cpp
35. #include <iostream>
using namespace std;
int main() {
    int x, y, z;
    x = 4; y = 5; z = 6;
    x += 2;
    y -= 1;
    z *= 3;
    cout << x << " " << y << " " << z << endl;
    return 0;
}
```

```cpp
36. #include <iostream>
#include <iomanip>
#include <string>
using namespace std;
int main() {
    string userInput;
    cout << "What is your name? ";
    getline(cin, userInput);
    cout << "Hello " << userInput << endl;
    return 0;
}
```

```cpp
37. #include <iostream>
#include <iomanip>
using namespace std;
int main() {
    long seconds;
    double minutes, hours, months, years;
    cout << "Enter the number of seconds that have passed:\n";
    cout << "I will tell you how many minutes, hours,\n";
    cout << "months, and years have passed: ";
    cin >> seconds;
    minutes = seconds / 60.0;
    hours = seconds / 3600.0;
    months = seconds / 2592000.0;
    years = seconds / 31536000.0;
    cout << minutes << " " << hours << " " << months << " " << years << endl;
    return 0;
}
```

### 编程挑战

#### 6. 配料调整器

一份饼干配方需要以下配料：

- 1.5 杯糖
- 1 杯黄油
- 2.75 杯面粉

用这些数量的配料可以制作 48 块饼干。编写一个程序，询问用户想要制作多少块饼干，然后显示制作指定数量饼干所需的每种配料杯数。

#### 7. 票房

电影院只保留门票销售收入的百分比。剩余部分归电影发行商所有。编写一个程序，计算电影院每晚的票房总利润和净利润。程序应询问电影名称，以及售出了多少张成人票和儿童票。（成人票价为 $10.00，儿童票价为 $6.00。）它应该显示一份类似于下面的报告：

电影名称：“狂怒之轮”

成人票销售量：382

儿童票销售量：127

总利润：$ 4,582.00

净利润：$ 916.40

付给发行商的金额：$ 3,665.60

> 注意：假设电影院保留了总票房的 20%。

#### 8. 有多少小部件？

育空组件公司（Yukon Widget Company）制造每个重 12.5 磅的小部件。编写一个程序，根据托盘的总重量计算托盘上堆叠了多少个小部件。程序应询问用户单个部件的重量以及堆叠在托盘上的部件总重量。然后计算并显示托盘上的小部件数量。

#### 9. 有多少卡路里？

一袋饼干含有 30 块饼干。袋上的热量信息声称有 10 “份”，且每一袋等于 300 卡路里。编写一个程序，询问用户实际吃了多少块饼干，然后报告消耗了多少卡路里。

#### 10. 需要多少保险？

许多财务专家建议，房主为其房屋或建筑购买的保险金额至少应达到重建结构成本的 80%。编写一个程序，询问用户输入建筑的重建成本，显示其物业应购买的最低保险金额。

#### 11. 汽车费用

编写一个程序，询问用户输入运营其汽车时产生的以下费用的每月费用：贷款还款、保险、汽油、机油、轮胎、维修。程序随后显示这些费用的每月总费用和年度总费用。

#### 12. 摄氏度转华氏度

编写一个将摄氏度温度转换为华氏度的程序。公式为

```
F = \frac{9}{5}C + 32
```

`F` 是华氏温度，`C` 是摄氏温度。

#### 13. 货币

编写一个程序将美元金额转换为日元和欧元，并将转换因子存储在常量 `YEN_PER_DOLLAR` 和 `EUROS_PER_DOLLAR` 中。为了获取最新的汇率，请在互联网上搜索“汇率”（currency exchange rate）。如果你找不到最新的汇率，请使用以下数值：

- 1 美元 = 98.93 日元
- 1 美元 = 0.74 欧元

以固定点符号格式化你的货币金额，保留两位小数，并确保始终显示小数点。

#### 14. 每月销售税

一家零售公司必须提交一份每月销售税报告，列出当月的销售额和收到的销售额。编写一个程序，询问月份、年份以及收银台收到的总金额（即销售额加销售税）。假设州销售税为 4%，县销售税为 2%。
