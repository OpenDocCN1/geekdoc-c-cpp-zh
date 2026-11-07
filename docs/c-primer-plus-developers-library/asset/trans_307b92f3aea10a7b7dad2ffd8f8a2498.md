
## 初始化顺序

当成员初始化列表初始化多个项时，这些项按它们在类中声明的顺序初始化，而不是按它们在初始化列表中出现的顺序初始化。例如，假设你这样编写一个 Student 构造函数：

```cpp
Student(const char * str, const double * pd, int n)
    : scores(pd, n), name(str) {}
```

name 成员仍会首先被初始化，因为它在类定义中首先声明。确切的初始化顺序在这个例子中并不重要，但如果代码使用一个成员的值作为另一个成员初始化表达式的一部分，那就很重要了。

## 使用被包含对象的接口

被包含对象的接口不是公有的，但可以在类方法内部使用。例如，下面是如何定义一个返回学生成绩平均值的函数：

```cpp
double Student::Average() const
{
    if (scores.size() > 0)
        return scores.sum()/scores.size();
    else
        return 0;
}
```

这定义了一个可由 Student 对象调用的方法。在内部，它使用 valarray 的 size() 和 sum() 方法。这是因为 scores 是一个 valarray 对象，所以它可以调用 valarray 类的成员函数。简而言之，Student 对象调用一个 Student 方法，而该 Student 方法使用被包含的 valarray 对象来调用 valarray 方法。

类似地，你可以定义一个友元函数，它使用 string 版本的 << 运算符：

```cpp
// use string version of operator<<()
ostream & operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << ":\n";
    ...
}
```

因为 stu.name 是一个 string 对象，所以它调用 operator<<(ostream &, const string &) 函数，该函数作为 string 类包的一部分提供。注意，operator<<(ostream & os, const Student & stu) 函数必须是 Student 类的友元，以便它能访问 name 成员。（或者，该函数可以使用公有的 Name() 方法，而不是私有的 name 数据成员。）

类似地，该函数可以使用 valarray 的 << 实现进行输出；不幸的是，并没有这样的实现。因此，该类定义了一个私有辅助方法来处理此任务：

```cpp
// private method
ostream & Student::arr_out(ostream & os) const
{
    int i;
    int lim = scores.size();
    if (lim > 0)
    {
        for (i = 0; i < lim; i++)
        {
            os << scores[i] << " ";
            if (i % 5 == 4)
                os << endl;
        }
        if (i % 5 != 0)
            os << endl;
    }
    else
        os << "empty array";
    return os;
}
```

使用这样的辅助函数可以将杂乱的细节集中在一处，并使友元函数的编码更整洁：

```cpp
// use string version of operator<<()
ostream & operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << ": \n";
    stu.arr_out(os); // use private method for scores
    return os;
}
```

如果你选择提供其他用户级输出函数，该辅助函数也可以作为它们的构建块。

程序清单 14.2 展示了 Student 类的类方法文件。它包括允许你使用 [] 运算符访问 Student 对象中各个成绩的方法。

### 程序清单 14.2 studentc.cpp

```cpp
// studentc.cpp -- Student class using containment
#include "studentc.h"
using std::ostream;
using std::endl;
using std::istream;
using std::string;

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
    return scores[i];          // use valarray<double>::operator[]()
}

double Student::operator[](int i) const
{
    return scores[i];
}

// private method
ostream & Student::arr_out(ostream & os) const
{
    int i;
    int lim = scores.size();
    if (lim > 0)
    {
        for (i = 0; i < lim; i++)
        {
            os << scores[i] << " ";
            if (i % 5 == 4)
                os << endl;
        }
        if (i % 5 != 0)
            os << endl;
    }
    else
        os << " empty array ";
    return os;
}

// friends
// use string version of operator>>()
istream & operator>>(istream & is, Student & stu)
{
    is >> stu.name;
    return is;
}

// use string friend getline(istream &, const string &)
istream & getline(istream & is, Student & stu)
{
    getline(is, stu.name);
    return is;
}

// use string version of operator<<()
ostream & operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << ":\n";
    stu.arr_out(os);  // use private method for scores
    return os;
}
```

除了私有辅助方法之外，程序清单 14.2 不需要太多新代码。使用包含可以让你利用自己或他人已经编写的代码。

## 使用新的 Student 类

让我们编写一个小程序来测试新的 Student 类。为简单起见，它应使用一个仅包含三个 Student 对象的数组，每个对象保存五个测验成绩。并且它应使用一个简单的输入循环，不验证输入，也不允许你提前结束输入过程。程序清单 14.3 给出了测试程序。请务必将其与 studentc.cpp 一起编译。

### 程序清单 14.3 use_stuc.cpp

```cpp
// use_stuc.cpp -- using a composite class
// compile with studentc.cpp
#include <iostream>
#include "studentc.h"
using std::cin;
using std::cout;
using std::endl;

void set(Student & sa, int n);

const int pupils = 3;
const int quizzes = 5;

int main()
{
    Student ada[pupils] =
        {Student(quizzes), Student(quizzes), Student(quizzes)};

    int i;
    for (i = 0; i < pupils; ++i)
        set (ada[i], quizzes);
    cout << "\nStudent List:\n";
    for (i = 0; i < pupils; ++i)
        cout << ada[i].Name() << endl;
    cout << "\nResults:";
    for (i = 0; i < pupils; ++i)
    {
        cout << endl << ada[i];
        cout << " average: " << ada[i].Average() << endl;
    }
    cout << "Done.\n";
    return 0;
}

void set(Student & sa, int n)
{
    cout << "Please enter the student's name: ";
    getline(cin, sa);
    cout << "Please enter " << n << " quiz scores:\n";
    for (int i = 0; i < n; i++)
        cin >> sa[i];
    while (cin.get() != '\n')
        continue;
}
```

下面是程序清单 14.1、14.2 和 14.3 中程序的示例运行：

```text
Please enter the student's name: Gil Bayts
Please enter 5 quiz scores:
92 94 96 93 95
Please enter the student's name: Pat Roone
Please enter 5 quiz scores:
83 89 72 78 95
Please enter the student's name: Fleur O'Day
Please enter 5 quiz scores:
92 89 96 74 64
Student List:
Gil Bayts
Pat Roone
Fleur O'Day

Results:
Scores for Gil Bayts:
92  94  96  93  95
average: 94

Scores for Pat Roone:
83  89  72  78  95
average: 83.4

Scores for Fleur O'Day:
92  89  96  74  64
average: 83
Done.
```

## 私有继承

C++ 有第二种实现 *有一个* 关系的方法：私有继承。使用 *私有继承* 时，基类的公有成员和保护成员成为派生类的私有成员。这意味着基类的方法不会成为派生对象公有接口的一部分。不过，它们可以在派生类的成员函数内部使用。

让我们更仔细地研究接口主题。使用公有继承时，基类的公有方法成为派生类的公有方法。简而言之，派生类继承基类的接口。这是 *是一个* 关系的一部分。使用私有继承时，基类的公有方法成为派生类的私有方法。简而言之，派生类不继承基类的接口。正如你在被包含对象中看到的那样，这种不继承是 *有一个* 关系的一部分。

使用私有继承时，类确实继承实现。例如，如果你以 string 类作为 Student 类的基类，Student 类最终会得到一个继承的 string 类组件，可用于存储字符串。此外，Student 方法可以在内部使用 string 方法访问该 string 组件。

包含将一个对象作为命名成员对象添加到类中，而私有继承将一个对象作为未命名的继承对象添加到类中。本书使用术语 *子对象* 来表示通过继承或包含添加的对象。

因此，私有继承提供了与包含相同的特性：获得实现，不获得接口。因此，它也可以用来实现 *有一个* 关系。事实上，你可以生成一个使用私有继承的 Student 类，并且其公有接口与包含版本相同。因此，两种方法之间的差异影响的是实现，而不是接口。让我们看看如何使用私有继承重新设计 Student 类。

