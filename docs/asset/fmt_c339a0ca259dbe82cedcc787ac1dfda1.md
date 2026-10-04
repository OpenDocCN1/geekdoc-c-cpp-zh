
`std::string d_phone;` // 电话号码

`size_t d_mass;` // 以 kg 为单位的

public:

`void setName(std::string const& name);`

`void setAddress(std::string const& address);`

`void setPhone(std::string const& phone);`

`void setMass(size_t mass);`

`std::string name() const;`

`std::string address() const;`

`std::string phone() const;`

`size_t mass() const;`

};

在接口中声明的成员函数必须实现。这些成员的实现就是它们的定义。

除了成员函数外，类还定义了由这些成员函数操作的数据。这些数据称为数据成员。在 `Person` 中，它们是 `d_name`、`d_address`、`d_phone` 和 `d_mass`。数据成员应该具有私有权限。由于类默认使用私有访问，它们通常列在类接口的顶部。

外部与类数据之间的所有通信都通过类的成员函数进行。数据成员可以接收新值（例如使用 `setName`）或被检索以检查（例如使用 `name`）。仅返回存储在对象中的值而不允许调用者修改这些内部存储值的函数称为访问器（accessors）。

在语法上，类和结构体（struct）之间只有微小的区别。类默认定义私有成员，而结构体定义公有成员。从概念上说，它们存在差异。在 C++ 中，结构体的使用方式与在 C 中相同：用于聚合数据，这些数据都是可以自由访问的。相反，类将其数据隐藏在外部之外（这部分称为数据隐藏），并提供成员函数来定义外部与类数据之间的通信。

遵循 Lakos (Lakos, 2001) 的《大规模 C++ 软件设计》(Addison-Wesley)，我建议采用以下类接口设置：

- 所有数据成员具有私有访问权限，并放置在接口顶部。
- 所有数据成员以 `d_` 开头，后跟一个指示其含义的名称（在第 8 章中我们还会遇到以 `s_` 开头的数据成员）。
- 非私有数据成员确实存在，但为数据成员定义非私有访问权限时应谨慎（另见第 13 章）。

## 7.1. 构造函数

- 成员函数大分为两类：操作器（manipulators）和接收器（acceptors）。操作器允许对象的用户修改对象的内部数据。按照习惯，操作器以 `set` 开头，例如 `setName`。
- 在接收器中，仍然经常遇到 `get-` 前缀，例如 `getName`。然而，Qt 推广的约定（参见 https://doc.qt.io，其类 `QByteArray` 和 `QString`）已经废弃了 `get-` 前缀。因此，与其定义一个成员 `getAddress`，不如直接简单地命名为 `address`。
- 通常情况下（异常除外），类的公有成员函数列在类数据成员之后。它们是接口的重要元素，因为它们定义了类向用户提供的功能。将它们列在接口高处是出于方便考虑的。关键字 `private` 位于公有成员之后，用于将从公有切换到私有的访问权限，从而将可以被“公众”使用的成员与类的辅助成员隔离开来。

风格约定通常需要很长时间才能形成。这些约定并没有强制性，我建议那些有竞争方法且不遵循上述风格约定的读者使用自己的约定。对于其他人，我强烈建议采用上述风格约定。

最后，回到第 3.1.2 节，它将用于大多数（如果不是所有）源代码示例中。正如第 7.11 和 7.11.1 节所示，`using` 指令应该在预处理器指令（包括头文件）之后，使用如下设置：

```
#include <iostream>
#include "person.h"
using namespace std;

int main() {
  ...
}
```

## 7.1 构造函数

C++ 类包含两类特殊的成员函数以及析构函数，它们对于类的正常工作至关重要。这些类别是构造函数和析构函数。析构函数的主要任务是在对象离开“作用范围”时返回由公共池分配的内存。内存分配将在第 9 章讨论，对析构函数的深度覆盖将推迟到到达该章节。在本章中，重点是类的内部操作及其构造函数。

构造函数通过其名称来识别，该名称与类名相同。构造函数不返回值，除非返回类型为 `void`。例如，`Person` 类可以定义一个构造函数 `Person::Person()`。C++ 运行时系统确保在定义类变量时调用该类的构造函数。可以定义一个缺少任何构造函数的类。在这种情况下，当定义该类的对象时，编译器会定义一个默认构造函数。在这种情况下发生的情况取决于该类定义的数据成员（参见 7.3.1）。

对象可以局部定义，也可以是全局定义。然而，在 C++ 中，大多数对象都是局部定义的。全局定义的对象很少需要，并且已经有些过时。

当函数定义一个局部对象时，每调用一次该函数，该对象的构造函数就会被调用。对象的构造函数在定义对象的地方激活（一个微妙之处是，对象可能是隐式定义的，例如作为表达式中的临时变量）。

当对象被定义为静态对象时，它在程序启动时构造。在这种情况下，它的构造函数甚至在 `main` 函数开始之前就会调用。示例：

```
#include <iostream>
using namespace std;

class Demo
{
public:
    Demo();
};

Demo::Demo()
{
    cout << "Demo constructor called\n";
}

Demo d;

int main()
{
/*
    生成的输出:
Demo constructor called
*/
```

程序包含一个 `Demo` 类的全局对象，`main` 函数体为空。尽管如此，程序仍然产生了由全局定义的 `Demo` 对象生成的输出。

构造函数起着非常重要且定义明确的作用。它们确保在对象构造完成后，类的所有数据成员都有合理或至少是定义明确的值。我们将回到这个任务。默认构造函数没有参数。如果还需要默认构造函数，则必须显式定义（参见 7.6）。我们的类的构造函数确保数据成员被赋予了合理值。因此，对象不会受到未初始化值的影响。数据成员可以被赋予新值，但不应允许直接这样做。良好的类设计的核心原则（称为数据隐藏）是数据成员是私有的。因此，数据成员的修改完全由成员函数控制，间接地由类设计者控制。类封装了对其数据成员的所有操作，由于这种封装，类对象对其数据完整性负责。以下是操作成员的最小定义：

```
#include "person.h" // 前文给出
namespace std;

void Person::setName(string const &name)
{
    d_name = name;
}

void Person::setAddress(string const &address)
{
    d_address = address;
}

void Person::setPhone(string const &phone)
{
    d_phone = phone;
}

void Person::setMass(size_t mass)
{
    d_mass = mass;
}
```

这是一个没有执行任何检查的最小定义。但显然检查很容易实现。例如，为了确保电话号码只包含数字，可以定义：

```
void Person::setPhone(string const &phone)
{
    if (phone.empty())
        d_phone = "- not available";
    else if (phone.find_first_not_of("0123456789") != string::npos)
        d_phone = phone;
    else
        cout << "电话号码可能只能包含数字\n";
}
```

注意这种实现中的双重否定。双重否定非常难读，而封装的成员 `hasOnly` 处理了测试，并提高了 `setPhone` 的可读性：

```
bool Person::hasOnly(char *characters, string const &object)
{
    // 对象只包含 'characters'
    return object.find_first_not_of(characters) == string::npos;
}
```

然后 `setPhone` 变为：

```
void Person::setPhone(string const &phone)
{
    if (phone.empty())
        d_phone = "- not available";
    else if (hasOnly("0123456789", phone))
        d_phone = phone;
}
```

### 7.1.1 首次应用

# 第 7 章 类

```
d_phone = phone;
else cout << "A phone number may only contain digits\n";
```

由于 `hasOnly` 是一个封装的成员函数，我们可以确保它只与非空字符串一起，因为 `hasOnly` 本身不需要检查这一点。

对数据成员的访问通过访问器成员（accessor members）来控制。访问器确保了数据成员不会受到不受控的修改。从概念上讲，访问器不会修改对象的数据（仅检索数据）；这些成员函数被赋予了 `const` 谓词。它们被称为 `const` 成员函数，保证不会修改其对象的数据，并且可以被可修改对象和常量（const）对象调用（见第 7.7 节）。

为了防止“后门”，我们必须确保数据成员不会通过访问器的返回值被修改。对于内置原始类型的值，这很容易办到，因为它们通常是按值返回的，即变量中值的副本。但此类对象可能相当大；通过按引用返回对象可以避免创建副本。通过引用返回数据成员会创建一个后门，如下例所示，在函数定义下方展示了允许的滥用：

```
string &Person::name() const
{
    return d_name;
}
```

```
Person somebody;
somebody.setName("Nemo");
```

```
somebody.name() = "Eve"; // 哎，后门修改了名字
```

为了防止后门，对象以 `const` 引用的形式从访问器返回。以下是 Person 访问器的实现：

```
#include "person.h" // 前文
using namespace std;
```

```
string const &Person::name() const
{
    return d_name;
}
```

```
string const &Person::address() const
{
    return d_address;
}
```

```
string const &Person::phone() const
{
    return d_phone;
}
```

```
size_t Person::mass() const
{
    return d_mass;
}
```

Person 类接口仍然类设计的起点：它的成员函数定义了可以向 Person 对象提出的问题。最后，其成员的实现只是允许 Person 对象能够工作的技术性细节。

## 7.1. 构造函数

下一个示例展示了如何使用 Person 类。一个对象被初始化并传递给函数 `printperson()`，打印该人的数据。注意函数 `printperson` 列表中的引用符号。传递给函数的是对已存在的 Person 对象的引用，而不是整个对象。`printperson` 不修改其参数，这一点从参数声明为 `const` 显而易见。

```
#include <iostream>
#include "person.h" // 前文
using namespace std;

void printperson(Person const &p)
{
    cout << "Name: " << p.name() << "\n";
    cout << "Address: " << p.address() << "\n";
    cout << "Phone: " << p.phone() << "\n";
    cout << "Mass: " << p.mass() << "\n";
}

int main()
{
    Person p;
    p.setName("Linus Torvalds");
    p.setAddress("E-mail: Torvalds@cs.helsinki.fi");
    p.setPhone("");
    p.setMass(75); // kg.
    printperson(p);
}
```

```
/*
产生输出：
Name : Linus Torvalds
Address : E-mail: Torvalds@cs.helsinki.fi
Phone : not available -
Mass : 75
*/
```

### 7.1.2 构造函数：带参数和不带参数

到目前，Person 类的构造函数还没有接收参数。C++ 允许构造函数以带参数或不带参数的形式定义。参数在定义对象时提供。对于 Person 类来说，期望三个字符串和一个 `size_t` 可能是很有用的。表示性地展示人的姓名、地址。这种构造函数可以如下实现（参见第 7.3 节）：

```
Person::Person(string const &name, string const &address,
    string const &phone, size_t mass)
{
    d_name = name;
    d_address = address;
    setPhone(phone);
    d_mass = mass;
}
```

它必须在类接口中声明：

```
class Person
{
    // 数据成员
    public:
        Person();
        Person(string const &name, string const &address, string const &phone, size_t mass);
        // 附加成员
};
```

既然这个构造函数已经声明了，默认构造函数也必须显式声明，如果我们想要构造一个不带数据成员初始值的普通 Person 对象。Person 类因此支持两种构造函数，其声明部分变为：

- Person 对象的随机值；
- 静态 Person 对象的 0。

所以，即使是默认构造函数也有工作要做：初始化数据成员。它的实现可以为：

```
Person::Person()
{
    d_mass = 0;
}
```

接下来的示例将展示如何使用带参数和不带参数的构造函数。在构造需要参数的对象时，建议用大括号包围参数。以下是示例：

```
int main() {
    Person karel("Karel", "Rietvelaan 37", "542 6044", 70);
    Person anon();
}
```

这两个 Person 对象在 main 开始时作为局部对象定义，其生命周期持续到 main 活跃结束。

如果 Person 对象必须使用其他参数定义，则必须向 Person 接口添加构造函数。通过重载类构造函数，还可以提供带有默认参数值的构造函数。这些默认参数必须在类接口构造函数的声明中指定，如下：

```
class Person {
public:
    Person(std::string const &name, 
           std::string const &address = "--unknown-",
           std::string const &phone = "--unknown-",
           size_t mass = 0);
};
```

### 7.1.2.2 构建顺序

向构造函数传递参数的可能性允许我们在程序执行期间监控对象的构造顺序。如下使用 Test 类的程序所示：

```
#include <iostream>
#include <string>
using namespace std;

class Test
```

```
{
  public:
    Test(string const &name); // 带参数的构造函数
};
```

```
Test::Test(string const &name)
{
  cout << "Test object " << name << " created" << '\n';
}
```

```
Test globaltest("global");
```

```
void func()
{
  Test functest("func");
}
```

```
int main()
{
  Test first("main first");
  func();
  Test second("main second");
}
```

```
/*
Generated output:
Test object global created
Test object main first created
Test object func created
```
