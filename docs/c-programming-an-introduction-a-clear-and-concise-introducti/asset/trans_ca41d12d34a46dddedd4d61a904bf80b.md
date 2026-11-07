
| | | | | |
|---|---|---|---|---|
| 1 x 1 = 1 | 1 x 2 = 2 | 1 x 3 = 3 | 1 x 4 = 4 | 1 x 5 = 5 |
| 2 x 1 = 2 | 2 x 2 = 4 | 2 x 3 = 6 | 2 x 4 = 8 | 2 x 5 = 10 |
| 3 x 1 = 3 | 3 x 2 = 6 | 3 x 3 = 9 | 3 x 4 = 12 | 3 x 5 = 15 |
| 4 x 1 = 4 | 4 x 2 = 8 | 4 x 3 = 12 | 4 x 4 = 16 | 4 x 5 = 20 |
| 5 x 1 = 5 | 5 x 2 = 10 | 5 x 3 = 15 | 5 x 4 = 20 | 5 x 5 = 25 |

我们可以清楚地看到，行可以由一个 for 循环（内层循环）控制，列由另一个 for 循环（外层循环）控制。现在让我们看看这个程序：

```cpp
// ForLoop.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

int main(array<System::String ^> ^args)
{
    int product;
    for(int leftOp = 1; leftOp <= 5; ++leftOp)
    {
        for(int rightOp = 1; rightOp <= 5; ++rightOp)
        {
            product = leftOp * rightOp;
            cout << leftOp << " x " << rightOp << " = "
                 << product << "\t";
        }
        cout << endl;
    }
    Console::ReadKey();
    return 0;
}
```

以下是该程序的输出：

| | | | | |
|---|---|---|---|---|
| 1 x 1 = 1 | 1 x 2 = 2 | 1 x 3 = 3 | 1 x 4 = 4 | 1 x 5 = 5 |
| 2 x 1 = 2 | 2 x 2 = 4 | 2 x 3 = 6 | 2 x 4 = 8 | 2 x 5 = 10 |
| 3 x 1 = 3 | 3 x 2 = 6 | 3 x 3 = 9 | 3 x 4 = 12 | 3 x 5 = 15 |
| 4 x 1 = 4 | 4 x 2 = 8 | 4 x 3 = 12 | 4 x 4 = 16 | 4 x 5 = 20 |
| 5 x 1 = 5 | 5 x 2 = 10 | 5 x 3 = 15 | 5 x 4 = 20 | 5 x 5 = 25 |

每行中的间距由制表符（`\t`）控制。

在之前所有的 for 循环中，我们都使用单字母变量作为循环控制变量。这是可以接受的，因为阅读代码的人很容易理解该变量的用途。然而，对于这个程序，我们决定为循环控制变量使用更有意义的名称：leftOp 和 rightOp，因为这有助于读者更容易理解程序。

## 练习

- 1. 编写一个程序，要求用户输入一个数字，然后计算从 1 到该数字的平方和。例如，如果用户输入 4，则平方和为 30（1 + 4 + 9 + 16）。输出应包含用户输入的数字和结果。
- 2. 编写一个程序，从文件中读取一组数字，并显示文件中偶数的个数和奇数的个数。提示：使用 % 运算符判断一个数字是偶数还是奇数。
- 3. 编写一个程序，计算 16 到 36 范围内的偶数。在程序中使用 for 循环。
- 4. 使用 while 循环和 for 循环编写一个程序，从文件中读取一组数字，并为每个数字打印一串星号。输出应如下所示：

  ```
  5 -   *****
  10 -  **********
  7 -   *******
  ```

## 第8章：向量

到目前为止，我们讨论的数据类型适用于存储单个项。用于存储姓名的变量只能存储一个姓名；用于存储数字的变量只能存储一个数字。我们经常需要能够使用同一个变量名存储多个值。这个问题的一种解决方案是向量。向量允许我们在一个名称下存储多个相同数据类型的项。这种数据结构可以看作一个列表，例如成绩列表或姓名列表。

### 什么是向量？

如上所述，向量可以看作相同数据类型的数据项列表。列表中的每一项由列表中的索引位置指定。添加到向量的第一个项放在索引位置 0，下一项放在索引位置 1，再下一项放在索引位置 2，依此类推。

从图形上看，向量如下所示（第一列是索引，并且该向量被声明为最初有 10 个元素）：

| 索引 | 元素 |
|---:|---|
| 0 | 数据项 |
| 1 | 数据项 |
| 2 | 数据项 |
| 3 | 数据项 |
| 4 | 数据项 |
| 5 | 数据项 |
| 6 | 数据项 |
| 7 | 数据项 |
| 8 | 数据项 |
| 9 | 数据项 |

向量的一个特殊性质是，向量会自动增长以容纳添加到向量中的新项。这种能力将向量与数组区分开来，数组与向量类似，但不具备自动增长的能力。

### 创建向量

向量的声明方式很特殊。以下是向量声明的一般形式：

```cpp
vector<data type> vector-name(number of items, default-value);
```

在 C++ 程序中使用向量之前，必须提供一条预处理器指令，将 vector 类导入程序。将以下行添加到其他预处理器指令中：

```cpp
#include <vector>
```

向量声明以关键字 vector 开头。接下来是存储在向量中的元素的数据类型。数据类型括在小于号和大于号中，这种用法通常称为尖括号。你可以选择在圆括号内提供一个参数，指定最初要存储在向量中的项数。还可以选择为向量元素提供默认值。以下是一些向量声明的示例：

```cpp
// create string vector with 20 elements
vector<string> names(20);
// create integer vector with 100 elements
vector<int> numbers(100);
// create double vector with 0 elements
vector<double> ratios;
// create int vector all 0s
vector<int> numbers(100, 0);
```

### 向向量添加元素

向向量添加元素最常见的方法是使用类方法 push_back()。该方法将其参数放入向量中的下一个可用位置。以下示例演示如何创建一个新向量并向其中填充两个数据项：

```cpp
vector<string> names;
names.push_back("Raymond");
names.push_back("Jennifer");
```

该向量如下所示：

| | |
|---|---|
| 0 | Raymond |
| 1 | Jennifer |

使用 push_back() 添加的每个新数据项都直接放在之前添加的数据项之后。

以下代码片段允许用户通过交互式循环将姓名输入向量：

```cpp
char answer;
string name;
cout << "Do you want to enter names? ";
cin >> answer;
while (answer == 'y')
{
    cout << "Enter a name to store in the vector: ";
    getline(cin, name);
    names.push_back(name);
    cout << "Do you want to enter more names? ";
    cin >> answer;
}
```

### 访问向量元素

通过指定索引位置来访问向量元素。例如，以下行显示上面 names 向量中的第一个姓名：

```cpp
cout << names[0];
```

如果要访问向量的所有元素，请使用从向量的第一个元素开始、到最后一个元素结束的 for 循环。使用这种技术的一个问题是，你可能无法预先知道向量中最后一个元素的位置。你可以使用向量方法 size()，它返回当前向量中的元素个数。

以下程序将数字 1 到 10 存储在一个向量中，然后使用 for 循环对向量元素求和：

```cpp
// Vector.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <vector>
using namespace std;

int main(array<System::String ^> ^args)
{
    vector<int> numbers;
    for(int i = 1; i <= 10; ++i)
    {
        numbers.push_back(i);
    }
    int sum = 0;
    for(int i = 0; i < numbers.size(); ++i)
    {
        sum += numbers[i];
    }
    cout << "The sum of the integers 1 to 10 is: "
         << sum << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出为：

整数 1 到 10 的和为：55

为 `rand()` 函数设置种子后，就可以生成随机数了。你可能希望为随机数指定一个范围。为此，请使用以下公式：

```
rand() % maxNumber + 1
```

例如，如果你希望随机数范围是 1 到 100，可以使用以下语句生成随机数：

```cpp
// generate random number between 1 and 100
int randomNumber = rand() % 100 + 1;
```

将值加 1 可确保该函数可能生成范围内的最大值。

让我们看一个如何生成随机数的示例。以下程序可以作为儿童猜数字游戏的基础，用户尝试猜一个 1 到 10 之间的数字：

```cpp
// RandomNumber.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main(array<System::String ^> ^args)
{
    srand(time(NULL));
    int numberToGuess = rand() % 10 + 1;
    int guess;
    cout << "Enter a guess: ";
    cin >> guess;
}
```
