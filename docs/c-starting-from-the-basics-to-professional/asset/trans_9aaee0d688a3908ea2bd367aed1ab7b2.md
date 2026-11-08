

## 运算符函数与隐式转换

正如本章前文以及前面几章所指出的，允许从double到Box的隐式转换并不是一个好主意。因为这类转换会导致令人不快的结果，所以Box对应的单参数构造函数确实应当声明为explicit。但并非所有单参数构造函数都如此。例如，你在第12章练习中较早处理的Integer类就提供了一个很好的例子。从本质上看，这个类是这样的：

```cpp
class Integer
{
public:
    Integer(int value = 0) : m_value{value} {}
    int getValue() const { return m_value; }
    void setValue(int value) { m_value = value; }
private:
    int m_value;
};
```

对这个类而言，允许隐式转换并无害处。主要原因是Integer对象比Box对象更接近int。你已经知道的其他无害（而且方便！）的隐式转换示例，包括从字符串字面量到std::string对象，或者从T值到std::optional<T>对象的转换。

对于允许隐式转换的类，将运算符重载为成员函数的一般准则通常会发生改变。以Integer类为例。你自然希望为Integer对象提供诸如operator+()这样的二元算术运算符。当然，你还希望它们也能用于Integer + int和int + Integer形式的加法。显然，你仍然可以像我们为Integer和Box的operator+()所做的那样定义三个运算符函数——两个成员函数和一个非成员函数。但还有一个更简单的选择。你只需要如下定义一个非成员运算符函数：

```cpp
Integer operator+(const Integer one, const Integer& other)
{
    return one.getValue() + other.getValue();
}
```

将这个函数与前面简单的Integer类定义一起放进一个integer模块中。为-、*、/和%添加类似的函数。由于int值会隐式转换为Integer对象，这五个运算符函数就足以让下面的测试程序正常工作。如果不依赖隐式转换，你至少需要15个函数定义才能覆盖所有可能性！

```cpp
// Ex13_07.cpp
// Implicit conversions reduce the number of operator functions
import <iostream>;
import integer;

int main()
{
    const Integer i{1};
    const Integer j{2};
    const auto result = (i * 2 + 4 / j - 1) % j;
    std::cout << result.getValue() << std::endl;
}
```

需要改用非成员函数才能让任一操作数都支持隐式转换，原因是编译器从不对成员函数的左操作数执行转换。也就是说，如果你把`operator/()`定义为成员函数，那么像`4 / j`这样的表达式将不再能编译。

> **提示** 运算符重载应主要实现为成员函数。只有在无法使用成员函数，或者希望第一个操作数进行隐式转换时，才使用非成员函数。

### 重载一元运算符

到目前为止，我们只看到了重载二元运算符的例子。当然，你也可以重载一元运算符。为了说明问题，假设对盒子的一种常见操作是“旋转”它们，也就是交换它们的宽度和长度。如果这个操作确实经常使用，你可能会想为它引入一个运算符。因为旋转只涉及一个Box——不需要额外的操作数——所以你必须从可用的一元运算符中选择一个。可行的候选有+、-、~、!和*。其中，operator*()似乎是个不错的选择。和二元运算符一样，一元运算符既可以定义为成员函数，也可以定义为普通函数。仍然从Ex13_04中的Box类开始，前一种可能性看起来像这样：

```cpp
class Box
{
public:
    // Constructors
    Box(double l, double w, double h) : m_length{l}, m_width{w}, m_height{h} {}

    Box operator*() const
    {
        return Box{m_width, m_length, m_height}; // Width and length are swapped
    }

    // Remainder of the Box class as before...
};
```

按照惯例，operator*()返回一个新对象，就像我们在那些不修改左操作数的二元算术运算符中看到的那样。把Box的“旋转”运算符定义为非成员函数也同样不足为奇：

```cpp
Box operator*(const Box& box)
{
    return Box{ box.getWidth(), box.getLength(), box.getHeight() };
}
```

只要采用其中任意一种运算符重载，你就可以编写类似下面的代码：

```cpp
Box someBox{ 1, 2, 3 };
std::cout << *someBox << std::endl;
```

你可以在Ex13_08中找到这个示例。如果运行该程序，你将得到如下结果：

```
Box(2.0, 1.0, 3.0)
```

> **注意** 可以说，这个运算符重载违反了本章前文给出的关键准则。虽然它显然能带来非常紧凑的代码，但不一定能形成自然、可读的代码。如果不看类定义，恐怕你的程序员中没有人能猜到表达式*someBox在做什么。因此，除非*someBox这种写法在包装和盒子领域司空见惯，否则在这里定义一个普通函数可能更好，例如rotate()或getRotatedBox()。

### 重载自增和自减运算符

++和--运算符会给为类实现它们的函数带来一个新问题，因为它们的行为取决于它们是否位于操作数之前。每个运算符都需要两个函数：一个用于前缀情形，另一个用于后缀情形。任一运算符的后缀形式运算符函数，都通过一个类型为int的哑元参数来与前缀形式区分。这个参数只用于区分这两种情形，除此之外并不使用。为任意类MyClass重载++的函数声明将如下所示：

```cpp
class MyClass
{
public:
  MyClass& operator++();          // Overloaded prefix increment operator

  const MyClass operator++(int);  // Overloaded postfix increment operator

  // Rest of MyClass class definition...
};
```

前缀形式的返回类型通常需要是对当前对象*this的引用，并且是在自增操作已应用于该对象之后。下面是Box类前缀形式的一种可能实现：

```cpp
Box& Box::operator++()  // Prefix ++ operator
{
  ++m_length;
  ++m_width;
  ++m_height;
  return *this;
}
```

这只会把每个尺寸都加一，然后返回当前对象。

> **注意** 自增或自减运算符的后缀形式返回的值应始终是原始对象在自增或自减之前的副本；前缀形式返回的值应始终是对当前（因而已经自增或自减）对象的引用。原因在于，这正是对应的内置运算符作用于基本类型时的行为。

### 重载下标运算符

下标运算符[]为某些种类的类提供了非常有趣的可能性。显然，这个运算符主要旨在从若干对象中选择一个对象，你可以把这些对象解释为数组，但这些对象可能存放在多种不同容器中的任意一种里。你可以重载下标运算符来访问稀疏数组（其中许多元素为空）、关联数组，甚至链表的元素。数据甚至可以存储在文件中，而你可以使用下标运算符来隐藏文件输入和输出操作的复杂性。

Ex12_17中的Truckload类就是一个可以支持下标运算符的类的例子。Truckload对象包含一组有序对象，因此下标运算符可以提供一种通过索引值访问这些对象的方式。索引0会返回列表中的第一个对象，索引1会返回第二个，依此类推。下标运算符的内部工作会负责遍历列表以找到所需对象。

Truckload类的operator[]函数需要接受一个索引值作为参数，该值表示列表中的位置，并返回指向该位置处Box对象的指针。Truckload类中该成员函数的声明如下：

```cpp
class Truckload
{
public:
  // Rest of the class as before...
  SharedBox operator[](size_t index) const;  // Overloaded subscript operator
  // ...
};
```

你可以像这样实现该函数：

```cpp
SharedBox Truckload::operator[](size_t index) const
{
  size_t count {};                         // Package count
  for (Package* package{m_head}; package; package = package->m_next)
  {
    if (count++ == index)                   // Up to index yet?
      return package->m_box;                // If so return the pointer to Box
  }
  return nullptr;
}
```

for循环遍历列表，并在每次迭代时递增count。当count的值与index相同时，循环已经到达位置index处的Package对象，因此返回指向该Package对象中Box对象的智能指针。如果遍历完整个列表时count仍未达到index的值，那么index一定超出范围，因此返回nullptr。让我们再试一个例子，看看这在实践中会如何发展。

