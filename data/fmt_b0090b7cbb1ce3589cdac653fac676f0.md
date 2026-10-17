
- LLVM: Read-only variable is not assignable

> **常见错误 7.2**
>
> 声明常量变量时不初始化是编译错误。
>
> **常见错误 7.3**
>
> 在独立语句中为常量变量赋值是编译错误。
>
> **良好编程实践 7.1**
>
> 将数组定义为常量变量而不是字面常量更加清晰且容易更新。这种技术消除了所谓的魔数——即未解释的数值值。使用常量变量允许你为字面常量提供名称，并帮助解释该值在程序中的用途。

### 7.4.4 数组求和

通常，数组的元素表示用于计算的一系列值。例如，如果数组元素代表考试成绩，教授可能希望计算元素的总和，并使用该值计算当年的级平均分。

图 7.6 中的程序求和四元素整数数组中包含的值。程序在第 9 行声明、创建并初始化数组。对于该语句（第 13-15 行），它执行计算。值可以作为数组的初始化器提供，也可以从键盘或磁盘上的文件读取（参见第 14 章文件处理）。例如，语句：

```cpp
for (size_t j=0; j < a.size(); j++) {
    cin >> a[j];
}
```

每次从键盘读取一个值并存储在 `a[j]` 中。

```cpp
// Fig 7.6: fig07_06.cpp
// 计算数组元素的总和。
#include <iostream>
#include <array>
using namespace std;

int main() {
    const size_t arraySize{4}; // 指定数组的大小
```

**图 7.6** 计算数组元素的总和。（部分部分，共两部分）。

+ 1. 在错误消息中，某些编译器会将常量基本类型值称为“const 对象”。C++ 标准将“对象”定义为任何“存储区域”。与对象一样，基本类型变量也占用内存空间，因此也被称为“对象”。

## 7.4 数组示例

```
array<int, arraySize> a{10, 20, 30, 40};
int total{0};
// 累加数组a的内容
for (size_t i=0; i < a.size(); ++i) {
    total += a[i];
}
cout << "Total of array elements: " << total << endl;
```

数组元素总和: 100

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_331_0.png)

## 7.4.5 使用图表图形化显示数组数据

许多程序以图形方式向用户展示数据。例如

```
// Fig. 7.7: fig07.cpp
// 柱状打印程序。
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;
```

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_331_1.png)

## 第7章 类模板 数组和vector：异常处理

```cpp
int main() {
    const size_t arraySize{11};
    array<int, arraySize> n{0, 0, 0, 0, 0, 1, 2, 4, 2, 1};
    cout << "Grade distribution:" << endl;

    // 遍历数组n的每个元素，输出图表的一柱
    for (size_t i=0; i < n.size(); ++i) {
        // 输出标签("0-9", ..., "90-99", "100")
        if (i == 0)
            cout << "0-9: ";
        else if (i == 10)
            cout << "100: ";
        else
            cout << i * 10 << "-" << (i * 10) + 9 << ": ";
    }

    // 打印星号柱形
    for (unsigned int stars=0; stars < n[i]; ++stars) {
        cout << "";
    }
    cout << endl; // 开始新的一行输出
}
```

成绩分布：

0-9:

10-19:

20-29:

30-39:

40-49:

50-59:

60-69: **

70-79: ***

80-89: ****

90-99: *****

100: *

> Fig. 7.7 | 柱状图打印程序。（2部分中的2部分）

## 7.4.6 使用数组元素作为计数器

有时程序使用计数器变量来汇总数据，例如调查结果。在6.7节中，我们在骰子程序中使用单独的计数器来跟踪当程序投掷60,000,000次时，骰子每个面出现的次数。该程序的数组版本在7.8节中。该版本还使用了6.9节中引入的C++11 随机数生成功能。

7.8 使用数组（第17行）来统计骰子值的出现次数。该程序第21行的单语句替换了图6.7中第22–43行的整个switch语句。第21行使用随机值来确定哪一个频率元素

```cpp
// Fig. 7.8: fig07.cpp
// 使用数组代替switch的骰子掷程序。
#include <iostream>
#include <cmath>
#include <array>
#include <random>
#include <ctime>
using namespace std;

int main() {
    // 使用默认随机数生成引擎
    // 产生1到6之间均匀分布的伪随机int值
    default_random_engine(static_cast<unsigned int>(time(0)));
    uniform_int_distribution<unsigned int> randomInt(1
```

| 面 | 频率 |

|---|---|

| 1 | 999790 |

| 2 | 999110 |

| 3 | 100172 |

| 4 | 100369 |

| 5 | 999706 |

| 6 | 100052 |

**Fig. 7.8** 使用数组代替switch的骰子掷程序。循环的每次迭代。第21行的循环产生一个1到6的随机下标，因此数组频率必须足够大以存储六个计数器。我们使用一个七元素数组，其中我们忽略了frequency[0]——定义面值1时增加frequency[1]会更清晰。因此，每个面值都直接用作数组频率的下标。我们还通过遍历频率数组替换了图6.7中的第46–51行以输出结果（图7.8, 27–29）。

## 7.4.7 使用数组汇总结果

我们的示例使用数组来汇总调查中收集的结果。考虑以下问题：要求20名学生按1到5的量表对食堂的质量进行评分，其中1代表“糟糕”，5代表“优秀”。这是一种流行的数组处理应用类型（图7.9）。

```cpp
// 7.9: fig09.cpp
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;

int main() {
    // 定义数组大小
    const size_t arraySize{11};
    // 定义频率数组并初始化为0
    array<unsigned int, arraySize> frequency{};

    // 使用随机数生成引擎
    default_random_engine engine(static_cast<unsigned int>(time(0)));
    uniform_int_distribution<unsigned int> randomInt(1, 5);

    // 模拟20次调查
    for (int i = 0; i < 20; ++i) {
        // 产生一个随机的评分
        unsigned int score = randomInt(engine);
        // 增加对应的频率计数
        frequency[score]++;
    }

    cout << "Rating distribution:" << endl;

    // 遍历频率数组输出结果
    for (size_t i = 0; i < frequency.size(); ++i) {
        if (i == 0)
            cout << "0-9: ";
        else if (i == 10)
            cout << "100: ";
        else
            cout << i * 10 << "-" << (i * 10) + 9 << ": ";

        // 根据频率打印星号柱
        for (unsigned int stars = 0; stars < frequency[i]; ++stars) {
            cout << "*";
        }
        cout << endl;
    }

    return 0;
}
```

| 评分分布: |

|---|---|

| 0-9: | |

| 10-19: | |

| 20-29: | |

| 30-39: | |

| 40-49: | |

| 50-59: | |

| 60-69: | |

| 70-79: | |

| 80-89: | |

| 90-99: | |

| 100: | |

（注：此处为示例汇总结果的逻辑）

# 常见编程错误 7.4

引用数组边界之外的元素是执行时的逻辑错误，而不是语法错误。

# 错误预防提示 7.1

在遍历数组时，索引永远不低于 0，且应小于数组元素的总数（比数组大小少 1）。确保循环终止条件防止访问此范围之外的元素。在第 7.5 节中，你将学习基于范围的 for 语句（range-based for statement），它可以帮助防止访问数组（或其他容器）边界之外的元素。

## 7.4.8 静态数组和自动局部数组

第 6 章讨论了存储类型 `static`。函数定义中的静态局部变量在整个函数的持续期内都存在，但仅在函数体内可见。

# 性能提示 7.1

我们可以对局部数组声明应用 `static`，这样它就不会在每次调用函数时被创建和初始化，也不会在每次函数结束时被销。这可以提高性能，特别是在使用大数组时。

程序在第一次遇到局部数组声明时会初始化它们。如果你没有手动初始化静态数组，编译器会在创建数组时将该数组的每个元素初始化为零。记住，C++ 不对其他局部变量执行默认初始化。

图 7.10 展示了 `staticArrayInit` 和 `automaticArrayInit`（第 23–40 行），使用了静态局部数组（第 25 行）和自动局部数组（第 45 行——局部变量有时被称为自动变量，因为它们在函数执行完毕后会自动销毁。

函数 `staticArrayInit` 被调用两次（第 13 和 17 行）。第一次调用函数时，静态局部数组 `array1` 被编译器初始化为零。该函数打印数组元素，将每个元素加 5 然后再次打印数组。第二次调用函数时，静态数组包含了函数调用期间存储的修改后的值。函数 `automaticArrayInit` 被调用两次（第 14 和 18 行）。自动局部数组 `array2` 的元素（第 45 行）初始化为值 1、2 和 3。该函数打印数组，将每个元素加 5 然后再次打印数组。第二次调用函数时，数组元素被重新初始化为 1、2 和 3。每次调用 `automaticArrayInit` 时，数组都会重新创建并重新初始化。

```
// Fig. 7.10: fig07_10.cpp
// 静态数组初始化和自动数组初始化。
#include <iostream>
#include <array>
using namespace std;

void staticArrayInit(); // function原型
```

**图 7.10** | 静态数组初始化和自动数组初始化。（3 部分中的第 1。）

## 7.4 使用数组的示例

```cpp
8 void automaticArrayInit(); // function原型
9 const size_t arraySize{3};
11 int main() {
12 cout << "First call to each function:\n";
13 staticArrayInit();
14 automaticArrayInit();
16 cout << "\nsecond call to each function:\n";
17 staticArrayInit();
18 automaticArrayInit();
20 cout << endl;
21 }
22 void staticArrayInit(void) {
24 // 第一次调用时初始化元素为 0
25 static int array1[arraySize] = {}; // 静态局部数组
27 cout << "\nValues on exiting staticArrayInit:\n";
29 // 输出 array1 的内容
30 for (size_t i=0; i < array1.size(); ++i) {
31 cout << "array1[" << i << "] = " << array1[i] << "";
33 }
35 cout << "\nValues on exiting staticArrayInit:\n";
37 // 修改并输出 array1 的内容
38 for (size_t j=0; j < array1.size(); ++j) {
39 cout << "array1[" << j << "] = " << array1[j] += 5 << "";
41 }
42 // 局部数组
43 void automaticArrayInit(void) {
45 // 每次调用时初始化
46 int array2[arraySize]={1, 2, 3}; // 自动局部数组
48 cout << "\nValues on enteringArrayInit:\n";
50 // 输出 array2 的内容
51 for (size_t i=0; i < array2.size(); ++i) {
52 cout << "array2[" << i << "] = " << array2[i] << "";
54 }
55 cout << "\nValues on exitingArrayInit:\n";
57 // 修改并输出 array2 的内容
58 for (size_t j=0; j < array2.size(); ++j) {
59 cout << "array2[" << j << "] = " << array2[j] += 5 << "";
61 }
```

图 7.10 | 静态数组初始化和自动数组初始化。（3 部分中的第 2。）

第一次调用每个函数：

Values entering staticArrayInit:

array1[0] = 0 array1[2] = 0

Values exiting staticArrayInit:

array1[0] = 5 array1[2] = 5

Values entering automaticArrayInit:

array2[0] = 1 array2[1] = 2 array2[2] = 3

Values exiting automaticArrayInit:

array2[0] = 6 array2[1] = 7 array2[2] = 8

第二次调用每个函数：

Values entering staticArrayInit:

array1[0] = 5 array1[2] = 5

Values exiting staticArrayInit:

array1[0] = 10 array1[2] = 10

Values entering automaticArrayInit:

array2[0] = 2 array2[1] = 2 array2[2] = 3

Values exiting automaticArrayInit:

array2[0] = 6 array2[1] = 7 array2[2] = 8

图 7.10 | 静态数组初始化和自动数组初始化。（3 部分中的第 3。）

## 7.5 基于范围的 for

正如我们所示，处理数组的所有元素是常见操作。C++11 基于范围的 for 语句允许你在不需要计数器的情况下完成这一点，避免了“越界”数组的可能性，并消除了实现边界检查的需求。图 7.11 使用基于范围显示数组内容（第 12–14 行）并将数组的每个元素值乘以 2（第 17–19 行）。

> **错误预防提示 7.2** 处理数组元素时，如果不需要访问元素的索引，请使用基于范围的 for 语句。

```cpp
// Fig. 7.11: fig07_11.cpp
// 使用基于范围将数组元素乘以 2。
#include <iostream>
#include <array>
using namespace std;
int main() {
    array<int, 5> items={1, 2, 3, 4, 5};
    // 显示修改前的 items
    cout << "items before modification: ";
}
```

图 7.11 | 使用基于范围将数组元素乘以 2。（2 部分中的第 1。）
