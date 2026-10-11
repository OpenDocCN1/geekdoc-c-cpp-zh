
和往常一样，类将数据成员设为私有。这意味着 `Student` 类的成员函数可以使用 `string` 和 `valarray<double>` 的公共接口来访问和修改 `name` 以及 `scores` 对象，但外部世界无法这样做。外部世界对 `name` 和 `scores` 的唯一访问方式是通过为 `Student` 类定义的公共接口（见图 14.1）。描述这种现象的一种常用方法是：`Student` 获得了其成员对象的实现，而不是继承其接口。例如，`Student` 对象使用 `string` 的实现，而不是 `char* name` 或 `char name` 实现来持有名称。但 `Student` 对象本身并不具备原生使用 `string` 的 `operator+=` 函数进行追加的能力。

## 接口与实现

通过公有继承，类继承了一个接口，可能还继承了一个实现。（基类中的纯虚函数可以提供一个没有实现的接口）。获取接口是“是一个”关系的一部分。另一方面，通过组合，类获得了实现而没有接口。不继承接口是“有一个”关系的一部分。

类对象自动获取被包含对象的接口，对于“有一个”关系来说是一件好事。例如，`string` 重载了 `+` 运算符来连接两个字符串，从概念上说说，连接两个 `Student` 对象是没有意义的。其中原因之一是在这种情况下不应该使用公有继承。另一方面，被包含类的接口部分内容对于新类来说可能是有意义的。例如，你可能想使用 `string` 接口中的 `operator<()` 方法，通过定义一个内部使用 `string::operator<>()` 函数的 `Student::operator<()` 成员函数来按名称对 `Student` 对象。让我们进入细节。

## 带有成员对象的类

![](img/cd111a87c1db9aff4db4b18834327463_803_0.png)

- 通过 `Student` 类作用域访问

```cpp
class Student
private:
    string name;
    valarray<double> scores;
};
```

### 初始化顺序

当你有一个初始化了多个项的成员初始化列表时，这些项是按照它们声明的顺序进行初始化的，而不是按照它们在初始化列表中出现的顺序。例如，你这样写一个 `Student` 构造函数：

```cpp
Student(const char * str, const double * pd, int n)
    : scores(pd, n), name(str) {}
```

`name` 成员仍然会被先初始化，因为它在类定义中是先声明的。对于这个例子来说，精确的初始化顺序并不重要，但如果代码在使用一个成员的值作为第二个成员初始化表达式的一部分，那么顺序就变得重要了。

### 对包含对象使用接口

被包含对象的接口不是公开的，但可以在类方法内部使用。例如，这里是定义一个返回学生分数平均值的方法：

```cpp
double Student::Average() const
{
    if (scores.size() > 0)
        return scores.sum()/scores.size();
    else
        return 0;
}
```

这定义了一个可以被 `Student` 对象调用的方法。在内部，它使用了 `vararray` 的 `size()` 和 `sum()` 方法。这是因为 `scores` 是一个 `vararray` 对象，所以它可以调用 `vararray` 类的成员函数。简而言之，`Student` 对象调用了一个方法，而 `Student` 方法使用包含的 `vararray` 对象来调用 `vararray` 方法。

同样，你可以定义一个使用字符串版本 `<<` 运算符的友函数：

```cpp
// use string version of operator<<()
ostream & operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << ":\n";
```

由于 `stu.name` 是一个字符串对象，它调用了 `operator<< (ostream &, const string&)` 函数，该函数是字符串类包的一部分。请注意，`operator<< (ostream & os, const Student & stu)` 函数必须是 `Student` 类的友元，这样它才能访问 `name` 成员。（或者，该函数可以使用公开的 `Name()` 方法而不是私有的 `name` 数据成员。）

同样，该函数可以使用 `vararray` 的 `<<` 实现来进行输出；遗憾的是，并没有这种实现。因此，该类定义了一个私有辅助方法来处理这项任务：

```cpp
// private method
ostream & Student::arr_out(ostream & os)
{
    int i;
    int lim = scores.size();
    if (lim > 0) {
        for (i = 0; i < lim; i++) {
            os << scores[i] << " ";
            if (i % 5 == 4)
                os << endl;
        }
        if (i % 5 != 0)
            os << endl;
    }
    else {
        os << " empty array ";
    }
    return os;
}
```

使用这样的辅助函数可以将杂乱的细节集中在一个处，并使友函数的编码更加简单：

```cpp
// use string version of operator<<(\ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << "\n";
    stu.arr_out(os); // use private method for scores
    return os;
}
```

如果你选择提供其他用户级输出函数，该辅助函数也可以作为这些函数的构建块。列表 14.2 显示了 `Student` 类的类方法。它包含了允许你使用 `[]` 运算符来访问 `Student` 对象中单个分数的方法。

### 列表 14.2 studentc.cpp

```cpp
// studentc.cpp - Student class using containment
#include "student.h"
using std::ostream;
using std::endl;
using std::istream;
using std::string;
```

# 第 14 章在 C++ 中复用代码

```cpp
//public methods
double Student::Average() const
{
    if (scores.size() > 0)
        return scores.sum()/scores.size();
    else
        return 0;
}
const string & Student::Name() const
{
    return name;
}
double & Student::operator[](int i)
{
    return scores[i]; // use valarray<double>::operator[]
}
double Student::operator[](int i) const
{
    return scores[i];
}
// private method
ostream & Student::arr_out(ostream & os)
{
    int i;
    int lim = scores.size();
    if (lim > 0) {
        for (i = 0; i < lim; i++) {
            os << scores[i] << " ";
            if (i % 5 == 4)
                os << endl;
        }
        if (i % 5 != 0)
            os << endl;
    }
    else {
        os << " empty array ";
    }
    return os;
}
// use string version of operator<<()
ostream & operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << "\n";
    stu.arr_out(os); // use private method for scores
    return os;
}
```

### Student 类示例的新版本

要实现私有继承，在定义类时使用 `private` 关键字而不是 `public`。（实际上，`private` 是默认访问权限，因此省略访问修饰符也会导致私有继承。）`Student` 类应该继承自两个类，因此声明中应该列出这两者：

```cpp
class Student : private std::string, private std::valarray<double>
{
public:
    ...
};
```

拥有多个基类被称为多重继承（MI）。通常情况下，多重继承（尤其是复杂的 MI）可能会导致必须通过额外的语法规则解决的问题。我们将在本章的晚些部分讨论此类问题。但在这种情况下，MI 没有产生问题。

请注意，新类不需要私有数据。这是因为继承的类已经提供了所有需要的数据成员。该示例的包含版本（containment version）提供了两个显式命名的对象作为成员。然而，私有继承提供了两个无名的子类作为继承成员。这是两种方法之间的主要区别之一。

### 初始化基类组件

使用隐式继承的组件代替成员对象会影响此示例的编码，因为你无法再使用名称和分数来描述对象。相反，你必须回到用于公共继承的技术。例如，包含方法使用了这种构造函数，考虑一下构造函数：

```cpp
Student(const char * str, const double * pd, int n)
    : name(str), scores(pd, n) {} // 包含使用对象名称
```

新版本应该使用成员初始化列表处理继承的类，该列表使用成员的类名来标识构造函数：

```cpp
Student(const char * str, ArrayDB*pd, int n)
    : std::string(str), ArrayDB(pd, n) {} // 继承使用类名
```

在前面的示例中，`ArrayDB` 是 `std::array<double>` 的类型定义。务必注意，成员初始化列表使用的是 `std::string(str)` 术语而不是 `name(str)`。这是两种方法之间的第二个主要区别。

### 列表 14.4 student.h

```cpp
// student.h -- 使用私有继承定义 Student 类
#ifndef STUDENT_H_
#define STUDENT_H_
#include <iostream>
#include <valarray>
#include <string>
class Student : private std::string, private std::valarray<double>
{
private:
    typedef std::valarray<double> ArrayDb;
    // 用于 ostream 输出的私有方法
    std::ostream & arr_out(std::ostream & os) const;
public:
    Student() : std::string("Null Student"), ArrayDb() {}
    explicit Student(const std::string& s)
        : std::string(s), ArrayDb() {}
    explicit Student(int n)
        : std::string("Null"), ArrayDb(n)
    Student(const std::string& s, int n)
        : std::string(s), ArrayDb(n)
    Student(const std::string& s, const ArrayDb& a)
        : std::string(s), ArrayDb(a)
    Student(const char * str, const double * pd, int n)
        : std::string(str), ArrayDb(pd, n)
    ~Student() {}
    double Average() const;
    double& operator[](int i);
    double operator[](int i) const;
    const std::string& Name() const;
private:
    // 友
    // 输入
    friend std::istream& operator>>(std::istream & is,
                                    Student & stu);
    friend std::istream& getline(std::istream & is,
                                 Student & stu);
    // 输出
    friend std::ostream& operator<<(std::ostream & os,
                                   const Student & stu);
};
#endif
```

### 访问基类方法

私有继承将基类方法的使用限制在派生类方法中。然而，你可能希望公开某些功能。例如，`Student` 类声明暗示可以使用 `Average()` 函数。与包含方法类似，实现此的技术是使用 `size()` 和 `sum()` 方法（见图 14.2）。包含是在对象内部调用方法：

```cpp
double Student::Average() const
{
    if (scores.size() > 0)
        return scores.sum()/scores.size();
    else
        return 0;
}
```

（图 1.2 对象中的对象：私有继承。）

```cpp
class Student:private string, private valarray<double>
    ...
};
```

在这里，继承允许你使用类名和作用域解析运算符来调用基类方法：

```cpp
double Student::Average() const
{
    if (ArrayDb::size() > 0)
        return ArrayDb::sum()/ArrayDb::size();
    else
        return 0;
}
```

简而言之，包含方法使用对象名称来调用方法，而私有继承则使用类名和作用域解析运算符。

### 访问基类对象

作用域解析运算符允许你访问基类方法，但如果你需要基类对象本身呢？例如，`Student` 类版本实现 `Name()` 方法的方法是让方法返回成员字符串对象。但通过私有继承，字符串对象没有名称。`Student` 如何访问内部对象？因为 `Student` 继承自 `string`，所以进行类型转换是可能的。

```cpp
const string & Student::Name() const
{
    return (const string &)*this;
}
```

### 访问基类友元

通过类名显式限定函数的方法对于友元函数是无效的，因为友元函数不属于某个特定类。例如，考虑以下友元定义：

```cpp
ostream& operator<<(ostream &os, const Student & stu)
{
    os << "Scores for " << (const string)stu << "\n";
}
```

如果 `plato` 是 `Student` 对象，那么以下语句将调用该函数，其中 `stu` 是 `plato` 的引用，`os` 是 `cout` 的引用：

```cpp
cout << plato;
```

# 第14章 在 C++ 中复用代码

考虑以下代码行：

```cpp
os << "Scores for " << (const String&)stu << "\n";
```
