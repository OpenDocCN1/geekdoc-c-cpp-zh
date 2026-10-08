
因此，以下三行程序代码将在屏幕上输出 9.0，$(3.0)^{2.0}$ 等于 9.0：

```
double result, x = 3.0, y = 2.0;
result = pow(x, y);
cout << result;
```

注意上述调用返回的是 9.0 而不是 9。该函数始终返回 `double` 类型的值，而不是 `int` 类型。还请注意该函数需要两个参数。函数可以有任意数量的参数。此外，每个参数位置都有指定的类型，在函数调用中使用的参数应该应该是该类型。在很多情况下，如果你使用了类型错误的参数，C++ 会为你完成一些自动类型转换。然而，结果可能不是你预期的那样。当你调用函数时，应该使用为该函数指定类型的参数。一个例外是参数到 `double` 的自动转换。在许多情况下，当指定 `double` 类型参数时，你也可以使用 `int` 类型参数。

### 参数具有类型

`pow` 的许多实现对使用的参数有限制。在这些实现中，如果第一个参数是负数，那么第二个参数必须是一个数字。由于你在学习编程可能已经有足够的事情需要担心，当第一个参数非负时使用 `pow` 可能是最简单安全的方法。

### pow 的限制

## 随机数生成

游戏和模拟程序通常需要生成随机数。C++ 有预定义函数来生成伪随机数。伪随机数看起来随机，但实际上是由可预测的公式决定的。例如，这是一个简单的伪随机生成器的公式，它通过之前生成的随机数 $R_{i-1}$ 来指定第 $i$ 个随机数 $R_i$：

```
R_i = (R_{i-1} \times 7) \% 11
```

让我们初始化“种子”，$R_0 = 1$。第一次获取“随机”数时，我们计算 $R_1$：

```
R_1 = (R_0 \times 7) \% 11 = (1 \times 7) \% 11 = 7 \% 11 = 7
```

第二次获取“随机”数时，我们计算 $R_2$：

```
R_2 = (R_1 \times 7) \% 11 = (7 \times 7) \% 11 = 49 \% 11 = 5
```

第三次获取“随机”数时，我们计算 $R_3$：

```
R_3 = (R_2 \times 7) \% 11 = (5 \times 7) \% 11 = 35 \% 11 = 2
```

以此类推。

![](img/67be1289808bc3852827f7f3e329d82_217_0.png)

## 4.2 预定义函数

`int` 类型的常量不会为你提供任何额外的能力。当你想要将 `9` 转换为 `double` 类型的值时，可以使用 `9.0` 代替 `static_cast<double>(9)`。然而，如果除法只涉及变量，那么类型转换可能是你唯一的关键属性。通过类型转换，我们可以重写之前的示例，使得变量 `candyPerPerson` 接收正确的值 `4.5` 而不是 `4.0`；为了实现这一点，我们唯一的更改是替换 `static_cast<double>(totalCandy)`，如下所示：

```cpp
int totalCandy, numberOfPeople;
double candyPerPerson;
// 程序显示 totalCandy 的值为 9
// numberOfPeople 的值为 2。
// 程序如何执行的并不重要。
candyPerPerson = static_cast<double>(totalCandy)/numberOfPeople;
```

注意代码中类型转换部分括号的位置。你希望在除法之前进行类型转换，这样除法操作就是针对 `double` 类型的值运行的。如果你等到除法完成后再进行，小数点后的数字已经丢失了。如果你在上段代码的最后一行使用以下代码，那么 `candyPerPerson` 的值是 `4.0` 而不是 `4.5`。

```cpp
candyPerPerson = static_cast<double>(totalCandy)/numberOfPeople); // 错误！
```

### 从 int 转换为 double 的函数

`static_cast<double>` 符号可以作为预定义函数使用，并将某些其他类型的值转换为 `double` 类型的值。例如，`static_cast<double>(2)` 返回 `2.0`。这被称为强制转换。（类型转换可以用 `double` 以外的类型进行，但在本书的后续章节之前，我们将仅对 `double` 类型进行类型转换。）

语法

```cpp
static_cast<double>(Expression_of_Type_int)
```

示例

```cpp
int totalPot, numberOfOfWinners;
double yourWinnings;
yourWinnings = static_cast<double>(totalPot)/numberOfWinners;
```

## 转换的类型转换形式

如上一节所述，使用 `static_cast<double>` 是执行类型转换的首选方法。然而，旧版本的 C++ 使用了不同的表示法进行类型转换。如果它是一个函数名，那么 `double(9)` 返回 `9.0`。因此，如果 `candyPerson` 是一个 `double` 类型变量，且 `totalCandy` 和 `numberOfPeople` 都是 `int` 类型变量，那么以下两个赋值语句为：

```cpp
candyPerson = static_cast<double>(totalCandy)/numberOfPeople;
```

和

```cpp
candyPerson = double(totalCandy)/numberOfPeople;
```

虽然 `static_cast<double>(totalCandy)` 和 `double(totalCandy)` 几乎相等，但你应该使用 `static_cast<double>` 形式，因为 `double(totalCandy)` 形式在 C++ 的后续版本可能会被弃用。

## 陷阱 整数除法丢失小数部分

在除法中，计算 `11/2` 时，很容易忘记 `11/2` 的结果是 `5` 而不是 `5.5`。结果是下一个较小的整数。例如：

```cpp
double d;
d = 11/2;
```

在这里，除法是通过整数除法完成的；除法结果为 `5`，然后转换为 `double` 并赋值给 `d`。并没有产生小数部分。注意，`d` 是 `double` 类型这一事实并没有改变除法结果。变量 `d` 接收到 `5.0` 而不是 `5.5`。

## 自测练习

+ 1. 确定每个算术表达式的值：

| sqrt(16.0) | sqrt(16) | pow(2.0, 3.0) |

| :--- | :--- | :--- |

| pow(2, 3) | pow(2.0, 3.0) | pow(1.1, 2) |

| abs(3) | abs(-3) | abs(0) |

| fabs(-3.0) | fabs(-3.5) | fabs(3.5) |

| ceil(5.1) | ceil(5.8) | floor(5.1) |

| floor(5.8) | pow(3.0, 2)/2 | pow(3.0, 2)/2 |

| 7/(-2) | | |

+ 2. 将每个数学表达式转换为：

- $\sqrt{x+y}$

- $\sqrt{x-y}$

- $\sqrt{x/y}$

- $\sqrt{y/x}$

- $\sqrt{x^2+y^2}$

- $\sqrt{x^2-y^2}$

- $\sqrt{(x+y)^2}$

- $\sqrt{(x-y)^2}$

+ 3. 确定你的编译器是否允许以下操作：

- `candyPerson = static_cast<double>(totalCandy)/numberOfPeople;`

- `candyPerson = double(totalCandy)/numberOfPeople;`

+ 4. 编写一个程序演示以下内容：

- 接收两个整数并返回和的函数

- 接收一个 double 并返回其平方的函数

- 接收三个整数并返回其乘积的函数

- 接收一个字符串并返回其长度的函数

+ 5. 定义以下函数：

- 接收两个整数并返回和的函数

- 接收一个 double 并返回其平方的函数

- 接收三个整数并返回其乘积的函数

- 接收一个字符串并返回其长度的函数

## 第 4 章 / 过程抽象与返回值的函数

### 语法

```
Type_Returned Function_Name(Parameter_List);   不要忘记
Function_Declaration_Comment             这个分号。
```

其中 Parameter_List 是一个用逗号分隔的参数列表，

```
Type_1 Formal_Parameter_1, Type_2 Formal_Parameter_2...
      ... Type_LastFormal_Parameter_Last
```

### 示例

```
double totalWeight(int number, double weightOfOne);
// 返回 number 个物品的总重量，
// 每个物品的重量为 weightOfOne。
```

在显示 4.3 中，函数定义位于显示内容的底部，并以颜色显示。函数定义描述了函数如何计算其返回的值。如果你将函数看作你程序内部的一个小程序，那么函数定义就像是这个小程序的代码。函数定义的语法与程序主部分的语法非常相似。函数定义由一个函数头和随后的函数体组成。函数头部的写法与函数声明相同，但头部的结尾没有分号。这使得函数头看起来有些重复，但没关系。

虽然函数声明告诉了你编写函数所需的所有信息，但它并没有告诉你将返回什么值。返回的值由函数体中的语句决定。函数体紧随函数头之后并完成了函数定义。函数体由封装在双括号内的声明和可执行语句组成。函数体就像程序的主部分体一样。当函数被调用时，参数会被填入形式参数中，然后执行体中的语句。函数返回的值在函数执行 `return` 语句时确定。（这种“填入”过程的细节将在后面的章节中讨论。）

`return` 语句使用关键字 `return` 后面紧跟一个表达式。显示 4.3 中的函数定义包含以下 `return` 语句：

```
return (subtotal + subtotal) * TAX_RATE);
```

当执行此 `return` 语句时，后续表达式的值将作为函数调的值返回：

```
(subtotal + subtotal) * TAX_RATE
```

## 4.3 程序员定义的函数

括号不是必须的。如果将 `return` 语句写如下所示，程序的运行结果将完全相同：

```
return subtotal + subtotal * TAX_RATE;
```

然而，对于较大的表达式，括号会让 `return` 语句更易读。为了保持一致性，一些程序员主张即使在简单的表达式上也使用这些括号。在显示 4.3 的函数定义中，`return` 语句之后没有语句，但如果有，它们将不会被执行。当执行 `return` 语句时，函数调用即结束。

![](img/67be1289808bc3852827f7f3e32e9d82_226_0.png)

让我们看看当在显示 4.3 所示的程序执行以下函数调用时到底发生了什么：

```
bill1 = totalCost(number, price);
```

首先，参数和 `price` 的值被填入形式参数中；也就是说，参数和 `price` 的值被替换为 `numberPar` 和 `pricePar`。在示例对话中，`number` 接收值 2，`price` 接收值 10。因此，2 和 10 分别被替换了 `numberPar` 和 `pricePar`。这种替换过程被称为**值传递机制**（call-by-value mechanism），形式参数通常被称为值传递参数，或简单称为值传递参数。关于这个替换过程，你应该注意三点：

- 1. 填入形式参数的是参数的值。如果参数是变量，那么填入的是变量的值，而不是变量本身。

- 2. 第一个参数填入参数列表中的第一个形式参数，第二个参数填入列表中的第二个形式参数，依此类推。

- 3. 当一个参数填入一个形式参数时（例如， 2 填入 `numberPar`），该参数会填入函数体中出现的所有形式参数实例中（例如，每当 `numberPar` 在函数体中出现时，都会填入 2）。

显示 4.3 中函数调用涉及的整个过程在显示 4.4 中进行了详细描述。

## 显示 4.4 函数调用的细节

> 1. 在调用函数之前，通过 `cin` 语句将变量 `number` 和 `price` 的值设置为 2 和 10.10（你可以在显示 4.3 中看到示例对话）。

> 2. 函数执行，`number` 的值（为 2）填入 `numberPar`，`price` 的值（为 10.10）填入 `pricePar`。

> 3. 函数体执行，此时 `numberPar` 设置为 2，`pricePar` 设置为 10.10，在 `subtotal` 中产生值 20.20。

> 4. 当执行 `return` 语句时，计算 `return` 表达式的值并由函数返回。在这种情况下，`(subtotal + subtotal * TAX_RATE)` 为 `(20.2 + 20.2 * 0.05)`，即 21.21。

> 5. 值 21.21 返回到调用函数的地方。`totalCost(number, price)` 的结果为 21.21。

## 4.3 程序员定义的函数

## 返回值的值的函数

函数可以返回一个值。返回真（true）或假（false）的函数称为**谓词**（predicate）。这种函数可以用于 `if-else` 语句或控制循环。例如，以下函数：

```cpp
bool appropriate(int rate)
{
    return rate >= 10;
}
```

可以这样使用：

```cpp
if (appropriate(rate))
{
    // ...
}
```

## 声明的另一种形式

你不需要在函数声明中列出参数名称。以下两个声明是等价的：

```cpp
double totalCost(int numberPar, double pricePar);
```

```cpp
double totalCost(int, double);
```

我们将使用第一种形式，以便在函数定义中引用这些参数。参数名称对于程序员和编译器之间的通信至关重要。

## 陷阱 参数顺序错误

当函数被调用时，计算机将第一个参数替换为第一个形式参数，第二个参数替换为第二个形式参数，依此类推。它不会检查合理性。如果你混淆了函数调用中参数的顺序，程序将不会按照你的预期运行。为了看到可能会发生什么，请考虑显示 4.5 中的程序。编写该程序的程序员粗率地反转了调用函数时参数的顺序。函数调用本应该是：

```cpp
letterGrade = grade(score, needToPass);
```

## 显示 4.5 错误的参数顺序（部分 1/2）

```cpp
// 用户的成绩。成绩分为通过或不通过。
#include <iostream>
using namespace std;

char grade(int receivedPar, int minScorePar);
// 返回 'P' 表示通过，如果 receivedPar 大于或等于
// minScorePar。否则返回 'F' 表示不通过。

int main()
{
  int score, needToPass;
  char letterGrade;
  cout << "输入你的成绩"
  cout << " 以及通过分数:\n";
  cin >> score >> needToPass;
  letterGrade = grade(needToPass, score);
}
```

## 4.3 程序定义的函数

### 显示 4.5 顺序错误的参数（部分 2 / 2）

```cpp
20  cout << "You received a score of " << score << endl;
21      << "Minimum to pass is " << needToPass << endl;
22
23      if (letterGrade == 'P')
24          cout << "You Passed. Congratulations!\n";
25      else
26          cout << "Sorry. You failed.\n";
27
28      cout << letterGrade
29          << " will be entered in your record.\n";
30
31          return 0;
32
33  )
34  char grade(int receivedPar, int minScorePar)
35  {
36      if (receivedPar >= minScorePar)
37          return 'P';
38      else
39          return 'F';
40  }
```

### 示例对话

输入你的分数和通过所需的最低分数：

98 60

你收到的分数是 98

通过的最低分数是 60

对不起。你失败了。

F 将记入你的记录。

在显示 4.5 中，编译器不会对参数的顺序报错，因为无论参数顺序如何，函数参数类型都会与形式参数类型匹配。

## 函数定义-语法总结

函数声明通常放在程序的主部分之前，而函数定义通常放在程序的主部分之后（或者，如我们在书后面部分看到的，放在单独的文件中）。显示 4.6 给出了函数声明和定义的语法总结。实际上，自由度比该显示的要大得多。函数定义中的声明和执行语句可以混合使用，只要每个变量在使用之前都已声明。关于混合声明和执行语句的规则

![](img/67be1289808bc3852827f7f3e32e9d82_230_0.png)

# 234 第 4 章 / 过程抽象与返回值的函数
