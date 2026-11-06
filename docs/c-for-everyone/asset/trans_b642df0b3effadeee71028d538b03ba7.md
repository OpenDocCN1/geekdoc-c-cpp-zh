

如果省略长度，则会获取从给定位置到字符串末尾的所有字符。例如，`greeting.substr(7)`是字符串“world!”（包括感叹号）。

下面是一个运用这些概念的简单程序。该程序要求用户输入自己的姓名和伴侣的姓名，然后输出两人的姓名首字母。

操作`first.substr(0, 1)`会生成一个由一个字符组成的字符串，该字符取自`first`的开头。程序对第二个姓名执行相同的操作。然后，它将得到的两个单字符字符串与字符串字面量`"&"`连接起来，得到一个长度为 3 的字符串，即姓名首字母字符串。（参见图 4。）

![](img/5e58fb4c840712efd6ed6fa82bb97f57_86_0.png)

*姓名首字母由每个姓名的第一个字母组成。*

![](img/5e58fb4c840712efd6ed6fa82bb97f57_86_1.png)

**图 4** 构建姓名首字母字符串

**ch02/initials.cpp**

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    cout << "Enter your first name: ";
    string first;
    cin >> first;
    cout << "Enter your significant other's first name: ";
    string second;
    cin >> second;
    string initials = first.substr(0, 1)
        + "&" + second.substr(0, 1);
    cout << initials << endl;
    return 0;
}
```

**程序运行结果**

```text
Enter your first name: Rodolfo
Enter your significant other's first name: Sally
R&S
```

### 表 8 字符串操作

| 语句 | 结果 | 注释 |
|---|---|---|
| `string str = "C";`<br>`str = str + "++";` | `str`被设置为`"C++"` | 用于字符串时，`+`表示连接。 |
| `string str = "C" + "++";` | **错误** | **错误：**不能连接两个字符串字面量。 |
| `cout << "Enter name: ";`<br>`cin >> name;`<br>（用户输入：Harry Morgan） | `name`包含`"Harry"` | `>>`运算符会将下一个单词放入字符串变量中。 |
| `cout << "Enter name: ";`<br>`cin >> name >> last_name;`<br>（用户输入：Harry Morgan） | `name`包含`"Harry"`，`last_name`包含`"Morgan"` | 使用多个`>>`运算符可以读取多个单词。 |
| `string greeting = "H & S";`<br>`int n = greeting.length();` | `n`被设置为 5 | 每个空格都算作一个字符。 |
| `string str = "Sally";`<br>`string str2 = str.substr(1, 3);` | `str2`被设置为`"all"` | 提取从位置 1 开始、长度为 3 的子字符串。（起始位置为 0。） |
| `string str = "Sally";`<br>`string str2 = str.substr(1);` | `str2`被设置为`"ally"` | 如果省略长度，则会包含从该位置到字符串末尾的所有字符。 |
| `string a = str.substr(0, 1);` | `a`被设置为`str`中的首字母 | 提取从位置 0 开始、长度为 1 的子字符串。 |
| `string b = str.substr(str.length() - 1);` | `b`被设置为`str`中的最后一个字母 | 最后一个字母的位置是`str.length() - 1`。无需指定长度。 |

## 自我检查

![](img/5e58fb4c840712efd6ed6fa82bb97f57_87_0.png)

- **25.** 字符串`"C++ Program"`的长度是多少？
- **26.** 考虑以下字符串变量。

    ```cpp
    string str = "C++ Program";
    ```

    写出一个子字符串成员函数调用，使其返回子字符串`"gram"`。
- **27.** 使用字符串连接，将自我检查题 26 中的字符串变量`str`转换为`"C++ Programming"`。
- **28.** 以下语句序列会输出什么？

    ```cpp
    string str = "Harry";
    cout << str.substr(0, 1) + str.substr(str.length() - 1);
    ```
- **29.** 写出一条输入语句，以读取形如`"John Q. Public"`的姓名。

**练习** 现在你可以尝试本章末尾的以下练习：R2.6、R2.9、P2.12、P2.19。

### R2.13

为一个计算数字首位和末位数字的程序编写伪代码。例如，如果输入是 23456，程序应输出 2 和 6。提示：x、log₁₀。

### R2.14

修改“How To 2.1”中程序的伪代码，使程序能够以 25 美分、10 美分和 5 美分硬币的形式找零。可以假设价格是 5 美分的整数倍。为了编写伪代码，先使用几个具体数值进行计算。

### R2.15

鸡尾酒调酒器由三个圆锥台部分组成。

使用合理的半径和高度值，并利用自我检查题 24 中给出的圆锥台部分体积公式，计算总体积。然后开发一个适用于任意尺寸的算法。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_92_0.png)

### R2.16

如下图所示，你正在切下一块派，其中`c`是直线部分的长度（称为弦长），`h`是这块派的高度。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_92_1.png)

面积有一个近似公式：

\[
A \approx \frac{2}{3}ch + \frac{h^3}{2c}.
\]

然而，`h`不太容易测量，而派的直径`d`通常是已知的。计算派的直径为 12 英寸、该部分的弦长为 10 英寸时的面积。将其推广为一个能够计算任意直径和弦长所对应面积的算法。

### R2.17

以下伪代码描述了如何根据星期编号获取星期名称（0 = 星期日，1 = 星期一，依此类推）。

```text
定义一个名为 names 的字符串，其中包含 "SunMonTueWedThuFriSat"。
将起始位置计算为 3 × 星期编号。
从 names 的起始位置开始，提取长度为 3 的子字符串。
```

使用星期编号 4 检查这段伪代码。绘制所计算字符串的示意图，类似于第 59 页的图 4。

### R2.18

以下伪代码描述了如何交换单词中的两个字母。

```text
给定一个字符串 str 和两个位置 i、j。（i 在 j 之前）
将 first 设置为从字符串开头到 i 之前最后一个位置的子字符串。
将 middle 设置为从位置 i + 1 到 j - 1 的子字符串。
将 last 设置为从位置 j + 1 到字符串末尾的子字符串。
连接以下五个字符串：first、仅包含位置 j 处字符的字符串、middle、仅包含位置 i 处字符的字符串，以及 last。
```

使用字符串`"Gateway"`以及位置 2 和 4 检查这段伪代码。绘制所计算字符串的示意图，类似于第 59 页的图 4。

### R2.19

运行以下程序，并解释所得的输出。

```cpp
#include <iostream>

using namespace std;

int main()
{
    int total;
    cout << "Please enter a number: ";
    double x1;
    cin >> x1;
    total = total + x1;
    cout << "total: " << total << endl;
    cout << "Please enter a number: ";
    double x2;
    cin >> x2;
    total = total + x2;
    cout << "total: " << total << endl;
    total = total / 2;
    cout << "total: " << total << endl;
    cout << "The average is " << total << endl;
    return 0;
}
```

注意**跟踪消息**（以蓝色显示），这些消息用于显示`total`变量当前的内容。如何修复该程序？（该程序有两个独立的错误。）

### R2.20

编写一个程序，输出以下值：

```text
3 * 1000 * 1000 * 1000
3.0 * 1000 * 1000 * 1000
```

解释结果。

### R2.21

本章针对变量和常量提出了许多建议，这些建议可以使程序更易于阅读和维护。简要总结这些建议。

## 编程练习

- **1. P2.1** 编写一个程序，以毫米为单位显示信纸大小（8.5 × 11 英寸）纸张的尺寸。1 英寸等于 25.4 毫米。在程序中使用常量和注释。
- **2. P2.2** 编写一个程序，计算并显示信纸大小（8.5 × 11 英寸）纸张的周长及其对角线长度。
- **3. P2.3** 编写一个程序，读取一个数字并显示其平方、立方和四次方。仅对四次方使用`pow`函数。
- **4. P2.4** 编写一个程序，提示用户输入两个整数，然后输出：
    - 和
    - 差

