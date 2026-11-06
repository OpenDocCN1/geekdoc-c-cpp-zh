
但如果那段初始化代码可能导致错误呢？例如，假设构造函数无法连接到互联网。那该怎么办？记住：构造函数不返回值。所以你不能让它返回例如一个 `bool` 来表示它是否成功完成了工作。

对此你有很多选择，不同的人似乎对哪种选择最好持有相当强烈的意见。（有强烈意见的程序员？这倒是个不太可能的概念。）以下是我们见过的一些做法：

- **干脆别这么做：** 编写构造函数时，让它创建对象但不做任何实际工作。相反，把工作代码放到一个单独的成员函数中，该函数可以返回一个 `bool`，表示是否成功。
- **让构造函数完成工作：** 如果工作失败（例如无法连接到互联网），让构造函数把错误代码保存到一个成员变量中。创建实例时，你可以检查该成员变量，看看它是否正常工作。
- **让构造函数多做一点工作：** 如果工作失败，就抛出异常。那么在你的代码中，就要用 `try` 块包裹实例的创建，并包含一个异常处理程序。（关于 `try` 块和异常处理程序的更多信息，请参见本章后面的“为规则编写异常处理”。）

![](img/6ba99460b0feb3585671a4612ff5fabb_510_0.png)

我们不喜欢这种选择。如果其他人正在使用我们编写的类，我们不希望他们不得不走个过场，把它包在 `try` 块和异常处理程序里。但除了做个好人之外，避免这种选择还有一个实际原因：如果我们的队友是编程初学者，他们可能干脆跳过那部分。“哦，糟了。它永远不会失败的，”这可能是他们的态度。而当它真的在客户的电脑上失败时——只要有可能，就一定会发生，墨菲先生！——客户会因为其应用程序无法连接到互联网并崩溃而非常不高兴。

## 销毁你的实例

尽管构造函数用途广泛，似乎人们可以围绕它们写出整本书（很适合家庭故事时间阅读），但析构函数很简单，没有太多可说的。不过，你确实需要了解一些信息，才能让它们正常工作。

首先，析构函数不接受参数，而且（和构造函数一样）它们没有返回类型。所以关于这一点也没有太多可说的了。

有时你可能希望一个对象持有另一个类的实例，但又希望在删除包含它的对象之后仍保留该实例。在这种情况下，你就不会在析构函数中删除另一个实例。

下面是对 Container 类（见 Destructor02 示例）的修改，它会删除第二个实例：

```cpp
class Container
{
public:
    LittleInst first;
    LittleInst *second;
    Container();
    ~Container() { delete second; }
};
```

然后，当你再次运行下面这两行代码时

```cpp
Container *inst = new Container;
delete inst;
```

你会看到如下输出，它删除了两个实例：

```
2
1
```

在上面的输出中，你可以看到它先删除了第二个实例。原因是应用程序在销毁直接成员之前会先调用析构函数。在这种情况下，当我们删除 Container 实例时，应用程序先调用我们的析构函数，然后才删除我们的第一个成员。这实际上是个好主意，因为在我们析构函数的代码中，我们可能希望在成员变量被清除之前对它们做一些处理。

### 虚析构函数

你可以（而且应该）让析构函数成为虚函数——与构造函数不同。原因是你可以把派生类的实例传给一个接受基类的函数，就像这样：

```cpp
void ProcessAndDelete(DeleteMe *inst)
{
    cout << inst->Number << endl;
    delete inst;
}
```

这个函数接受 DeleteMe 类的实例，对它做一些处理，然后删除它。现在，假设你有一个从 DeleteMe 派生的类，比如 Derived 类。根据继承规则，你可以把 Derived 的实例传给这个函数。但根据*多态*的规则（如第二册第1章“用多态进行特化”一节所述），如果你希望 ProcessAndDelete() 函数调用 Derived 中重载的成员函数，就需要让该成员函数成为虚函数。所有析构函数也是如此。清单 3-3 中所示的 Destructor03 示例演示了这一点。

**清单 3-3：让析构函数成为虚函数**

```cpp
#include <iostream>

using namespace std;

class DeleteMe
{
public:
    int Number;
    virtual ~DeleteMe();
};

class Derived : public DeleteMe
{
public:
    virtual ~Derived();
};

DeleteMe::~DeleteMe()
{
    cout << "DeleteMe::~DeleteMe()" << endl;
}

Derived::~Derived()
{
    cout << "Derived::~Derived()" << endl;
}

void ProcessAndDelete(DeleteMe *inst)
{
    cout << inst->Number << endl;
    delete inst;
}

int main()
{
    DeleteMe *MyObject = new Derived;
    MyObject->Number = 10;
    ProcessAndDelete(MyObject);
    return 0;
}
```

运行这个应用程序时，由于析构函数中的 cout 调用，delete 会调用 Derived 的析构函数（它又会调用基类的析构函数）。输出如下：

```
10
Derived::~Derived()
DeleteMe::~DeleteMe()
```

## 构造函数和析构函数的顺序

当基类和派生类中都有构造函数和析构函数，并且你创建派生类的实例时，请记住这个顺序：计算机首先创建基类的成员，然后调用基类的构造函数。接下来，计算机创建派生类的成员，然后调用派生类的构造函数。

销毁的顺序相反。当你销毁派生类的实例时，计算机首先调用派生类的析构函数，然后删除派生类的成员。接下来，计算机调用基类的析构函数，然后删除基类的成员。

第一行是 `ProcessAndDelete` 函数的输出。中间一行是 `Derived` 析构函数的输出，第三行是 `DeleteMe` 析构函数的输出。我们传入了一个 `Derived` 实例，应用程序调用了 `Derived` 析构函数。

现在试试这个：从 `DeleteMe` 析构函数中移除 `virtual`：

```cpp
class DeleteMe
{
public:
    int Number;
    ~DeleteMe();
};
```

现在，当你编译并运行该应用程序时，应用程序会调用基类的析构函数。因为 `ProcessAndDelete()` 函数接受的是 `DeleteMe` 实例，所以你会看到如下输出：

```
10

DeleteMe::~DeleteMe()
```

在上面的示例中，析构函数不是虚函数；当你传入 `Derived` 实例时，它无法找到正确的析构函数。所以它只会调用参数中所列类型的析构函数。

![](img/6ba99460b0feb3585671a4612ff5fabb_514_0.png)

养成始终让析构函数成为虚函数的习惯是个好主意。这样一来，如果其他人编写了诸如 `ProcessAndDelete()` 这样的函数，你就可以确信他或她的函数会自动调用正确的析构函数。

## 为规则编写异常处理

*异常*是软件中发生的一种糟糕情况，它会导致应用程序不得不处理这种糟糕情况。例如，如果你尝试写入一个文件，但该文件不知怎么损坏了，你无法写入，操作系统可能会*抛出*一个异常。或者你可能有一个处理某些数据的函数，如果该函数遇到损坏的数据，它可能会抛出异常。

异常对 C++ 来说是新的；它们在 C 中并不存在。当异常刚出现时，人们对其有点怀疑，有些人甚至认为它们是坏的（这里的“坏”要加一个大大的*坏*字）。原因在于：反对异常的人觉得，编写过于依赖异常的代码太容易了。但你应该使用它们，因为它们能帮助你处理那些原本可能无法预料的情况。

清单 3-4 中所示的 Exception01 示例包含我们编写的一个会抛出异常的函数，以及一个使用该函数的完整应用程序。

**清单 3-4：抛出和捕获异常**

```cpp
#include <iostream>
#include <string>

using namespace std;

void ProcessData()
{
    throw new string("Oops, I found some bad data!");
}

int main()
{
    try
    {
        ProcessData();
        cout << "No problems!" << endl;
    }
    catch (string *excep)
    {
        cout << "Found an error. Here's the message:";
        cout << endl;
        cout << *excep;
        cout << endl;
    }
    cout << "All finished." << endl;

    return 0;
}
```
