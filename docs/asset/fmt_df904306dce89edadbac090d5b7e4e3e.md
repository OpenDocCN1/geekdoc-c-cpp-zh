
Enter the employee ID you wish to search for: 199

That is found at element 4 in the array.

# 表 8-1 产品

| 产品标题 | 产品描述 | 产品编号 | 单价 |
|---|---|---|---|
| 领导力的六个步骤 | 书籍 | 914 | $12.95 |
| 领导力的六个步骤 | 音频 CD | 915 | $14.95 |
| 卓越之路 | DVD | 916 | $18.95 |
| 质量的七堂课 | 书籍 | 917 | $16.95 |
| 质量的七堂课 | 音频 CD | 918 | $21.95 |
| 质量的七堂课 | DVD | 919 | $31.95 |
| 团队是培养出来的不是生的 | 书籍 | 920 | $14.95 |
| 未来领导力 | 书籍 | 921 | $14.95 |
| 未来领导力 | 音频 CD | 922 | $16.95 |

电话营销小组的经理要求你编写一个程序，帮助订单输入员查询产品价格。该程序应提示用户输入产品编号，然后显示该产品的标题、描述和价格。

## 变量

表 8-2 列出了所需的变量：

## 表 8-2 变量

| 变量 | 描述 |
|---|---|
| `NUM_PRODS` | 常量型整数，初始化为 Demeters 力中心销售的产品数量。此值将用于程序数组的定义。 |
| `MIN_PRODNUM` | 常量型整数，初始化为最低产品编号。 |
| `MAX_PRODNUM` | 常量型整数，初始化为最高产品编号。 |
| `id` | 整数数组。存储每个产品编号。 |
| `title` | 字符串数组，初始化为产品标题。 |
| `description` | 字符串数组，初始化为每个产品的描述。 |
| `prices` | 双精度浮点数数组。存储每个产品的价格。 |

## 模块

程序将由表 8-3 列出的函数组成。

## 表 8-3 函数

| 函数 | 描述 |
|---|---|
| `main` | 程序的主函数。它调用程序的其他函数。 |
| `getProdNum` | 提示用户输入产品编号。该函数验证输入并拒绝任何超出正确产品编号范围的值。 |
| `binarySearch` | 标准二分查找例程。在数组中搜索指定值。如果找到该值，则返回其下标。如果没有找到，则返回 -1。 |
| `displayProd` | 使用标题、描述和价格数组的公共下标来显示产品的标题、描述和价格。 |

## 8.2 关注问题解决与程序设计：案例研究

### 函数 main

函数 `main` 包含变量定义并调用其他函数。以下是它的伪代码：

```
do
    调用 getProdNum
    调用 binarySearch
    如果 binarySearch 返回 -1
        通知用户未找到产品编号
    否则
        调用 displayProd
    结束 如果
    询问用户是否应该重复程序
当用户想要重复程序时
```

以下是其实际 C++ 代码：

```cpp
do
{
    // 获取所需的产品编号。
    prodNum = getProdNum();
    // 搜索产品编号。
    index = binarySearch(id, NUM_PRODS, prodNum);
    // 显示搜索结果。
    if (index == -1)
        cout << "That product number was not found.\n";
    else
        displayProd(title, description, prices, index);
    // 用户想再次执行此吗？
    cout << "Would you like to look up another product? (y/n) ";
    cin >> again // 'y'
} while (again == 'y' || again == 'Y');
```

命名常量 `NUM_PRODS` 是全局定义的，并初始化值为 9。数组 `id`、`title`、`description` 和 `prices` 已经初始化了数据。

### getProdNum 函数

`getProdNum` 函数提示用户输入产品编号。它会测试该值以确保它在 914-922 范围内（这些是有效的产品编号）。如果输入了无效值，它会被拒绝并再次提示用户。当输入有效的产品编号时，该函数返回它。伪代码如下所示。

```
显示输入产品编号的提示
读取 prodNum
当 prodNum 无效时
    显示错误信息
    读取 prodNum
结束 当
返回 prodNum
```

# 第 8 章 数组的搜索与排序

以下是实际的 C++ 代码：

```cpp
int getProdNum()
{
    int prodNum;
    cout << "Enter the item's product number: ";
    cin >> prodNum;
    // 验证输入。
    while (prodNum < MIN_PRODNUM || prodNum > MAX_PRODNUM)
    {
        cout << "Enter a number in the range of " << MIN_PRODNUM << " through " << MAX_PRODNUM << ".\n";
        cin >> prodNum;
    }
    return prodNum;
}
```

### binarySearch 函数

`binarySearch` 函数与本章之前讨论的函数相同。

### displayProd 函数

`displayProd` 函数具有名为 `title`、`desc`、`price` 和 `index` 的参数变量。这些变量接收标题、描述和价格数组以及一个下标值。该函数显示数据的标题、描述和价格。这里是 C++ 代码：

```cpp
void displayProd(const string title[], const string desc[], double price[], int index)
{
    cout << "Title: " << title[index] << endl;
    cout << "Description: " << desc[index] << endl;
    cout << "Price: " << price[index] << endl;
}
```

### 整个程序

该程序允许用户输入产品编号，然后显示产品的标题、描述和价格。

```cpp
#include <iostream>
#include <string>
using namespace std;

const int NUM_PRODS = 9; // 产品数量
const int MIN_PRODNUM = 914; // 最低编号
const int MAX_PRODNUM = 922; // 最高编号

// 函数原型声明
int getProdNum();
int binarySearch(const int [], int, int);
void displayProd(const string [], const string [], double [], int);

int main()
{
    // 编号数组
    int id[] = {914, 915, 916, 917, 918, 919, 920, 921, 922};
    // 标题数组
    string title[] = {
        "Six Steps to Leadership",
        "Six Steps to Leadership",
        "The Road to Excellence",
        "Seven Lessons of Quality",
        "Seven Lessons of Quality",
        "Seven Lessons of Quality",
        "Teams Are Made, Not Born",
        "Leadership for the Future",
        "Leadership for the Future"
    };
    // 描述数组
    string description[] = {
        "Book",
        "Audio CD",
        "DVD",
        "Book",
        "Audio CD",
        "DVD",
        "Book",
        "Book",
        "Audio CD"
    };
    // 价格数组
    double price[] = {12.95, 14.95, 18.95, 16.95, 21.95, 31.95, 14.95, 14.95, 16.95};

    int prodNum; // 用于产品编号
    int index; // 用于搜索结果
    char again; // 用于是否执行

    do
    {
        // 获取所需的产品编号。
        prodNum = getProdNum();
        // 搜索产品编号。
        index = binarySearch(id, NUM_PRODS, prodNum);

        // 显示搜索结果。
        if (index == -1)
        {
            cout << "That product number was not found.\n";
        }
        else
            displayProd(title, description, price, index);

        // 用户想再次执行此吗？
        cout << "Would you like to look up another product? (y/n) ";
        cin >> again;
    } while (again == 'y' || again == 'Y');

    return 0;
}
```

## 8.2 关注问题解决与程序设计：案例研究

```cpp
112
113
while (!found && first <= last)
  {
    middle = (first + last) / 2; // 计算中间位置
    if (array[middle] == value) // 如果中间找到了值
    {
      found = true;
      position = middle;
    }
    else if (array[middle] > value) // 如果值在左半部分
      last = middle - 1;
    else
      first = middle + 1; // 如果值在右半部分
  }
  return position;
}
```

```cpp
****************************************************************
// displayProd 函数接受三个数组和一个整数。
// 数组参数预期包含 main 函数中定义的标题、
// 描述和价格。index 参数
// 保存一个下标。该函数显示每个数组中在该下标处所包含的信息。
****************************************************************
void displayProd(const string title[], const string desc[],
                 double price[], int index) {
  cout << "Title: " << title[index] << endl;
  cout << "Description: " << desc[index] << endl;
  cout << "Price: " << price[index] << endl;
}
```

# 程序输出（示例输入已加粗显示）

输入产品编号：916 回车

标题：The Road to Excellence

描述：DVD

价格：$18.95

你想查询另一个产品吗？(y/n) 回车

输入产品编号：920 回车

标题：Teams Are Made, Not Born

描述：书

价格：$14.95

你想查询另一个产品吗？(y/n) 回车

# 节点

- 8.1 描述线性查找与二分查找之间的区别。
- 8.2 平均而言，对于一个拥有 20,000 个元素的数组，线性查找将执行多少次比较？（假设要查找的项目始终能在数组中找到。）

## 第 8 章 数组的搜索与排序

8.3 对于一个拥有 20,000 个元素的数组，二分查找执行的最大比较次数是多少？

8.4 如果对数组进行线性查找，且已知某些项目的查找频率高于其他项目，应如何重新排列数组的内容以提高搜索的平均性能？

## 8.3 关注软件工程：排序算法简介

概念：排序算法用于将数据按某种顺序排列。

# 排序算法

许多编程任务要求对数组中的数据按某种顺序排序。例如，客户列表通常按字母顺序排序。学生成绩可能从高到低排序，产品代码可以进行排序，使得所有相同颜色的产品存储在一起。为了对数组中的数据排序，程序员必须使用合适的排序算法。排序算法是一种遍历数组并按某种顺序重新排列内容的技术。

数组中的数据可以按升序或降序排序。如果数组按升序排序，意味着数组中的值是从低到高存储的。如果值按降序排序，则是从高到低存储的。本节将介绍两种简单的排序算法：冒泡排序和选择排序。

# 冒泡排序

冒泡排序按升序或降序排列数据的一种简单方法。它被称为冒泡排序算法是因为它通过遍历数组并比较元素，每一轮遍历中，某些值都会“泡”向数组的末尾。例如，如果你使用该算法按升序排序数组，较大的值会移向末尾。如果你使用该算法按降序排序数组，较小的值会移向末尾。在本节中，你将看到冒泡排序算法如何升序排序数组。

假设我们有一个如图8-1所示的数组。让我们看看如何使用冒泡排序将数组元素按升序排列。

## 图 8-1 数组

| 7 | 2 | 3 | 8 | 9 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

冒泡排序从比较数组的前两个元素开始。如果元素 0 大于元素 1，则交换它们。现在数组看起来如图 8-2 所示。

## 图 8-2 元素 0 和 1

| 2 | 7 | 3 | 8 | 9 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

冒泡排序继续比较下两个元素。如果元素 1 大于元素 2，则交换它们。现在数组看起来如图 8-3 所示。

## 图 8-3 元素 1 和 2

| 2 | 3 | 7 | 8 | 9 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

冒泡排序继续比较下两个元素。如果元素 2 大于元素 3，则交换它们。现在数组看起来如图 8-4 所示。

## 图 8-4 元素 2 和 3

| 2 | 3 | 8 | 7 | 9 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

冒泡排序继续比较下两个元素。如果元素 3 大于元素 4，则交换它们。现在数组看起来如图 8-5 所示。

## 图 8-5 元素 3 和 4

| 2 | 3 | 8 | 9 | 7 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

冒泡排序继续比较下两个元素。如果元素 4 大于元素 5，则交换它们。现在数组看起来如图 8-6 所示。

## 图 8-6 元素 4 和 5

| 2 | 3 | 8 | 9 | 1 | 7 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

第一轮遍历完成后，最大的元素（9）已处于其最终位置。对剩余元素重复此过程，直到整个数组排序完毕。

## 图 8-7 所有元素排序后的数组

| 1 | 2 | 3 | 7 | 8 | 9 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 元素 0 | 元素 1 | 元素 2 | 元素 3 | 元素 4 | 元素 5 |

## 8.3 关注软件工程：排序算法简介

```cpp
  if (array[index] > array[index + 1]) {
    swap(array[index], array[index + 1]);
  }
}
```

在第 3 行和第 4 行中，定义了以下局部变量：

- `maxElement` 变量将存储与其相邻元素比较的最后一个元素的下标。
- `index` 变量在其中一个循环中用数组下标。

函数使用了两个循环，一个嵌套在另一个内部。外层循环从第 6 行开始，如下：

```
for (maxElement = size - 1; maxElement > 0; maxElement--)
```
