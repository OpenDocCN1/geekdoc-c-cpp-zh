
## 清单 3-2：自定义实例的复制

```cpp
#include <iostream>

using namespace std;

class Copyable {
protected:
    static int NextAvailableID;
    int UniqueID;
public:
    int SomeNumber;
    int GetID() { return UniqueID; }
    Copyable();
    Copyable(int x);
    Copyable(const Copyable& source);
};

Copyable::Copyable() {
    UniqueID = NextAvailableID;
    NextAvailableID++;
}

Copyable::Copyable(int x) {
    UniqueID = NextAvailableID;
    NextAvailableID++;
    SomeNumber = x;
}

Copyable::Copyable(const Copyable& source) {
    UniqueID = NextAvailableID;
    NextAvailableID++;
    SomeNumber = source.SomeNumber;
}

int Copyable::NextAvailableID;

int main() {
    Copyable take1 = 100;
    Copyable take2;
    take2.SomeNumber = 200;
    Copyable take3 = take1;
    cout << take1.GetID() << " "
         << take1.SomeNumber << endl;
    cout << take2.GetID() << " "
         << take2.SomeNumber << endl;
    cout << take3.GetID() << " "
         << take3.SomeNumber << endl;
    return 0;
}
```

运行此应用程序时，你会看到以下输出：

```text
0 100
1 200
2 100
```

关于这段代码，你需要了解两件事：

- **带 const 实例的复制构造函数。** C++ 有一条规则：必须使用 const 实例来创建副本。如果省略 const，这一行将无法正确编译。
- **手动从一个实例复制属性到另一个实例。** 既然该类有了自己的复制构造函数，计算机就不会像代码缺少复制构造函数时那样复制成员。

清单 3-2 使用一个静态成员来跟踪下一个可用的 UniqueID。记住，一个类在其所有实例之间共享单个静态成员。因此，只有一个 NextAvailableID 实例，并且它由 Copyable 类的所有实例共享。

## 当构造函数出错时

假设你正在编写一个类，它将连接到互联网并自动下载 Upper Zamboni 国的最新天气报告。问题在于：你是否把连接互联网的代码放进构造函数中？

人们经常面临这个常见的设计问题。把初始化代码放在构造函数中有许多优点。其一，你可以生成一个可用的实例，而不必先创建它，再调用一个单独的初始化方法。一般来说，这种方法效果很好。

然而，有时初始化过程可能产生错误。例如，假设构造函数无法连接互联网。记住：构造函数不返回值。因此，你不能让它返回例如一个 bool 来表示它是否成功完成了工作。

```cpp
class Container {
public:
  LittleInst first;
  LittleInst *second;
  Container();
};

Container::Container() {
  first.MyNumber = 1;
  second = new LittleInst;
  second->MyNumber = 2;
}
```

你看到了两个类：LittleInst 和 Container。Container 类持有一个 LittleInst 实例（名为 first 的属性）和一个指向 LittleInst 的指针。构造函数设置两个 LittleInst 实例。对于 first，它已经存在，你只需配置 first 的 MyNumber 成员。但 second 只是一个指针，因此代码会先创建实例，然后才能配置 second 的 MyNumber 成员。于是我们有了两个实例：一个是指针，一个是常规实例。

现在假设你这样使用这些类：

```cpp
Container *inst = new Container;
delete inst;
```

Container 没有析构函数，因此问题在于 first 和 second 是否会被销毁。你会看到以下输出：

```text
1
```

这是 LittleInst 析构函数的输出。数字 1 对应 first 成员。所以你可以看到 first 被销毁了，而 second 没有。

![](img/128ab511de4e7360e167e3b15cdd5dd0_578_0.png)

规则如下：删除类的实例时，直接成员（即不是指针的成员）也会被删除。但是，如果有任何指针，你必须在析构函数中（或其他地方）手动删除它们。

有时你可能希望一个对象持有另一个类的实例，但希望在删除包含它的对象后仍保留该实例。在这种情况下，你就不会在析构函数中删除另一个实例。

## 构造函数、析构函数和异常

下面是对 `Container` 类的修改（见于 `Destructor02` 示例），它会删除第二个实例：

```cpp
class Container {
public:
  LittleInst first;
  LittleInst *second;
  Container();
  ~Container() { delete second; }
};
```

然后，当你再次运行这两行代码时：

```cpp
Container *inst = new Container;
delete inst;
```

你会看到以下输出，它删除了两个实例：

```text
2
1
```

在前面的输出中，你可以看到它先删除了第二个实例。原因是应用程序在销毁直接成员之前先调用析构函数。在这种情况下，当代码删除 `Container` 实例时，应用程序会先调用析构函数，再删除 first 成员。这实际上是个好主意，因为在析构函数代码中，你可能希望在属性被清除之前对它们做一些处理。

### 将析构函数设为虚函数

你可以（也应该）将析构函数设为虚函数——与构造函数不同（构造函数不能是虚函数，因为执行类的构造函数时，内存中还没有虚表，这意味着尚未定义虚指针）。原因在于，你可以将派生类的实例传递给接受基类的函数，如下所示：

```cpp
void ProcessAndDelete(DeleteMe *inst) {
  cout << inst->Number << endl;
  delete inst;
}
```

这个函数接受 `DeleteMe` 类的实例，对它做一些处理，然后删除它。现在，假设你有一个派生自 `DeleteMe` 的类——比如类 `Derived`。根据继承规则，你允许将 Derived 的实例传递给这个函数。但根据多态规则（如第 2 册第 3 章“用多态进行特化”一节所述），如果你希望 ProcessAndDelete() 函数调用 Derived 的重载方法，就需要将该方法设为虚函数。所有析构函数也是如此。清单 3-3 所示的 Destructor03 示例演示了如何将析构函数设为虚函数。

### 清单 3-3：将析构函数设为虚函数

```cpp
#include <iostream>

using namespace std;

class DeleteMe {
public:
  int Number;
  virtual ~DeleteMe();
};

class Derived : public DeleteMe {
public:
  virtual ~Derived();
};

DeleteMe::~DeleteMe() {
  cout << "DeleteMe::~DeleteMe()" << endl;
}

Derived::~Derived() {
  cout << "Derived::~Derived()" << endl;
}

void ProcessAndDelete(DeleteMe *inst) {
  cout << inst->Number << endl;
  delete inst;
}

int main() {
  DeleteMe *MyObject = new(Derived);
  MyObject->Number = 10;
  ProcessAndDelete(MyObject);
  return 0;
}
```

运行此应用程序时，delete 会调用 `Derived` 的析构函数，而后者又会调用基类的析构函数。得益于析构函数中的 cout 调用，你可以看到这一切是如何工作的。输出如下：

```text
10
Derived::~Derived()
DeleteMe::~DeleteMe()
```

第一行是 ProcessAndDelete() 的输出。中间一行是 Derived() 析构函数的输出，第三行是 DeleteMe() 析构函数的输出。代码传入一个 Derived 实例，应用程序调用 Derived 析构函数。

现在试试这个：从 DeleteMe 析构函数中移除 virtual：

```cpp
class DeleteMe {
public:
    int Number;
    ~DeleteMe();
};
```

编译并运行应用程序时，应用程序会调用基类析构函数。由于 ProcessAndDelete() 接受 DeleteMe 实例，你会看到以下输出：

```text
10
DeleteMe::~DeleteMe()
```

### 构造函数与析构函数的顺序

当基类和派生类中都有构造函数和析构函数，并且你创建派生类的实例时，请记住顺序：计算机首先创建基类的成员，然后调用基类的构造函数。接下来，计算机创建派生类的成员，然后调用派生类的构造函数。

销毁顺序相反。当销毁一个基类实例时，计算机首先调用派生类的析构函数，然后删除派生类的成员。接下来，计算机调用基类的析构函数，然后删除基类的成员。

