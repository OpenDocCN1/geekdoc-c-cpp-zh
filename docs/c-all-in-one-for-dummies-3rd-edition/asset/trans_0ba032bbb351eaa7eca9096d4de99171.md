

Constructor02 示例演示了如何在类定义内部直接添加初始化器，如下所示：

```cpp
class MySharona
{
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona() : OneHitWonders(1), NumberRecordings(10) {}
};
```

当你创建这个类的一个实例时，OneHitWonders 成员获得值 1，NumberRecordings 成员获得值 10。注意语法：构造函数名和参数列表（此处为空）后面跟一个冒号。成员变量出现在其后，每个成员变量后面括号中跟一个初始值。成员变量之间用逗号分隔。

在成员变量之后，是左花括号，用于包含你想在构造函数中放入的任何代码。在这个例子中，我们没有代码，所以立即放了一个右花括号。

![](img/6ba99460b0feb3585671a4612ff5fabb_497_0.png)

你可以将类的任何成员变量放入初始化列表中，但不一定要包含全部。如果你不想初始化某些成员，可以不初始化。还要注意，你不能将继承来的成员放入初始化列表；只能包含类自身的成员。

你也可以通过构造函数传入这些初始值。下面是同一个类稍作修改的版本。这次构造函数有一个参数，我们将其保存在 NumberRecordings 成员中：

```cpp
class MySharona
{
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records) : OneHitWonders(1),
        NumberRecordings(Records) {}
};
```

通过将初始化列表与构造函数关联，你可以让不同的构造函数使用不同的初始化器。你不必为所有构造函数以相同方式初始化数据。

![](img/6ba99460b0feb3585671a4612ff5fabb_497_1.png)

你可能已经注意到，成员初始化的格式与初始化继承构造函数的方式类似。看看我们在这段代码中是如何调用基类构造函数的：

```cpp
class MySharona : public MusicInfo
{
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records, int Phone) : OneHitWonders(1),
        NumberRecordings(Records), MusicInfo(Phone) {}
};
```

仔细看区别：MySharona 类现在有两个参数。第二个是整数，我们通过以下部分将其传入基类：

```
MusicInfo(Phone)
```

因此，要使用这个类，你可以这样做：

```cpp
MySharona CD(20, 5551212);
```

这段代码创建了一个 MySharona 实例，其成员初始化为 OneHitWonders = 1、NumberRecordings = 20 和 PhoneNumber = 5551212。

如果你有重载的构造函数，你可以拥有不同的初始化集合。例如，再看一下 Constructor02 示例最终版本的又一次修改：

```cpp
class MusicInfo
{
public:
    int PhoneNumber;
    MusicInfo(int Phone) : PhoneNumber(Phone) {}
};

class MySharona : public MusicInfo
{
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records, int Phone) : MusicInfo(Phone),
        OneHitWonders(1), NumberRecordings(Records) {}

    MySharona(int Records) : MusicInfo(8675309),
        OneHitWonders(1), NumberRecordings(Records) {}
};
```

现在这个类有两个构造函数。我们结合了前两个版本，所以现在你可以使用任一构造函数。例如，你可以定义以下两个变量，每个使用不同的构造函数：

```cpp
MySharona CD(20, 5551212);
MySharona OldCD(30);
cout << CD.PhoneNumber << endl;
cout << OldCD.PhoneNumber << endl;
```

当你运行 cout 行时，它们对 PhoneNumber 成员有不同的值。第一个传入特定值；第二个接受默认值：

```text
5551212
8675309
```

你应该先初始化基类的值。否则，编译器在编译应用程序时可能会显示警告信息。

如果不同构造函数之间唯一的实际区别是用户是否提供一个值（如前一个示例所示），你可以使用一种稍好的方法。构造函数（实际上，C++ 中的任何函数）可以有默认值。Constructor03 示例通过使用默认值缩短了前面的示例。结果是相同的：

```cpp
class MusicInfo
{
public:
    int PhoneNumber;
    MusicInfo(int Phone) : PhoneNumber(Phone) {}
};

class MySharona : public MusicInfo
{
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records, int Phone=8675309) :
        MusicInfo(Phone), OneHitWonders(1),
        NumberRecordings(Records) {}
};
```

在前面的代码中，构造函数的第二个参数后面有一个等号和一个数字。这意味着类的使用者不必指定该参数。如果该参数不存在，它会自动获得值 8675309。

你可以在构造函数或任何其他函数中拥有任意数量的默认参数，但规则是默认参数必须放在末尾。一旦你有了一个默认参数，其后的所有参数都必须有默认值。因此，下面这类代码是不允许的。

```cpp
MySharona(int Records = 6, int Phone) :
    MusicInfo(Phone), OneHitWonders(1),
    NumberRecordings(Records) {}
```

![](img/6ba99460b0feb3585671a4612ff5fabb_500_0.png)

![](img/6ba99460b0feb3585671a4612ff5fabb_500_1.png)

![](img/6ba99460b0feb3585671a4612ff5fabb_500_2.png)

![](img/6ba99460b0feb3585671a4612ff5fabb_500_3.png)

## 第 IV 卷，第 3 章：构造函数、析构函数和异常

这种禁止有一个实际原因：当用户调用构造函数时（通过创建类型为 *MySharona* 的变量），没有办法只省略第一个参数而只保留第二个参数。除非 C++ 允许一个空参数后跟逗号，如 *MySharona(,8675309)*，否则这是不可能的。但这是不允许的。

### 添加默认构造函数

*默认构造函数*是不带参数的构造函数。你可以通过两种方式在类中拥有默认构造函数：自己编写一个，或者让编译器为你*隐式*生成一个。所谓*隐式生成*，是指你的代码中实际上没有构造函数，但编译器在编译代码时会为你提供一个。

你可能以前见过默认构造函数。这个类没有构造函数，所以编译器会为你生成一个隐式构造函数。它看起来像这样：

```cpp
class Simple
{
public:
    int x, y;
    void Write()
    {
        cout << x << " " << y << endl;
    }
};
```

当然，前面的类不会做太多事情。它等同于这样：

```cpp
class Simple
{
public:
    int x, y;
    void Write()
    {
        cout << x << " " << y << endl;
    }
    Simple() {}
};
```

然而，认识到默认构造函数的存在是很重要的。你需要意识到编译器在什么时候*不会*自动创建构造函数，因为你可能会遇到一些问题。看看这个类的修改版本（见 Constructor04 示例）：

```cpp
class Simple
{
public:
    int x, y;
    void Write()
    {
        cout << x << " " << y << endl;
    }
    Simple(int startx) { x = startx; }
};
```

我们在这段代码中加入了自己编写的带参数的构造函数。完成这一步后，该类不再获得隐式默认构造函数。如果我们之后有这样一行：

```
Simple inst;
```

编译器会给出类似这样的错误消息：

```
In function 'int main()':
error: no matching function for call to 'Simple::Simple()'
note: candidates are: Simple::Simple(const Simple&)
note:                 Simple::Simple(int)
```

然而，如果我们去掉我们添加的构造函数（回到之前的示例），这个错误就会消失！因此，如果你不提供任何构造函数，编译器会给你一个隐式默认构造函数。

![](img/6ba99460b0feb3585671a4612ff5fabb_502_0.png)

如果你使用 Code::Blocks 编译器，你会获得一些有用的额外信息。在这种情况下，你会看到两行注释，说明可用的构造函数候选。你可以将这些信息作为排查问题的一部分。

现在这里就是你可能遇到麻烦的地方：假设你构建了一个类，但没有为它提供任何构造函数。你把该类交给其他人使用。他们在自己的代码中使用它，都很开心，使用的是默认构造函数。然后有一天，别人（不是你——你不会犯错）决定通过添加一个带有多个参数的特殊构造函数来增强这个类。这个“流氓程序员”添加了构造函数并加以使用。流氓先生认为一切安好，因为他只使用自己的新构造函数。但他不知道：所有其他使用隐式默认构造函数的人会突然开始遇到编译器错误！

信不信由你，我们见过这种情况发生。有一天，你的代码突然无法编译。每当你尝试创建类的实例时，你开始得到错误，说编译器找不到 Simple::Simple()。哎呀，有人改了它。

但你可以通过确保显式包含一个默认构造函数来避免这个问题，即使它什么都不做：

```cpp
class Simple
{
public:
    int x,y;
    void Write()
    {
        cout << x << " " << y << endl;
    }
    Simple() {}
};
```

