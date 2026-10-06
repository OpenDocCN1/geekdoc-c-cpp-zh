
```cpp
delete [] ptr;
}
```

*****************************************************
// memError 函数。内存分配失败时显示错误信息并
// 终止程序。
*****************************************************

```cpp
template <class T>
void SimpleVector<T>::memError()
{
    cout << "ERROR: Cannot allocate memory.\n";
    exit(EXIT_FAILURE);
}
```

*****************************************************
// subError 函数。下标越界时显示错误信息并
// 终止程序。
*****************************************************

```cpp
template <class T>
void SimpleVector<T>::subError()
{
    cout << "ERROR: Subscript out of range.\n";
    exit(EXIT_FAILURE);
}
```

*****************************************************
// getElement 函数。参数是下标。
// 该函数返回数组中该下标处存储的
// 值。
*****************************************************

```cpp
template <class T>
T SimpleVector<T>::getElementAt(int sub)
{
    if (sub < 0 || sub >= arraySize)
        subError();
    return ptr[sub];
}
```

*****************************************************
// 重载的 [] 运算符。参数是下标。
// 该函数返回通过下标索引的
// 元素的引用。
*****************************************************

```cpp
template <class T>
T &SimpleVector<T>::operator[](const int &sub)
{
    if (sub < 0 || sub >= arraySize)
        subError();
    return ptr[sub];
}
```

注意：`Array` 变量被声明为 `int`，因为它持有数组的大小。这就是为什么成员函数返回 `int`。

### 定义类模板对象

类模板对象的定义与普通类相似，区别在于必须指定传递的类型。在紧跟类名的角括号内指定。例如，以下语句创建了 `intTable` 和 `doubleTable`：

```cpp
SimpleVector<int> intTable(10);
SimpleVector<double> doubleTable(10);
```

### 程序 16-11

此程序演示了 `SimpleVector` 模板。

```cpp
#include <iostream>
#include "SimpleVector.h"
using namespace std;

int main() {
    const int SIZE = 10; // 元素的数量
    int count;

    // 创建 int 类型的 SimpleVector
    SimpleVector<int> intTable(SIZE);

    // 创建 double 类型的 SimpleVector
    SimpleVector<double> doubleTable(SIZE);

    // 存储值
    for (count = 0; count < SIZE; count++) {
        intTable[count] = intTable[count] * 2;
        doubleTable[count] = doubleTable[count] * 2.0;
    }

    // 显示 SimpleVector 的值
    cout << "These values are in intTable:\n";
    for (count = 0; count < SIZE; count++) {
        cout << intTable[count] << " ";
    }
    cout << endl;

    cout << "These values are in doubleTable:\n";
    for (count = 0; count < SIZE; count++) {
        cout << doubleTable[count] << " ";
    }
    cout << endl;

    // 使用标准的 + 运算符处理元素
    for (count = 0; count < SIZE; count++) {
        intTable[count] = intTable[count] + 5;
        doubleTable[count] = doubleTable[count] + 5.0;
    }

    // 显示 SimpleVector 的值
    cout << "\nAdding 5 to each element of intTable and doubleTable:\n";
    for (count = 0; count < SIZE; count++) {
        cout << intTable[count] << " ";
    }
    cout << endl;

    cout << "These values are in doubleTable:\n";
    for (count = 0; count < SIZE; count++) {
        cout << doubleTable[count] << " ";
    }
    cout << endl;

    // 使用标准的 ++ 运算符处理元素
    for (count = 0; count < SIZE; count++) {
        intTable[count]++;
        doubleTable[count]++;
    }

    // 显示 SimpleVector 的值
    cout << "\nIncrementing each element of intTable and doubleTable:\n";
    for (count = 0; count < SIZE; count++) {
        cout << intTable[count] << " ";
    }
    cout << endl;

    cout << "These values are in doubleTable:\n";
    for (count = 0; count < SIZE; count++) {
        cout << doubleTable[count] << " ";
    }
    cout << endl;

    return 0;
}
```

# 程序输出

```
These values are in intTable:
0 2 4 6 8 10 12 14 16 18
These values are in doubleTable:
0 2.14 4.28 6.42 8.56 10.7 12.84 14.98 17.12 19.26 
Adding 5 to each element of intTable and doubleTable:
These values are in intTable:
5 7 9 11 13 15 17 19 21 23 
These values are in doubleTable:
5 7.14 9.28 11.42 13.56 15.7 17.84 19.98 22.12 24.26 
Incrementing each element of intTable and doubleTable:
These values are in intTable:
6 8 10 12 14 16 18 20 22 24 
These values are in doubleTable:
6 8.14 10.28 12.42 14.56 16.7 18.84 20.98 23.12 25.26 
```

# 类模板与继承

继承可以很容易地应用于类模板。例如，在下面的模板中，`SearchableVector` 派生自 `SimpleVector` 类。

## SearchableVector.h 的内容

```cpp
#ifndef SEARCHABLEVECTOR_H
#define SEARCHABLEVECTOR_H
#include "SimpleVector.h"

template <class T>
class SearchableVector : public SimpleVector<T>
{
public:
    // 默认构造函数
    SearchableVector() : SimpleVector<T>()
    { }

    // 构造函数
    SearchableVector(int size) : SimpleVector<T>(size)
    { }

    // 拷贝构造函数
    SearchableVector(const SearchableVector &);

    // 查找元素的访问器
    int findItem(const T);
};

/* // 拷贝构造函数 *********
template <class T>
SearchableVector<T>::SearchableVector(const SearchableVector &obj) :
SimpleVector<T>(obj.size)
{
    for (int count = 0; count <= this->size(); count++)
        this->operator[](count) = obj[count];
}

/* // findItem 函数 *
// 此函数搜索项。如果找到了项，
// 则返回下标。否则返回 -1。
**************************************************
template <class T>
int SearchableVector<T>::findItem(const T item)
{
    for (int count = 0; count <= this->size(); count++)
    {
        if (getElementAt(count) == item)
            return count;
    }
    return -1;
}
#endif
```

此类模板定义了 `SimpleVector` 类的可搜索版本。成员函数 `findItem` 接受一个参数，并执行线性搜索，以确定该参数的值是否存储在数组中。如果在数组中找到了该值，则返回它的下标。否则，返回 -1。

注意，每当在类模板中使用 `SimpleVector` 名称时，都会配合它使用参数 `T`。例如，这里是类声明的第一行（第 6 行），它将 `SimpleVector` 命名为基类：

```cpp
class SearchableVector : public SimpleVector<T>
```

此外，这里是类构造函数的函数头：

```cpp
SearchableVector() : SimpleVector<T>()
SearchableVector(int size) : SimpleVector<T>(size)
```

由于 `SimpleVector` 是一个类模板，类型参数必须传递给它。程序 16-12 通过在两个 `SearchableVector` 对象中存储值并在每个对象中搜索特定值来演示该类。

```cpp
// 此程序演示了 SearchableVector 模板。
#include <iostream>
#include "SearchableVector.h"
using namespace std;

int main() {
    const int SIZE = 10;      // 元素个数
    int count;               // 循环计数器
    int result;              // 用于存储搜索结果

    // 创建两个 SearchableVector 对象。
    SearchableVector<int> intTable(SIZE);
    SearchableVector<double> doubleTable(SIZE);

    // 在对象中存储值。
    for (int count = 0; count < SIZE; count++)
    {
        intTable[count] = (count * 2);
        doubleTable[count] = (count * 2.14);
    }
} // (程序继续)
```

## 程序 16-12（续）

```cpp
// 显示对象中的值。
cout << "These values are in intTable:\n";
for (int count = 0; count < SIZE; count++)
    cout << intTable[count] << " ";
cout << endl;

cout << "These values are in doubleTable:\n";
for (int count = 0; count < SIZE; count++)
    cout << doubleTable[count] << " ";
cout << endl;

// 在 intTable 中搜索值 6。
cout << "Searching for 6 in intTable:\n";
result = intTable.findItem(6);
if (result == -1)
    cout << "6 was not found in intTable:\n";
else
    cout << "6 was found at subscript " << result << endl;

// 在 doubleTable 中搜索值 12.84。
cout << "Searching for 12.84 in doubleTable:\n";
result = doubleTable.findItem(12.84);
if (result == -1)
    cout << "12.84 was not found in doubleTable:\n";
else
    cout << "12.84 was found at subscript " << result << endl;

return 0;
}
```

# 程序输出

```
These values are in intTable:
0 2 4 6 8 10 12 14 16 18
These values are in doubleTable:
0 2.14 4.28 6.42 8.56 10.70 12.84 14
Searching for 6 in intTable:
6 was found at subscript 3
Searching for 12.84 in doubleTable:
12.84 was found at subscript 6
```

## 特殊化模板

假设有一个适用于所有数据类型的模板，而特化模板是为特定类型设计的。例如，下面的 `Rectangle` 类：

```cpp
template <class T>
class Rectangle {
private:
    T width;
    T length;
public:
    void setData(T w, T l)
        { width = w; length = l; }
    T getWidth()
        { return width; }
    T getLength()
        { return length; }
};
```

# 检查点

假设定义如下类：

```cpp
template <class T>
```
