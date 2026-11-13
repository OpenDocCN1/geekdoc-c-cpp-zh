

可以将元素从一个数组复制到另一个数组，如以下 C++ 特性所述。

## C++ 特性

## C++ 标准库中的复制函数

标准库包含一个复制函数，用于轻松将元素从一个位置复制到另一个位置。该函数是 <algorithm> 设施中 std 命名空间的一部分，用法如下：

```
copy( <beginning location>, <ending location>, <destination> );
```

该函数从指定的起始位置开始，将一个元素复制到目标位置。它会越过起始位置，将越来越多的元素复制到目标的下一个位置，直到即将复制结束位置为止。结束位置不会被复制。所有三个参数通常都是数组中的位置。例如，假设 b 和 c 是数组。要将 b[0]..b[9] 的元素复制到 c[40]...c[49] 位置，我们将编写：

```
copy( b, b + 10, c + 40 );
```

此次 copy 调用从 b[0]、b[1]、b[2] ... 开始复制元素。当到达 b[10] 时停止（且 b[10] 不会被复制）。复制的元素进入数组 c，位于 c[40]、c[41]、c[42] ... 位置。目标位置不能与源位置重叠。

如本示例所示，要指定数组起始处的位置，只需使用数组名（如 b）。要指定数组中索引 i 处的位置，请写出数组名后跟 "+ i"（如 b + 10 或 c + 40）。

语句 copy( addend.data, addend.data + addend.used, data + used) 在图 3.4 中用于将元素从 addend.data 复制到 data 数组。复制的元素来自 addend.data 的开头，一直延续到但不包括 addend.data[addend.used]。复制的元素从 data[used] 位置开始放置在 data 数组中。

## 图 3.4 运算符 += 成员函数的实现

### 成员函数实现

```
void bag::operator +=(const bag& addend)
// Precondition: size() + addend.size() <= CAPACITY.
// Postcondition: Each item in addend has been added to this bag.
// Library facilities used: algorithm, cassert
{
    assert(size( ) + addend.size( ) <= CAPACITY);
    copy(addend.data, addend.data + addend.used, data + used);
    used += addend.used;
}
```

复制函数来自 C++ 标准库的 <algorithm> 部分。

## 运算符 +。

运算符 +。运算符 + 与我们的其他函数不同。它是一个普通函数，而不是成员函数。该函数必须接受两个 bag，将它们相加到第三个 bag 中，并返回这个第三个 bag。在此实现中，“第三个 bag”被声明为名为 answer 的局部变量：

```
bag operator +(const bag& b1, const bag& b2)
// Library facilities used: cassert
{
    bag answer;

    assert(b1.size( ) + b2.size( ) <= bag::CAPACITY);

    answer += b1; <------ Add in the items of b1.
    answer += b2; <------ Add in the items of b2.
    return answer;
}
```

请注意，此函数不需要是友元函数。为什么？（参见自测练习 11 的答案。）此外，函数实现可以使用 bag::CAPACITY 表示法访问静态成员常量。

## Bag 类——将各部分组合在一起

仅剩 erase 和 size 函数需要实现。我们将 erase 留作练习（它类似于 erase_one），而 size 将是第 118 页图 3.5 所示完成头文件中类定义的内联函数。请注意，在头文件中我们还列出了 bag 的 operator + 函数的原型。这不是一个成员函数，因此原型出现在 bag 类定义结束之后。

所有函数实现都收集在第 119 页图 3.6 所示的实现文件中。

## 编程提示

### 在实现文件中记录类不变式

我们在图 3.6 的实现文件顶部编写了 bag 类的不变式。这是记录类不变式的最佳位置。特别是，不要在头文件中编写不变式，因为使用该类的程序员不需要知道不变式如何规定私有字段的使用。但是，实现该类的程序员确实需要知道不变式。

## 图 3.5 Bag 类的头文件

### 头文件

```
// FILE: bag1.h
// CLASS PROVIDED: bag (part of the namespace main_savitch_3)
//
// See Figure 3.1 on page 105 for the other documentation that goes here.
//
#ifndef MAIN_SAVITCH_BAG1_H
#define MAIN_SAVITCH_BAG1_H
#include <cstddef> // Provides size_t
namespace main_savitch_3
{
    class bag
    {
    public:
        // TYPEDEFS and MEMBER CONSTANTS
        typedef int value_type;
        typedef std::size_t size_type;
        static const size_type CAPACITY = 30; // If your compiler does not permit
        // CONSTRUCTOR
        bag( ) { used = 0; }
        // MODIFICATION MEMBER FUNCTIONS
        size_type erase(const value_type& target);
        bool erase_one(const value_type& target);
        void insert(const value_type& entry);
        void operator +=(const bag& addend);
        // CONSTANT MEMBER FUNCTIONS
        size_type size( ) const { return used; }
        size_type count(const value_type& target) const;
    private:
        value_type data[CAPACITY]; // The array to store items
        size_type used; // How much of array is used
    };
    // NONMEMBER FUNCTIONS for the bag class
    bag operator +(const bag& b1, const bag& b2);
}
#endif
```

## 图 3.6 Bag 类的实现文件

### 实现文件

```cpp
// FILE: bag1.cxx
// CLASS IMPLEMENTED: bag (see bag1.h for documentation)
// INVARIANT for the bag class:
//   1. The number of items in the bag is in the member variable used.
//   2. For an empty bag, we do not care what is stored in any of data; for a non-empty bag,
//      the items in the bag are stored in data[0] through data[used-1], and we don't care
//      what's in the rest of data.
#include <algorithm> // Provides copy function
#include <cassert> // Provides assert function
#include "bag1.h"
using namespace std; // see namespace std;

namespace main_savitch_3
{
    const bag::size_type bag::CAPACITY;
    bag::size_type bag::erase(const value_type& target)
    {
        // See the solution to Self-Test Exercise 12 on page 147.
    }
    bool bag::erase_one(const value_type& target)
    {
        size_type index; // The location of target in the data array
        // First, set index to the location of target in the data array,
        // which could be as small as 0 or as large as used-1.
        // If target is not in the array, then index will be set equal to used.
        index = 0;
        while ((index < used) && (data[index] != target))
            ++index;
        if (index == used) // target isn't in the bag, so no work to do
            return false;
        // When execution reaches here, target is in the bag at data[index].
        // So, reduce used by 1 and copy the last item onto data[index].
        --used;
        data[index] = data[used];
        return true;
    }
}
```

有关此行的说明，请参见第 104 页的“静态成员常量”。

有关此步骤的替代方法，请参见自测练习 13。

## （图 3.6 续）

```
void bag::insert(const value_type& entry)
// Library facilities used: cassert
{
    assert(size( ) < CAPACITY);
    data[used] = entry;
    ++used;
}
```

有关这些步骤的替代方法，请参见自测练习 13。

```
void bag::operator +=(const bag& addend)
// Library facilities used: algorithm, cassert
{
    assert(size( ) + addend.size( ) <= CAPACITY);
    copy(addend.data, addend.data + addend.used, data + used);
    used += addend.used;
}
```

复制函数来自 C++ 标准库的 <algorithm> 部分。

```
bag::size_type bag::count(const value_type& target) const
{
    size_type answer;
    size_type i;

    answer = 0;
    for (i = 0; i < used; ++i)
        if (target == data[i])
            ++answer;

    return answer;
}
```

```
bag operator +(const bag& b1, const bag& b2)
// Library facilities used: cassert
{
    bag answer;

    assert(b1.size( ) + b2.size( ) <= bag::CAPACITY);

    answer += b1;
    answer += b2;

    return answer;
}
```

