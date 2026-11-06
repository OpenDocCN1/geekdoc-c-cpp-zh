
除了主要的 `EthicalCompetition` 类之外，你可能还会创建一些辅助类，供 `EthicalCompetition` 类使用，但你的同事不会直接创建它们的实例。其中一个可能是一个名为 `Connection` 的类，负责处理连接到参赛者计算机的任务。

第一个问题是：`Connection` 类可能是你编写的，但某个地方可能有*另一个*类也叫 `Connection`，而你的同事可能需要使用那个类。第二个问题是：如果你有这个 `Connection` 类，你可能不希望同事使用它。你只希望他们使用主接口，也就是 `EthicalCompetition` 类。

要解决名称唯一性的问题，你有几种选择。其一，你可以直接给这个类起一个稍微更独特的名字，例如 `EthicalCompetitionConnection`。但这有点长。而且，如果它除了在 `EthicalCompetition` 的代码内部使用之外根本不会被用到，又何必费这么多周折呢？不过，你也可以缩短类名，把它称为一个很可能唯一的名称，例如 `ECConnection`。

但同时，如果你的类的使用者查看头文件并看到一整组类，他们可能不清楚应该使用哪些类。（当然，你会编写一些文档来说明这一点，但你确实希望代码至少在某种程度上是不言自明的。）

一种解决方案是使用*嵌套*类。使用嵌套类时，你先编写主类 `EthicalCompetition` 的声明，然后在类内部编写支持类，如下所示：

```cpp
class EthicalCompetition
{
private:
    class Connection
    {
    public:
        void Connect();
    };

public:
    void HardWork();
};
```

注意，我们在一个类内部编写了一个类。我们没有提供函数本身的代码，因此如下所示：

```cpp
void EthicalCompetition::HardWork()
{
    Connection c;
    c.Connect();
    cout << "Connected" << endl;
}
```

下面是一系列技巧，专门向你展示如何创建那个内部类定义。第一个技巧是，我们需要向你展示如何用前向声明来声明该类，但把类定义放在外部类之外。（**注意：** 永远不要将内部类定义放在外部类定义的私有或受保护区段内；这样做行不通。）以下代码为你处理了该声明：

```cpp
class EthicalCompetition
{
private:
    class Connection;

public:
    void HardWork();
};

class EthicalCompetition::Connection
{
public:
    void Connect();
};
```

这里，在外部类内部，我们只为内部类写了一个头部和一个分号，而不是写出整个内部类；这就是前向声明。然后，我们在外部类之后编写了内部类的其余部分。为了让这种做法生效，我们必须再次完全限定类的名称，如下所示：

```cpp
class EthicalCompetition::Connection
```

![](img/6ba99460b0feb3585671a4612ff5fabb_541_0.png)

如果我们省略 `EthicalCompetition` 这个词和两个冒号，编译器会把该类当作另一个不同的类来编译。之后，编译器会报错，说找不到 `Connection` 类的其余声明。错误是

```
error: aggregate 'EthicalCompetition::Connection c' has incomplete type and
       cannot be defined
```

记住这条消息，这样当你忘记外部类名时，就知道如何更正它。

![](img/6ba99460b0feb3585671a4612ff5fabb_541_1.png)

通过在外层类之后声明内层类，你现在可以使用另一个技巧。其思路是编写代码，使得只有外层类能够访问这些成员。为此，你可以将内层类的所有成员设为私有或受保护，然后让外层类 `EthicalCompetition` 成为内层类 `Connection` 的友元。

以下是 Connection 类的修改版本：

```cpp
class EthicalCompetition::Connection
{
protected:
    friend class EthicalCompetition;
    void Connect();
};
```

只有外层类可以访问它的大多数成员。但我们说**大多数**，是因为我们遗漏了一些东西。尽管成员是受保护的，但没有任何东西能阻止 `EthicalCompetition` 之外的用户创建该类的实例。为了增加这层安全性，你需要为该类提供一个 *私有* 或 *受保护* 的构造函数。当你为构造函数这样做时，最好也对析构函数照做。把析构函数也设为私有或受保护。即使构造函数和析构函数不做任何事情，通过将它们设为私有或受保护，你也能阻止其他人创建该类的实例——这里说的其他人，是指除该类的任何友元之外的人。

因此，这里是该类的又一个版本：

```cpp
class EthicalCompetition::Connection
{
protected:
    friend class EthicalCompetition;
    void Connect();
    Connection() {}
    ~Connection() {}
};
```

这样就能达到目的。当我们在 `EthicalCompetition` 之外（例如在 `main()` 中）尝试创建该类的实例时，如下所示：

```cpp
EthicalCompetition::Connection myconnect;
```

我们会看到以下消息：

```
'EthicalCompetition::Connection::~Connection()' is protected
```

不过，我们仍然可以在 `EthicalCompetition` 的成员函数内部创建实例。成功了！代码清单 4-4 中所示的 ProtectingEmbedded 示例包含了最终应用程序。

### 代码清单 4-4：保护内嵌类

```cpp
#include <iostream>
using namespace std;

class EthicalCompetition {
private:
    class Connection;
public:
    void HardWork();
};
class EthicalCompetition::Connection {
protected:
    friend class EthicalCompetition;
    void Connect();
    Connection() {}
    ~Connection() {}
};

void EthicalCompetition::HardWork() {
    Connection c;
    c.Connect();
    cout << "Connected" << endl;
}
void EthicalCompetition::Connection::Connect() {
    cout << "Connecting..." << endl;
}
int main(int argc, char *argv[])
{
    // EthicalCompetition::Connection myconnect;
    EthicalCompetition comp;
    comp.HardWork();
    return 0;
}
```

我们特意保留了一行被注释掉的代码，其中我们尝试创建内部类 Connection 的实例。之前，我们把这一行放在那里，但没有注释掉；这样我们就能看到它会打印出哪条错误消息，并告诉你。如果你想看到该错误消息，可以移除两个斜杠，这样编译器就会尝试编译这一行。

### 类中的类型

当你声明一个类型（例如枚举）时，将它和一个类关联起来可能很方便。例如，你可能有一个名为 Cheesecake 的类。在这个类中，你可能有一个成员变量 SelectedFlavor。SelectedFlavor 成员可以是你自己定义的枚举类型，例如 Flavor，如下所示：

```cpp
enum Flavor
{
    ChocolateSuicide,
    SquishyStrawberry,
    BrokenBanana,
    PrettyPlainVanilla,
    CoolLuh,
    BizarrePurple
};
```

要将这些与一个类关联起来，你可以将它们放入一个类中，如下所示：

```cpp
class Cheesecake
{
public:
    enum Flavor
    {
        ChocolateSuicide, SquishyStrawberry, BrokenBanana,
        PrettyPlainVanilla, CoolLuh, BizarrePurple
    };

    Flavor SelectedFlavor;
    int AmountLeft;
};
```

![](img/6ba99460b0feb3585671a4612ff5fabb_545_0.png)

当你在类内部声明一个类型（使用 `typedef` 或 `enum`）时，使用该类型并不需要存在该类的实例。但你必须完全限定名称。因此，你可以创建一个 `Cheesecake::Flavor` 类型的变量，并在应用程序中使用它，而无需创建 `Cheesecake` 的实例。

![](img/6ba99460b0feb3585671a4612ff5fabb_545_1.png)

你有希望仅在类内部使用的类型吗？把它们设为受保护或私有。这样你就无法在类外部使用它们。

与嵌套类不同，你可以将类中的类型设为私有或受保护。如果这样做，你就只能在类的成员函数内部使用该类型。如果你尝试在类外部使用该类型（包括设置成员变量，如 `yum.SelectedFlavor = Cheesecake::SquishyStrawberry;`），就会遇到编译器错误。

![](img/6ba99460b0feb3585671a4612ff5fabb_545_2.png)

你也可以像在类中放置 `enum` 一样，在类中放置 `typedef`，如下例所示：

```cpp
class SpongeCake
{
public:
    typedef int SpongeNumber;
    SpongeNumber weight;
    SpongeNumber diameter;
};

int main(int argc, char *argv[])
{
    SpongeCake::SpongeNumber myweight = 30;
    SpongeCake fluff;
    fluff.weight = myweight;
    return 0;
}
```
