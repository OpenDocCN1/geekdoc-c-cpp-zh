

![](img/d61019b035dd82beb581604273c0ee6b_398_0.png)

## 图 10 高尔顿板阵列中小球的运动

下面的程序给出了详细实现。在示例程序运行中，请注意 1,000 个小球如何击中顶部钉子，以及最底部一排钉子如何近似呈现钟形曲线分布。

### sec05/galton.cpp

```cpp
#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <ctime>

using namespace std;

int main()
{
    srand(time(0));
    const int SIZE = 10;

    int* counts[SIZE];

    // Allocate the rows
    for (int i = 0; i < SIZE; i++)
    {
        counts[i] = new int[i + 1];
        for (int j = 0; j <= i; j++)
        {
            counts[i][j] = 0;
        }
    }

    const int RUNS = 1000;

    // Simulate 1,000 balls
    for (int run = 0; run < RUNS; run++)
    {
        // Add a ball to the top
        counts[0][0]++;
        // Have the ball run to the bottom
        int j = 0;
        for (int i = 1; i < 10; i++)
        {
            int r = rand() % 2;
            // If r is even, move down, otherwise to the right
            if (r == 1)
            {
                j++;
            }
            counts[i][j]++;
        }
    }

    // Print all counts
    for (int i = 0; i < SIZE; i++)
    {
        for (int j = 0; j <= i; j++)
        {
            cout << setw(4) << counts[i][j];
        }
        cout << endl;
    }

    // Deallocate the rows
    for (int i = 0; i < SIZE; i++)
    {
        delete[] counts[i];
    }

    return 0;
}
```

### 程序运行

1000
480 520
241 500 259
124 345 411 120
68 232 365 271 64
32 164 283 329 161 31
16 88 229 303 254 88 22
9 47 147 277 273 190 44 13
5 24 103 203 288 228 113 33 3
1 18 64 149 239 265 186 61 15 2

## 7.6 问题解决：绘制示意图

在设计使用指针的程序时，你需要可视化指针如何连接正在处理的数据。在大多数情况下，绘制一张显示这些连接的示意图是至关重要的。

首先从将通过指针访问或修改的数据开始。这些数据可能是账户余额、计数器、字符串或其他项目。重点关注指针所指向的内容。

然后绘制包含指针的变量。这些将成为你系统的前端。处理通常从指针开始，然后定位到实际数据。

最后，将指针绘制为箭头。如果指针在程序执行过程中会发生变化，请绘制一种典型的排列方式。绘制多张显示指针如何变化的示意图也很有用。

先绘制正在处理的数据，再绘制指针变量。绘制指针箭头时，展示一个典型的情形。

考虑以下问题：一所大学的媒体中心向教师和学生出借设备，如麦克风、线缆等。我们希望追踪每件物品的名称，以及借出该物品的用户姓名。

在本例中，被访问的数据是物品名称和用户名。我们将所有名称存储在一个较长的字符数组中，并在需要时将新名称添加到末尾。如果某个名称已经存在，我们不会重复存储。这是一种高效的字符串存储方式，前提是很少需要删除字符串。以下是该字符数组的一部分：

```
Microphone TX-10\0 Smith, Diane\0 Lee, Tim\0 Tape recorder\0 Mini DVI cable\0 ...
```

接下来，让我们绘制指向物品名称的指针。它们存储在一个名为 `items` 的指针数组中。有些物品可能具有相同的名称。在下面的示例中，我们有两个同名的麦克风。

![](img/d61019b035dd82beb581604273c0ee6b_400_0.png)

最后，还有一个并行的指针数组 `checked_out_to`，指向用户名。有时，物品可能被同一个用户借出。其他物品则根本没有被借出——用户名为空指针 `nullptr`。绘制示意图时，尽量包含所有情况的示例。

```
Microphone TX-10\0 Smith, Diane\0 Lee, Tim\0 Tape recorder\0 Mini DVI cable\0 ...
```

![](img/d61019b035dd82beb581604273c0ee6b_400_1.png)

现在你有了指针示意图，就可以用它来可视化对数据的操作。假设我们要打印一份当前所有已借出物品的报告。这可以通过访问两个数组中的所有指针来实现。指针 `items[i]` 给出物品名称，而 `checked_out_to[i]` 要么是 `nullptr`（这种情况下我们不希望包含该物品），要么是用户姓名。

由于使用指针进行编程较为复杂，每当使用指针时，都应绘制示意图。

![](img/d61019b035dd82beb581604273c0ee6b_401_0.png)

## 操作方法 7.1

### 使用指针

你使用指针是因为希望程序具有灵活性：即能够改变数据之间关系的能力。本操作方法将引导你完成使用指针时的决策过程。

### 问题陈述

我们将以一个模拟部门复印机部分控制逻辑的任务来说明这些步骤。复印的人输入一个用户编号。共有 100 个不同的用户，编号为 0 到 99。每个用户都链接到一个复印账户，要么是主账户，要么是十个项目账户之一。该链接由管理员维护，并且可能随着用户从事不同项目而发生变化。复印时，相应的账户应增加计数。

![](img/d61019b035dd82beb581604273c0ee6b_401_1.png)

© Bartosz Liszowski/iStockphoto.

用户在复印机控制面板上识别自己的身份。使用指针，用户与复印账户之间的关系可以很灵活。

### 第 1 步 绘制示意图。

如第 7.6 节所述，绘制一张显示程序中指针的示意图是一个好主意。

在我们的示例中，需要跟踪复印账户：一个主账户和十个项目账户。对于每个用户，我们需要一个指向复印账户的指针：

![](img/d61019b035dd82beb581604273c0ee6b_401_2.png)

### 第 2 步 声明指针变量。

这一步通常很简单。对于数值型数据，你会使用 `int*` 或 `double*` 类型的指针。如果操作字符数组，则使用 `char*` 指针。在第 10 章中，你将使用指向对象的指针。

```
double* account_pointer;
```

```
vector<char*> lines;
```

```
int* users[100];
```

### 第 3 步 使用变量地址或自由存储内存初始化指针。

你是要分配变量然后用 `&` 运算符获取它们的地址吗？如果你有固定数量的数据需要通过指针访问，这是可以的。否则，使用 `new` 运算符动态分配内存。完成后，务必使用 `delete` 或 `delete[]` 运算符释放内存。

在我们的示例中，不需要动态分配，因此我们只需获取变量的地址。

```
int master_account;
int project_accounts[10];
for (int i = 0; i < 100; i++)
{
    users[i] = &master_account;
}
// Here we reassign several users to project accounts.
// The following code is a simulation of the actions that would
// occur in an administration interface, which we do not implement.
users[2] = project_accounts + 1
users[3] = project_accounts + 2
users[99] = project_accounts + 2
```

### 第 4 步 使用 `*` 或 `[]` 运算符访问数据。

当通过指针访问单个变量时，使用 `*` 运算符读取或写入该变量。例如：

```
*account_pointer = *account_pointer + 20;
```

当你有指向数组的指针时，使用 `[]` 表示法。只需将指针视为数组即可：

```
account_array[i] = account_array[i] + 20;
```

如果你有一个指针数组或指针向量，则需要使用方括号获取单个指针，然后再使用另一个 `*` 或 `[]` 获取值。你在高尔顿板模拟器中见过一个示例，其中通过

```
counts[i][j]
```

访问了一个计数。

在实现算法时，请牢记这些访问规则。

在我们的示例中，我们读取用户 ID 和复印数量，然后增加相应的复印账户：

```
cin >> id >> copies;
*users[id] = *users[id] + copies;
```

练习 P7.2 要求你完成此模拟。

![](img/d61019b035dd82beb581604273c0ee6b_402_0.png)

## 工作示例 7.1

### 生成群发邮件

了解如何使用指针为群发邮件创建模板。请参阅你的电子文本或访问 wiley.com/go/bclo3。

