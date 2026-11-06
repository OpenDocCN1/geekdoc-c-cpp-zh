
当迭代器要在泛型算法中使用时，它们必须满足额外的要求。这是因为泛型算法会对其接收的迭代器类型进行检查。简单指针通常会被接受，但如果使用迭代器对象，则它必须能够指明其所代表的迭代器种类。

当从类 iterator 派生类时，迭代器的类型由类模板的*第一个*参数定义，而迭代器所引用的数据类型由类模板的*第二个*参数定义。

派生类所实现的迭代器类型通过一个所谓的*迭代器标签*（*iterator_tag*）来指定，该标签作为类 iterator 的第一个模板实参提供。对于五种基本迭代器类型，这些标签是：

- `std::input_iterator_tag`。此标签定义 InputIterator。此类型的迭代器允许读取操作，从迭代器所引用序列的第一个元素迭代到最后一个元素。

    InputIterator 解引用运算符应声明如下：

    ```cpp
    Type const &operator*() const;
    ```

    除标准运算符外，对 InputIterator 没有进一步要求。

- `std::output_iterator_tag`。此标签定义 OutputIterator。此类型的迭代器允许赋值操作，从迭代器所引用序列的第一个元素迭代到最后一个元素。

    OutputIterator 解引用运算符应允许对其解引用运算符所引用的数据进行赋值。因此，OutputIterator 解引用运算符应声明如下：

    ```cpp
    Type &operator*();
    ```

    除标准运算符外，对 OutputIterator 没有进一步要求。

- `std::forward_iterator_tag`。此标签定义 ForwardIterator。此类型的迭代器允许读取*和*赋值操作，从迭代器所引用序列的第一个元素迭代到最后一个元素。

    ForwardIterator 解引用运算符应允许对其解引用运算符所引用的数据进行赋值。因此，ForwardIterator 解引用运算符应声明如下：

    ```cpp
    Type &operator*();
    ```

    除标准运算符外，对 ForwardIterator 没有进一步要求。

- `std::bidirectional_iterator_tag`。此标签定义 BidirectionalIterator。此类型的迭代器允许读取*和*赋值操作，逐步迭代，可能以交替方向，遍历迭代器所引用序列的所有元素。

    BidirectionalIterator 解引用运算符应允许对其解引用运算符所引用的数据进行赋值，并且应允许向后步进。因此，BidirectionalIterator 除迭代器所需的标准运算符外，还应提供以下运算符：

    ```cpp
    Type &operator*();
    Iterator &operator--();
    ```

- `std::random_access_iterator_tag`。此标签定义 RandomAccessIterator。此类型的迭代器允许读取*和*赋值操作，使用任何可用的（随机）步长，可能以交替方向，遍历迭代器所引用序列的所有元素。RandomAccessIterator 类的解引用运算符应允许对其所引用的数据进行赋值，并且除迭代器所需的标准运算符外，还应提供以下运算符：

    - Type &operator*()，允许对解引用运算符所引用的数据进行赋值；
    - Iterator operator-()，允许向后单步；
    - Type operator-(Iterator const &rhs) const，返回当前迭代器与 rhs 迭代器之间的数据元素数量（如果 rhs 引用的数据元素位于此迭代器所引用的数据元素之后，则返回负值）；
    - Iterator operator+(int step) const，返回一个迭代器，指向此迭代器所引用数据元素之后 step 个数据元素处的数据元素；
    - Iterator operator-(int step) const，返回一个迭代器，指向此迭代器所引用数据元素之前 step 个数据元素处的数据元素；
    - bool operator<(Iterator const &rhs) const，如果此迭代器所引用的数据元素位于 rhs 迭代器所引用的数据元素之前，则返回 true。

每个迭代器标签都假定某一组运算符可用。`RandomAccessIterator` 是迭代器中最复杂的，因为它隐含了所有其他迭代器。

注意，迭代器总是定义在某个范围（`[begin, end)`）上。如果递增和递减操作产生的迭代器值指向该范围之外的位置，则可能导致迭代器的未定义行为。

通常，迭代器只访问其所引用序列的元素。在内部，迭代器可能使用普通指针，但迭代器几乎从不需要分配自己的内存。因此，由于赋值运算符和拷贝构造函数不必分配任何内存，它们的*默认实现*通常就足够了。出于同样的原因，迭代器通常不需要析构函数。

大多数提供返回迭代器的成员函数的类，都是让这些成员构造所需的迭代器，然后由这些成员函数将迭代器作为对象返回。由于这些成员函数的*调用者*只需*使用*或有时*拷贝*返回的迭代器对象，因此通常除拷贝构造函数外，无需提供任何公开可用的构造函数。因此，这些构造函数通常被定义为*私有*或*受保护*成员。为了允许外部类创建迭代器对象，迭代器类通常将外部类声明为其*友元*。

以下各节讨论 `RandomAccessIterator`（所有迭代器中最复杂的一种）的构造，以及*反向* `RandomAccessIterator` 的构造。必须为其开发随机访问迭代器的容器类，实际上可能以许多不同方式存储其数据元素（例如，使用容器或指向指针的指针）。因此，很难构造一个适用于大量不同容器类的模板迭代器类。

以下各节使用可用的 `std::iterator` 类来构造一个表示随机访问迭代器的内部类。读者可以按照其中展示的方法，为其他上下文构造迭代器类。第 23.8 节给出了这种模板迭代器类的示例。

接下来各节开发的随机访问迭代器会访问只能通过指针访问的数据元素。该迭代器类被设计为一个类的内部类，而这个类派生自一个字符串指针的 vector。

### 21.13.1 实现一个 'RandomAccessIterator'

在关于容器的一章（第 12 章）中曾指出，容器拥有其包含的信息。如果它们包含对象，那么一旦容器被销毁，这些对象也会被销毁。由于指针不是对象，因此不鼓励在容器中使用指针（不过，可以使用 STL 的 `unique_ptr` 和 `shared_ptr` 类型对象）。尽管不鼓励，我们在特定上下文中也许能够使用指针数据类型。在下面的类 `StringPtr` 中，一个普通类派生自 `std::vector` 容器，该容器使用 `std::string *` 作为其数据类型：

```cpp
#ifndef INCLUDED_STRINGPTR_H_
#define INCLUDED_STRINGPTR_H_

#include <string>
#include <vector>

class StringPtr: public std::vector<std::string *>
{
    public:
        StringPtr(StringPtr const &other);
        ~StringPtr();

        StringPtr &operator=(StringPtr const &other);
};

#endif
```

这个类需要一个析构函数：由于对象存储字符串指针，因此需要析构函数，以便在 StringPtr 对象本身被销毁后销毁这些字符串。类似地，还需要拷贝构造函数和重载赋值运算符。其他成员（特别是构造函数）在此没有显式声明，因为它们与本节的 topic 无关。

假设我们希望能够在 StringPtr 对象上使用 sort 泛型算法。该算法（见第 19.1.58 节）需要两个 RandomAccessIterator。尽管这些迭代器可用（通过 std::vector 的 begin 和 end 成员），但它们返回的是指向 std::string * 的迭代器，而这些指针无法进行有意义的比较。

为了解决这个问题，我们可以定义一个内部类型 StringPtr::iterator，它返回的不是指向指针的迭代器，而是指向这些指针所指向对象的迭代器。一旦有了这个迭代器类型，我们就可以将以下成员添加到 StringPtr 类接口中，从而隐藏其基类中同名但无用的成员：

```cpp
StringPtr::iterator begin();    // returns iterator to the first element
StringPtr::iterator end();      // returns iterator beyond the last
                                // element
```

由于这两个成员返回（正确的）迭代器，StringPtr 对象中的元素可以很容易地排序：

```cpp
int main()
{
    StringPtr sp;                 // assume sp is somehow filled

    sort(sp.begin(), sp.end()); // sp is now sorted
}
```

要使这一切正常工作，必须定义类型 StringPtr::iterator。正如其类型名所暗示的，iterator 是 StringPtr 的嵌套类型。要将 StringPtr::iterator 与 sort 泛型算法结合使用，它还必须是一个 RandomAccessIterator。因此，StringPtr::iterator 本身必须派生自现有的类 std::iterator。

要从 std::iterator 派生类，必须同时指定迭代器类型和迭代器所指向的数据类型。注意：我们的迭代器负责 string * 的解引用；因此所需的数据类型是 std::string，而不是 std::string *。类 iterator 将其接口指定为：

```cpp
class iterator:
    public std::iterator<std::random_access_iterator_tag, std::string>
```

由于其基类说明相当复杂，我们可以考虑使用以下 typedef 将此类型关联到一个更短的名称：

```cpp
typedef std::iterator<std::random_access_iterator_tag, std::string>
```
