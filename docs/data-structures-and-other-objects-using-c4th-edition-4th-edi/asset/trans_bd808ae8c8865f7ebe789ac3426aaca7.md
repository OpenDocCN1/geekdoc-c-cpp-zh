

揭示我们的实现，突然间一切都揭晓了！之所以有这个要求，是为了让编译器的工作更简单。我们建议你以一种后门方式来满足这个要求：将实现保存在单独的实现文件中，但在头文件底部放置一个包含指令来引入这些实现，如我们新 bag 的头文件（bag4.h）底部所示，如图 6.2 所示。在头文件的末尾，第 506 页，我们有以下一行，它会导致包含实现文件：

```cpp
#include "bag4.template" // Include the implementation.
```

## 陷阱

### 不要在模板实现中放置 using 指令

因为模板类的实现被包含在头文件中，所以我们不能在实现中放置任何 using 指令（否则，每个使用我们模板类的程序都会不经意地引入我们的 using 指令）。

## 关于模板实现文件的更多内容

图 6.2 显示了新的 bag 头文件（bag4.h）和实现文件（bag4.template）。实现文件的名称是 bag4.template（而不是 bag4.cxx），提醒我们这些实现不能单独编译。在实现中，我们本可以使用之前的任何 bag 技术：静态数组、动态数组或链表。我们在新模板类中实际采用的方法是使用动态数组的实现。

## 总结：如何将容器类转换为模板

- 1. 模板前缀位于每个函数原型或实现之前。
- 2. 在类定义之外，将类名与 <Item> 一起放置，例如 bag<Item>。
- 3. 使用 Item 代替 value_type。
- 4. 在成员函数和类定义本身之外，在使用类的任何类型名称之前添加关键字 typename。例如：typename bag<Item>::size_type
- 5. 实现文件名现在以 .template 结尾（而不是 .cxx），并通过包含指令包含在头文件中。
- 6. 消除实现文件中的任何 using 指令。因此，我们必须在任何标准库函数（如 std::copy）前面写上 std::。
- 7. 某些编译器要求任何默认参数同时出现在原型和函数实现中。

## 图 6.2 Bag 模板类的头文件和实现文件

### 头文件

```cpp
// FILE: bag4.h (part of the namespace main_savitch_6A)
// TEMPLATE CLASS PROVIDED: bag<Item>
//   TEMPLATE PARAMETER, TYPEDEFS, and MEMBER CONSTANTS for the bag<Item> class:
//     The template parameter, Item, is the data type of the items in the bag, also defined as
//     bag::value_type. It may be any of the C++ built-in types (int, char, etc.), or a class with a
//     default constructor, a copy constructor, an assignment operator, and operators to test
//     for equality (x == y) and non-equality (x != y). The definition bag::size_type is the data
//     type of any variable that keeps track of how many items are in a bag. The static const
//     DEFAULT_CAPACITY is the initial capacity of a bag created by the default constructor.
// CONSTRUCTOR for the bag<Item> template class:
//   bag(size_type initial_capacity = DEFAULT_CAPACITY)
//     Postcondition: The bag is empty with the specified initial capacity. The insert
//     function works efficiently (without allocating new memory) until this capacity is reached.
// MODIFICATION MEMBER FUNCTIONS for the bag<Item> template class:
//   size_type erase(const Item& target)
//     Postcondition: All copies of target have been removed from the bag.
//     The return value is the number of copies removed (which could be zero).
//   bool erase_one(const Item& target)
//     Postcondition: If target was in the bag, then one copy has been removed;
//     otherwise the bag was unchanged. A true return value indicates that one
//     copy was removed; false indicates that nothing was removed.
//   void insert(const Item& entry)
//     Postcondition: A new copy of entry has been inserted into the bag.
//   void operator +=(const bag& addend)
//     Postcondition: Each item in addend has been added to this bag.
//   void reserve(size_type new_capacity)
//     Postcondition: The bag's current capacity is changed to the new_capacity (but not less
//     than the number of items already in the bag). The insert function will work efficiently
//     (without allocating new memory) until the new capacity is reached.
// CONSTANT MEMBER FUNCTIONS for the bag<Item> template class:
//   size_type count(const Item& target) const
//     Postcondition: Return value is the number of times target is in the bag.
//   Item grab( ) const
//     Precondition: size( ) > 0.
//     Postcondition: The return value is a randomly selected item from the bag.
//   size_type size( ) const
//     Postcondition: The return value is the total number of items in the bag.
// NONMEMBER FUNCTIONS for the bag<Item> template class:
// bag<Item> operator +(const bag<Item>& b1, const bag<Item>& b2)
// Postcondition: The bag returned is the union of b1 and b2.
// VALUE SEMANTICS: Assignment and the copy constructor may be used with bag objects.
// DYNAMIC MEMORY USAGE by the bag<Item> template class:
// If there is insufficient dynamic memory, then the following functions throw bad_alloc:
// the constructors, reserve, insert, operator += , operator +, and the assignment operator.
#ifndef MAIN_SAVITCH_BAG4_H
#define MAIN_SAVITCH_BAG4_H
#include <cstddef> // Provides size_t
namespace main_savitch_6A
{
    template <class Item> // the template prefix
    class bag
    {
    public:
        // TYPEDEFS and MEMBER CONSTANTS
        typedef std::size_t size_type;
        static const size_type DEFAULT_CAPACITY = 30;
        // CONSTRUCTORS and DESTRUCTOR
        bag(size_type initial_capacity = DEFAULT_CAPACITY);
        bag(const bag& source);
        ~bag( );
        // MODIFICATION MEMBER FUNCTIONS
        size_type erase(const Item& target);
        bool erase_one(const Item& target);
        void insert(const Item& entry);
        void operator =(const bag& source);
        void operator +=(const bag& addend);
        void reserve(size_type capacity);
        // CONSTANT MEMBER FUNCTIONS
        size_type count(const Item& target) const;
        Item grab( ) const;
        size_type size( ) const { return used; }
    private:
        Item *data; // Pointer to partially filled dynamic array
        size_type used; // How much of array is being used
        size_type capacity; // Current capacity of the bag
    };
    // NONMEMBER FUNCTION
    template <class Item>
    bag<Item> operator +(const bag<Item>& b1, const bag<Item>& b2);
}
#include "bag4.template" // Include the implementation.
#endif
```

### （图 6.2 续）

大多数编译器要求将模板类的实现文件包含在头文件中。

### （图 6.2 续）

### 实现文件

```cpp
// FILE: bag4.template
// TEMPLATE CLASS IMPLEMENTED: bag<Item> (see bag4.h for documentation)
// This file should be included in the header file and not compiled separately.
// Because of this, we must not have any using directives in the implementation.
```

```cpp
// INVARIANT for the bag class:
// 1. The number of items in the bag is in the member variable used.
// 2. The actual items of the bag are stored in a partially filled array.
//    The array is a dynamic array, pointed to by the member variable data.
// 3. The size of the dynamic array is the member variable capacity.
```

```cpp
// #include <algorithm> // Provides copy
// #include <cassert> // Provides assert
// #include <cstddef> // Provides rand
```

在类定义之外，每个定义之前都有模板前缀。

```cpp
namespace main_savitch_6A
{
    template <class Item>
    const typename bag<Item>::size_type bag<Item>::DEFAULT_CAPACITY;

    template <class Item>
    bag<Item>::bag(size_type initial_capacity)
    {
        data = new Item[initial_capacity];
        capacity = initial_capacity;
        used = 0;
    }
```

在类定义之外，将 bag 用作类型名的用法更改为 bag<Item>。此外，关键字 typename 必须位于任何 bag<Item>::size_type 的使用之前，且值类型写为 Item。

```cpp
template <class Item>
bag<Item>::bag(const bag<Item>& source)
// Library facilities used: algorithm
{
    data = new Item[source.capacity];
    capacity = source.capacity;
    used = source.used;
    std::copy(source.data, source.data + used, data);
}
```

在实现文件中，我们不放置任何 using 指令，因此必须写 std::copy 而不是简单地写 copy。

```cpp
template <class Item>
bag<Item>::~bag( )
{
    delete[] data;
}
```

