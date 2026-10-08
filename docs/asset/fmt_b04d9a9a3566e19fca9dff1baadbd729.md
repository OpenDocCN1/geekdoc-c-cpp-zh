
## 显示 17.4 类模板 `GenericList` 的接口（部分 2/2）

```cpp
bool full() const;

// 如果列表已满，则返回 true。

void erase();

// 移除列表中的所有项，使列表为空。

friend ostream& operator << (ostream& outs,
    const GenericList<ItemType>& theList) {
    for (int i = 0; i < theList.currentLength; i++)
        outs << theList.item[i] << endl;
    return outs;
}// 重载了运算符 <<，使其能够输出列表的
// 内容。项按行输出。
// 前提条件：如果 outs 是文件输出流，则 outs 已经
// 连接到文件。
// 注意头文件中重载的 << 的具体实现！
// 这通常通过重载的友元模板完成。
// 由于 << 是友元函数，它不是类的成员，
// 而是在命名空间中，因此这是最简单的实现，
// 并且比放在 genericlist.cpp 中更有意义。

private:
    ItemType *item; // 指向持有列表的动态数组的指针。
    int maxLength; // 列表中允许的最大项数。
    int currentLength; // 列表中当前的项数。
};
```

## 显示 17.5 使用类模板 `GenericList` 的程序（部分 1/2）

```cpp
// 演示使用类模板 GenericList 的程序。
#include <iostream>
#include "genericlist.h"
#include "genericlist.cpp"
using namespace std;
using namespace listsavitch;

int main() {
    GenericList<int> firstList(2);
    firstList.add(1);
    firstList.add(2);
```

由于包含了 `genericlist.cpp`，你只需要编译此文件（带有 `main` 函数的那个）。

（续）

## 17.2 用于数据抽象的模板

## 显示 17.5 使用类模板 `GenericList` 的程序（部分 2/2）

```cpp
cout << "firstList = \n"
<< firstList;
GenericList<char> secondList(10);
secondList.add('A');
secondList.add('B');
secondList.add('C');
cout << "secondList = \n"
<< secondList;
return 0;
}
```

## 输出

```
firstList =
1
2
secondList =
A
B
C
```

## 显示 17.6 `GenericList` 的实现：`genericlist.cpp`（部分 1/2）

```cpp
// 这是实现文件：genericlist.cpp
// 这是名为 GenericList 的类模板的实现。
// 类模板 GenericList 的接口在
// 头文件 genericlist.h 中。
#ifndef GENERICLIST_CPP
#define GENERICLIST_CPP
#include <iostream>
#include <cstdlib>
#include "genericlist.h" // 当我们使用 using 包含此文件时，不需要它，
 // 但 genericlist.h 中的 #endif 确保了它是安全的。
using namespace std;
namespace listsavitch
{
// 使用类 ItemType
template<class ItemType>
GenericList<ItemType>::GenericList(int max) : maxLength(max),
currentLength(0)
```

（续）

## 显示 17.6 `GenericList` 的实现（部分 2/2）

```cpp
{
    item = new ItemType[max];
}
```

```cpp
template<class ItemType>
GenericList<ItemType>::~GenericList() {
    delete [] item;
}
```

```cpp
template<class ItemType>
int GenericList<ItemType>::length() const {
    return (currentLength);
}
```

```cpp
// 使用 iostream 和 cstdlib
template<class ItemType>
void GenericList<ItemType>::add(ItemType newItem) {
    if (full()) {
        cout << "Error: adding to a full list.\n";
        exit(1);
    } else {
        item[currentLength] = newItem;
        currentLength = currentLength + 1;
    }
}
```

```cpp
template<class ItemType>
bool GenericList<ItemType>::full() const {
    return (currentLength == maxLength);
}
```

```cpp
template<class ItemType>
void GenericList<ItemType>::erase() {
    currentLength = 0;
}
```

```cpp
//listsavitch
//endif // GENERICLIST_CPP 注意我们已经将所有模板
// 定义封装在 #ifndef.. #endif 中。
```

## 17.2 用于数据抽象的模板

关于编译显示 17.4、17.5 和 17.6 中的代码，需要说明一下。编译这些代码的有效解决方案是在使用之前 `#include` 模板类定义和模板函数定义，正如我们做的那样。在这种情况下，只需要编译显示 17.5 中的文件。请确保使用 `#ifndef #define` 机制来防止所有你将 `#include` 的文件被重复包含。

此外注意，重载运算符 `<<` 的实现被放在头文件中而不是实现文件中。这看起来不寻常，但在使用函数运算符或模板时非常常见。虽然我们将 `<<` 定义为 `GenericList` 的成员，但由于友元函数存在于类之外并属于命名空间。当从其他文件包含该类时，编译器将轻松找到 `<<` 的实现。

如果你想将重载运算符 `<<` 的实现从头文件中分离，那么需要一些额外的工作。我们必须对 `<<` 运算符进行前向声明，这需要 `GenericList` 类。。显示 17.7 展示了 `genericlist.h` 需要的更改，而显示 17.8 展示了 `genericlist.cpp` 的额外实现。

## 显示 17.7 不带实现的 `GenericList` 类模板接口（部分 1/2）

```cpp
// 此版本将重载 << 的实现移动到 .cpp 文件，
// 但需要添加前向声明。
#ifndef GENERICLIST_H
#define GENERICLIST_H
#include <iostream>
using namespace std;
namespace listsavitch{
    template<class ItemType>
    class GenericList;
    template<class ItemType>
    friend ostream& operator<<(ostream& outs, const GenericList<ItemType>& list);
}
#endif
```

（续）

## 显示 17.7 不带实现的 `GenericList` 类模板接口（部分 2/2）

```cpp
template<class ItemType>
class GenericList {
    ItemType *item;
    int maxLength;
    int currentLength;
public:
    GenericList(int max);
    ~GenericList();
    void add(ItemType newItem);
    bool full() const;
    void erase();
    int length() const;
    friend ostream& operator<<(ostream& outs, const GenericList<ItemType>& list);
};
```

## 显示 17.8 带重载运算符的 `GenericList`

```cpp
// 这是实现文件：genericlist.cpp
// 这是名为 GenericList 的类模板的实现。
// 类模板 GenericList 的接口在
// 头文件 genericlist.h 中。
#ifndef GENERICLIST_CPP
#define GENERICLIST_CPP
#include <iostream>
#include <cstdlib>
#include "genericlist.h" // 当我们使用 using 包含此文件时，不需要它，
 // 但 genericlist.h 中的 #endif 确保了它是安全的。
using namespace std;
namespace listsavitch
{
template<class ItemType>
GenericList<ItemType>::GenericList(int max) : maxLength(max),
currentLength(0)
{
    item = new ItemType[max];
}
template<class ItemType>
GenericList<ItemType>::~GenericList() {
    delete [] item;
}
template<class ItemType>
int GenericList<ItemType>::length() const {
    return (currentLength);
}
// 使用 iostream 和 cstdlib
template<class ItemType>
void GenericList<ItemType>::add(ItemType newItem) {
    if (full()) {
        cout << "Error: adding to a full list.\n";
        exit(1);
    } else {
        item[currentLength] = newItem;
        currentLength = currentLength + 1;
    }
}
template<class ItemType>
bool GenericList<ItemType>::full() const {
    return (currentLength == maxLength);
}
template<class ItemType>
void GenericList<ItemType>::erase() {
    currentLength = 0;
}
template<class ItemType>
ostream& operator<<(ostream& outs, const GenericList<ItemType>& list) {
    for (int i = 0; i < list.currentLength; i++)
        outs << list.item[i] << endl;
    return outs;
}}//listsavitch
#endif // GENERICLIST_CPP 注意我们已经将所有模板
// 定义封装在 #ifndef.. #endif。
```

### 自测题

7. 为“类模板语法”节中讨论的 `Pair` 类模板成员函数 `getElement` 提供定义。

8. 为“类模板语法”节中讨论的类模板提供零参数构造函数的定义。

9. 给出一个名为 `HeterogeneousPair` 的模板类的定义，它与“类模板语法”节中讨论的 `Pair` 类相似，但 `HeterogeneousPair` 的第一个和第二个位置可以存储不同类型的值。使用两个参数 `T1` 和 `T2`；第一个位置的所有项将是类型 `T1`，第二个位置的所有项将是类型 `T2`。模板类 `Pair` 中的单个修改器函数应该被模板类 `HeterogeneousPair` 中的两个修改器函数 `setFirst` 和 `setSecond` 替换。同样，模板类 `Pair` 中的单个访问器 `getElement` 应该被模板类 `HeterogeneousPair` 中的两个访问器 `getFirst` 和 `Second` 替换。

10. 下述是否正确？友元在模板类和非模板类中的用法完全相同。

## 章节总结

- 使用函数模板，你可以定义带有类型参数的函数。
- 使用类模板，你可以定义一个对类部分具有类型参数的类。

## 自测题答案

1. 函数声明：

```cpp
template<class T>
Tmaximum(T first, T second);
// 前提条件：为类型 T 定义了运算符 <。
// 返回 first 和 second 之间的最大值。
```

定义：

```cpp
template<class T>
Tmaximum(T first, T second)
{
    if (first < second)
        return first;
    return second;
}
```

2. 函数声明：

```cpp
template<class T>
T absolute(T value);
// 前提条件：当 x 的类型为 T 时，表达式 x < 0 和 -x 都是定义的。
// 返回其参数的绝对值。
```

定义：

```cpp
template<class T>
T absolute(T value)
{
    if (value < 0)
        return -value;
    else
        return value;
}
```

3. 模板提供了一种机制，允许定义具有类型类型名称参数的函数和类。

4. 任何类型，无论是基本类型（由 C++ 提供）还是用户定义的类型（类或结构体类型、枚举类型、定义的数组类型，或者 int、float、double 等）。

5. 这里给出了函数声明和函数定义。它们与显示 7.10 中给出的版本基本上相同，只是将参数列表中两个 `int` 实例更改为了 `BaseType`。

函数声明：

```cpp
template<class BaseType>
int search(const BaseType a[],
    int numberUsed, BaseType target);
// 前提条件：numberUsed 小于等于 a 的大小。
// 同时，a[0] 到 a[numberUsed-1] 有值。
// 返回满足 a[index] == target 的第一个索引，
// 如果存在这样的索引；否则返回 -1。
```

定义：

```cpp
template<class BaseType>
int search(const BaseType a[], int numberUsed,
    BaseType target)
{
    int index = 0, found = false;
    while ((found) && (index < numberUsed))
      if (target == a[index])
        found = true;
      else
        index++;
  if (found)
    return index;
  else
    return -1;
}
```

# 第 17 章 / 模板

```cpp
return second;
else
    return first;
}
```
