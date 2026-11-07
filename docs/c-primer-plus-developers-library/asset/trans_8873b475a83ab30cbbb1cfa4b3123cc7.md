
那是安全的。不过，强制转换 #3 之所以安全，是因为它将派生类对象的地址赋给基类指针。也就是说，公有派生保证一个 `Magnificent` 对象也是一个 `Superb` 对象（直接基类）和一个 `Grand` 对象（间接基类）。因此，将其地址赋给所有这三种类型的指针是安全的。虚函数确保使用这三种类型中任一类型的指针指向一个 `Magnificent` 对象时，将调用 `Magnificent` 的方法。

请注意，类型转换是否安全这个问题，比指向的是哪种对象这个问题更一般，也更有用。通常想知道类型的原因，是为了知道调用某个特定方法是否安全。你不一定需要精确的类型匹配才能调用方法。该类型可以是一个基类型，只要为该类型定义了该方法的虚版本。下一个例子说明了这一点。

不过，首先让我们看看 `dynamic_cast` 语法。该运算符的用法如下，其中 `pg` 指向一个对象：

```cpp
Superb * pm = dynamic_cast<Superb *>(pg);
```

这段代码询问指针 `pg` 能否（如前所述）安全地类型转换为 `Superb *` 类型。如果可以，该运算符返回对象的地址。否则，它返回 0，即空指针。

> **注意**
>
> 一般来说，如果被指向的对象 `(*pt)` 的类型为 `Type`，或者直接或间接派生自 `Type` 类型，则下面的表达式会将指针 `pt` 转换为 `Type *` 类型的指针：
>
> `dynamic_cast<Type *>(pt)`
>
> 否则，该表达式的值为 0，即空指针。

程序清单 15.17 说明了这一过程。首先，它定义了三个类，恰好命名为 `Grand`、`Superb` 和 `Magnificent`。`Grand` 类定义了一个虚函数 `Speak()`，其他每个类都重新定义了它。`Superb` 类定义了一个虚函数 `Say()`，`Magnificent` 重新定义了它（见图 15.4）。该程序定义了一个 `GetOne()` 函数，它随机创建并初始化这三种类型之一的对象，然后以 `Grand *` 类型指针返回该地址。（`GetOne()` 函数模拟交互式用户做出决策。）一个循环将该指针赋给名为 `pg` 的 `Grand *` 类型变量，然后使用 `pg` 调用 `Speak()` 函数。由于该函数是虚函数，代码会正确调用适合被指向对象的 `Speak()` 版本：

```cpp
for (int i = 0; i < 5; i++)
{
    pg = GetOne();
    pg->Speak();
    ...
}
```

![](img/9afc44517b591d64e2e19f623c9308ef_950_0.png)

图15.4   Grand 类族。

你不能使用这种完全相同的方法（使用指向 Grand 的指针）来调用 `Say()` 函数；它并未为 `Grand` 类定义。不过，你可以使用 `dynamic_cast` 运算符来查看 `pg` 能否类型转换为指向 `Superb` 的指针。如果对象是 `Superb` 类型或 `Magnificent` 类型，结果将为真。无论哪种情况，你都可以安全地调用 `Say()` 函数：

```cpp
if (ps = dynamic_cast<Superb *>(pg))
    ps->Say();
```

回想一下，赋值表达式的值是其左侧的值。因此，if 条件的值是 ps。如果类型转换成功，ps 为非零值，即为真。如果类型转换失败（当 pg 指向 Grand 对象时就会失败），ps 为零，即为假。程序清单 15.17 展示了完整代码。（顺便说一句，一些编译器注意到程序员通常会在 if 语句条件中使用 `==` 运算符，因此可能会对非预期的赋值发出警告。）

**程序清单 15.17   rtti1.cpp**

```cpp
// rtti1.cpp -- using the RTTI dynamic_cast operator
#include <iostream>
#include <cstdlib>
#include <ctime>

using std::cout;

class Grand
{
private:
    int hold;
public:
    Grand(int h = 0) : hold(h) {}
    virtual void Speak() const { cout << "I am a grand class!\n"; }
    virtual int Value() const { return hold; }
};

class Superb : public Grand
{
public:
    Superb(int h = 0) : Grand(h) {}
    void Speak() const { cout << "I am a superb class!!\n"; }
    virtual void Say() const
        { cout << "I hold the superb value of " << Value() << "!\n"; }
};

class Magnificent : public Superb
{
private:
    char ch;
public:
    Magnificent(int h = 0, char c = 'A') : Superb(h), ch(c) {}
    void Speak() const { cout << "I am a magnificent class!!!\n"; }
    void Say() const { cout << "I hold the character " << ch <<
        " and the integer " << Value() << "!\n"; }
};

Grand * GetOne();

int main()
{
    std::srand(std::time(0));
    Grand * pg;
    Superb * ps;
    for (int i = 0; i < 5; i++)
    {
        pg = GetOne();
        pg->Speak();
        if( ps = dynamic_cast<Superb *>(pg) )
            ps->Say();
    }
    return 0;
}

Grand * GetOne()    // generate one of three kinds of objects randomly
{
    Grand * p;
    switch ( std::rand() % 3)
    {
        case 0: p = new Grand(std::rand() % 100);
                break;
        case 1: p = new Superb(std::rand() % 100);
                break;
        case 2: p = new Magnificent(std::rand() % 100,
                                    'A' + std::rand() % 26);
                break;
    }
    return p;
}
```

> **注意**
>
> 即使你的编译器支持 RTTI，它也可能默认关闭该特性。如果该特性未启用，程序可能仍会编译，但会产生运行时错误。如果你发现是这种情况，应查阅文档或浏览菜单选项。

程序清单 15.17 中的程序说明了一个重要观点。应尽可能使用虚函数，仅在必要时使用 RTTI。以下是一些示例输出：

```text
I am a superb class!!
I hold the superb value of 68!
I am a magnificent class!!!
I hold the character R and the integer 68!
I am a magnificent class!!!
I hold the character D and the integer 12!
I am a magnificent class!!!
I hold the character V and the integer 59!
I am a grand class!
```

如你所见，`Say()` 方法仅针对 `Superb` 和 `Magnificent` 类被调用。（每次运行的输出会有所不同，因为程序使用 `rand()` 选择对象类型。）

你也可以将 `dynamic_cast` 与引用一起使用。用法略有不同：没有与空指针类型相对应的引用值，因此没有可用于表示失败的特殊引用值。相反，当被不恰当的请求触发时，`dynamic_cast` 会抛出 `bad_cast` 异常，该异常派生自 exception 类，并在 typeinfo 头文件中定义。因此，该运算符可以如下使用，其中 rg 是对 Grand 对象的引用：

```cpp
#include <typeinfo> // for bad_cast
...
try {
    Superb & rs = dynamic_cast<Superb &>(rg);
    ...
}
catch(bad_cast &) {
    ...
};
```

## `typeid` 运算符与 `type_info` 类

`typeid` 运算符让你能够判断两个对象是否为同一类型。它有点类似 `sizeof`，接受两种参数：

- 类的名称
- 求值结果为对象的表达式

`typeid` 运算符返回对 `type_info` 对象的引用，其中 `type_info` 是在 `typeinfo` 头文件（原为 `typeinfo.h`）中定义的类。`type_info` 类重载了 `==` 和 `!=` 运算符，因此你可以使用这些运算符比较类型。例如，如果 `pg` 指向一个 Magnificent 对象，则下面的表达式求值为 bool 值 true，否则为 false：

```cpp
typeid(Magnificent) == typeid(*pg)
```

如果 `pg` 恰好是空指针，程序会抛出 `bad_typeid` 异常。该异常类型派生自 `exception` 类，并在 `typeinfo` 头文件中声明。

`type_info` 类的实现因供应商而异，但它包含一个 `name()` 成员，该成员返回依赖于实现的字符串，通常（但不一定）是类的名称。例如，下面的语句显示为指针 `pg` 所指向对象的类定义的字符串：

```cpp
cout << "Now processing type " << typeid(*pg).name() << ".\n";
```

程序清单 15.18 修改了程序清单 15.17，使其使用 `typeid` 运算符和 `name()` 成员函数。请注意，它们用于 `dynamic_cast` 和虚函数不处理的情况。`typeid` 测试用于选择一个甚至不是类方法的操作，因此它不能通过类指针调用。`name()` 方法语句展示了如何在调试中使用该方法。请注意，该程序包含了 `typeinfo` 头文件。

**程序清单 15.18   rtti2.cpp**

```cpp
// rtti2.cpp -- using dynamic_cast, typeid, and type_info
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <typeinfo>
using namespace std;
```

