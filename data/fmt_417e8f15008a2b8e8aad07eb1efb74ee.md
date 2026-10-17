
# 程序输出（加粗显示示例输入）

How many values do you wish to average? **4**[Enter]
Enter an integer value: **12**[Enter]
Enter an integer value: **3**[Enter]
Enter an integer value: **7**[Enter]
Enter an integer value: **9**[Enter]

# 程序输出（加粗显示不同示例输入）

How many values do you wish to average? **0**[Enter]
No values to average.
Average: 0

# Vector 成员函数总结

表 8-3 提供了我们讨论过的 `vector` 成员函数以及一些额外的函数总结。

| 成员函数 | 描述 |
| --- | --- |
| `at(position)` | 返回 `vector` 中位于 *position* 元素的值。<br>Example: `x = vect.at(5);` // 将 `vect[5]` 的值赋值给 `x`。 |
| `capacity()` | 返回 `vector` 在不重新分配内存可以存储的元素数量。（这与成员函数的返回值不同）<br>Example: `x = vect.capacity();` // 将 `vect` 的容量赋值给 `x`。 |
| `clear()` | 清空所有元素<br>Example: `vect.clear();` // 从 `vect` 中移除所有元素。 |
| `empty()` | 如果 `vector` 为空则返回 `true`，否则返回 `false`。<br>Example: `if (vect.empty())` // 如果 `vector` 为空 `cout << "The vector is empty.";` // 显示消息。 |
| `pop_back()` | 从 `vector` 中移除最后一个元素。<br>Example: `vect.pop_back();` // 移除 `vect` 的最后一个元素，大小减 1。 |
| `push_back(value)` | 将值存储在 `vector` 的最后一个元素中。如果 `vector` 已满或为空，则创建一个新元素。<br>Example: `vect.push_back(7);` // 将 7 存储在 `vect` 的最后一个元素中。 |
| `reverse()` | 反转 `vector` 中元素的顺序（最后一个变为第一个，第一个变为最后一个）。<br>Example: `vect.reverse();` // 反转 `vect` 中元素的顺序。 |
| `resize(n)` | 将 `vector` 调整为包含 `n` 个元素，其中 `n` 大于 `vector` 当前的大小。如果包含了可选值，则每个新元素将用该值初始化。<br>假设 `vect` 当前有四个元素：`vect.resize(6,99);` // 在 `vector` 末尾添加两个元素，每个都初始化为 99。 |
| `size()` | 返回 `vector` 中元素的数量。<br>Example: `numElements = vect.size();` |
| `swap(vector2)` | 交换该 `vector` 内容与 `vector2` 的内容。<br>Example: `vect1.swap(vect2);` // 交换 `vect1` 和 `vect2` 的内容。 |

# 8-31

```cpp
// 此程序使用了对象的对象的数组。
// 这些对象是 Circle 类的实例。
#include <iostream>
#include <iomanip>
#include "Circle.h" // Circle 类声明头文件
using namespace std;

const int NUM_CIRCLES = 4;

int main()
{
    Circle circle[NUM_CIRCLES]; // 定义一个 Circle 对象数组

    // 使用循环来初始化每个对象的半径
    for (int index = 0; index < NUM_CIRCLES; index++)
    {
    double radius;
    cout << "Enter the radius for circle " << (index+1) << ": ";
    cin >> radius;
    circle[index].setRadius(radius);
    }

    // 使用循环获取并打印每个对象的面积
    cout << fixed << setprecision(2);
    cout << "Here are the areas of the " << NUM_CIRCLES
        << " circles.\n";
    for (int index = 0; index < NUM_CIRCLES; index++)
    {
        cout << "circle" << (index+1) << setw(8)
            << circle[index].findArea() << endl;
    }
    return 0;
}
```

### 示例输入以加粗表示的程序输出

Enter the radius for circle 1: 0
Enter the radius for circle 2: 2
Enter the radius for circle 3: 2.5
Enter the radius for circle 4: 10

Here are the areas of the 4 circles.
circle 1     0.00
circle 2     12.56
circle 3     19.63
circle 4     314.00

> 注意：每当在没有构造函数参数的情况下创建对象数组时，如果默认构造函数存在，它将为数组中的每个对象运行。这在程序 8-31 中就发生了。

## 第 8 章 数组

当第一次创建 `Circle` 对象数组时，默认构造函数为数组中的每个对象执行一次，并将其半径赋值为 1.0。我们从未见过这一现象，因为对每个对象的 `setRadius` 成员函数的调用将它的 1.0 替换为传递给 `setRadius` 的新值。如果我们注释掉程序 8-31 的第 15 到 20 行，则不会对 `setRadius` 进行任何调用。因此，当执行第 26 到 29 行的循环打印面积时，数组中的每个对象半径仍为 1.0。输出将如下所示：

Here are the areas of the 4 circles.
circle 1 3.14
circle 2 3.14
circle 3 3.14
circle 4 3.14

此版本的程序 8-31 可以在书籍配套资料的第 8 章文件夹中找到，文件名为 `pr8-31B.cpp`。
也可以创建一个为每个对象调用另一个构造函数的对象数组。要实现此点，我们使用初始化列表。下面的数组定义和初始化列表初始化了四个 `Circle` 对象，并将它们初始化为与原始程序 8-31 运行结果相同的四个值。

```cpp
Circle circle[NUM_CIRCLES] = {0.0, 2.0, 2.5, 10.0};
```

这调用了接受一个 `double` 参数的构造函数，并设置了此处显示的半径。

| 对象 | 半径 |
| :--- | :--- |
| `circle[0]` | 0.0 |
| `circle[1]` | 2.0 |
| `circle[2]` | 2.5 |
| `circle[3]` | 10.0 |

如果初始化列表比对象数量短，任何剩余对象将由默认构造函数初始化。例如，以下语句为前三个对象调用接受一个 `double` 参数的构造函数，而第四个对象被分配了默认半径 1.0。
`Circle circle[NUM_CIRCLES] = {0.0, 2.0, 2.5};`
这在程序 8-32 中得到了阐明。

## 程序 8-32

```cpp
// 此程序演示了在创建对象数组时
// 重载构造函数是如何工作的。
#include <iostream>
#include <iomanip>
#include "Circle.h" // Circle 类声明头文件
using namespace std;
```

（程序继续）

## 8.13 对象数组

## 8-32（续）

```cpp
const int NUM_CIRCLES = 4;

int main()
{
    // 定义一个包含 4 个 Circle 对象的数组。使用初始化列表
    // 调用 1 个参数的构造函数
    Circle circle[NUM_CIRCLES] = {0.0, 2.0, 2.5};

    // 显示对象的面积
    cout << fixed << setprecision(2);
    cout << "Here are the areas of the " << NUM_CIRCLES
         << " circles.\n";
    for (int index = 0; index < NUM_CIRCLES; index++)
        cout << "circle" << (index+1) << setw(8)
            << circle[index].findArea() << endl;
    return 0;
}
```

### 程序输出

```
Here are the areas of the 4 circles.
circle 1 0.00
circle 2 12.56
circle 3 19.63
circle 4 314.00
```

要调用接受一个 `double` 参数的构造函数，对于前三个对象是这样做的，而第四个对象被分配了默认半径 1.0。
这在程序 8-32 中得到了阐明。

就像访问类对象一样访问它们。你可以通过简单地在下标后使用点运算符和成员名称来访问元素的成员。例如，以下表达式引用了 `bookList[5]` 的标题：

```
bookList[5].title
```

以下循环遍历数组，显示存储在每个元素中的数据：

```
for (int index = 0; index < 20; index++)
{
    cout << bookList[index].title << endl;
    cout << bookList[index].author << endl;
    cout << bookList[index].publisher << endl;
    cout << bookList[index].price << endl;
}
```

由于成员 `title`、`author` 和 `publisher` 是字符串对象，因此也可以访问构成字符串的单个字符。以下语句显示 `bookList[10]` 标题的第一个字符：

```
cout << bookList[10].title[0];
```

接下来的语句将字符 't' 存储在 `bookList[2]` `publisher` 成员的第四个位置：

```
bookList[2].publisher[3] = 't';
```

程序 8-33 是程序 8-15 的修改版本，用于计算并显示一组员工的工资信息。原始程序使用两个数组来存储员工的工时间和薪资率。此修改版本使用单个结构体数组。

## 程序 8-33

```
1 // 此程序使用结构体数组存储工资数据。
2 #include <iostream>
3 #include <iomanip>
4 using namespace std;
5
6 struct PayInfo    // 定义一个包含 2 个变量的结构体
7 {
8     int hours;         // 工时长
9     double payRate      // 小时薪资
10};
11
12 int main()
13 {
14 const int NUM_EMPS = 3;    // 员工人数
15 PayInfo workers[NUM_EMPS]; // 定义 PayInfo 结构体数组
16 double grossPay;
17
18 // 获取工资数据
19 cout << "Enter the hours worked and hourly pay rates of \n"
20 cout << NUM_EMPS << " employees.\n";
21
```

（程序继续）

## 程序 8-33（续）

```
| 22 | for (int index = 0; index < NUM_EMPS; index++) |
| 23 | { cout << "\nHours worked by employee #" << (index + 1) << ": "; |
| 24 | cin >> workers[index].hours; |
| 25 | cout << "Hourly pay rate for this employee: $"; |
| 26 | cin >> workers[index].payRate; |
| 27 | } |
| 28 | // 显示每位员工的总工资 |
| 29 | cout << "\nHere is the gross pay for each employee:\n"; |
| 30 | cout << fixed << setw(2) << grossPay |
| 31 | |
| 32 | for (int index = 0; index < NUM_EMPS; index++) { |
| 33 | grossPay = workers[index].hours * workers[index].payRate; |
| 34 | cout << "Employee #" << (index + 1) << ": $" << setw(7) << grossPay << endl; |
| 35 | } |
| 36 | return 0; |
| 37 | } |
```

### 程序输出（示例输入加粗显示）

输入 3 名员工的工时间和每小时薪资。

员工 #1 的工时长：**10[回]**

该员工的小时薪资：**$9.75[回]**

员工 #2 的工时长：**15[回]**

该员工的小时薪资：**$8.65[回]**
