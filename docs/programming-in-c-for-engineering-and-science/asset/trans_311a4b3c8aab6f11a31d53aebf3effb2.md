

将摄氏温度并在屏幕上显示此华氏温度以及适当的描述性文本。

### 6.1.2.2 对象

从期望行为的描述中，我们可以识别出以下对象：

| 问题对象 | 类型 | 类别 | 名称 |
|---|---|---|---|
| screen | output device | variable | `cout` |
| prompt | text string | constant | none |
| Celsius temperature | double | variable | *tempCelsius* |
| keyboard | input device | variable | `cin` |
| Fahrenheit temperature | double | variable | *tempFahrenheit* |
| descriptive text | text string | constant | none |

### 6.1.2.3 操作

将华氏温度转换为摄氏温度的公式为

$$F = 1.8 \times C + 32$$

其中 *C* 是摄氏温度，*F* 是相应的华氏温度。我们现在有两个额外的数据对象——数值 1.8 和 32。然而，我们通常不会将此类常量值包含在对象列表中，因为它们在 C++ 中始终提供。

根据我们对程序行为的描述和该公式，我们可以识别出以下操作：

- 1. 在屏幕上显示一个字符串。
- 2. 从键盘读取一个数字。
- 3. 使用实数的乘法和加法计算摄氏温度的华氏等价值。
- 4. 在屏幕上显示一个字符串和一个数字。

### 6.1.2.4 算法

由于这些操作都已在 C++ 中提供，我们可以继续将它们与对象组织成算法：

重复以下操作：

- 1. 向 `cout` 显示摄氏温度的提示。
- 2. 从 `cin` 输入 *tempCelsius*。
- 3. 计算 *tempFahrenheit* = 1.8 * *tempCelsius* + 32。
- 4. 将 *tempFahrenheit* 连同适当的描述性文本输出到 `cout`。

### 6.1.2.5 编码和测试

示例 6.1 中的程序实现了该算法。它使用 while 循环来控制重复，用户输入小于最低可能温度 −273.15 摄氏度的任何值即可停止。

**示例 6.1 转换温度——版本 1**

```cpp
/* This program converts temperatures from Celsius to Fahrenheit,
using the standard Celsius-to-Fahrenheit conversion formula.
Entering any value less than -273.15 Celsius (approx. absolute
zero) terminates the program.

Input: tempCelsius
Output: tempFahrenheit
------------------------------------------------------------*/

#include <iostream>
using namespace std;

int main()
{
    cout << "Program to convert Celsius temperatures to Fahrenheit.\n";

    double tempCelsius,      // Celsius temperature
           tempFahrenheit;   // Fahrenheit temperature

    cout <<"\nEnter a Celsius temperature (< -273.15 to stop): ";
    cin >> tempCelsius;
    while (tempCelsius >= -273.15)
    {
        tempFahrenheit = 1.8 * tempCelsius + 32;

        cout << tempCelsius << " degrees Celsius is equivalent to "
             << tempFahrenheit << " degrees Fahrenheit\n";
        cout <<"\nEnter a Celsius temperature (< -273.15 to stop): ";
        cin >> tempCelsius;
    }
}
```

**SAMPLE RUN:**

```
Program to convert Celsius temperatures to Fahrenheit.

Enter a Celsius temperature (-273.15 or less to stop): 100
100 degrees Celsius is equivalent to 212 degrees Fahrenheit

Enter a Celsius temperature (-273.15 or less to stop): 0
0 degrees Celsius is equivalent to 32 degrees Fahrenheit

Enter a Celsius temperature (-273.15 or less to stop): -72.3
-72.3 degrees Celsius is equivalent to -98.14 degrees Fahrenheit

Enter a Celsius temperature (-273.15 or less to stop): -333
```

## 6.2 入门示例：带函数的温度转换

要将像示例 6.1 中那样用于将摄氏温度转换为华氏温度的程序代码合并到另一个程序中，就必须先在程序中搜索它，然后将其复制并粘贴到自己的程序中。在某些情况下，此代码可能分散，需要花费一些精力才能找到所有内容。如果我们能构造一个封装该代码的函数，并将其附加到可以在需要时调用的另一个程序中，那就方便得多，如示例 6.2 所示。

**示例 6.2 转换温度——版本 2**

```cpp
/* This program converts temperatures from Celsius to Fahrenheit,
   using the standard Celsius-to-Fahrenheit conversion formula.
   Entering any value less than -273.15 Celsius (approx. absolute
   zero) terminates the program.

   Input:  tempCelsius
   Output: tempFahrenheit
---------------------------------------------------------------*/

#include <iostream>
using namespace std;

double celsiusToFahrenheit(double tempCels); // function prototype

int main()
{
    cout << "Program to convert Celsius temperatures to Fahrenheit.\n";

    double tempCelsius,      // Celsius temperature
           tempFahrenheit;   // Fahrenheit temperature

    cout <<"\nEnter a Celsius temperature (< -273.15 to stop): ";
    cin >> tempCelsius;
    while (tempCelsius >= -273.15)
    {
        tempFahrenheit = celsiusToFahrenheit(tempCelsius);

        cout << tempCelsius << " degrees Celsius is equivalent to "
             << tempFahrenheit << " degrees Fahrenheit\n";
        cout <<"\nEnter a Celsius temperature (< -273.15 to stop): ";
        cin >> tempCelsius;
    }
}

double celsiusToFahrenheit(double tempCels) // function definition
{
    return 1.8 * tempCels + 32;
}
```

示例 6.2 中的程序产生的输出与示例 6.1 中的完全相同，但执行流程非常不同。在这里，摄氏到华氏的转换是使用在 main 函数之后定义的函数来执行的。下面的图表说明了此新程序中的控制流。

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_169_0.png)

程序的执行从 main() 的开头开始，并以通常的方式进行（1），直到到达对函数 celsiusToFahrenheit() 的调用（2）。此时，函数的参数 tempCelsius 被求值（3）并复制到函数 celsiusToFahrenheit() 中的参数 tempCels 中（4）。控制从 main 函数转移到函数 celsiusToFahrenheit()，该函数开始执行（5）。表达式

```
1.8 * tempCels + 32.0
```

被求值，并且由于 tempCels 包含 tempCelsius 的值的副本，因此所得值是 tempCelsius 的值的华氏等价值。return 语句使该值成为 celsiusToFahrenheit() 的返回值并将执行转移回 main 函数（6）。在那里，celsiusToFahrenheit() 的返回值被赋给 tempFahrenheit（7），并且执行通过 main 函数的其余部分正常进行（8）。

> 请参阅正文前言中给出的文本网站，了解我们为何谈论函数的“调用”和“库”。

在下一节中，我们将描述如何构造此类 C++ 函数，并以示例 6.2 中的程序为例进行说明。

## 6.3 程序员定义的函数

在前几章中，我们看到了 C++ 提供的函数的示例；例如，来自 C++ cmath 库的 pow() 和 sqrt() 以及来自其 cassert 库的 assert()。在前一节中，我们看到了程序员如何通过在 main 函数之前包含其原型并在其后包含其定义，将他们自己的函数（如 celsiusToFahrenheit()）添加到程序中的示例。在本节中，我们将更详细地研究此类程序员定义的函数。

函数的定义可以概括描述如下：

**C++ 函数定义**

形式：

```
return_type function_name(parameter-declaration_list)
{
    statement_list
}
```

其中：

- return_type 是函数返回的值的类型，或如果函数不返回值则为关键字 void；
- function_name 是命名函数的标识符；
- parameter-declaration_list 是函数参数的声明列表，可能为空，以逗号分隔；
- statement_list 描述函数的行为。

目的：

对函数的调用会导致其中的语句被执行。之后，当执行 return 语句或到达函数的语句列表末尾时，执行返回到调用程序单元。

因此，在示例 6.2 的程序中，行

```
double celsiusToFahrenheit(double tempCels)
{
    return 1.8 * tempCels + 32;
}
```
