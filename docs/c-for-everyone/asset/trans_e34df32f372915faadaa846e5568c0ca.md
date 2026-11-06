

## R10.12 以下程序输出什么？

```cpp
class B
{
public:
    void print(int n) const;
};

void B::print(int n) const
{
    cout << n << endl;
}

class D : public B
{
public:
    void print(int n) const;
};

void D::print(int n) const
{
    if (n <= 1) { B::print(n); }
    else if (n % 2 == 0) { print(n / 2); }
    else { print(3 * n + 1); }
}

int main()
{
    D d;
    d.print(3);
    return 0;
}
```

请手动确定答案，不要通过编译和运行程序来确定。

## R10.13 假设类 D 继承自 B。以下哪些赋值是合法的？

```cpp
B b;
D d;
B* pb;
D* pd;
```

- a. `b = d;`
- b. `d = b;`
- c. `pd = pb;`
- d. `pb = pd;`
- e. `d = pd;`
- f. `b = *pd;`
- g. `*pd = *pb;`

## R10.14 假设类 Sub 派生自类 Sandwich。以下哪些赋值是合法的？

```cpp
Sandwich* x = new Sandwich();
Sub* y = new Sub();
```

- a. `x = y;`
- b. `y = x;`
- c. `y = new Sandwich();`

## 编程练习

- 1. **P10.1** 在第 10.1 节的问题层次结构中添加一个 `NumericQuestion` 类。如果响应与预期答案相差不超过 0.01，则接受该响应为正确答案。

- 2. **P10.2** 在第 10.1 节的问题层次结构中添加一个 `FillInQuestion` 类。这类问题使用一个包含答案的字符串构造，答案由 `__` 包围，例如："The inventor of C++ was __Bjarne Stroustrup__"。问题应显示为：

  The inventor of C++ was ______

  提供一个能够演示该类的主函数。

- 3. **P10.3** 修改 `Question` 类的 `check_answer` 成员函数，使其不考虑不同的空格或大小写字符。例如，响应 "bjarne stroustrup" 应与答案 "Bjarne Stroustrup" 匹配。

- 4. **P10.4** 在第 10.1 节的问题层次结构中添加一个 `MultipleChoiceQuestion` 类，使其允许多个正确选项。答题者应提供任意一个正确选项。答案字符串应包含所有正确选项，并以空格分隔。

- 5. **P10.5** 在第 10.1 节的问题层次结构中添加一个 `ChooseAllCorrect` 类，使其允许多个正确选项。答题者应提供所有正确选项，并以空格分隔。

- 6. **P10.6** 向 `Question` 基类添加一个 `add_text` 成员函数，并提供 `ChoiceQuestion` 的另一种实现，使其调用 `add_text`，而不是存储选项向量。

- 7. **P10.7** 修改《How To 10.1》中的 `CheckingAccount` 类，使其在每月超过三笔免费交易后，对额外的存款或取款收取 1 美元的费用。将费用计算代码放入一个私有成员函数中，并从存款和取款成员函数中调用该函数。

- 8. **P10.8** 从 `Employee` 派生一个 `Programmer` 类。提供一个调用基类构造函数的构造函数 `Programmer(string name, double salary)`。提供一个 `get_name` 函数，以 `"Hacker, Harry (Programmer)"` 的格式返回姓名。

- 9. **P10.9** 实现一个基类 `Person`。从 `Person` 派生 `Student` 和 `Instructor` 类。人员具有姓名和生日。学生具有专业，教师具有薪水。为所有类编写类定义、构造函数以及 `display` 成员函数。

- 10. **P10.10** 从 `Employee` 派生一个 `Manager` 类。添加一个名为 `department`、类型为 `string` 的数据成员。提供一个 `display` 函数，显示经理的姓名、部门和薪水。从 `Manager` 派生一个 `Executive` 类。提供一个 `display` 函数，显示字符串 Executive，随后显示存储在 `Manager` 基类对象中的信息。

- 11. **P10.11** 实现一个基类 `Account` 以及派生类 `Savings` 和 `Checking`。在基类中提供 `deposit` 和 `withdraw` 成员函数。提供一个 `daily_interest` 函数，用于计算并添加每日利息。为便于计算，假设每个月有 30 天。对于余额超过 1,000 美元的部分，支票账户按年利率 3% 计息。储蓄账户按全部余额的年利率 6% 计息。编写一个测试程序，执行一个月内的存款和取款操作，并计算每天的利息。

- **P10.12** 实现一个基类 `Appointment` 以及派生类 `OneTime`、`Daily`、`Weekly` 和 `Monthly`。预约包含描述（例如“看牙医”）以及日期和时间。编写一个虚函数 `occurs_on(int year, int month, int day)`，检查预约是否发生在指定日期。例如，对于每月预约，必须检查月份中的日期是否匹配。然后用各种预约填充一个 `Appointment*` 向量。让用户输入一个日期，并打印出当天发生的所有预约。

- **P10.13** 改进练习 P10.12 中的预约簿程序。允许用户添加新的预约。用户必须指定预约类型、描述以及日期和时间。

- **P10.14** 通过允许用户将预约数据保存到文件并从文件重新加载，改进练习 P10.12 和 P10.13 中的预约簿程序。保存部分比较直接：实现一个虚函数 `save`。保存类型、描述、日期和时间。加载部分并不容易。必须首先确定要加载的预约类型，使用其默认构造函数创建该类型的对象，然后调用虚拟的 `load` 函数来加载其余数据。

- **P10.15** 使用多态性执行练习 P8.10 和 P8.11 中所描述的图像处理操作。设计一个基类 `Effect` 以及派生类 `Sunset` 和 `Grayscale`。使用一个虚函数 `process`。程序中的文件处理部分应反复通过 `Effect*` 指针调用 `process`，而不必知道所应用的是哪种效果。

- **工程题 P10.16** 在本题中，你将对由任意配置的电阻器组成的电路进行建模。提供一个带有 `get_resistance` 成员函数的基类 `Circuit`。提供一个表示单个电阻器的派生类 `Resistor`。提供派生类 `Serial` 和 `Parallel`，它们各自包含一个 `vector<Circuit*>`。串联电路表示一组串联的电路，其中每个电路可以是单个电阻器，也可以是另一个电路。同样，并联电路表示一组并联的电路。例如，下面的电路是一个 `Parallel` 电路，其中包含一个单独的电阻器和一个 `Serial` 电路。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_503_0.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_503_1.png)

使用欧姆定律计算总电阻。

- **工程题 P10.17** 下图的 (a) 部分展示了一个称为*放大器*的电路的符号表示。放大器的输入是电压 *vᵢ*，输出是电压 *vₒ*。放大器的输出与输入成正比。这个比例常数称为放大器的“增益”。

  (b)、(c) 和 (d) 部分展示了三种特定类型放大器的原理图：*反相放大器*、*同相放大器*和*分压放大器*。这三种放大器都由两个电阻器和一个运算放大器组成。每种放大器的增益值取决于其电阻值。具体来说，反相放大器的增益 *g* 为 $g = -\frac{R_2}{R_1}$。类似地，同相放大器和分压放大器的增益分别为 $g = 1 + \frac{R_2}{R_1}$ 和 $g = \frac{R_2}{R_1 + R_2}$。

  ![](img/5e58fb4c840712efd6ed6fa82bb97f57_504_0.png)

  (a) 放大器

  ![](img/5e58fb4c840712efd6ed6fa82bb97f57_504_1.png)

  (b) 反相放大器

  ![](img/5e58fb4c840712efd6ed6fa82bb97f57_504_2.png)

  (c) 同相放大器

  ![](img/5e58fb4c840712efd6ed6fa82bb97f57_504_3.png)

  (d) 分压放大器

  编写一个 C++ 程序，将放大器表示为基类，并将反相放大器、同相放大器和分压放大器表示为派生类。为基类提供两个虚函数：`get_gain`，以及返回用于标识放大器的字符串的 `get_description` 函数。每个派生类都应具有一个带两个参数的构造函数，这两个参数表示放大器的电阻值。

  派生类需要重写基类的 `get_gain` 和 `get_description` 函数。

  为该 C++ 程序编写一个主函数，使用电阻值的示例值演示所有派生类均能正常工作。

## 工程题 P10.18

谐振电路用于从其他相互竞争的信号中选择一个信号（例如某个广播电台或电视频道）。谐振电路的特征由下图所示的频率响应表示。谐振频率响应由三个参数完全描述：谐振频率 $\omega_0$、带宽 $B$ 以及谐振频率处的增益 $k$。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_504_4.png)

频率（弧度/秒，对数刻度）

