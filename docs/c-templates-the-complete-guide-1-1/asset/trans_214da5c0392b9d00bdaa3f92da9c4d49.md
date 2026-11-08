
```cpp
}
ListModeIterator<T>* current = nullptr;
}
```

ListModeIterator 提供了前向迭代器所需的全部正确操作和嵌套类型，而且实现这些内容所需的代码非常少。大部分困难的工作——为所有必需操作定义成员函数——只需少量额外工作。

### 隐藏接口

我们的 ListModeIterator 实现有一个缺点：必须将所有被算法使用的操作（operator*、operator++、operator== 等）作为 public 暴露出来。为了满足这一要求，我们可以改造 IteratorFacade，使其通过一个单独的访问类（我们称之为 IteratorFacadeAccess）在派生类中执行其所有操作：

点击此处查看代码图片

```
Iterator/IteratorFacadeChecked.hpp
```

```cpp
// "friend" this class to allow IteratorFacade access
// to the operations of IteratorFacadeAccess
class IteratorFacadeAccess
{
  // only IteratorFacade can use these definitions
  template<typename Derived, typename Value, typename
    Reference, typename Difference>
  friend class IteratorFacade;

  // required of all iterators
  template<typename Reference, typename Iterator>
  static Reference dereference(Iterator const& i) {
    return i.dereference();
  }

  // required of bidirectional iterators
  template<typename Iterator>
  static void decrement(Iterator& i) {
    return i.decrement();
  }

  // required of random-access iterators
  template<typename Iterator, typename Distance>
  static void advance(Iterator& i, Distance n) {
    return i.advance(n);
  }

  // ...
};
```

这个类为每个核心迭代器操作提供静态成员函数，并调用所提供迭代器中对应的（静态）成员函数。所有静态成员函数都是 private，只允许 IteratorFacade 本身访问。因此，我们的 ListModeIterator 可以把 IteratorFacadeAccess 设为 friend，并将接口嵌套在门面中：

点击此处查看代码图片

```cpp
friend class IteratorFacadeAccess;
```

### 迭代器适配器

我们的 IteratorFacade 让构建迭代器适配器变得容易：适配器接收一个已有迭代器并修改其行为。当需要在底层序列的变换视图上复用迭代器时，这提供了更大的灵活性。例如，我们可能有一个存放 Person 对象的容器：

点击此处查看代码图片

```
Iterator/iterator_adaptor.hpp
```

```cpp
std::string firstName;
std::string lastName;

friend std::ostream& operator<<(std::ostream& stm,
    const Person& p) {
    return stm << p.firstName << " " << p.lastName;
}
```

然而，我们不想遍历容器中的所有 Person 值，只想查看名字。在本节中，我们开发一个名为 ProjectionIterator 的迭代器适配器，它允许我们把底层（基础）迭代器的值“投影”到某个指向数据成员的指针，例如 Person::firstName。

投影迭代器是根据基础迭代器（Iterator）以及该迭代器将暴露的值类型（T）定义的迭代器。

点击此处查看代码图片

```
iterator/projector-iterator-1.cpp
```

```cpp
template<typename Iterator, typename T>
class ProjectionIterator
{
public:
    typedef typename
        std::iterator_traits<Iterator>::value_type
        value_type;

    typedef typename
        std::iterator_traits<Iterator>::difference_type
        difference_type;

    typedef typename
        std::iterator_traits<Iterator>::reference
        reference;

    typedef typename
        std::iterator_traits<Iterator>::pointer
        pointer;

    using Base = typename std::iterator_traits<Iterator>::value_type;
    using Class =
        typename std::iterator_traits<Iterator>::difference_type;

    Iterator iter;
    T Base::* member;

    friend class IteratorFacadeAccess;

    // implement core iterator operations for Iterator
public:
    ProjectionIterator(Iterator iter, T Base::* member)
      : iter(iter), member(member) {}
};

template<typename Iterator, typename T>
auto project(Iterator iter, T Base::* member) {
    return ProjectionIterator<Iterator, T>(iter, member);
}
```

每个投影迭代器存储两个值：它存储指向底层序列（基础值）的迭代器，更重要的是，还存储一个指向数据成员的指针，用于描述要投影到哪个成员。考虑到这一点，我们来看提供给 Iterator 门面类的模板参数。第一个是 Iterator（基础迭代器）本身（用于处理 C++）。第二个（T）和第三个（T&）参数是投影迭代器的值类型和引用类型，将其定义为 T 值序列。Base 是底层迭代器值类型的类型。因此，当投影迭代器的基础迭代器是输入迭代器时，它就是 InputIterator；当其基础迭代器是双向迭代器时，它就是 Bidirectional Iterator，依此类推。project() 函数让构建投影迭代器变得容易。

唯一缺少的部分是 ProjectionIterator 核心要求的实现。最有趣的是 operator==()，它比较底层迭代器，然后通过指向数据成员的指针进行投影。

点击此处查看代码图片

其余操作基于底层迭代器实现：

点击此处查看代码图片

```cpp
void increment() {
    ++iter;
}

bool equal(const ProjectionIterator& other) const {
    return iter == other.iter;
}

void decrement() {
    --iter;
}
```

为简洁起见，我们省略了随机访问迭代器的定义，其实现方式类似。

就是这样！借助投影迭代器，我们可以打印出包含 Person 值的 vector 中每个人的名字：

点击此处查看代码图片

```
*include/projectioniterator.cpp*
```

```cpp
#include <vector>
#include <algorithm>
#include <iterator>

int main()
{
    std::vector<Person> authors = {
        {"David", "..."},
        {"Nicolas", "..."},
        {"Douglas", "..."}
    };

    std::copy(project(authors.begin(), &Person::firstName),
              project(authors.end(), &Person::firstName),
              std::ostream_iterator<std::string>(std::cout, "\n"));
}
```

该程序输出：

- David
- Nicolas
- Douglas

门面模式对于创建符合某种特定接口的新类型特别有用。新类型只需暴露少量核心操作（对于我们的迭代器门面来说，是三到六个操作），门面就会通过 CRTP 和 Barton-Nackman trick 的组合，负责提供完整且正确的公共接口。

## 2.1.3 混入（MIXINS）

考虑一个简单的 Polygon 类，它由一系列点组成：

点击此处查看代码图片

```cpp
class Point
{
public:
    double x, y;
    Point() : x(0), y(0) { }
    Point(double x, double y) : x(x), y(y) { }
};

class Polygon
{
public:
    std::vector<Point> points;

public:
    // public operations
};
```

如果用户能够扩展与每个 Point 关联的信息集，使其包含应用程序特定的数据（例如每个点的颜色），或者为每个点关联一个标签，那么这个 Polygon 类会更有用。使这种扩展成为可能的一种选择是：根据点的类型对 Polygon 进行参数化：

点击此处查看代码图片

```cpp
template<typename T>
class Polygon
{
private:
    std::vector<T> points;

public:
    // public operations
};
```

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_345_0.png)

```cpp
class LabeledPoint : public Point
{
public:
    std::string label;
    LabeledPoint() : Point(), label("") { }
    LabeledPoint(double x, double y) : Point(x, y), label("") { }
};
```

这种实现有其缺点。其一，它要求向用户暴露 `Point` 类型，以便用户可以从它派生。此外，带标签的 `Point` 的作者需要小心地正确使用与 `Point` 相同的接口（例如，继承或提供与 `Point` 相同的所有构造函数）。`LabeledPoint` 无法与期望 `Point` 的类型一起工作，因为它没有相同的接口。

如果 `Point` 从一个版本的 C++ 模板变为另一个版本，这种限制会变得更有问题！新增一个 `Point` 构造函数可能要求更新每个派生类。

混入提供了一种替代方式，可以在不继承某个类型的情况下自定义该类型的行为。混入本质上反转了正常的继承层次结构，因为新类不是作为若干派生类创建的，而是作为类模板的基类“混入”继承层次结构中。虽然混入类不会被直接继承，但它们用于提供额外的行为、数据成员和其他操作，而无需重复任何接口。

支持混入的类模板通常会接受任意数量的额外类类型，并从中派生：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_345_1.png)

```cpp
template<typename... Mixins>
class Point : public Mixins...
{
public:
    double x, y;
    Point() : Mixins()..., x(0.0), y(0.0) { }
    Point(double x, double y) : Mixins()..., x(x), y(y) { }
};
```

现在，我们可以“混入”一个包含标签的基类，从而生成 `LabeledPoint`：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_345_2.png)

```cpp
class Label
{
public:
    std::string label;
    Label() : label("") { }
};

using LabeledPoint = Point<Label>;
```

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_345_3.png)

```cpp
class Color
{
public:
    unsigned char red = 0, green = 0, blue = 0;
};

using MyPoint = Point<Label, Color>;
```

有了这种基于混入的 `Point`，就可以轻松地向 `Point` 引入额外信息而不改变其接口，因此 `Polygon` 变得更易于使用和演进。用户只需应用从点特化到其混入（标签或颜色）的隐式转换，或者访问这些数据或接口。此外，`Point` 类可以完全隐藏，而把混入提供给 `Polygon` 类模板本身。

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_345_4.png)

```cpp
template<typename... Mixins>
class Polygon
{
public:
    std::vector<Point<Mixins...>> points;
    // ...
};
```

当模板需要少量自定义时——例如用用户指定的数据装饰内部存储的对象——混入非常有用，而且无需库公开并记录其内部数据类型及其接口。
