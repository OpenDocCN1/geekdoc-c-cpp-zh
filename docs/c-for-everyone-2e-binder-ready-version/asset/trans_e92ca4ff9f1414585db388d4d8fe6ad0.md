

**R10.12** 以下程序输出什么？

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

**R10.13** 假设类 `D` 继承自 `B`。以下哪些赋值是合法的？

```cpp
B b;
D d;
B* pb;
D* pd;
```

- **a.** `b = d;`
- **b.** `d = b;`
- **c.** `pd = pb;`
- **d.** `pb = pd;`
- **e.** `d = pd;`
- **f.** `b = *pd;`
- **g.** `*pd = *pb;`

**R10.14** 假设类 `Sub` 派生自类 `Sandwich`。以下哪些赋值是合法的？

```cpp
Sandwich* x = new Sandwich();
Sub* y = new Sub();
```

- **a.** `x = y;`
- **b.** `y = x;`
- **c.** `y = new Sandwich();`
- **d.** `x = new Sub();`
- **e.** `*x = *y;`
- **f.** `*y = *x;`

**R10.15** 程序输出什么？通过跟踪每次调用的流程来解释你的答案。

```cpp
class B
{
public:
   B();
   virtual void p() const;
   void q() const;
};

B::B() {}
void B::p() const { cout << "B::p\n"; }
void B::q() const { cout << "B::q\n"; }

class D : public B
{
public:
   D();
   virtual void p() const;
   void q() const;
};

D::D() {}
void D::p() const { cout << "D::p\n"; }
void D::q() const { cout << "D::q\n"; }

int main()
{
   B b;
   D d;
   B* pb = new B;
   B* pd = new D;
   D* pd2 = new D;

   b.p(); b.q();
   d.p(); d.q();
   pb->p(); pb->q();
   pd->p(); pd->q();
   pd2->p(); pd2->q();
   return 0;
}
```

**R10.16** 使用习题示例 10.1 中的 `Employee` 类（配套代码中的 `ch10/salaries.cpp`），从 `Employee` 创建一个子类 `Volunteer`，并提供构造函数 `Volunteer(string name)`，使其将工资设置为 0。

**R10.17** 在“如何做 10.1”的 `accounts.cpp` 程序中，将 `get_balance` 函数声明为虚函数是否合理？请解释你的理由。

**R10.18** 仅在 `ChoiceQuestion` 类中将 `display` 成员函数声明为虚函数，会产生什么效果？

## 编程练习

- **P10.1** 在第 10.1 节的问题层次结构中添加一个 `NumericQuestion` 类。如果回答与预期答案的差异不超过 0.01，则接受该回答为正确。

- **P10.2** 在第 10.1 节的问题层次结构中添加一个 `FillInQuestion` 类。这种问题使用一个包含答案的字符串构造，答案由 `_ _` 包围，例如：“C++ 的发明者是 `_Bjarne Stroustrup_`”。问题应显示为

  ```
  The inventor of C++ was ____
  ```

  提供一个 `main` 函数演示你的类。

- **P10.3** 修改 `Question` 类的 `check_answer` 成员函数，使其不考虑不同的空格或大小写字符。例如，回答 `" bjarne stroustrup"` 应与答案 `"Bjarne Stroustrup"` 匹配。

- **P10.4** 在第 10.1 节的问题层次结构中添加一个 `MultipleChoiceQuestion` 类，使其支持多个正确选项。答题者只需提供任意一个正确选项。答案字符串应包含所有正确选项，并用空格分隔。

- **P10.5** 在第 10.1 节的问题层次结构中添加一个 `ChooseAllCorrect` 类，使其支持多个正确选项。答题者必须提供所有正确选项，并用空格分隔。

- **P10.6** 向 `Question` 基类添加一个 `add_text` 成员函数，并提供 `ChoiceQuestion` 的另一种实现，使其调用 `add_text`，而不是存储一个选项向量。

- **P10.7** 修改“如何做 10.1”中的 `CheckingAccount` 类，使其在每月超过三笔免费交易后，对存款或取款收取 1 美元的费用。将费用计算代码放入一个私有成员函数中，并从 `deposit` 和 `withdraw` 成员函数中调用它。

- **P10.8** 从 `Employee` 派生一个 `Programmer` 类。提供构造函数 `Programmer(string name, double salary)`，该构造函数调用基类构造函数。提供一个 `get_name` 函数，以 `"Hacker, Harry (Programmer)"` 的格式返回姓名。

- **P10.9** 实现一个基类 `Person`。从 `Person` 派生 `Student` 和 `Instructor` 类。人员具有姓名和生日。学生具有专业，教师具有工资。为所有类编写类定义、构造函数和 `display` 成员函数。

- **P10.10** 从 `Employee` 派生一个 `Manager` 类。添加一个名为 `department`、类型为 `string` 的数据成员。提供一个 `display` 函数，用于显示经理的姓名、部门和工资。从 `Manager` 派生一个 `Executive` 类。提供一个 `display` 函数，显示字符串 `Executive`，后面跟随存储在 `Manager` 基类对象中的信息。

- **P10.11** 实现一个基类 `Account` 和派生类 `Savings`、`Checking`。在基类中提供成员函数 `deposit` 和 `withdraw`。提供一个 `daily_interest` 函数，用于计算并添加每日利息。计算时假设每个月有 30 天。余额超过 1,000 美元的支票账户按年利率 3% 计息。储蓄账户按整个余额的年利率 6% 计息。编写一个测试程序，进行一个月的存款和取款，并计算每天的利息。

- **P10.12** 实现一个基类 `Appointment` 和派生类 `Onetime`、`Daily`、`Weekly`、`Monthly`。预约包含描述（例如“看牙医”）以及日期和时间。编写一个虚函数 `occurs_on(int year, int month, int day)`，用于检查预约是否发生在指定日期。例如，对于每月预约，必须检查月份中的日期是否匹配。然后用各种预约填充一个 `vector<Appointment*>`。让用户输入一个日期，并打印出当天发生的所有预约。

- **P10.13** 改进练习 P10.12 中的预约簿程序。让用户可以选择添加新的预约。用户必须指定预约类型、描述以及日期和时间。

- **P10.14** 通过让用户能够将预约数据保存到文件并从文件重新加载，改进练习 P10.12 和 P10.13 中的预约簿程序。保存部分比较直接：编写一个虚函数 `save`，保存类型、描述、日期和时间。加载部分则不太容易。必须首先确定要加载的预约类型，使用该类型的默认构造函数创建一个对象，然后调用虚函数 `load` 来加载其余数据。

- **P10.15** 使用多态来执行练习 P8.10 和 P8.11 中描述的图像处理。设计一个基类 `Effect` 以及派生类 `Sunset` 和 `Grayscale`。使用一个虚函数 `process`。程序的文件处理部分应反复通过 `Effect*` 指针调用 `process`，而无需知道应用的是哪种效果。

- **工程 P10.16** 在本题中，你将对由任意配置的电阻器组成的电路进行建模。提供一个带有成员函数 `get_resistance` 的基类 `Circuit`。提供一个表示单个电阻器的派生类 `Resistor`。提供派生类 `Serial` 和 `Parallel`，每个类都包含一个 `vector<Circuit*>`。串联电路表示一组串联的电路，其中每个电路可以是单个电阻器，也可以是另一个电路。同样，并联电路表示一组并联的电路。例如，下面的电路是一个 `Parallel` 电路，其中包含一个单独的电阻器和一个 `Serial` 电路。

  ![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_503_0.png)

  ![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_503_1.png)

  使用欧姆定律计算组合电阻。

- **工程 P10.17** 下图的（a）部分展示了一个称为放大器的电路的符号表示。放大器的输入是电压 vi，输出是电压 vo。放大器的输出与输入成正比。这个比例常数称为放大器的“增益”。

  图中的（b）、（c）和（d）部分展示了三种特定类型放大器的原理图：反相放大器、同相放大器和分压放大器。这三种放大器均由两个电阻器和一个运算放大器组成。每种放大器的增益值取决于其电阻值。具体而言，增益 g 为

