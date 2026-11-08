
```cpp
cout << "Error in Person::print!\n";
return 1;                 // propagate error outward
}
}
```

清单 12.8 “print” 将一个流作为参数。

特别是，使用 `ostringstream` 揭示了一个特殊的方面：如果你想自动测试一个打印函数是否工作正常，字符串很容易处理和检查所需的结果。如果你直接写到 `cout`，你该如何测试呢？提取输出将变得相当困难。传递输出流的真正优点之一是函数易于测试。

## 12.5 与其他输出一样的输出

下一步实际上只是外观上的。要将对象输出到 `ostream`，实践中有一个常用的方法：为 `ostream&` 和你的类型重载全局 `operator<<` 运算符。

```cpp
std::ostream& Person::print(std::ostream& os) {
    return os << format("{} {} from {}", name_, age_, city_);
}
std::ostream& operator<<(std::ostream& os, Person p) {
    return p.print(os);
}
```

清单 12.9 你可以重载标准运算符用于输出。

与其调用 `p.print()`，你也可以直接输出字段：

```cpp
std::ostream& operator<<(std::ostream& os, Person p) {
    return os << format("{} {} from {}", p.name_, p.age_, p.city_);
}
```

你是否注意到返回类型不是 `void`？通过返回作为参数传入的 `ostream`，你可以在表达式内重用这个返回值。你已经在 `operator<<` 上经常这样做。在下面的清单中看看你的新输出运算符的实际效果。

```cpp
// https://godbolt.org/z/a7q5xsWGj
// Excerpt ...
        std::ostream& print(std::ostream& os);
};
std::ostream& Person::print(std::ostream& os) {
    return os << format("{} ({}) from {}", name_, age_, city_);
}

std::ostream& operator<<(std::ostream& os, Person p) {
    return p.print(os);
}

int main() {
    Person paul {"Paul", 23, "Irvine"};
    cout << "You are " << paul << ", right?\n";
}
```

**清单 12.10** 通过重载自由函数实现了 `<<` 输出。

这样你就可以像其他数据类型一样在输出中使用 `Person` 对象。完整的输出如下所示：

You are Paul (23) from Irvine, right?

## 12.6 内联定义方法

你是否注意到，在声明并随后定义类的方法时，我使用了一个你已经知道的技术——方法的*前向声明*？首先，在结构体中只提到*方法头*，然后在外部进行实际定义。（严格来说，它仍然是一个聚合体，但很快就会成为一个类。一切都仍然是公共的，没有构造函数或虚方法。）

这也是你通常应该处理结构体和类的方式。然而，如果一个方法很短，例如，你可以像对待普通函数一样对待它。你也可以当场定义它——就在结构体内部。

```cpp
// https://godbolt.org/z/Y3eWIkh8v
#include <string>
#include <iostream>    // ostream
#include <format>

using std::string; using std::ostream; using std::format;

struct Person {
    string name_;
    int age_;
    string city_;
    ostream& print(ostream& os) {       // method defined inline
        return os << format("{} ({}) from {}", name_, age_, city_);
    }
};
```

**清单 12.11** 方法也可以内联定义。

但是，只有在方法非常短时才使用这个选项。

通过这种方式在类中编写方法，编译器会尝试将实现的代码直接插入到调用函数的位置：这被称为*内联*。虽然这可能使你的代码更快（函数调用会花费很多时间），但也会使代码变得更大。

如果你内联了太多函数，你的代码可能会变得太大，以至于速度优势被抵消。最好只内联那些简单或非常频繁调用的方法。

## 12.7 分离实现与定义

将定义和实现分开，对程序的清晰性是有益的。甚至到了这种程度：你应该将结构体定义放在头文件中，将实现放在一个实现的 *.cpp* 文件中（见图 12.2）。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_285_0.png)

图 12.2 将类拆分为头文件和实现。

如果你在程序的多个部分需要 `Person`，请在那些地方使用 `#include "person.hpp"`，使编译器知道该数据类型。

为了防止你通过多种包含间接或直接地多次包含 `person.hpp`，有下面这些外围行：

```cpp
#ifndef PERSON_HPP
#define PERSON_HPP
// ... actual content
#endif // PERSON_HPP
```

这些*包含守卫*可以防止 `struct Person` 被定义两次，如果你直接或间接地写了两次 `#include "person.hpp"`。使用这些守卫不是*必须*的，但这是非常常见的做法。

### 不要在头文件中使用 “using”

正如我在本书开头提到的，为了简洁起见，我并没有像你在实践中应该做的那样完全不用 `using`。在图 12.2 中，你可以看到正确的做法：

- 不要在头文件中使用全局 `using`。
- 在 *.cpp* 文件中，可以使用 `using std::identifier`。
- 但是，你不应该全局使用 `using namespace std;`，即使在 *.cpp* 文件中也不应该。

## 12.8 通过构造函数进行初始化

你已经熟悉简单的 `struct Person`：

```cpp
struct Person { string name_; int age_; string city_; };
```

你也知道可以用三种元素以四种正确方式初始化聚合体 `Person`：

```cpp
Person p1 { name, age, city };
Person p2 { name, age };
Person p3 { name };
Person p4 { };
```

现在，如果我们加上 C++20 引入的*指定初始化器*，还有七种可能性：

```cpp
Person p1 { .name_=name, .age_=age, .city_=city };
Person p2 { .name_=name, .city_=city };            // and 2 more
Person p3 { .age_=age };                           // and 2 more
```

所有这些变体都是有效的，并且会初始化所有字段。未列出的字段会被值初始化，意思是用一个有意义的、通常类似空值的值或默认构造函数填充。但是，如果你想强制要求在初始化时总是指定 `city_`，该怎么办？或者如果你想提供省略 `name_` 而不是 `city_` 的可能性，而不必指定指定初始化器呢？

为此，有构造函数。*构造函数*是结构体的一种特殊方法，专门用于初始化对象。你写构造函数*几乎*就像写普通方法一样，区别如下：

- 构造函数的名字总是结构体的名字——这里是 `Person(...)`。
- 构造函数没有返回值或返回类型，甚至没有 `void`。
- 在构造函数体之前，你可以（也应该）用 `field{value}, ...` 初始化类的字段。

你必须像结构体中的方法一样声明构造函数：

```cpp
struct Person {
    string name_;
    int age_;
    string city_;
    Person();          // declare constructor
};
Person::Person()
    : name_{"no name"}    // initialization value for name_
    , age_{-1}             // initialization value for age_
    , city_{"no city"}    // initialization value for city_
{ }
```

**清单 12.12** 如何定义构造函数。

如果你现在初始化一个 `Person p{};`，值初始化将不再执行；取而代之的是这个构造函数。在进入（此处为空的）函数体之前，所有变量都用指定的值进行初始化。除了花括号 `{}`，你也可以使用圆括号 `(…)`。这里没有区别——只是花括号可能会让你在其他地方更喜欢这种形式。你也可以选择与前面所示不同的格式，例如：

```cpp
Person::Person()
    : name_("no name"), age_(-1), city_("no city")
{ }
```

你在这里没有指定的初始化将按照你未初始化相应类型变量的方式执行。这意味着内建数据类型保持未定义，而类会被值初始化。

### 自我初始化还是依靠规则？

> 我建议你初始化所有数据字段。如果你在别人的代码中偶然发现忘记初始化的情况，你应该可以毫无羞愧地补上缺失的初始化。如果省略了提及，何时以及如何初始化的规则太复杂了，即使是像 Scott Meyers 这样的专家也不想去记住这些规则。当然，主要原因不是缺乏脑力，而是因为数据字段的定义与其初始化相去甚远，这是事情的本质。每次初始化时都要查找声明来决定是否...
