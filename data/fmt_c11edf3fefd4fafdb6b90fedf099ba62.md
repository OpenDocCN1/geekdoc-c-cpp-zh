
# 编程挑战

## 7. CustomerData 类

为这些成员变量编写相应的访问和修改函数。

接下来，设计一个名为 `CustomerData` 的类，它派生自 `PersonData` 类。`CustomerData` 类应该拥有以下成员变量：

- 客户编号（`customerNumber`）
- 邮件列表（`mailingList`）

`customerNumber` 变量将用于存储每个客户唯一的整数。`mailingList` 变量应为布尔值。如果客户希望加入邮件列表，则设为真；如果不想则设为假。为这些成员变量编写相应的访问和修改函数。通过一个简单的程序演示 `CustomerData` 对象。

## 8. PreferredCustomer 类

一家零售店拥有一种优选客户计划，客户在购买时可以获得折扣。客户的折扣金额取决于其在商店内的累计购买金额。

- 当优选客户消费达到 $500 时，他或她在未来的所有购买中将获得 5% 的折扣。
- 当优选客户消费达到 $1,000 时，他或她在未来的所有购买中将获得 6% 的折扣。
- 当优选客户消费达到 $1,500 时，他或她在未来的所有购买中将获得 7% 的折扣。
- 当优选客户消费达到 $2,000 或更多时，他或她在未来的所有购买中将获得 10% 的折扣。

设计一个名为 `PreferredCustomer` 类，派自你在编程挑战 7 中创建的 `CustomerData` 类。`PreferredCustomer` 类应具有以下成员变量：

- `purchasesAmount` (double)
- `discountLevel` (double)

`purchasesAmount` 变量存储客户截至为止的购买总额。`discountLevel` 变量应根据商店的优选客户计划设置为正确的折扣百分比。为该类编写适当的成员函数并在简单程序中演示。

输入验证：不要接受任何销售数字的负值。

## 9. 文件过滤器 (File Filter)

文件过滤器读取输入文件，对其进行某种转换，并将结果写入输出文件。创建一个抽象文件类，定义一个用于转换字符的纯虚函数。为你的文件过滤器类创建一个派生类：一个执行加密，另一个将文件转换为全大写，再加一个创建原始文件的未修改副本。该类应具有以下成员函数：

```cpp
void doFilter(istream &in, ofstream &out)
```

调用此函数以执行实际的过滤。转换单个字符的成员函数原型应为：

```cpp
char transform(char ch)
```

加密类应具有一个构造函数，接受一个整数作为参数并将其作为加密密钥。

## 10. 文件双倍行距 (File Double-Spacer)

为编程挑战 9（文件过滤器）中的抽象文件类创建一个派生类，对文件进行双倍行距，即在文件的任意两行之间插入一个空行。

## 11. 课程成绩 (Course Grades)

在一门课程中，老师给出了以下测试和作业：

- 实验活动由老师观察并分配数字分数。
- 一场包含十道题的通过/不通过考试。最低及格分数为 70。
- 一篇分配数字分数的论文。
- 期末考试有 50 道题。

### 编程挑战 985

编写一个名为 `CourseGrades` 的类。该类应有一个名为 `grades` 的成员，它是一个 `GradedActivity` 指针数组。`grades` 数组应有四个元素，对应之前描述的每个作业。该类应具有以下成员函数：

- `setLab`：此函数接受一个 `GradedActivity` 对象的地址作为参数。该对象应该已经包含了学生实验活动的分数。`grades` 数组的元素 0 应该引用此对象。
- `setPassFailExam`：此函数接受一个 `PassFailExam` 对象的地址作为参数。该对象应该已经包含了通过/不通过考试的分数。`grades` 数组的元素 1 应该引用此对象。
- `setEssay`：此函数接受一个 `Essay` 对象的地址作为参数。（参见编程挑战 6 中的 `Essay` 类。如果你没有完成编程挑战 6，则使用 `GradedActivity` 对象。）该对象应该已经包含了学生的分数。`grades` 数组的元素 2 应该引用此对象。
- `setFinalExam`：此函数接受一个 `FinalExam` 对象的地址作为参数。该对象应该已经包含了期末考试的分数。`grades` 数组的元素 3 应该引用此对象。
- `print`：此函数应显示 `grades` 数组中每个元素的数字分数和等级。

在程序中演示该类。

## 12. 船 (Ship)、邮轮 (CruiseShip) 和 货船 (CargoShip) 类

设计一个 `Ship` 类，具有以下成员：

- 船的名称（string）
- 建造年份（string）
- 适当的构造函数、访问函数和修改函数

设计一个 `CruiseShip` 类派自 `Ship`，具有以下成员：

- 最大乘客人数（int）
- 适当的构造函数、访问函数和修改函数
- 覆盖基类的打印函数

设计一个 `CargoShip` 类派自 `Ship`，具有以下成员：

- 吨位（int）
- 适当的构造函数、访问函数和修改函数
- 覆盖基类的打印函数

在程序中演示这些类。

## 15. 继承、多态和虚函数

在程序中演示这些类，程序有一个 `Ship` 指针数组。数组应使用动态分配的 `CruiseShip` 和 `CargoShip` 对象初始化。遍历数组并调用每个对象的打印函数。

## 13. 抽象类 (Abstract Class)

定义一个名为 `BasicShape` 的纯抽象类。该类应具有以下成员：

私有变量：

- `area` (double)

公共函数：

- `getArea`：返回面积的值
- `calcArea`：一个纯虚函数

接下来，定义一个名为 `Circle` 的类派自 `BasicShape`。它应具有以下成员：

私有变量：

- `centerX` (long)
- `centerY` (long)
- `radius` (double)

公共函数：

- 构造函数：接受 `centerX`、`centerY` 和 `radius`。应调用 `calcArea`。
- `getCenterX`：返回 `centerX` 的值
- `getCenterY`：返回 `centerY` 的值
- `calcArea`：计算面积（3.14159 * `radius` * `radius`）并将结果存储在 `area` 中

接下来，定义一个名为 `Rectangle` 的类派自 `BasicShape`。它应具有以下成员：

私有变量：

- `width` (long)
- `length` (long)

公共函数：

- 构造函数：接受 `width` 和 `length`。应调用 `calcArea`。
- `getWidth`：返回 `width` 的值
- `getLength`：返回 `length` 的值
- `calcArea`：计算面积（`length` * `width`）并将结果存储在 `area` 中

创建这些类后，创建一个驱动程序定义一个 `Circle` 对象和一个 `Rectangle` 对象。证明每个对象都能正确计算并报告其面积。

## 14. 银行账户 (Bank Accounts)

此程序应由学生小组设计并编写。以下建议：

- 一个或多个学生可以负责一个类。
- 应分析程序需求，以便给每个学生分配相似的工作量。
- 应预先确定每个函数和类成员函数的参数和返回类型。
- 程序最好以多文件形式实现。

设计一个通用类来存储银行账户的信息：

- 余额
- 本月存款次数
- 本月取款次数
- 年利率
- 月费

该类应具有以下成员函数：

- 构造函数：接受余额和年利率。
- `deposit`：一个虚函数，接受存款金额作为参数。该函数应将金额加入账户余额。它还应增加存款计数器。
- `withdraw`：一个虚函数，接受取款金额作为参数。该函数应从余额中减去金额。它还应增加取款计数器。
- `calcInt`：一个虚函数，通过计算账户赚取的利息并更新余额。这通过以下公式执行：

  Monthly Interest Rate = (Annual Interest Rate / 12)

  Monthly Interest = Balance * Monthly Interest Rate

  Balance = Balance + Monthly Interest

- `monthlyProc`：一个虚函数，从余额中减去月费，调用 `calcInt` 函数，然后将取款次数、存款次数和月费变量置零。

如果储蓄账户的余额低于 $25，它将变为非激活状态。（状态成员可以是一个标志位变量）。在余额升至 $25 以上之前，无法进行取款，此时账户将重新变为激活状态。储蓄账户类应具有以下成员函数：

- `withdraw`：在执行取款前检查账户是否处于非激活状态。（如果账户未激活，则不允许取款。）然后通过调用基类的函数版本执行取款。
- `deposit`：在执行存款前检查账户是否处于非激活状态。如果账户是非激活状态且存款使余额超过 $25，则账户将重新变为激活状态。然后通过调用基类的函数版本执行存款。
- `monthlyProc`：在调用基类函数之前，此函数检查取款次数。如果当月的取款次数超过 4 次，则每个超过 4 次的取款将产生 $1 的服务费，并添加到存储每月服务费的基类变量中。（不要忘记在扣除服务费后检查账户余额。如果余额低于 $25，账户将变为非激活状态。）

接下来，设计一个支票账户类，它也派自通用账户类。它应该具有以下成员函数：

- `withdraw`：在调用基类函数之前，此函数将确定取款（开具支票）是否会导致余额低于 $0。如果余额低于 $0，则将从账户中扣除 $15 的服务费。（将不会执行取款。）如果账户没有足够的资金支付服务费，余额将变为负数，客户将向银行欠该负金额。
- `monthlyProc`：在调用基类函数之前，此函数将每笔取款（开具支票）的 $5 或 $10 费用添加到存储每月服务费的基类变量中。

编写一个完整的程序来演示这些类，要求用户输入储蓄账户和支票账户的存款和取款金额。程序将显示该月的统计信息，包括期初余额、存款总额、服务费和期末余额。

> 注意：你可能需要为上述类添加更多的成员变量和函数。

# 16 异常与模板

## 主题

- 16.1 异常
- 16.2 函数模板
- 16.3 侧重软件工程：定义模板时从何处开始
- 16.4 类模板

## 16.1 异常

> 概念：异常用于信号程序运行过程中发生的错误或意外事件。

错误测试通常是一个直接的过程，涉及 `if` 语句或其他控制机制。例如，以下代码段将在除以零的错误发生前捕获它：

```cpp
if (denominator == 0)
    cout << "ERROR: Cannot divide by zero.\n";
else
    quotient = numerator / denominator;
```

但如果类似的代码是返回商的函数的一部分呢，如下例所示：

```cpp
// 一个不可靠的除法函数
double divide(int numerator, int denominator)
{
    if (denominator == 0)
    {
        cout << "ERROR: Cannot divide by zero.\n";
        return 0;
    }
    else
        return static_cast<double>(numerator) / denominator;
}
```

函数通常通过返回一个预定的值来信号错误条件。示例中的函数在尝试除以零时返回 0。然而，这是不可靠的，因为 0 是除法运算的有效结果。尽管函数显示了错误信息，调用该函数的程序部分并不知道错误何时发生。此类问题需要高级的错误处理技术。

### 抛出异常

处理复杂错误条件的一种方法是使用*异常*。异常是一个信号错误的值或对象。当错误发生时，异常就会被“抛出”。例如，`divide` 代码显示了 `divide` 函数，它被修改为尝试除以零时抛出异常：

```cpp
double divide(int numerator, int denominator)
{
    if (denominator == 0)
        throw "ERROR: Cannot divide by zero.\n";
    else
        return static_cast<double>(numerator) / denominator;
}
```

以下语句会导致异常的抛出：

```cpp
throw "ERROR: Cannot divide by zero.\n"
```

关键字后面跟着一个参数，该参数可以是任何值。正如你将看到的，参数的值被用于确定错误的性质。上面的函数简单地抛出一个包含错误信息的字符串。

包含 `throw` 语句的行被称为*抛出点*（throw point）。当执行 `throw` 语句时，控制权将传递给程序的另一个部分，称为*异常处理器*（exception handler）。当函数抛出异常时，该函数会终止。

### 处理异常

为了处理异常，程序必须有一个*try/catch* 构造。`try/catch` 构造的通用格式为：

```cpp
try
{
    // 此处调用函数或对象成员
    // 可能会抛出异常的函数
}
catch(ExceptionParameter)
{
    // 此处处理异常
    // 根据需要重复多个 catch 块
}
```

构造的第一部分是*try 块*（try block）。它以关键字 `try` 开始，后面跟着一个代码块，该块执行任何可能直接或间接导致抛出异常的语句。`catch` 块以关键字 `catch` 开始，后面跟着一组包含异常参数定义的括号。例如，这里有一个可以与 `divide` 函数使用的 `try/catch` 构造：

```cpp
try {
  quotient = divide(num1, num2);
  cout << "The quotient is " << quotient << endl;
} catch (string exceptionString) {
  cout << exceptionString;
}
```

如果 `divide` 函数抛出一个值为字符串的异常，`catch` 块将捕获该错误信息并显示它。让我们看看整个程序，看看 `throw` 和 `catch` 是如何工作的。在程序 16-1 的首次运行中，给出有效数据。

```cpp
// 此程序演示了异常的抛出和捕获
#include <iostream>
#include <string>
using namespace std;

// 函数原型
double divide(int, int);

int main() {
  int num1, num2; // 用于存储数字
  double quotient; // 用于存储商

  // 获取两个数字
  cout << "Enter two numbers: ";
  cin >> num1 >> num2;

  // 将 num1 除以 num2 并捕获任何可能的异常
  try {
    quotient = divide(num1, num2);
    cout << "The quotient is " << quotient << endl;
  } catch (string exceptionString) {
    cout << exceptionString;
  }

  cout << "End of the program.\n";
  return 0;
}

// divide 函数将分子除以分母。如果分母为
// 0，函数将抛出异常。
double divide(int numerator, int denominator) {
  if (denominator == 0) {
    string exceptionString = "ERROR: Cannot divide by zero.\n";
    throw exceptionString;
  }
  return static_cast<double>(numerator) / denominator;
}
```

（继续）

### 示例输入的程序输出

Enter two numbers: 12 2

The quotient is 6

End of the program.

### 不同示例输入的程序输出

Enter two numbers: 12 0

ERROR: Cannot divide by zero.

End of the program.

> 从第二个输出屏幕可以看到，异常导致程序跳出 `divide` 函数并进入 `catch` 块。在 `catch` 块完成后，程序从 `try/catch` 构造后的第一个语句继续执行。如图 16-1 所示。

### 图 16-1 try/catch 构造的工作原理

| 如果此语句抛出异常... | try { |
| :--- | :--- |
| `quotient = divide(num1, num2);` | |
| `cout << "The quotient is " << quotient << endl;` | |
| ...那么这条语句将被跳过。 | `catch (string exceptionString) {` |
| | `cout << exceptionString;` |
| 如果异常是字符串，程序将跳转到此 catch 子句。 | `}` |
| 在 catch 块完成后，程序从此处继续执行。 | `cout << "End of the program.\n"` |
| | `return 0;` |

### 图 16-2 未抛出异常

在第一个输出屏幕中，用户输入非负值。`try` 块中没有抛出异常，因此程序跳过了 `catch` 块，跳转到 `try/catch` 结构之后的后续语句，即第 30 行。这如图 16-2 所示。
