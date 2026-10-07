
在 `c` 作为成员的类中查找这些函数，它使用了基类的成员函数。

## 派生类构造函数

我们的程序中存在一个潜在的缺陷。如果我们想将一个 `CountDn` 对象初始化为一个值呢？`Counter` 中的单参数构造函数可以使用吗？不，不能！

虽然编译器会替换来自基类的默认构造函数，但它在更复杂的构造函数面前就停止了。因此，类必须为派生类编写一组新的构造函数：

```
class CountDn : public Counter {
public:
    CountDn() : Counter() {}
    CountDn(int c) : Counter(c) {}
    CountDn operator--() {
        --count;
        return *this;
    }
};

int main() {
    CountDn c1, c2(100);
    return 0;
}
```

在这里，

```
CountDn() : Counter() {}
```

导致 `CountDn` 的默认构造函数调用基类中的 `Counter` 默认构造函数

```
CountDn(int c) : Counter(c)
```

导致 `CountDn` 的单参数构造函数调用基类中的 `Counter` 单参数构造函数。

注意，CountDn 构造函数可以添加自己的语句，但在这种情况下它不需要这样做，大括号是空的。但如果它定义了一个新的数据成员，它可以在这里初始化它，然后调用基类构造函数来初始化对象的其余部分。稍后会详细介绍。

## 保护访问修饰符

- 类的成员函数可以访问私有和公共成员。
- 类的对象只能访问公共成员。
- 私有成员是私有的。

如果我们不使用继承，这些就是我们需要知道的。有了继承，就有了新的可能性。我们目前关注的问题是：

派生类的成员函数可以访问基类的数据成员吗？例如，`CountDn` 中的 `operator--()` 可以访问 `Counter` 中的 `count` 吗？

答案是，如果成员是公有的或保护的，那么成员函数就可以访问基类的成员。它们无法访问私有成员。

我们不希望将 `count` 设置为公共，因为那将允许程序中任何位置的函数访问它，并消除数据隐藏的优势。相反，保护成员可以被其所属类或任何派生自该类的成员函数访问。它不能从类外部的函数访问，例如 `main()`，这正是我们想要的！

所以，保护类成员是私有成员和公共成员之间的折中方案。

- 与公共成员一样，保护成员只能被其他类成员函数访问。在类外部，保护成员是不可见的。
- 与公共成员一样，保护成员被派生类继承，并可以被派生类中的成员函数访问。

在决定将成员设为私有、保护还是公共时，请记住以下规则：

- 私有成员仅供声明该私有成员的类中的成员访问。
- 保护成员可以被其所属类的成员以及任何派生类中的任何成员访问。
- 公共成员可以被类自身的成员、派生类的成员以及该类的所有其他用户访问。

| 访问修饰符 | 从所属类访问 | 从派生类访问 | 从类外对象访问 |
| --- | --- | --- | --- |
| private | 是 | 否 | 否 |
| protected | 是 | 是 | 否 |
| public | 是 | 是 | 是 |

其道理是，如果你正在编写一个怀疑未来某个时间点可能会被其他类使用的类，那么派生类可能需要访问的任何数据都应该是受保护的而不是私有的。这确保了类是“为继承就绪的”——这是借用电视广告的一句说法。

注意，继承不是反向的。基类及其对象并不知道任何派生自基类的类。例如，在类中：

```
Counter c;
```

基类无法使用任何派生自基类的类。如果你想让 `CountDn` 使用 `operator()`，它必须是 `Counter`。

## Employee 类

考虑以下 `Employee` 类：

```
// employee.h

#ifndef EMPLOYEE_H
#define EMPLOYEE_H

using namespace std;

class Employee {
protected:
    char *name;
    char *address;
    int age;
    int dependent;
    int jobClass;
public:
    Employee(char *, char *, int, int);
    ~Employee();
    void display();
    int getAge();
    int getDependent();
    int getClassName();
};

#endif
```

```cpp
// employee.cpp

#include <iostream>
#include <string>
#include "employee.h"

Employee::Employee(char *nm, char *ad, int a, int d) {
    name = new char[strlen(nm) + 1];
    strcpy(name, nm);
    address = new char[strlen(ad) + 1];
    strcpy(address, ad);
    age = a;
    dependent = d;
    jobClass = 0;
}

Employee::~Employee() {
    delete[] name;
    delete[] address;
}

void Employee::display() {
    cout << name << endl;
    cout << address << endl;
    cout << age << endl;
    cout << dependent << endl;
    cout << jobClass << endl;
}

int Employee::getAge() {
    return age;
}

int Employee::getDependent() {
    return dependent;
}

int Employee::getClassName() {
    return jobClass;
}
```

`Employee` 构造函数会初始化 `name`、`address`、`age` 和 `dependent`。`jobClass` 被初始化为 0。

`CountDn` 派生类定义如下：

```cpp
// countdn.h

#ifndef COUNTDN_H
#define COUNTDN_H

#include "employee.h"

class CountDn : public Employee {
private:
    int count;
public:
    CountDn();
    CountDn(int c);
    ~CountDn();
    CountDn& operator--();
    void display();
};

#endif
```

```cpp
// countdn.cpp

#include <iostream>
#include <string>
#include "countdn.h"

CountDn::CountDn() : Employee("Default", "Default", 0, 0) {
    count = 0;
}

CountDn::CountDn(int c) : Employee("Default", "Default", 0, 0) {
    count = c;
}

CountDn::~CountDn() {
}

CountDn& CountDn::operator--() {
    --count;
    return *this;
}

void CountDn::display() {
    Employee::display();
    cout << count << endl;
}
```

找到这些函数在 `c` 作为成员的类中，它使用了基类的成员函数。

## 派生类构造函数

我们的程序中存在一个潜在的缺陷。如果我们想将一个 `CountDn` 对象初始化为一个值呢？`Counter` 中的单参数构造函数可以使用吗？不，不能！

虽然编译器会替换来自基类的默认构造函数，但它在更复杂的构造函数面前就停止了。因此，类必须为派生类编写一组新的构造函数：

```
class CountDn : public Counter {
public:
    CountDn() : Counter() {}
    CountDn(int c) : Counter(c) {}
    CountDn operator--() {
        --count;
        return *this;
    }
};

int main() {
    CountDn c1, c2(100);
    return 0;
}
```

在这里，

```
CountDn() : Counter() {}
```

导致 `CountDn` 的默认构造函数调用基类中的 `Counter` 默认构造函数

```
CountDn(int c) : Counter(c)
```

导致 `CountDn` 的单参数构造函数调用基类中的 `Counter` 单参数构造函数。

注意，CountDn 构造函数可以添加自己的语句，但在这种情况下它不需要这样做，大括号是空的。但如果它定义了一个新的数据成员，它可以在这里初始化它，然后调用基类构造函数来初始化对象的其余部分。稍后会详细介绍。

## 保护访问修饰符

- 类的成员函数可以访问私有和公共成员。
- 类的对象只能访问公共成员。
- 私有成员是私有的。

如果我们不使用继承，这些就是我们需要知道的。有了继承，就有了新的可能性。我们目前关注的问题是：

派生类的成员函数可以访问基类的数据成员吗？例如，`CountDn` 中的 `operator--()` 可以访问 `Counter` 中的 `count` 吗？

答案是，如果成员是公有的或保护的，那么成员函数就可以访问基类的成员。它们无法访问私有成员。

我们不希望将 `count` 设置为公共，因为那将允许程序中任何位置的函数访问它，并消除数据隐藏的优势。相反，保护成员可以被其所属类或任何派生自该类的成员函数访问。它不能从类外部的函数访问，例如 `main()`，这正是我们想要的！

所以，保护类成员是私有成员和公共成员之间的折中方案。

- 与公共成员一样，保护成员只能被其他类成员函数访问。在类外部，保护成员是不可见的。
- 与公共成员一样，保护成员被派生类继承，并可以被派生类中的成员函数访问。

在决定将成员设为私有、保护还是公共时，请记住以下规则：

- 私有成员仅供声明该私有成员的类中的成员访问。
- 保护成员可以被其所属类的成员以及任何派生类中的任何成员访问。
- 公共成员可以被类自身的成员、派生类的成员以及该类的所有其他用户访问。

| 访问修饰符 | 从所属类访问 | 从派生类访问 | 从类外对象访问 |
| --- | --- | --- | --- |
| private | 是 | 否 | 否 |
| protected | 是 | 是 | 否 |
| public | 是 | 是 | 是 |

其道理是，如果你正在编写一个怀疑未来某个时间点可能会被其他类使用的类，那么派生类可能需要访问的任何数据都应该是受保护的而不是私有的。这确保了类是“为继承就绪的”——这是借用电视广告的一句说法。注意，继承不是反向的。基类及其对象并不知道任何派生自基类的类。例如，在类中：

```
Counter c;
```

基类无法使用任何派生自基类的类。如果你想让 `CountDn` 使用 `operator()`，它必须是 `Counter`。

## Employee 类

考虑以下 `Employee` 类：

```
// employee.h

#ifndef EMPLOYEE_H
#define EMPLOYEE_H

using namespace std;

class Employee {
protected:
    char *name;
    char *address;
    int age;
    int dependent;
    int jobClass;
public:
    Employee(char *, char *, int, int);
    ~Employee();
    void display();
    int getAge();
    int getDependent();
    int getClassName();
};

#endif
```

```cpp
// employee.cpp

#include <iostream>
#include <string>
#include "employee.h"

Employee::Employee(char *nm, char *ad, int a, int d) {
    name = new char[strlen(nm) + 1];
    strcpy(name, nm);
    address = new char[strlen(ad) + 1];
    strcpy(address, ad);
    age = a;
    dependent = d;
    jobClass = 0;
}

Employee::~Employee() {
    delete[] name;
    delete[] address;
}

void Employee::display() {
    cout << name << endl;
    cout << address << endl;
    cout << age << endl;
    cout << dependent << endl;
    cout << jobClass << endl;
}

int Employee::getAge() {
    return age;
}

int Employee::getDependent() {
    return dependent;
}

int Employee::getClassName() {
    return jobClass;
}
```

`Employee` 构造函数会初始化 `name`、`address`、`age` 和 `dependent`。`jobClass` 被初始化为 0。

`CountDn` 派生类定义如下：

```cpp
// countdn.h

#ifndef COUNTDN_H
#define COUNTDN_H

#include "employee.h"

class CountDn : public Employee {
private:
    int count;
public:
    CountDn();
    CountDn(int c);
    ~CountDn();
    CountDn& operator--();
    void display();
};

#endif
```

```cpp
// countdn.cpp

#include <iostream>
#include <string>
#include "countdn.h"

CountDn::CountDn() : Employee("Default", "Default", 0, 0) {
    count = 0;
}

CountDn::CountDn(int c) : Employee("Default", "Default", 0, 0) {
    count = c;
}

CountDn::~CountDn() {
}

CountDn& CountDn::operator--() {
    --count;
    return *this;
}

void CountDn::display() {
    Employee::display();
    cout << count << endl;
}
```
