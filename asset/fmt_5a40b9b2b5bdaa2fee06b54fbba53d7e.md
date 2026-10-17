
#include <string>

**图 5.8 | `DollarAmount` 类以整数的形式存储美元金额。（部分 I/2）**

## 第5章 控制语句：第 2 部分；逻辑运算符

```cpp
#include <cmath>

class DollarAmount {
public:
// 从 int64_t 值初始化金额
    explicit DollarAmount(int64_t value) : amount{value} {}
    // 将右侧对象的金额加上当前对象的金额
    void add(DollarAmount right) {
        // 访问同类其他对象的私有数据
        amount += right.amount;
    }
    // 从当前对象中减去右侧金额
    void subtract(DollarAmount right) {
        // 访问同类其他对象的私有数据
        amount -= right.amount;
    }
    // 使用整数算术计算利息，
    // 然后将其加上金额
    void addInterest(int rate, int divisor) {
        // 创建代表利息的 DollarAmount
        DollarAmount interest{(amount * rate + divisor) / divisor};
        add(interest); // 将利息加上当前对象的金额
    }
    // 返回 DollarAmount 对象的字符串表示
    std::string toString() const {
        std::string dollars(std::to_string(amount / 100));
        std::string cents(std::to_string(std::abs(amount % 100)));
        return dollars + "." + (cents.size() == 1 ? "0" : "") + cents;
    }
private:
    int64_t amount{0}; // 以分数为单位的金额
};
```

**图 5.8** | `DollarAmount` 类以整数形式存储金额。（2 个部分中的第 2 部分）

### C++11 `int64_t`

我们希望数据成员 `amount` 能够处理从小数字到大美元的值，以便我们的 `DollarAmount` 能够用于许多货币应用。在大多数计算机上，`int` 的值是从 -2,147,483,647 到 2,147,483,647。对于以“分”为单位的金额，这将 `DollarAmount` 限制在约 +2100 万左右——对于货币应用来说太小了，因此我们需要一个更大的范围。

C++11 `long long` 支持的范围为 -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807。这将使得 `DollarAmount` 的值能够达到 ±92 万亿，对于任何已知的货币应用来说可能绰绰有余。

### 5.7 使用类 `DollarAmount` 进行基于整数的货币计算

`long long`（以及 C 语言其他整数类型）的范围在不同平台之间可能不同。为了可移植性，我们倾向于使用在所有平台上相同的类型。为了实现，C++11 引入了整数类型名称，你可以为程序选择合适的数值范围。对于 `DollarAmount`，我们选择了 `int64_t`，它支持精确的 -9,223,372,036,854,778 到 9,223,372,036,854,775。C++11 其他整数类型名称的列表请参见头文件 `<cstdint>`。

### `DollarAmount` 构造函数

为了简单起见，`DollarAmount` 的构造函数（图 5.8，第 9 行）接收一个分数的数值，并使用该类型初始化数据成员。在练习 5.30 中，定义一个接收两个参数（代表美元和分）的 `DollarAmount` 构造函数，使用这些值计算并存储相应的位数范围。（练习 5.30–5.34 与增强和使用类 `DollarAmount` 相关。）

### `DollarAmount` 成员函数 `add` 和 `subtract`

`add` 函数（第 12–15 行）接收另一个 `DollarAmount` 作为参数，并将其值加到调用该函数的 `DollarAmount` 对象上。第 14 行使用 `+=` 运算符将右侧金额（即参数对象中的金额）加到当前对象的 `amount`，并对其进行修改。这是同类对象之间的一种特殊关系——类的成员函数可以访问传递给该函数的同类对象的私有数据。`subtract` 函数（第 18–21 行）的工作原理与 `add` 类似，但它使用 `-=` 运算符从当前对象的 `amount` 中减去右侧金额。

### `DollarAmount` 成员函数 `addInterest`

`addInterest` 成员函数（第 25–32 行）使用其 `rate` 和 `divisor` 参数进行利息计算，并将利息加上金额。利息计算通常会产生需要舍入的碎数。我们只进行整数计算以避免 `double` 的表示误差，正如你所看到的，仍然需要舍入。

在此示例中，使用四舍五入将 0.75 和 0.2 舍入到最近的整数。使用四舍五入，.5 及以上应进入，其他所有值应舍入；0.75 进入到 1，0.2 舍入到 0。

现在，让我们考虑利息计算的结果。假设我们正在为 $10.75 计算 5% 的利息。在整数算术中，我们将 10.75 视为 1075，计算 5% 时乘以 5，然后除以 100。我们先将 1075 乘以 5，得到整数值 5375，这代表 53 分和 75 百分之一分。在这种情况下，75 百分之一分应该进入到一整分，结果为 54 分。更通地说：

- 50 到 99 百分之一分应该进入到下一个更高的分
- 1 到 49 百分之一分应该舍入到下一个更低的分

如果我们将 5375 除以 100 来完成利息计算，结果是 53，这是错误的——记住整数算术会截断计算的小数部分。为了修复这个问题，我们必须给 5375 加上一个值，以便除以 100 后得到 54 分。50 让我们能够确保 50 到 99 百分之一分进入。例如：

- 5350 + 50 得到 5400——除以 100 得到 54
- 5375 + 50 得到 5425——除以 100 得到 54
- 5399 + 50 得到 5449——除以 100 得到 54

类似地：

- 5301 + 50 得到 5351——除以 100 得到 53
- 5325 + 50 得到 5375——除以 100 得到 53
- 5349 + 50 得到 5399——除以 100 得到 54

### `do...while` 循环语句

`do...while` 循环语句与 `while` 语句相似。在 `while` 中，程序在循环开始时、执行循环体之前测试循环条件；如果条件为假，则循环体永不执行。`do...while` 语句在执行执行循环体后测试循环条件；因此，循环体至少执行一次。当 `do...while` 语句终止时，执行将继续到下一条语句。图 5.9 使用 `do...while` 输出数字 1–10。

```cpp
// Fig. 5.9: DohwhileTest.cpp
// do...while 循环语句。
#include <iostream>
using namespace std;
int main() {
    unsigned counter{1};
    do {
        cout << counter << " ";
        counter++;
    } while (counter <= 10); // 结束 do...while
}
```

**图 5.9** | `do...while` 循环语句。（第 2 部分。）

### 银行舍入法 (Banker’s Rounding)

四舍五入是有偏的的-.1, .2, .3 和 .4 舍入，而 .5, .6, .7 和 .8 进入。因为进入的情况多于舍入，这会导致货币计算中的差异。银行舍入法通过将 .5 舍入到偶整数来解决这个问题。

### 即使 `int64_t` 有限的

尽管 `DollarAmount` 可以表示很大的值，但 `int64_t` 支持的值范围仍然是的。通过 C++ 的类机制，你会发现你可以定义名为 `BigInteger` 或 `HugeInteger` 的类（如在练习 10.9 中所示），它可以存储并处理任意大小的整数。

### 关于算术运算符和修改操作数的说明

第14和20行在执行算术计算时会修改 `DollarAmount`。这与运算符处理基本类型的方式不同。例如，表达式 `value1+value2` 将两个值相加产生临时结果，但 `+` 运算符不会修改其左左右操作数。在第 10 章，我们将演示 C++ 的运算符重载功能，它允许你为自己的用户类型定义运算符。

## 第 5 章控制语句：部分 2；逻辑运算符

```cpp
13
14	cout << endl;
15	}
 1 2 3 4 5 6 7 8 9 10
```

第 7 行清空并初始化控制变量计数器。进入 `do...while` 语句后，第 10 行输出计数器的值并增加计数器。然后程序评估该行底部的循环继续测试（第 12 行）。如果条件为真，循环在第一个体语句（第 11 行）中继续。如果条件为假，循环终止，程序从循环后的下一个语句继续。

**`do...while` 迭代语句的 UML 活动图**

图 5.10 包含了 `do...while` 语句的 UML 活动图。该图清楚地表明，循环继续条件在循环执行了*至少一次*操作*之后* 才会进行评估。将此活动图与 `while` 语句的图（图 4.8）进行比较。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_220_0.png)

**图 5.10** | `do..while` 迭代语句 UML 活动图。

### 5.9 `switch` 多路选择语句

C++ 提供了 `switch` 多选择语句，根据变量或表达式的可能值在多个不同的动作之间进行选择。每个动作与一个整数常量（即常量值）相关联。

#### 使用 `switch` 统计 A、B、D 和 F 级

图 5.11 计算用户输入的一组数字成绩的平均值，使用 `switch` 语句判断成绩是否等同于 A、B、D 或 F，并增加相应的计数器。

```cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    unsigned int total{0}; // 成绩总和
    unsigned int gradeCounter{0}; // 成绩数量
    unsigned int aCount{0}; // A 的计数
    unsigned int bCount{0}; // B 的计数
    unsigned int cCount{0}; // C 的计数
    unsigned int dCount{0}; // D 的计数
    unsigned int fCount{0}; // F 的计数
    int grade;
    cout << "Enter the integer grades in the range 0-100" << endl;
    cout << "Type the end-of-file character to terminate input:" << endl;
    cout << "On Unix/Linux/Mac type <Ctrl> d then press Enter"
    cout << "On Windows type <Ctrl> z then press Enter" << endl;
    // 循环直到用户输入文件结束指示
    while (cin >> grade) {
        total += grade; // 将成绩加入总和
        gradeCounter++; // 增加成绩数量
        // 增加字母等级计数器
        switch (grade / 10) {
            case 9: // 成绩在 90 之间
            case 10: // 且 100，包含在内
                aCount++;
                break; // 退出 switch
            case 8: // 成绩在 80 到 89 之间
                bCount++;
                break; // 退出 switch
            case 7: // 成绩在 70 到 79 之间
                cCount++;
                break; // 退出 switch
            case 6: // 成绩在 60 到 69 之间
                dCount++;
                break; // 退出 switch
            default: // 成绩小于 60
                fCount++;
                break; // 可选；强制退出 switch
        } // 结束 switch
    } // 结束 while
    // 设置浮点数格式
    cout << fixed << precision(2);
    // 显示成绩报告
    cout << "\nGrade Report:" << endl;
    // 如果用户至少输入了一个成绩
    if (gradeCounter != 0) {
        // 计算所有输入成绩的平均值
        double average = static_cast<double>(total) / gradeCounter;
        // 输出结果摘要
        cout << "Total of the " << gradeCounter << " grades entered is " << total;
        cout << "\nClass average is " << average;
        cout << "\nNumber of students who received each grade:";
        cout << "\nA: " << aCount << "\nB: " << bCount << "\nC: " << cCount;
        cout << "\nD: " << dCount << "\nF: " << fCount << endl;
    }
    else { // 未输入成绩，输出相应消息
```
