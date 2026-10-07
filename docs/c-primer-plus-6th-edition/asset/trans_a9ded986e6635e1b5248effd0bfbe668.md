
## 第 7 章 函数：C++ 编程模块

消息提醒你，C++ 将声明 `const double ar[]` 解释为 `const double *ar`。因此，该声明表示 `ar` 指向一个常量值。我们将在完成当前示例后详细讨论这一点。与此同时，这里是 `show_array()` 函数的代码：

```cpp
void show_array(const double ar[], int n)
{
    using namespace std;
    for (int i = 0; i < n; i++) {
        cout << "Property #" << (i + 1) << ": ";
        cout << ar[i] << endl;
    }
}
```

## 修改数组

此示例中，数组的第三种操作是将每个元素乘以相同的重估因子。你需要向函数传递三个参数：因子、数组和元素个数。不需要返回值，所以函数可以像像所示：

```cpp
void revalue(double r, double ar[], int n)
{
    for (int i = 0; i < n; i++) {
        ar[i] *= r;
    }
}
```

因为这个函数旨在修改数组值，所以你在声明 `ar` 时不使用 `const`。

## 将部分组合在一起

现在你已经根据数据的存储方式（数组）和使用方式（三个函数）定义了数据类型，你可以组合出一个已经构建了所有数组处理工具的程序，这极地简化了 `main()` 的编程。程序的作用是检查用户对重估因子的提示响应是否为数字。在这种情况下，程序并没有在用户编译失败时停止，而是使用循环要求用户进行正确操作。剩余的大部分编程工作由 `main()` 调用你刚刚开发的函数组成。列表 7.7 显示了结果。它仅在那些 `iostream` 的函数中放置了 `using` 指令。

列表 7.7 arrfun3.cpp

```cpp
// arrfun3.cpp array functions and const
#include <iostream>
const int Max = 5;

// 函数原型
int fill_array(double ar[], int limit);
void show_array(const double ar[], int n); // 不修改数据
void revalue(double r, double ar[], int n);

int main() {
    using namespace std;
    double properties[Max];

    int size = fill_array(properties, Max);
    show_array(properties, size);
    if (size > 0) {
        cout << "Enter revaluation factor: ";
        double factor;
        while (!(cin >> factor)) // 输入错误 {
            cin.clear();
            while (cin.get() != '\n')
                continue;
            cout << "Bad input; Please enter a number: ";
        }
        revalue(factor, properties, size);
        show_array(properties, size);
    }
    cout << "Done.\n";
    cin.get();
    cin.get();
    return 0;
}

int fill_array(double ar[], int limit) {
    using namespace std;
    double temp;
    int i;
    for (i = 0; i < limit; i++) {
        cout << "Enter value #" << (i + 1) << ": ";
        if (!(cin)) // 输入错误 {
            cin.clear();
            while (cin.get() != '\n')
                continue;
            cout << "Bad input; input process terminated.\n";
            break;
        }
        cin >> temp;
        if (temp < 0) // 终止信号
            break;
        ar[i] = temp;
    }
    return i;
}

// 下一个函数可以使用，但不能修改
// 地址为 ar 的数组
void show_array(const double ar[], int n)
{
    using namespace std;
    for (int i = 0; i < n; i++) {
        cout << "Property #" << (i + 1) << ": ";
        cout << ar[i] << endl;
    }
}

// 将 ar[] 的每个元素乘以 r
void revalue(double r, double ar[], int n)
{
    for (int i = 0; i < n; i++) {
        ar[i] *= r;
    }
}
```

该程序有两个示例运行结果：

Enter value #1: 10
Enter value #2: 20
Enter value #3: 30
Enter value #4: 40
Enter value #5: 50
Property #1: 10
Property #2: 20
Property #3: 30
Property #4: 40
Property #5: 50
Enter revaluation factor: 0.5
Property #1: 5
Property #2: 10
Property #3: 15
Property #4: 20
Property #5: 25
Done.

Enter value #1: 10
Enter value #2: 20
Enter value #3: 30
Enter value #4: -1
Property #1: 10
Property #2: 20
Property #3: 30
Enter revaluation factor: 2.0
Property #1: 20
Property #2: 40
Property #3: 60
Done.

回 `fill_array()` 规定当用户输入负数时输入应停止。第一个输出示例说明了属性限制，第二个输出示例说明了输入阶段。

## 编程笔记

我们已经讨论了与数组示例相关的重要编程细节，让我们反思一下这个过程。你从考虑数据类型开始并设计了适当的函数来处理数据。然后你将它们组合成程序。这有时被称为自底而上的编程，因为设计过程是从组件到整体。这种方法非常适合面向对象编程（OOP），因为它首先关注数据表示和操纵。另一方面，传统的过程化编程倾向于自顶而下的编程，即先开发设计，然后关注细节。

## 数组函数惯例

假设你想让一个函数处理 `double` 类型的数组。如果该函数旨在修改数组，原型可能如下：

```cpp
void f_modify(double array[], int n);
```

如果函数保留值，则原型可能如下：

```cpp
void f_no_change(const double array[], int n);
```

当然，你可以省略原型中的变量名，且返回类型可以是 `void`。要点是数组是指向第一个元素的指针，只要是 `double` 数组，就可以使用任何大小的数组：

```cpp
double rewards[1000];
double faults[50];
f_modify(rewards, 1000);
f_modify(faults, 50);
```

这种惯例（将数组名和大小作为参数）通过传递两个数字——数组地址和元素个数来工作。正如你所见，函数丢失了关于原始数组的某些知识；它依赖于传递正确的元素个数。

## 函数范围

正如你所见，处理数组的 C++ 函数需要了解数组的数据类型、数组的起始位置以及元素的个数。传统的 C/C++ 处理数组的方法是将数组起始指针作为第一个参数，并将数组的大小作为第二个参数。（指针告诉函数在哪里找到数组以及其中的数据类型。）这为函数提供了所需的所有信息。

另一种赋予函数所需信息的方法是指定元素范围。这可以通过传递两个指针来实现——一个标识数组开始，另一个标识数组结束。C++ 标准模板库（STL，在第 16 章“字符串类与模板库”中介绍）扩展了范围方法。STL 方法使用“末尾之后”的概念来指示范围。也就是说，在数组的情况下，标识数组结束的指针是最后一个元素之后的位置。例如，假设你有如下声明：

```cpp
double element[20];
```

那么两个指针 `element` 和 `element + 20` 定义了范围。首先，`element` 作为数组名，指向第一个元素。表达式 `element + 19` 指向最后一个元素（即 `element[19]`），所以 `element + 20` 指向数组末尾之后。向函数传递范围可以告诉要处理哪些元素。列表 7.8 修改了列表 7.6，使用两个指针来指定范围。

## 列表 7.8 arrfun4.cpp

```cpp
// arrfun4.cpp 使用范围的函数
#include <iostream>
const int ArSize = 8;
int sum_arr(const int * begin, const int * end);
int main()
{
    using namespace std;
    int cookies[ArSize] = {1,2,4,8,16,32,64,128};
    // 一些系统要求在 int 前加 static 以 启用数组初始化

    int sum = sum_arr(cookies, cookies + ArSize);
    cout << "Total cookies eaten: " << sum << endl;
    sum = sum_arr(cookies, cookies + 3); // 前三个元素
    cout << "First three eaters ate " << sum << " cookies.\n";
}
```
