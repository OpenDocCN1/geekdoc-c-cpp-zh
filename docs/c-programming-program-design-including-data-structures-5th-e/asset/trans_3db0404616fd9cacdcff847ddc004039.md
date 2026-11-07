

| 表达式 | 效果 |
|---|---|
| `strVar.capacity()` | 返回为 `strVar` 分配的存储空间大小。 |
| `strVar.erase(pos);` | `pos` 是 `string::size_type` 类型的参数。<br>从索引 `pos` 开始删除 `strVar` 中的所有字符。 |
| `strVar.resize(n, ch);` | 将 `strVar` 的存储分配大小改为 `n`。如果 `n` 小于 `strVar` 当前的存储大小，则字符串的存储大小会被截断为 `n`。如果 `n` 大于当前存储大小，则字符串会扩展到大小 `n`，并且额外空间会用字符变量 `ch` 指定的字符副本填充。 |

## 附录 G：系统中的内存大小与随机数生成器

一个与下面类似的程序会打印你系统中内置数据类型的内存大小。（该程序的输出显示了运行此程序时内置数据类型的大小。）

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

**示例运行：**

```
Size of char = 1
Size of int = 4
Size of short = 2
Size of unsigned int = 4
Size of long = 4
Size of bool = 1
Size of float = 4
Size of double = 8
Size of long double = 8
Size of unsigned short = 2
Size of unsigned long = 4
```

### 随机数生成器

要生成随机数，可以使用 C++ 函数 `rand`。要使用函数 `rand`，程序必须包含头文件 `cstdlib`。头文件 `cstdlib` 还包含常量 `RAND_MAX`。通常，`RAND_MAX` 的值为 32767。要查找 `RAND_MAX` 的准确值，请查阅系统文档。函数 `rand` 生成一个介于 0 和 `RAND_MAX` 之间的整数。以下程序演示如何使用函数 `rand`。它还会打印 `RAND_MAX` 的值：

```cpp
#include <iostream>
#include <cstdlib>
#include <iomanip>

using namespace std;

int main()
{
    cout << fixed << showpoint << setprecision(5);
    cout << "The value of RAND_MAX: " << RAND_MAX << endl;
    cout << "A random number: " << rand() << endl;
    cout << "A random number between 0 and 9: "
         << rand() % 10 << endl;
    cout << "A random number between 0 and 1: "
        << static_cast<double> (rand())
        / static_cast<double> (RAND_MAX)
        << endl;

    return 0;
}
```

**示例运行：**

```
The value of RAND_MAX: 32767
A random number: 41
A random number between 0 and 9: 7
A random number between 0 and 1: 0.19330
```

## 附录 H：参考文献

- 1. G. Booch，*面向对象分析与设计*，第二版，Addison-Wesley，1995。
- 2. E. Horowitz、S. Sahni 和 S. Rajasekaran，*计算机算法 C++*，Computer Science Press，1997。
- 3. N.M. Josuttis，*C++ 标准库：教程与参考手册*，Addison-Wesley，Reading，MA，1999。
- 4. D.E. Knuth，*计算机程序设计艺术，第 1 卷：基本算法*，第 3 版，Addison-Wesley，Reading，MA，1997。
- 5. D.E. Knuth，*计算机程序设计艺术，第 2 卷：半数值算法*，第 3 版，Addison-Wesley，Reading，MA，1998。
- 6. D.E. Knuth，*计算机程序设计艺术，第 3 卷：查找与排序*，第 2 版，Addison-Wesley，Reading，MA，1998。
- 7. S.B. Lippman 和 L. Lajoie，*C++ 入门*，第三版，Addison-Wesley，Reading，MA，1998。
- 8. D.S. Malik 和 M.K. Sen，*离散数学：理论与应用（修订版）*，Cengage Learning Asia，Singapore，2010。
- 9. E.M. Reingold 和 W.J. Hansen，*Pascal 数据结构*，Little Brown and Company，Boston，MA，1986。
- 10. R. Sedgewick，*C 语言算法*，第三版，Addison-Wesley，Reading，MA，第 1–4 部分，1998；第 5 部分，2002。
- 11. B. Stroustrup，*C++ 的设计与演化*，Addison-Wesley，Reading，MA，1994。

![](img/f97f778697507bb6fdd80c5991210cba_1564_0.png)

## 附录 I：奇数编号习题答案

### 第 1 章

- 1. a. 假；b. 假；c. 真；d. 假；e. 假；f. 假；g. 假；h. 真；i. 真；j. 假；k. 真；l. 假
- 3. 屏幕和打印机。
- 5. 操作系统监控计算机的整体活动并提供服务。这些服务中的一些包括内存管理、输入/输出活动和存储管理。
- 7. 在机器语言中，程序使用二进制代码编写，而在高级语言中，程序更接近自然语言。执行时，高级语言程序会被翻译成机器语言，而机器语言无需翻译成任何其他语言。
- 9. 因为计算机无法直接执行用高级语言编写的指令，所以需要编译器将用高级语言编写的程序翻译成机器代码。
- 11. 每台计算机都能直接理解自己的机器语言。因此，要让计算机执行用高级语言编写的程序，必须将高级语言程序翻译成该计算机的机器语言。
- 13. 在链接过程中，目标程序会与程序中使用的库里的其他程序组合，以创建可执行代码。
- 15. 要计算四次测试成绩的加权平均值，首先需要知道每次测试成绩及其权重。接下来，将每次测试成绩乘以其权重，再将这些数相加得到平均值。因此：
  1. 获取 testScore1、weightTestScore1
  2. 获取 testScore2、weightTestScore2
  3. 获取 testScore3、weightTestScore3
  4. 获取 testScore4、weightTestScore4
  5. 计算加权平均值：

     ```
     weightedAverage = testScore1 * weightTestScore1 +
                       testScore2 * weightTestScore2 +
                       testScore3 * weightTestScore3 +
                       testScore4 * weightTestScore4;
     ```
- 17. 要计算每平方英寸的价格，首先需要求出披萨的面积。然后，用披萨的价格除以披萨的面积。设 radius 表示半径，area 表示圆的面积，price 表示披萨的价格。另外，设 pricePerSquareInch 表示每平方英寸的价格。
  - a. 获取 radius。
  - b. area = π * radius * radius
  - c. 获取 price。
  - d. pricePerSquareInch = price / area
- 19. 要计算商品的销售价格，我们需要知道商品的原始价格（商店购买该商品所支付的价格）。然后可以使用以下公式求出销售价格。

  ```
  sellingPrice = originalPrice + originalPrice * .60
  ```

  算法如下：

  - a. 获取 originalPrice。
  - b. 使用以下公式计算 sellingPrice：

    ```
    sellingPrice = originalPrice + originalPrice * .60
    ```

  计算销售价格所需的信息是原始价格和加价百分比。
- 21. 假设 numOfPages 表示要传真的页数，billingAmount 表示已传真页面的总费用。要计算总费用，需要知道已传真的页数。

  如果 numOfPages 小于或等于 10，则账单金额为服务费 + (numOfPages × 0.20)；否则，账单金额为服务费 + 10 × 0.20 + (numOfPages − 10) × 0.10。也就是说，

  现在可以按如下方式编写算法：

  - a. 获取 numOfPages。
  - b. 使用以下公式计算账单金额：

    ```
    if (numOfPages is less than or equal to 10)
        billingAmount = 3.00 + (numOfPages × 0.20);
    otherwise
        billingAmount = 3.00 + 10 × 0.20 + (numOfPages − 10) × 0.10;
    ```
- 23. 假设 averageTestScore 表示平均测试成绩，highestScore 表示最高测试成绩，testScore 表示一个测试成绩，sum 表示所有测试成绩之和，count 表示班级中的学生人数，studentName 表示学生姓名。

