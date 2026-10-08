
| TIP | 确保你编译脚本绑定时使用的 Python 版本与构建 Boost Python 库时使用的版本一致。 |

此时，你可以使用 `import` 关键字将动态库加载到 Python 中。这里是一些示例 Python 代码，用于加载我们的 C++ 库并演示创建 `Person` 和 `PhoneBook` 对象。例如，访问 `Person` 对象的正确语法（如 `p.name`）与 `PhoneBook` 成员的方法调用语法（如 `book.add_person(p)`）对比。

```python
#!/usr/bin/python

import phonebook

# 创建电话簿

book = phonebook.PhoneBook()

# 添加一个联系人

p = phonebook.Person()

p.name = "Martin"

p.home_number = "(123) 456-7890"

book.add_person(p)

# 添加另一个联系人

p = phonebook.Person("Genevieve")
```

### 11.3.3 构造函数

对于 `Person` 类，我定义了两个属性 `name` 和 `home_number`，并提供了 C++ getter/setter 函数来控制对这些属性的访问（如果我只提供 getter，则该方法将是只读的）。对于 `PhoneBook` 类，我分别定义了标准方法，命名为 `size()`、`add_person()`、`remove_person()` 和 `find_person()`。我还必须显式指定编译 `find_person()` 指针值的行为。

在 `phonebook_wrap.cpp` 文件中，我指定了类有一个默认构造函数和一个构造函数。然而，在 C++ API 中，`Person` 类有两个构造函数：

```cpp
class Person {
public:
    Person();
    Person(const std::string& name);
```

你可以通过更新代码来告诉 Boost Python 暴露这些构造函数：

```cpp
class_<Person>("Person")
    .def(init<>())
    .def(init<std::string>())
    .add_property("name", &Person::GetName, &Person::SetName)
    .add_property("home_number", &Person::GetHomeNumber,
                  &Person::SetHomeNumber);
```

### 11.3.4 扩展 Python API

在我谈论扩展 Python API 时，我想指出，Python 的动态性质意味着你实际上可以在运行时为类添加新方法。这并不是 Python 的特性，而是 Python 语言本身的核心能力。例如，你可以在 Python 级别定义 `__str__()` 方法，如下：

```python
#!/usr/bin/python
import phonebook

def __str__(self):
    return "Name: %s\nHome: %s" % (self.name, self.home_number)

# 重写 Person 类的 __str__ 方法
phonebook.Person.__str__ = __str__

p = phonebook.Person()
p.name = "Martin"
p.home_number = '(123) 456-7890'

print p
```

将在 shell 中输出以下文本。

Name: Martin
Home: (123) 456-7890

### 11.3.5 C++ 中的继承

C++ 和 Python 都支持多重继承，而 Boost Python 能够轻松地暴露任何 C++ 类的所有基类。我将展示如何通过将 `Person` 类转换为基类（即提供虚析构函数），并添加一个名为 `PersonWithCell` 的派生类来实现此，该类增加了指定手机号的能力。这并不是一个特别好的设计选择，但它满足我们本示例的需求。

```cpp
// phonebook.h
#include <string>
class Person {
public:
    Person();
    explicit Person(const std::string&name);
    virtual ~Person();
    void SetName(const std::string&name);
    std::string GetName() const;
    void SetHomeNumber(const std::string&number);
    std::string GetHomeNumber() const;
};
class PersonWithCell : public Person {
public:
    PersonWithCell();
    explicit PersonWithCell(const std::string&name);
    void SetCellNumber(const std::string&number);
    std::string GetCellNumber() const;
};
```

```cpp
BOOST_PYTHON_MODULE(phonebook)
class_<Person>("Person", init<>()
 .def(init<std::string>)
 .add_property("name", &Person::GetName, &Person::SetName)
 .add_property("home_number", &Person::GetHomeNumber, &Person::SetHomeNumber)
class_<PersonWithCell, bases<Person>>("PersonWithCell")
 .def(init<std::string>())
 .add_property("cell_number", &PersonWithCell::GetCellNumber, &PersonWithCell::SetCellNumber)
```

然后你可以通过如下方式更新包装文件在 Python 中表示这种层级结构：

### 11.3 使用 Boost Python 添加 Python 绑定

现在你可以按照如下方式从 Python 创建 `PersonWithCell` 对象：

```python
#!/usr/bin/python
import phonebook

book = phonebook.PhoneBook()
p = phonebook.Person()
p.name = 'Martin'
p.home_number = '(123) 456-7890'
book.add_person(p)

p = phonebook.PersonWithCell()
p.name = 'Genevieve'
p.home_number = '(123) 456-7890'
p.cell_number = '(123) 097-2134'
book.add_person(p)
```

### 11.3.6 跨语言多态

你可以在 Python 中创建派生自你用 Boost 暴露的 C++ 类。例如，下面的 Python 程序展示了你如何在 Python 中直接创建 `PersonWithCell`，并且仍然能够将该类的实例添加到 `PhoneBook` 中。

```python
#!/usr/bin/python
import phonebook

book = phonebook.PhoneBook()

class PersonWithCell(phonebook.Person):
    def get_cell_number(self):
        return self.cell
    def set_cell_number(self, n):
        self.cell = n
    cell_number = property(get_cell_number, set_cell_number)

p = PyPersonWithCell()
p.name = 'Martin'
p.home_number = '(123) 456-7890'
p.cell_number = '(123) 097-2134'
book.add_person(p)
```

当然，`PyPersonWithCell` 上的 `cell_number` 属性只能从 Python 调用。C++ 并不会知道该方法已动态地被添加到继承的类中。同样重要的是，即使是可以在 Python 中被重写的 C++ 虚函数也无法从 C++ 调用。如果跨语言多态对你的 API 关重要，Boost 提供了一种实现方法。这是通过定义一个既继承自 C++ 类又继承自 Boost 包装类模板的包装类来实现的。该包装类可以检查某个虚函数是否在 Python 中定义了重写，如果已定义，则调用该方法。例如，给出一个名为 `Base` 且具有虚方法的 C++ 类，你可以如下创建包装类：

```cpp
class Base {
public:
    virtual ~Base();
    virtual int f();
};
```

```cpp
class BaseWrap : Base, wrapper<Base> {
public:
    int f() {
        // 检查 Python 中是否有重写
        if (override f = this->get_override("f"))
            return f();
        // 或者调用 C++ 的实现
        return Base::f();
    }
    int default_f() {
        return this::Base::f();
    }
};
```

你可以如下方式暴露 `Base` 类：
`class_<BaseWrap, boost::non_copyable>("Base").def f("f", &Base::f, &BaseWrap::default_f);`

### 11.3.7 支持迭代器

Boost Python 允许你在 C++ API 中定义的 STL 接口上创建 Python 迭代器。这允许你能够在 Python 中创建在遍历容器元素方面行为更“Python 风格”的对象。例如，你可以为 `PhoneBook` 类添加 `begin()` 和 `end()` 方法，提供访问 STL 迭代器的接口以遍历电话簿中的所有联系人。

```cpp
class PhoneBook {
public:
    int GetSize() const;
    void AddPerson(Person *p);
    void RemovePerson(const std::string&name);
    Person *FindPerson(const std::string&name);
    typedef std::vector<Person *> PersonList;
    PersonList::iterator begin();
    PersonList::iterator end();
};
```

通过这些额外方法，你可以扩展 `PhoneBook` 类的包装以指定 `__iter__()` 方法，这允许 Python 对象返回一个迭代器。

```cpp
BOOST_PYTHON_MODULE(phonebook)
{
    class_<PhoneBook>("PhoneBook")
        def("size", &PhoneBook::GetSize)
        def("add_person", &PhoneBook::AddPerson)
        def("remove_person", &PhoneBook::RemovePerson)
        def("find_person", &PhoneBook::FindPerson, return_value_policy<reference_existing_object>())
        def("__iter__", range(&PhoneBook::begin, &PhoneBook::end));
}
```

现在，你可以编写如下 Python 代码来遍历 `PhoneBook` 对象中的所有联系人：

```python
#!/usr/bin/python
import phonebook

book = phonebook.PhoneBook()
book.add_person(p)
for person in book:
    print
```

### 11.4 Putting Together

结合之前的章节，这里是 `phonebook.h`、`phonebook_wrap.cpp` 以及所有引入的最终定义。

```cpp
// phonebook.h
#include <string>
#include <vector>
class Person {
public:
    Person();
    explicit Person(const std::string&name);
    virtual ~Person();
    void SetName(const std::string&name);
    std::string GetName() const;
    void SetHomeNumber(const std::string&number);
    std::string GetHomeNumber() const;
};
class PersonWithCell : public Person {
public:
    PersonWithCell();
    explicit PersonWithCell(const std::string&name);
    void SetCellNumber(const std::string&number);
    std::string GetCellNumber() const;
};
class PhoneBook {
public:
    int GetSize() const;
    void AddPerson(Person *p);
    void RemovePerson(const std::string&name);
    Person *FindPerson(const std::string&name);
    typedef std::vector<Person *> PersonList;
    PersonList::iterator begin();
    PersonList::iterator end();
};
```

```cpp
// phonebook_wrap.cpp
#include "phonebook.h"
#include <boost/python.hpp>
#include <iostream>
#include <sstream>
using namespace boost::python;

std::ostream& operator<<(std::ostream& os, const Person& p) {
    os << p.GetName() << " :" << p.GetHomeNumber();
    return os;
}

static std::string PrintWithCell(const PersonWithCell* p) {
    std::ostringstream stream;
    stream << "Name: " << p->GetName() << ", Home: " << p->GetHomeNumber() << ", Cell: " << p->GetCellNumber();
    return stream.str();
}

BOOST_PYTHON_MODULE(phonebook)
{
  class_<Person>("Person", init<()>)
    .def(init<std::string>)
    .add_property("name", &Person::GetName, &Person::SetName)
    .add_property("home_number", &Person::GetHomeNumber, &Person::SetHomeNumber);
  class_<PersonWithCell, bases<Person>>("PersonWithCell")
    .def(init<std::string>())
    .add_property("cell_number", &PersonWithCell::GetCellNumber, &PersonWithCell::SetCellNumber);
  class_<PhoneBook>("PhoneBook")
    .def("size", &PhoneBook::GetSize)
    .def("add_person", &PhoneBook::AddPerson)
    .def("remove_person", &PhoneBook::RemovePerson)
