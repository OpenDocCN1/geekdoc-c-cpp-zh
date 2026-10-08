
Since the output is in thousands of units, the program will scale the values of the array elements. If the total output for plant number 3 is 4040 units, the value of `production[2]` will initially be set to 4040. This value of 4040 will be scaled to 4 so that the value of `production[2]` is changed to 4, and four asterisks will be output in the graph to represent the output for plant number 3.

The task for our program can be divided into the following subtasks:

- `inputData`: Read the input data for each plant and scale the value of the indexed variable `production[plantNumber - 1]` to the total production for that plant, where `plantNumber` is the number of the plant.
- `scale`: For each `plantNumber`, change the value of the indexed variable `production[plantNumber - 1]` to the correct number of asterisks.
- `graph`: Output the bar graph.

The entire array `production` will be an argument for the functions that carry out these subtasks. As usual with array parameter, this means we must have an additional formal parameter for the size of the array, which in this case is same as the number of plants. We will use a defined constant for the number of plants, and this constant will serve as the size of the array `production`. The main part of our program, together with the function declarations that perform the subtasks and the defined constant for the number of plants, is shown in Display 7.5. Notice that, since there is no reason to change the array parameter to the function `graph`, we have made array parameter a constant by adding the `const` modifier. The material in Display 7.5 is the outline for our program, and if it is in a separate file, that file can be compiled so that we can check for any syntax errors in this before we go on to define the functions corresponding to the function declarations shown.

Having compiled the file shown in Display 7.5, we are ready to design the implementation of the functions for the three subtasks. For each of these, we will design an algorithm, write the code for the function, and test the function before we go on to design the next function.

### Subtasks

434 CHAPTER 7 / Arrays

### Algorithm Design for inputData

The function declaration and descriptive comment for the body of the function `inputData` is shown in Display 7.5. As indicated in Display 7.5), when `inputData` is called, the formal array parameter `a` will be replaced with the array `production`, and since the last part of the program also the last plant number is the same as the number of plants, the formal parameter `lastPlantNumber` will be replaced by `NUMBER_OF_PLANTS`. The algorithm for `inputData` is straightforward:

- For `plantNumber` equal to each of 1, 2, through `lastPlantNumber` do the following:
  Read in all the data for plant number is `plantNumber`.
  Sum the numbers.
  Set `production[plantNumber -1]` equal to that total.

### Coding for inputData

The algorithm for the function `inputData` translates to the following code:

```cpp
//Uses iostream:
void inputData(int a [], int lastPlantNumber)
{
    using namespace std;
    for (int plantNumber = 1; plantNumber <= lastPlantNumber; plantNumber++)
    {
        // 逻辑实现
    }
}
```

（注：由于原文文本存在大量重复和乱码，翻译已根据核心逻辑进行去重处理）

## 7.2 函数中的数组

# DISPLAY 7.6 函数 inputData 的测试（3 部分中的第 1 部分）

```cpp
// 测试函数 inputData。
#include <iostream>
const int NUMBER_OF_PLANTS = 4;

void inputData(int a[], int lastPlantNumber);
// 前置条件：lastPlantNumber 是数组 a 的大小。
// 后置条件：对于 plantNumber = 1 到 lastPlantNumber；
// [plantNumber - 1] 等于工厂编号 plantNumber 的总产量；

void getTotal(int &sum);
// 从键盘读取非负整数并
// 将它们的总和存放在 sum 中。

int main()
{
    using namespace std;
    int production[NUMBER_OF_PLANTS];
    char ans;

    do
{
        inputData(production, NUMBER_OF_PLANTS);
        cout << endl;
        cout << "每个工厂的总产量：\n"
        cout << " 1 到 4 号工厂：\n";
        for (int number = 1; number <= NUMBER_OF_PLANTS; number++)
            cout << production[number - 1] << " ";
        cout << endl;
        cout << "再次测试?(输入 y 或回车）： ";
        cin >> ans;
    } while ((ans != 'N') && (ans != 'n'));

    cout << endl;
    return 0;
}
// 使用 iostream：
void inputData(int a[], int lastPlantNumber)
{
    using namespace std;
    for (int plantNumber = 1;
        plantNumber <= lastPlantNumber; plantNumber++)
        cout << endl << "输入第 "
 号工厂的产量数据 "
```

（上接）

# DISPLAY 7.6 函数 input_data 的测试（3 部分中的第 2 部分）

```cpp
47 << plantNumber << endl;
48 getTotal(aplantNumber - 1);
49 }
50 }
```

```cpp
53 // 使用 iostream：
54 void getTotal(int&sum)
55 {
56 using namespace std;
57 cout << "输入每个部门的产量。\n"
58 << "在列表末尾添加一个负数。\n"
59
60 sum = 0;
61 int next;
62 cin >> next;
63 while (next >= 0)
64 {
65 sum = sum + next;
66 cin >> next;
67 }
68 }
```

### 示例对话

输入第 1 号工厂的产量数据

输入每个部门的产量。

在列表末尾添加一个负数。

1 2 3 -1

总计 = 6

输入第 2 号工厂的产量数据

输入每个部门的产量。

在列表末尾添加一个负数。

0 2 3 -1

总计 = 5

输入第 3 号工厂的产量数据

输入每个部门的产量。

在列表末尾添加一个负数。

2 -1

总计 = 2

（上接）

# 7.2 函数中的数组

# DISPLAY 7.6 函数 input_data 的测试（3 部分中的第 3 部分）

```text
输入第 4 号工厂的产量数据
输入每个部门的产量。
在列表末尾添加一个负数。
-1
总计 = 0
1 到 6 号工厂的工厂产量
5 20
```

再次测试?(输入 y 或 n 并回车): n

```cpp
void scale(int a[], int size)
{
    using namespace std;
    for (int index = 0; index < size; index++)
        a[index] = (int)round(a[index] / 1000.0);
}
```

注意除以 1000.0 的结果。如果执行的是整数除法，2600/1000 会得到 2，但我们希望得到 3。通过 2600/1000.0 得到 2.6，使用 `round()` 函数可以得到 3。对于 2400/1000.0，结果是 2.4，`round()` 得到 2；对于 2500/1000.0，`round()` 得到 3（取决于舍入规则）。对于 2600/1000.0，结果是 2.6，`round()` 得到 3。

在 `scale` 函数中，`a[index]` 被修改为 1000 的倍数。为了确保 `round()` 函数正常工作，让我们看看例子。对于 2400/1000.0，结果是 2.4，`round()` 得到 2；对于 2500/1000.0，结果是 2.5，`round()` 得到 3；对于 2600/1000.0，结果是 2.6，`round()` 得到 3。这意味着 `round()` 函数会将浮点数舍入到最近的整数。

`<cmath>` 头文件提供了 `round()`、`ceil()` 和 `floor()` 函数。`floor()` 返回向下取整到最大的整数，而 `ceil()` 返回向上取整到最小的整数。例如

```text
floor(2.4) = 2
floor(2.6) = 2
ceil(2.4) = 3
ceil(2.6) = 3
```

Display 7.7 包含一个 `scale` 函数的演示程序，但 `round` 和 `scale` 的测试程序应该比这个简单的程序更复杂。特别是，它们应该允许你多次测试函数，而不是只一次。我们不会提供完整的测试程序，但你应该先为 `round`（即 scale）编写一个驱动程序，然后为 `scale` 编写驱动程序。测试 `round` 函数的参数应包括 0、向上舍入（如 2.6）和向下取整（如 2.3）。测试 `scale` 函数的程序应该测试数组元素的各种值。

# DISPLAY 7.8 产量图表程序（3 部分中的第 1 部分）

```cpp
// 读取数据并显示每个工厂的产量图表。
#include <iostream>
#include <cmath>
const int NUMBER_OF_PLANTS = 4;

void inputData(int a[], int lastNumber);
// 前置条件：lastNumber 是数组 a 的声明大小。
// 后置条件：对于 lastNumber = 1 到 lastNumber:
// a[lastNumber - 1] 等于工厂编号 Number 的总产量。

void scale(int a[], int size);
// 前置条件：a[i] 到[size-1] 每个都是非负值。
// 后置条件：a[i] 已被修改为 1000 的倍数（舍入到整数），
// 对于所有 i 0 <= i <= size - 1。

void graph(int asteriskCount[], int lastNumber);
// 前置条件：asteriskCount[0] 到 asteriskCount[lastNumber - 1]
// 是非负值。
// 后置条件：显示了一个条形图，说明工厂
// 号 N 生产了 asteriskCount[N - 1] 个 1000 单位，
// 对于每个满足条件的 N。
```

## 442 第7 章 / 数组

## 显示 7.8 生产图表程序（3/3 部分）
