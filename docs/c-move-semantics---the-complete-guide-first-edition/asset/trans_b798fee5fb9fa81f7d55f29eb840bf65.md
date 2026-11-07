
### 3.3.1 特殊成员函数

让我们先简要了解一下术语*特殊成员函数*，因为它的用法有所不同。C++ 标准将以下六个操作定义为*特殊成员函数*：

- 默认构造函数
- 拷贝构造函数
- 拷贝赋值运算符
- 移动构造函数（自 C++11 起）
- 移动赋值运算符（自 C++11 起）
- 析构函数

然而，在许多情况下，例如在*五法则*中，我们只讨论其中五个操作，因为默认构造函数与其他五个（或在 C++11 之前是三个）操作略有不同。其他五个操作通常不会被声明，并且具有更复杂的依赖关系。因此，请确保你始终了解特殊成员函数的含义（到目前为止，我一直尽量避免使用这个术语）。

图 3.1 概述了特殊成员函数何时会自动生成，这取决于声明了哪些（其他）构造函数和特殊成员函数。³

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_66_0.png)

*图 3.1. 特殊成员函数自动生成的规则*

³ 本表经 Howard Hinnant 友好许可后采用。

你可以从这张表中看到几条基本规则：

- 仅当没有其他构造函数被用户声明时，默认构造函数才会被自动声明。
- 特殊的拷贝成员函数和析构函数会禁用移动支持。特殊移动成员函数的自动生成会被禁用（除非同时声明了移动操作）。然而，移动对象的请求通常仍然有效，因为拷贝成员函数会作为回退被使用（除非特殊移动成员函数被显式删除）。
- 特殊的移动成员函数会禁用普通的拷贝和赋值。拷贝操作和其他移动特殊成员函数会被删除，这样你就只能移动（赋值）而不能拷贝（赋值）一个对象（除非也声明了其他操作）。

让我们来看一些细节。

### 3.3.2 默认情况下，我们拥有拷贝和移动

如前所述，默认情况下，一个类会生成拷贝和移动特殊成员函数。假设有如下 Person 类的声明：

```cpp
class Person {
    ...
public:
    ...
    // NO copy constructor/assignment declared

    // NO move constructor/assignment declared

    // NO destructor declared
};
```

在这种情况下，Person 对象既可以拷贝也可以移动：

```cpp
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p);              // OK, copies p
coll.push_back(std::move(p));   // OK, moves p
```

### 3.3.3 声明拷贝会禁用移动（启用回退）

当声明一个拷贝特殊成员函数（或析构函数）时，移动特殊成员函数的自动生成会被禁用：假设有如下 Person 类的声明：

```cpp
class Person {
    ...
public:
    ...

    // copy constructor/assignment declared:
    Person(const Person&) = default;
    Person& operator=(const Person&) = default;

    // NO move constructor/assignment declared
};
```

由于回退机制生效，拷贝和移动`Person`对象都能编译通过，但移动操作是以拷贝方式执行的：

```cpp
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p);                 // OK, copies p
coll.push_back(std::move(p));      // OK, copies p
```

因此，使用`= default`声明一个特殊成员函数与完全不声明并不相同。拷贝构造函数和拷贝赋值运算符是用户声明的，这会禁用移动构造和移动赋值，从而使移动回退为拷贝。已声明的析构函数也有同样的效果。

你可能想知道为什么声明析构函数会禁用移动语义。关于被移动后的状态的章节讨论了一个具体示例，展示了一个带有析构函数的类如何导致生成的移动语义无法正常工作。

### 3.3.4 声明移动会禁用拷贝

如果你有用户声明的移动语义，那么拷贝语义就被禁用了。拷贝特殊成员函数会被删除。

换句话说，如果显式声明了移动构造函数或移动赋值运算符（无论是实现、使用`= default`生成，还是使用`= delete`禁用），那么拷贝构造函数和拷贝赋值运算符就会被声明为`= delete`，从而对它们的调用被禁用。假设有如下`Person`类的声明：

```cpp
class Person {
    ...
public:
    ...
    // NO copy constructor declared

    // move constructor/assignment declared:
    Person(Person&&) = default;
    Person& operator=(Person&&) = default;
};
```

在这种情况下，我们拥有一个仅移动类型。`Person`对象可以被移动，但不能被拷贝：

```cpp
std::vector<Person> coll;

Person p{"Tina", "Fox"};
coll.push_back(p);                 // ERROR: copying disabled
coll.push_back(std::move(p));      // OK, moves p

coll.push_back(Person{"Ben", "Cook"});  // OK, moves temporary person into coll
```

同样，使用`= default`声明一个特殊成员函数与完全不声明并不相同。不过，这次调用的后果更为严重：尝试拷贝一个对象将不再能编译通过。

一个支持移动操作但不支持拷贝操作的类是有意义的。你可以使用这种*仅移动*类型来传递资源的所有权或句柄，而无需共享或拷贝它们。在 C++ 标准库中有一些仅移动类型（例如 I/O 流类、线程类和`std::unique_ptr<>`）。详细信息请参阅关于仅移动类型的章节。

### 3.3.5 删除移动操作没有意义

出于同样的原因，如果你将移动构造函数声明为删除，那么你就不能移动（你已经禁用了该操作；任何回退都不会被使用），也不能拷贝（因为声明移动构造函数会禁用拷贝操作）：

```cpp
class Person {
  public:
    ...
    // NO copy constructor declared

    // move constructor/assignment declared as deleted:
    Person(Person&&) = delete;
    Person& operator=(Person&&) = delete;
    ...
};
```

```cpp
Person p{"Tina", "Fox"};
coll.push_back(p);           // ERROR: copying disabled
coll.push_back(std::move(p)); // ERROR: moving disabled
```

通过将拷贝特殊成员函数声明为删除，你可以获得相同的效果，而且这对其他程序员来说可能更不容易造成困惑。

删除移动操作而启用拷贝操作确实毫无意义：

```cpp
class Person {
  public:
    ...
    // copy constructor explicitly declared:
    Person(const Person& p) = default;
    Person& operator=(const Person&) = default;

    // move constructor/assignment declared as deleted:
    Person(Person&&) = delete;
    Person& operator=(Person&&) = delete;
    ...
};
```

```cpp
Person p{"Tina", "Fox"};
coll.push_back(p);           // OK: copying enabled
coll.push_back(std::move(p)); // ERROR: moving disabled
```

在这种情况下，`= delete`会禁用回退机制（因此这也与完全不声明不同）。编译器会找到该声明并将此调用报告为错误。

一个支持拷贝但在调用移动时却失败的类型毫无意义。对于这种类的用户来说，拷贝有时能工作，有时不能。作为一条准则：永远不要对特殊的移动成员函数使用`= delete`。⁴ 如果你想同时禁用拷贝和移动，删除拷贝特殊成员函数就足够了。

### 3.3.6 在启用拷贝语义的情况下禁用移动语义

基于我们刚才的讨论，我们现在知道了在拷贝仍有意义时如何禁用移动语义。将特殊移动成员函数声明为删除通常不是正确的做法，因为这会禁用回退机制。

在提供拷贝语义的同时禁用移动语义的正确方法是声明其他特殊成员函数之一（拷贝构造函数、赋值运算符或析构函数）。我建议你为拷贝构造函数和赋值运算符使用 `= default`（声明其中一个就足够了，但可能会引起不必要的困惑）：

```cpp
class Customer {
    ...
public:
    ...
    Customer(const Customer&) = default;            // disable move semantics
    Customer& operator=(const Customer&) = default; // disable move semantics
};
```

因为找不到生成的特殊移动成员函数，所以一个匿名的临时 Customer 对象，甚至一个用`std::move()`标记的 Customer 对象，现在都会被拷贝：

```cpp
std::vector<Customer> customers;
...
customers.push_back(createCustomer());           // OK, falls back to copying
customers.push_back(std::move(customers[0]));     // OK, falls back to copying
```

然而，通常最好实现特殊的移动成员函数，以修复默认生成的移动操作可能存在的任何问题。关于被移动后的状态的章节将讨论实际中的示例。

请注意，仅声明特殊的拷贝成员函数就会破坏常见的“五法则”，我们稍后将详细讨论这一点。你必须声明特殊的拷贝成员函数，但不能同时声明特殊的移动成员函数（无论是删除还是默认声明都不行，实现它们则会使类变得不必要地复杂）。因此，如果你只是为了禁用移动语义而显式声明一个拷贝特殊成员函数，请加上一个醒目的注释，以确保该声明既不会被移除，也不会因添加特殊移动成员函数的声明而被扩展。
