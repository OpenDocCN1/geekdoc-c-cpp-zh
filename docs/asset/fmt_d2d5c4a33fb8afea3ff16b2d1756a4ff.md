
# 14.5 运算符重载

## 重载 `==` 运算符

```cpp
bool FeetInches::operator == (const FeetInches &right)
{
    if (feet == right.feet && inches == right.inches)
        status = true;
    else
        status = false;
    return status;
}
```

程序 14-10 展示了这些重载运算符。（该文件也可以在学生源代码文件夹第 14 章 FeetInches 版本 3 目录中找到。）

### 程序 14-10

```cpp
// 此程序演示了 FeetInches 类重载的运算符
// 关系运算符。
#include <iostream>
#include "FeetInches.h"
using namespace std;

int main() {
    int feet, inches; // 用于存储脚和英寸的输入

    // 创建两个 FeetInches 对象。构造函数的
    // 第、第二个参数默认值；
    FeetInches first, second;

    // 从用户处获取距离。
    cout << "Enter a distance in feet and inches: ";
    cin >> feet >> inches;

    // 将距离存储在 first 中。
    first.setFeet(feet);
    first.setInches(inches);

    // 获取另一个距离。
    cout << "Enter another distance in feet and inches: ";
    cin >> feet >> inches;

    // 将距离存储在 second 中。
    second.setFeet(feet);
    second.setInches(inches);

    // 比较两个对象。
    if (first == second)
        cout << "first is equal to second.\n";

    if (first > second)
        cout << "first is greater than second.\n";

    if (first < second)
        cout << "first is less than second.\n";

    return 0;
}
```

### 示例输入对应的程序输出

**输入：**
```
Enter a distance in feet and inches: 6 5
Enter another distance in feet and inches: 3 10
```

**输出：**
```
first is greater than second.
```

### 程序 14-10（续）

**输入：**
```
Enter a distance in feet and inches: 5 5
Enter another distance in feet and inches: 5 5
```

**输出：**
```
first is equal to second.
```

**输入：**
```
Enter a distance in feet and inches: 3 4
Enter another distance in feet and inches: 3 7
```

**输出：**
```
first is less than second.
```

## 重载 `<<` 和 `>>` 运算符

重载数学运算符和关系运算符让你能够像处理整数、浮点数和其他内置类型一样，自然地对类对象编写这些类型的表达式。然而，如果对象的主要数据成员是私有的，你仍然必须显式地调用成员函数来为它们赋值。例如，假设 `distance` 是 `FeetInches` 对象。以下语句显示了它的内部值：

```cpp
cout << distance.getFeet() << " feet, " << distance.getInches() << " inches";
```

同样需要调用成员函数来设置 `FeetInches` 对象的数据。例如，以下语句将距离对象设置为用户指定的值：

```cpp
cout << "Enter a value in feet: ";
cin >> f;
distance.setFeet(f);
cout << "Enter a value in inches: ";
cin >> i;
distance.setInches(i);
```

通过重载流插入运算符 (`<<`)，你可以像下面的代码所示将对象发送到 `cout`，并让屏幕以正确的格式输出。同样，通过重载流提取运算符 (`>>`)，距离对象可以直接从 `cin` 获取值。

然而，重载这些运算符的方法与重载其他运算符略有不同。这些运算符实际上是 C++ 运行时库定义的 `ostream` 和 `istream` 类的一部分。`cout` 和 `cin` 分别是 `ostream` 和 `istream` 的实例。你必须编写运算符函数来重载 `ostream` 版本的 `<<` 和 `istream` 版本的 `>>`，以便直接与 `FeetInches` 等类一起工作。学生源代码文件夹第 14 章 FeetInches 版本 4 中的 `FeetInches` 类包含了重载 `<<` 和 `>>` 运算符的函数。这里是重载 `<<` 运算符的函数：

```cpp
ostream& operator << (ostream& strm, const FeetInches &obj)
{
    strm << obj.feet << " feet, " << obj.inches << " inches";
    return strm;
}
```

注意，该函数有两个参数：一个 `ostream` 引用对象和一个 `FeetInches` 引用对象。`ostream` 参数是 `<<` 运算符左侧实际 `ostream` 对象的引用。第二个参数是 `FeetInches` 对象的引用。该参数将引用 `<<` 运算符右侧的对象。此函数告诉 C++ 如何处理任何具有以下形式的表达式：

```
ostreamObject << FeetInchesObject
```

因此，当 C++ 遇到以下语句时，它将调用重载的 `operator<<` 函数：

```cpp
cout << distance;
```

注意函数的返回类型是 `ostream`。这意味着当执行 `return strm;` 语句时，返回的不是 `strm` 的拷贝，而是它的引用。这允许你使用重载的 `<<` 运算符连接多个表达式，例如：

```cpp
cout << distance1 << " " << distance2 << endl;
```

这里是重载流提取运算符的函数：

```cpp
istream& operator >> (istream& strm, FeetInches &obj)
{
    strm >> obj.feet >> obj.inches;
    return strm;
}
```

相同的原理也适用于此运算符。函数返回 `istream` 对象的引用，因此可以将多个此类链在一起：

```cpp
cin >> distance1 >> distance2;
```

### 程序 14-11

```cpp
// 此程序演示了 FeetInches 类重载的 << 和 >> 运算符。
#include <iostream>
#include "FeetInches.h"
using namespace std;

int main() {
    FeetInches first, second;

    cout << "输入以英尺和英寸为单位的距离。\n";
    cout << "英尺: ";
    cin >> first;
    cout << "英寸: ";
    cin >> first; // 注意：原文逻辑可能有误，此处保留原文结构
    cout << "输入另一个以英尺和英寸为单位的距离。\n";
    cout << "英尺: ";
    cin >> second;
    cout << "英寸: ";
    cin >> second;

    cout << "输入的值为：\n";
    cout << first << " and " << second << endl;
    return 0;
}
```

### 带有示例输入的程序输出

**输入：**
```
输入以英尺和英寸为单位的距离。
英尺: 5
英寸: 5
输入另一个以英尺和英寸为单位的距离。
英尺: 10
英寸: 10
```

**输出：**
```
输入的值为：
5 feet, 5 inches and 10 feet, 10 inches
```

## 重载 `[]` 运算符

除了传统的运算符外，C++ 还允许你更改 `[]` 符号的工作方式。这让你能够编写具有类数组行为的类。例如，`string` 类重载了 `[]` 运算符，因此你可以访问存储在字符串类对象中的单个字符。假设程序中存在以下定义：

```cpp
string name = "William";
```

第一个字符 'W' 存储在 `name[0]` 中，因此以下语句将在屏幕上显示 W。

```cpp
cout << name[0];
```

你可以使用重载的 `[]` 运算符来创建一个数组类，如下所示。该类的行为类似于普通数组，但执行了 C++ 缺失的边界检查。

### IntArray.h 的内容

```cpp
// IntArray 类的规范文件
#ifndef INTARRAY_H
#define INTARRAY_H

class IntArray
{
private:
    int *ptr; // 指向数组的指针
    int arraySize; // 保存数组大小
    void subscriptError(); // 处理无效下标
public:
    IntArray(int); // 构造函数
    IntArray(const IntArray &); // 拷贝构造函数
    ~IntArray(); // 析构函数

    int size(void) const // 返回数组大小
    { return arraySize; }

    const IntArray& operator=(const IntArray &); // 重载 = 运算符
    int& operator[](const int &); // 重载 [] 运算符
};
#endif
```

### IntArray.cpp 的内容

```cpp
// IntArray 类的实现文件
#include <iostream>
#include <cstdlib> // 用于 exit 函数
#include "IntArray.h"
using namespace std;

// IntArray 类的构造函数。设置数组的大小并为其分配内存。
IntArray::IntArray(int s)
{
    arraySize = s;
    ptr = new int[s];
    for (int count = 0; count < arraySize; count++)
        *(ptr + count) = 0;
}

// IntArray 类的拷贝构造函数。
IntArray::IntArray(const IntArray &obj)
{
    arraySize = obj.arraySize;
    ptr = new int[arraySize];
    for (int count = 0; count < arraySize; count++)
        *(ptr + count) = *(obj.ptr + count);
}

// IntArray 类的析构函数。
IntArray::~IntArray()
{
    if (arraySize > 0)
        delete [] ptr;
}

// subscriptError 函数。当下标超出范围时，显示错误消息并终止程序。
void IntArray::subscriptError()
{
    cout << "ERROR: Subscript out of range.\n";
    exit(0);
}

// 重载的 = 运算符
const IntArray& IntArray::operator=(const IntArray &right)
{
    if (this != &right)
    {
        delete [] ptr;
        arraySize = right.arraySize;
        ptr = new int[arraySize];
        for (int count = 0; count < arraySize; count++)
            *(ptr + count) = *(right.ptr + count);
    }
    return *this;
}

// 重载的 [] 运算符。参数是一个下标。
// 此函数返回数组中由下标索引元素的引用。
int& IntArray::operator[](const int &sub)
{
    if (sub < 0 || sub >= arraySize)
        subscriptError();
    return ptr[sub];
}
```

在定义重载的 `[]` 运算符之前，让我们来看构造函数和析构函数。

**构造函数：**
```cpp
IntArray::IntArray(int s)
{
    arraySize = s;
    ptr = new int[s];
    for (int count = 0; count < arraySize; count++)
        *(ptr + count) = 0;
}
```
当定义类的实例时，所需的元素数量被传递给构造函数 `s`。`arraySize` 被赋值为 `s`。`ptr` 被分配了包含 `s` 个整数的数组。循环将数组中的每个元素初始化为 0。

**拷贝构造函数：**
```cpp
IntArray::IntArray(const IntArray &obj)
{
    arraySize = obj.arraySize;
    ptr = new int[arraySize];
    for (int count = 0; count < arraySize; count++)
        *(ptr + count) = *(obj.ptr + count);
}
```
该类还有一个拷贝构造函数，当使用另一个对象初始化时使用。

**析构函数：**
```cpp
IntArray::~IntArray()
{
    if (arraySize > 0)
        delete [] ptr;
}
```
如果 `arraySize` 大于 0，则会释放 `ptr` 指向的内存。

`subscriptError` 函数在下标超出范围时显示错误消息并终止程序。

**重载的 `=` 运算符：**
```cpp
const IntArray& IntArray::operator=(const IntArray &right)
{
    if (this != &right)
    {
        delete [] ptr;
        arraySize = right.arraySize;
        ptr = new int[arraySize];
        for (int count = 0; count < arraySize; count++)
            *(ptr + count) = *(right.ptr + count);
    }
    return *this;
}
```
它检查 `this` 是否等于 `right`，如果不等，则释放现有内存，拷贝 `arraySize` 并分配新内存，最后拷贝每个元素。
