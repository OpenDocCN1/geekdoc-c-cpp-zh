

## F.1. 声明与使用数组

```cpp
int x;
int v[10]; // 创建一个有 10 个可用空间的数组
cin >> x; // 用户在运行时输入 x
v[x] = 1; // 这样可以吗？x 是什么？
```

编译器无法预测用户输入什么数字。这意味着误用索引可能会导致运行时错误。为了说明这一点，请考虑列表 F.1 (arrayoutofbounds.cpp)。

# Listing E.1: arrayoutofbounds.cpp

```cpp
#include <iostream>
using namespace std;

int main() {
    const int SIZE = 3;
    int a[SIZE] = { 5, 5, 5 };
    // 打印数组的内容
    cout << "contains: ";
    for (int i = 0; i < SIZE; i++)
        cout << a[i] << " ";
    cout << endl;
    // 将数组中的 5 改为 8
    for (int i = 0; i <= SIZE; i++) // 错误：应该是 <
        a[i] = 8;
    // 打印数组的内容
    cout << "contains: ";
    for (int i = 0; i < SIZE; i++)
        cout << a[i] << " ";
    cout << endl;
}
```

列表 F.1 (arrayoutofbounds.cpp) 包含一个逻辑错误，重新赋值循环越过了数组 a 的末尾。访问数组边界之外的元素被称为**未定义行为**（undefined behavior）。C++ 语言标准使用该术语表示程序的行为未规定，编译器编写者可以随心所欲。可能的行为包括：

- 编译后的代码可以检查索引是否在范围内，并产生一个智能的运行时错误消息，
- 程序可能会其妙地崩溃。
- 程序可能会继续运行而没有任何问题迹象，并且大多数时候表现得正常，

或者任何其他可能的可能。在其他情况下，实际的程序行为取决于系统和编译器。表现出未定义行为的程序中的代码被视为逻辑错误，因为它的行为在不同平台和编译器之间是不一致的。简单来说，程序的行为是不可预测的。不可预测的行为是不正确的。

在大多数情况下，越界访问访问数组外部的内存。这包括不属于执行程序的内存；现代操作系统会杀死该程序并产生某些错误消息。在 Visual C++ 中，当程序被编译为调试版本时，程序首先打印数组的内容，但在第二次打印之前就会崩溃。Microsoft Windows 随后会显示图 11.4 所示的对话框。在 Linux 或 OS X 下运行的程序可能会在终端打印：

## F.2. 数组与函数

```cpp
Segmentation fault
```

如果你的程序正在使用数组，并以此类消息终止，你应该仔细检查其源代码，查找可能发生数组越界访问的地方。

以下代码片段展示了一些正确和不适当的数组访问：

```cpp
int numbers[10];      // 声明数组
numbers[0] = 5;      // 将值 5 放在第一个
numbers[9] = 2;      // 将值 2 放在最后一个
numbers[-1] = 5;     // 越界；第一个有效索引是 0
numbers[10] = 5;     // 越界；最后一个有效索引是 9
numbers[1.3] = 5;    // 越界；1.3 不是整数
```

注意注释检查了索引的类型是否为有效表达式。

在如下带有 for 循环的数组中

```cpp
for (int i = 0; i < SIZE; i++)
    cout << a[i] << endl;
```

很容易确保 x 越出数组边界，但在使用任意值之前应该进行检查：

```cpp
int x;
int a[10];            // 创建一个有 10 个可用空间的数组
cin >> x;             // 用户运行时输入 x
if (0 < x && x < 10) // 确保 x 在数组范围内
    a[x] = 1;         // 现在是安全的
else
    cout << "Index provided is out of range" << endl;
```

在这里，if 语句确保数组访问在数组边界内。

### F.2. 数组与函数

数组可以传递给函数，如列表 F.2 (arraytoofunc.cpp) 所示

# Listing F.2: arraytoofunc.cpp
```cpp
#include <iostream>

using namespace std;

/*
* print(a, n)
* 打印 int 数组的内容
* a 是要打印的数组
* n 是数组的大小
*/

## F.2. 数组与函数

```cpp
void print(int a[], int n) {
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
}

/* sum(a, n)
* 累加 int 数组的内容
* a 是要求和的数组
* n 是数组的大小
*/

int sum(int a[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++)
        result += a[i];
    return result;
}

int main() {
    int list[] = { 2, 4, 6, 8 };
    // 打印数组的内容
    print(list, 4);
    // 计算并显示和
    cout << sum(list, 4) << endl;
    // 将 list 的元素置零
    for (int i = 0; i < 4; i++)
        list[i] = 0;
    // 再次打印数组的内容
    print(list, 4);
    // 计算并显示和
    cout << sum(list, 4) << endl;
}
```

如 print 函数的定义所示

```cpp
void print(int a[], int n)
```

当声明数组参数时，其方括号是空的。程序员可以在方括号内提供数字，但编译器会忽略它。调用接受数组参数的函数时

```cpp
print(list, 4);
```

程序员必须随数组名称传递大小。这是因为数组仅仅表示内存块，没有大小的概念。因此，当通过引用传递数组时（如 F.2 arraytoofunc.cpp 所示），方括号是空的。## F.2 数组与函数

列表 F.3 (cleararray.cpp) 的输出显示函数可以读取内容但不修改它们。为了保护数组不受损坏，参数必须声明为 `const`。

# Listing F.3: cleararray.cpp
```cpp
#include <iostream>

using namespace std;

/*
* print(a, n)
* 打印 int 数组的内容
* a 是要打印的数组
* n 是数组的大小
*/
void print(int a[], int n) {
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
}

/* sum(a, n)
* 累加 int 数组的内容
* a 是要求和的数组
* n 是数组的大小
*/

int sum(int a[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++)
        result += a[i];
    return result;
}

int main() {
    int list[] = { 2, 4, 6, 8 };
    // 打印数组的内容
    print(list, 4);
    // 计算并显示和
    cout << sum(list, 4) << endl;
    // 将 list 的元素置零
    for (int i = 0; i < 4; i++)
        list[i] = 0;
    // 再次打印数组的内容
    print(list, 4);
    // 计算并显示和
    cout << sum(list, 4) << endl;
}
```

在其他情况下，实际程序的行为取决于系统和编译器。表现出未定义行为的程序代码被视为逻辑错误，因为它的行为在不同平台和编译器之间是不一致的。简单来说，程序的行为是不可预测的。不可预测的行为是不正确的。

在大多数情况下，越界访问访问数组外部的内存。这包括不属于执行程序的内存；现代操作系统会杀死程序并产生某些错误消息。在 Visual C++ 中，当程序被编译为调试版本时，程序首先打印数组的内容，但在第二次打印之前就会崩溃。Microsoft Windows 随后会显示图 11.4 所示的对话框。在 Linux 或 OS X 下运行的程序可能会在终端打印：

```cpp
Segmentation fault
```

如果你的程序正在使用数组，并以此消息终止，你应该仔细检查其源代码，查找可能发生数组越界访问的地方。

以下代码片段展示了一些正确和不适当的数组访问：

```cpp
int numbers[10];      // 声明数组
numbers[0] = 5;      // 将值 5 放在第一个
numbers[9] = 2;      // 将值 2 放在最后一个
numbers[-1] = 5;     // 越界；第一个有效索引是 0
numbers[10] = 5;     // 越界；最后一个有效索引是 9
numbers[1.3] = 5;    // 越界；1.3 不是整数
```

注意注释检查了索引的类型是否为有效表达式。

在如下带有 for 循环的数组中

```cpp
for (int i = 0; i < SIZE; i++)
    cout << a[i] << endl;
```

很容易确保 x 越出数组边界，但在使用任意值之前应该进行检查：

```cpp
int x;
int a[10];            // 创建一个有 10 个可用空间的数组
cin >> x;             // 用户运行时输入 x
if (0 < x && x < 10) // 确保 x 在数组范围内
    a[x] = 1;         // 现在是安全的
else
    cout << "Index provided is out of range" << endl;
```

在这里，if 语句确保数组访问在数组边界内。

数组可以传递给函数，如列表 F.2 (arraytoofunc.cpp) 所示

# Listing F.2: arraytoofunc.cpp
```cpp
#include <iostream>

using namespace std;

/*
* print(a, n)
* 打印 int 数组的内容
* a 是要打印的数组
* n 是数组的大小
*/

void print(int a[], int n) {
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
}

/* sum(a, n)
* 累加 int 数组的内容
* a 是要求和的数组
* n 是数组的大小
*/

int sum(int a[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++)
        result += a[i];
    return result;
}

int main() {
    int list[] = { 2, 4, 6, 8 };
    // 打印数组的内容
    print(list, 4);
    // 计算并显示和
    cout << sum(list, 4) << endl;
    // 将 list 的元素置零
    for (int i = 0; i < 4; i++)
        list[i] = 0;
    // 再次打印数组的内容
    print(list, 4);
    // 计算并显示和
    cout << sum(list, 4) << endl;
}
```

