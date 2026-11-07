
| 函数名和参数 | 参数类型 | 函数返回值 |
|---|---|---|
| `sqrt(x)` | x 是浮点表达式，其中 x ≥ 0.0。 | x 的平方根 |
| `tan(x)` | x 是浮点表达式；x 以弧度为单位 | 该角度的三角正切 |
| `tanh(x)` | x 是浮点表达式 | x 的双曲正切 |

## 头文件 `cstddef` (`stddef.h`)

除其他内容外，该头文件还包含以下符号常量的定义：**NULL**：依赖于系统的空指针（通常为 0）。

## 头文件 `cstring` (`string.h`)

下表列出了各种字符串函数。

| 函数名和参数 | 参数类型 | 函数返回值 |
|---|---|---|
| `strcat(destStr, srcStr)` | `destStr` 和 `srcStr` 是以 null 结尾的 `char` 数组；`destStr` 必须足够大以容纳结果 | 返回 `destStr` 的基地址；`srcStr`（包括 null 字符）被连接到 `destStr` 的末尾。 |
| `strncat(destStr, srcStr, limit)` | `destStr` 和 `srcStr` 是以 null 结尾的 `char` 数组；`destStr` 必须足够大以容纳结果；`limit` 是非负整数值 | 此函数与上一个函数 `strcat` 相同，只是最多追加 `limit` 个字符。 |
| `strcmp(str1, str2)` | `str1` 和 `str2` 是以 null 结尾的 `char` 数组 | 返回值如下：<br>• 若 `str1 < str2`，则返回一个小于 0 的 `int` 值<br>• 若 `str1 == str2`，则返回 `int` 值 0<br>• 若 `str1 > str2`，则返回一个大于 0 的 `int` 值 |
| `strncmp(str1, str2, limit)` | `str1` 和 `str2` 是以 null 结尾的 `char` 数组，`limit` 是非负整数值 | 此函数与上一个函数 `strcmp` 相同，只是最多比较 `limit` 个字符。 |
| `strcpy(destStr, srcStr)` | `destStr` 和 `srcStr` 是以 null 结尾的 `char` 数组 | 返回 `destStr` 的基地址；`srcStr` 被复制到 `destStr` 中。 |
| `strncpy(destStr, srcStr, limit)` | `destStr` 和 `srcStr` 是以 null 结尾的 `char` 数组，`limit` 是非负整数值 | 将字符串 `srcStr` 复制到字符串变量 `destStr` 中。最多将 `limit` 个字符复制到 `destStr` 中。 |
| `strlen(str)` | `str` 是以 null 结尾的 `char` 数组 | 返回一个 ≥ 0 的整数值，指定 `str` 的长度（不包括 `\0`）。 |

## 头文件 `string`

该头文件——不要与头文件 `cstring` 混淆——提供了名为 `string` 的程序员定义数据类型。与 `string` 类型相关联的是一个数据类型 `string::size_type` 和一个命名常量 `string::npos`。它们的定义如下：

|  |  |
|---|---|
| `string::size_type` | 一种无符号整数类型 |
| `string::npos` | `string::size_type` 类型的最大值 |

`string` 类型包含若干用于字符串操作的函数。除表 7-1 中列出的字符串函数外，下表描述了其他字符串函数。在下表中，我们假设 `strVar` 是一个字符串变量，`str` 是一个字符串变量、字符串常量或字符数组。函数名以粗体显示。

| 表达式 | 作用 |
|---|---|
| `getline(istreamVar, strVar);` | `istreamVar` 是输入流变量（类型为 `istream` 或 `ifstream`）。<br><br>从 `istreamVar` 输入字符直到换行符，并存储到 `strVar` 中。（换行符被读取，但不存储到 `strVar` 中。）此函数的返回值通常被忽略。 |
| `strVar.append(str, n);` | 将字符数组 `str` 的前 n 个字符追加到 `strVar`。 |
| `strVar.c_str()` | 返回与 `strVar` 中的字符相对应的、以 null 结尾的 C 字符串的基地址。 |
| `strVar.capacity()` | 返回为 `strVar` 分配的存储空间大小。 |
| `strVar.erase(pos);` | `pos` 是 `string::size_type` 类型的参数。从索引 `pos` 开始删除 `strVar` 中的所有字符。 |
| `strVar.resize(n, ch);` | 将 `strVar` 的存储分配大小更改为 n。如果 n 小于 `strVar` 当前的存储大小，则字符串的存储大小被截断为 n。如果 n 大于当前存储大小，则字符串被扩展为大小 n，并用字符 `ch` 的副本填充额外空间。 |

## 附录 G

### 系统上的内存大小

类似下面的程序会打印你的系统中内置数据类型的内存大小。（该程序的输出显示了运行此程序时内置数据类型的大小。）

```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Size of char = " << sizeof(char) << endl;
    cout << "Size of int = " << sizeof(int) << endl;
    cout << "Size of short = " << sizeof(short) << endl;
    cout << "Size of unsigned int = " << sizeof(unsigned int)
         << endl;
    cout << "Size of long = " << sizeof(long) << endl;
    cout << "Size of long long = " << sizeof(long long)
         << endl;
    cout << "Size of bool = " << sizeof(bool) << endl;
    cout << "Size of float = " << sizeof(float) << endl;
    cout << "Size of double = " << sizeof(double) << endl;
    cout << "Size of long double = " << sizeof(long double)
         << endl;
    cout << "Size of unsigned short = "
         << sizeof(unsigned short) << endl;
    cout << "Size of unsigned long = "
         << sizeof(unsigned long) << endl;

    return 0;
}
```

示例运行：

```
Size of char = 1
Size of int = 4
Size of short = 2
Size of unsigned int = 4
Size of long = 4
Size of long long = 8
Size of bool = 1
Size of float = 4
Size of double = 8
Size of long double = 8
Size of unsigned short = 2
Size of unsigned long = 4
```

![](img/b217c421655b51e7494cf3b89bb5432d_1668_0.png)

## 附录 H

### 参考文献

© HunThomas/Shutterstock.com

- 1. G. Booch，*面向对象分析与设计*，第 2 版，Addison-Wesley，Reading, MA，1995。
- 2. E. Horowitz、S. Sahni 和 S. Rajasekaran，*计算机算法 C++*，Computer Science Press，1997。
- 3. N.M. Josuttis，*C++ 标准库：教程与参考手册*，Addison-Wesley，Reading, MA，1999。
- 4. D.E. Knuth，*计算机程序设计艺术，第 1 卷：基本算法*，第 3 版，Addison-Wesley，Reading, MA，1997。
- 5. D.E. Knuth，*计算机程序设计艺术，第 2 卷：半数值算法*，第 3 版，Addison-Wesley，Reading, MA，1998。
- 6. D.E. Knuth，*计算机程序设计艺术，第 3 卷：排序与查找*，第 2 版，Addison-Wesley，Reading, MA，1998。
- 7. S.B. Lippman 和 J. Lajoie，*C++ Primer*，第 3 版，Addison-Wesley，Reading, MA，1998。
- 8. D.S. Malik 和 M.K. Sen，*离散数学：理论与应用（修订版）*，Cengage Learning Asia，Singapore，2010。
- 9. E.M. Reingold 和 W.J. Hensen，*Pascal 数据结构*，Little Brown and Company，Boston, MA，1986。
- 10. R. Sedgewick，*C 算法*，第 3 版，Addison-Wesley，Reading, MA，第 1–4 部分，1998；第 5 部分，2002。
- 11. B. Stroustrup，*C++ 的设计与演化*，Addison-Wesley，Reading, MA，1994。

![](img/b217c421655b51e7494cf3b89bb5432d_1670_0.png)

## 附录 I

### 奇数编号习题答案

### 第 1 章

- 1. a. 真；b. 假；c. 假；d. 真；e. 假；f. 真；g. 真；h. 真；i. 假；j. 假；k. 真；l. 真；m. 真；n. 真；o. 真；p. 假；q. 真；r. 真；s. 真
- 3. 以 2 为底，即二进制。
- 5. 在链接过程中，目标程序与程序中使用的库中的其他程序组合，以创建可执行代码。
- 7. #
- 9. 编程是一个解决问题的过程。
- 11. （1）分析并概述问题及其解决方案需求，并设计解决问题的算法。（2）用编程语言（如 C++）实现该算法，并验证算法有效。（3）通过使用程序并在问题领域发生变化时修改程序来维护程序。
- 13. 要计算四个测试分数的加权平均值，首先需要知道每个测试分数及其权重。接下来，将每个测试分数乘以其权重，然后把这些数相加得到平均值。因此，

```
1.  Get testScore1, weightTestScore1
2.  Get testScore2, weightTestScore2
3.  Get testScore3, weightTestScore3
4.  Get testScore4, weightTestScore4
5.  weightedAverage = testScore1 * weightTestScore1 +
                     testScore2 * weightTestScore2 +
                     testScore3 * weightTestScore3 +
                     testScore4 * weightTestScore4;
```

