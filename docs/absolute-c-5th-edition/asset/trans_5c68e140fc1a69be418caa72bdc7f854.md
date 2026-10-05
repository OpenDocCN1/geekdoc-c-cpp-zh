

# 714 第16章 模板

## 显示 16.6 <class> PFArray 模板类的实现（3部分中的第2部分）

```cpp
template<class T>
PFArray<T>::PFArray(int size) : capacity(size), used (0)
{
    a = new T[capacity];
}
```

```cpp
template<class T>
PFArray<T>::PFArray(const PFArray<T>& pfaObject)
    : capacity(pfaObject.getCapacity()),
      used(pfaObject.getNumberUsed())
{
    a = new T[capacity];
    for (int i = 0; i < used; i++)
        a[i] = pfaObject[i];
}
```

```cpp
template<class T>
void PFArray<T>::addElement(const T& element)
{
    if (used >= capacity)
    {
        cout << "Attempt to exceed capacity in PFArray.";
        exit(0);
    }
    a[used] = element;
    used++;
}
```

```cpp
template<class T>
bool PFArray<T>::full() const
{
    return (capacity == used);
}
```

```cpp
template<class T>
int PFArray<T>::getCapacity() const
{
    return capacity;
}
```

```cpp
template<class T>
int PFArray<T>::getNumberUsed() const
{
    return used;
}
```

## 显示 16.6 PFArray 模板类的实现（3部分中的第3部分）

```cpp
template<class T>
void PFArray<T>::emptyArray()
{
    used = 0;
}
```

```cpp
template<class T>
T& PFArray<T>::operator[](int index)
{
    if (index >= used)
    {
        cout << "Illegal index in PFArray.";
        exit(0);
    }
    return a[index];
}
```

```cpp
template<class T>
PFArray<T>::operator=(const PFArray<T>& rightSide)
{
    if (capacity != rightSide.capacity)
    {
        delete [];
        a = new T[rightSide.capacity];
    }
    capacity = rightSide.capacity;
    used = rightSide.used;
    for (int i = 0; i < used; i++)
        a[i] = rightSide[i];
    }
    return *this;
}
```

```cpp
template<class T>
PFArray<T>::~PFArray()
{
    delete [];
}
```

## 显示 16.7 PFArray 模板类的演示程序（2部分中的第1部分）

```cpp
// 用于演示模板类 PFArray 的程序。
#include <iostream>
#include <string>
using std::cin;
using std::cout;
using std::endl;

#include "pfarray.h"
#include "pfarray.cpp"
using PFArray::PFArray;

int main() {
    PFArray<int> a(10);

    cout << "输入最多10个非负整数。\n";
    cout << "在末尾输入一个负数。\n";
    int next;
    cin >> next;
    while ((next >= 0) && (!a.full())) {
        a.addElement(next);
        cin >> next;
    }
    if (next >= 0) {
        cout << "无法读取所有数字。\n";
        // 清除未使用的输入：
        while (next >= 0) {
            cin >> next;
        }
    }

    cout << "你输入的以下内容：\n";
    int index;
    int count = a.getNumberUsed();
    for (index = 0; index < count; index++) {
        cout << a[index] << " ";
    }
    cout << endl;
    PFArray<string> b(3);

    cout << "输入三个单词:\n";
    string nextWord;
```

## 显示 16.7 PFArray 模板类的演示程序（2部分中的第2部分）

```cpp
for (index = 0; index < 3; index++)
{
    cin >> nextWord;
    b.addElement(nextWord);
}

cout << "你写了以下内容：\n";
count = b.getNumberUsed();
for (index = 0; index < count; index++)
    cout << b[index] << " ";
cout << endl;
cout << "我希望你是认真的。\n";
```

### 示例对话

输入最多10个非负整数。
在末尾输入一个负数。
1 2 3 4 5 -1

你输入的以下内容：
1 2 3 4 5

输入三个单词：
I love you

你写了以下内容：
I love you
I hope you mean it

### 友元函数

友元函数在模板类中使用方法与普通类类相同。唯一的区别是，必须在适当的地方包含类型参数。

## 自测练习

- 12. 你需要做什么才能使以下函数成为显示 16.5 中模板类 PFArray 的友元函数？

```cpp
void showData(PFArray<T> Object);
// 将 Object 中的数据显示在屏幕上。
// 假设类型 T 的值已定义了 <<。
```
