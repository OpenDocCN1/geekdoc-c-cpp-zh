

# 364 — 9 集合及其组织

```cpp
//构造函数
template <class T>
Array<T>::Array(int sz)
{
```

```cpp
  //sz 是数组的大小（元素个数）。如果小于或等于
  // 0，则输出错误信息
  if(sz<0)
    Error(invalidArraySize);
  size = sz;
```

```cpp
  //将数组的大小赋值给
  // 为类型为 T 的 size 个元素 分配内存空间
  // 如果内存分配失败
  // 输出错误信息
  alist = new T[size];
  if (alist == NULL)
```

```cpp
    Error(memoryAllocationError);
}
```

```cpp
//析构函数
template <class T>
Array<T>::~Array(void)
{ delete [] alist; }
```

```cpp
// 拷贝构造函数
template <class T>
Array<T>::Array(const Array<T>& X)
```

```cpp
  // 从对象 X 获取数组大小，并赋值给当前对象
  int n = X.size;
  size = n;
  // 检查内存分配过程中的错误
  // 为 n 个类型为 T 的元素 分配内存空间
  // 如果分配失败
  // 输出错误信息
  alist = new T[n];
  if (alist == NULL)
```

```cpp
    Error(memoryAllocationError);
// 将对象 X 中的数组元素拷贝到当前对象
T* srcptr = X.alist;
//X.alist 是对象 X 中
// 数组的地址
T* destptr = alist;
//alist 是当前对象中
// 数组的地址
// 逐个拷贝元素
while (n--)
```

# 9.2 线性集合 — 365

```cpp
*destptr++ = *srcptr++;
}

/* 重载赋值运算符 "=", 将右侧对象（rhs）赋值给当前对象。
实现对象之间的整个赋值 */
template<class T>
Array<T>& Array<T>::operator=(const Array<T>& rhs)
{
    int n = rhs.size; // 获取 rhs 中数组的大小
    /* 如果当前对象的数组大小与 rhs
       rhs 不同，则释放现有内存并重新分配 */
    if (size != n)
    {
        delete[] alist; // 释放数组的现有内存
        alist = new T[n]; // 重新分配 n 个元素的内存
        if (alist == NULL) // 如果失败则输出错误
            Error(memoryAllocationError); // 分配失败
        }
        size = n; // 保存当前
        // 对象中数组的大小
    }
    // 将元素从对象 rhs 拷贝到当前对象
    T* destptr = alist;
    T* srcptr = rhs.alist;
    while (n--)
        *destptr++ = *srcptr++;
    return *this; // 返回当前
    // 引用
}

/* 重载下标运算符，使其能够像普通数组一样通过索引访问
 元素，并具有索引检查的功能 */
template<class T>
T& Array<T>::operator[](int n)
{
    if (n < 0 || n > size-1) // 检查索引是否越界
    {
        Error(indexOutOfRange,n);
    }
    return alist[n]; // 返回索引为 n 的
    // 元素
}
```

```cpp
/* 重载指针运算符，将 Array 对象转换为 T 的
 指针，该指针指向对象的私有数组。因此
 可以像使用普通数组地址一样使用 Array 对象 */
template <class T>
Array<T>::operator T* (void) const
{
    return alist; // 返回当前
    // 对象
}
```

```cpp
// 获取数组的大小
template <class T>
Array<T>::ListSize(void) const
{
    return size;
}
```

```cpp
// 修改数组的大小
template <class T>
Array<T>::Resize(int sz)
{
    if (sz <= 0) // 如果 sz 小于等于 0
        Error(invalidArraySize);
    if (sz == size) // 如果指定的大小等于当前大小，什么都不做
        return;
    T* newList = new T[sz]; // 分配新数组内存
    if (newList == NULL) // 分配是否成功
        Error(memoryAllocationError);
    int n = (sz < size) ? sz : size; // 取 sz 和当前大小的较小值
    T* srcptr = alist; // 原始数组地址
    T* destptr = newList; // 新数组地址
    while (n--) // 将原始数组元素拷贝到新数组
        *destptr++ = *srcptr++;
    delete[alist]; // 释放原始数组
    alist = newList; // 让 alist 指向新数组
    size = sz; // 更新大小
}
#endif //ARRAY_CLASS
```

# 9.2 线性集合 367

Array 在访问元素之前会越界检查，其大小可以在运行时更改。程序员将 Array 当作数组使用，因为下标运算符会在运行时进行检查。Array 有三个问题：1) 为什么构造函数如此复杂，2) 为什么某些赋值返回引用而不是值，3) 为什么 Array 要重载转换运算符？

以下章节解决了这些问题：

## 浅拷贝深拷贝

正如 6.4 节所示，浅拷贝只拷贝引用而不拷贝内容。这里是浅拷贝的示例：

```cpp
template <class T>
Array<T>::Array(const Array<T>& X)
{
  int n = X.size;
  size = n;
  alist = new T[n];
  if (alist == NULL)
    Error(memoryAllocationError);
  T* srcptr = X.alist;
  T* destptr = alist;
  while (n--)
    *destptr++ = *srcptr++;
}
```

考虑以下函数：

```cpp
int main()
{
    Array<int> A(10);
    Array<int> B = A;
    ...
}
```

赋值的结果将共享相同的内存，这对于 A 和 B 来说会导致严重的错误。在程序结束时，析构函数会释放数组的现有内存，A 和 B 均会导致运行时错误。正确的做法是：

```cpp
template <class T>
Array<T>::operator=(const Array<T>& rhs)
{
    int n = rhs.size;
    if (size != n)
    {
        delete[] alist;
        alist = new T[n];
        if (alist == NULL)
            Error(memoryAllocationError);
        }
        size = n;
    }
    ...
}
```

# 3. 类型转换运算符

让我们考虑以下程序：

```cpp
#include <iostream>
using namespace std;
```

