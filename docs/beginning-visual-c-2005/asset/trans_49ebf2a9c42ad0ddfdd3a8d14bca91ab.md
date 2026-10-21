

你还可以尝试向类中添加一个命名索引属性：

```
ref class Name
{
    // 代码如前...

    // 用于返回首字母的索引属性
    property wchar_t Initials[int]
    {
        wchar_t get(int index)
        {
            if(index >= Names->Length)
                throw gcnew Exception(L"Index out of range");
            return Names[index][0];
        }
    }
};
```

这个索引属性名为 `Initials`，因为它的功能是返回由索引指定的名字的首字母。你定义命名索引属性的方式与定义默认索引属性基本相同，只是用属性名称代替了 `default` 关键字。

如果你重新编译程序并再次运行，你将看到以下输出。

```
Name 1 is Ebenezer
Name 2 is Isaiah
Name 3 is Ezra
Name 4 is Inigo
Name 5 is Oberwurst
The initials are: E.I.E.I.O.
Press any key to continue . . .
```

这些首字母是通过在 `for` 循环中访问命名索引属性产生的，输出表明它们按预期工作。

## 更复杂的索引属性

如前所述，索引属性可以定义为需要多个索引才能访问一个值，而且索引不必是数字。下面是一个具有此类索引属性的类的示例：

```
enum class Day { Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };

// 定义商店的类
ref class Shop
{
public:
    property String^ Opening[Day, String^]      // 营业时间
    {
        String^ get(Day day, String^ AmOrPm)
        {
            switch(day)
            {
                case Day::Saturday:             // 周六营业：
                    if(AmOrPm == L"am")
                        return L"9:00";         //     上午9点
                    else
                        return L"14:30";        //     下午2:30
                    break;

                case Day::Sunday:               // 周日营业：
                    return L"closed";           //     全天关闭
                    break;

                default:
                    if(AmOrPm == L"am")         // 周一至周五营业：
                        return L"9:30";         //     上午9:30
                    else
                        return L"14:00";        //     下午2点
                    break;
            }
        }
    }
};
```

表示商店的类有一个指定营业时间的索引属性。第一个索引是 `Day` 类型的枚举值，用于标识星期几；第二个索引是一个字符串句柄，用于确定是上午还是下午。你可以像这样输出某个 `Shop` 对象的 `Opening` 属性值：

```
Shop^ shop = gcnew Shop;
Console::WriteLine(shop->Opening[Day::Saturday, L"pm"]);
```

第一条语句创建了 `Shop` 对象，第二条语句显示该商店周六下午的营业时间。如你所见，你只需将属性的两个索引值放在方括号内并用逗号分隔即可。第二条语句的输出是字符串 `"14:30"`。如果你能想出需要它们的理由，你还可以在类中定义具有三个或更多索引的索引属性。

## 静态属性

静态属性与静态类成员类似，它们是为类定义的，并且对于该类的所有对象都是相同的。你可以在属性定义中添加 `static` 关键字来定义静态属性。下面是你可以在之前见过的 `Length` 类中定义静态属性的方式：

```
value class Length
{
    // 代码如前...
public:
    static property String^ Units
    {
        String^ get() { return L"feet and inches"; }
    }
};
```

这是一个简单的属性，它将类所采用的单位作为字符串提供。你访问静态属性的方式是用类名限定属性名称，就像访问类的任何其他静态成员一样：

```
Console::WriteLine(L"Class units are {0}.", Length::Units);
```

无论是否创建了类的任何对象，静态类属性都存在。这与实例属性不同，实例属性对于类的每个对象都是特定的。当然，如果你已经定义了一个类对象，你也可以使用变量名来访问静态属性。例如，如果你创建了一个名为 `len` 的 `Length` 对象，你可以使用以下语句输出静态 `Units` 属性的值：

```
Console::WriteLine(L"Class units are {0}.", len.Units);
```

要通过指向对象类型的句柄访问引用类中的静态属性，你需要使用 `->` 运算符。

## 保留的属性名称

尽管属性与字段不同，但属性的值仍然需要存储在某个地方，并且存储位置需要以某种方式标识。在内部，属性会为所需的存储位置创建名称，这样的名称在具有属性的类中是保留的，因此你不能将这些名称用于其他目的。

如果你在类中定义了一个名为 `NAME` 的标量或命名索引属性，则名称 `get_NAME` 和 `set_NAME` 在该类中被保留，因此你不能将它们用于其他目的。无论你是否为该属性定义 `get()` 和 `set()` 函数，这两个名称都是保留的。当你在类中定义默认索引属性时，名称 `get_Item` 和 `set_Item` 会被保留。存在使用下划线字符的保留名称，这是避免在 C++/CLI 程序中的自定义名称中使用下划线字符的一个很好的理由。

## initonly 字段

字面量字段是将常量引入类的便捷方式，但它们的局限性在于其值必须在编译程序时定义。C++/CLI 还在类中提供了 `initonly` 字段，这些是可以在构造函数中初始化的常量。以下是一个骨架版本的 `Length` 类中 `initonly` 字段的示例：

```
value class Length
{
private:
    int feet;
    int inches;

public:
    initonly int inchesPerFoot;              // initonly 字段

    // 构造函数
    Length(int ft, int ins) :
        feet(ft), inches(ins),              // 初始化字段
        inchesPerFoot(12)                   // 初始化 initonly 字段
    {}
};
```

这里的 `initonly` 字段名为 `inchesPerFoot`，并在构造函数的初始化列表中初始化。这是一个非静态 `initonly` 字段的示例，每个对象都有它自己的副本，就像普通字段 `feet` 和 `inches` 一样。当然，`initonly` 字段与普通字段的最大区别在于，之后你无法更改 `initonly` 字段的值——一旦它被初始化，它将永远固定。请注意，在声明非静态 `initonly` 字段时，你不能为其指定初始值；这意味着你*必须*在构造函数中初始化所有非静态 `initonly` 字段。

你不必在构造函数的初始化列表中初始化非静态 `initonly` 字段——你也可以在构造函数体内完成：

```
Length(int ft, int ins) :
    feet(ft), inches(ins)                // 初始化字段
{
    inchesPerFoot = 12;                  // 初始化 initonly 字段
}
```

现在该字段在构造函数体内被初始化。通常，你会将非静态 `initonly` 字段的值作为参数传递给构造函数，而不是像我们这里这样使用显式字面量，因为这类字段的意义在于它们的值是实例特定的。如果在编写代码时该值已知，你还不如使用字面量字段。

你还可以在类中将 `initonly` 字段定义为 `static`，在这种情况下，它由类的所有成员共享，并且如果它是公共 `initonly` 字段，则可以通过用类名限定字段名来访问它。`inchesPerFoot` 字段作为静态 `initonly` 字段更有意义——该值实际上不会从一个对象变化到另一个对象。以下是带有静态 `initonly` 字段的 `Length` 类的新版本：

```
value class Length
{
private:
    int feet;
    int inches;

public:
    initonly static int inchesPerFoot = 12;     // 静态 initonly 字段

    // 构造函数
    Length(int ft, int ins) :
        feet(ft), inches(ins)                   // 初始化字段
    {}
};
```

现在 `inchesPerFoot` 字段是静态的，并且其值在声明中指定，而不是在构造函数初始化列表中指定。事实上，你不允许在构造函数中设置任何类型的静态字段的值。如果你仔细想想，这是有道理的，因为静态字段是在类的所有对象之间共享的，因此在每次调用构造函数时为这些字段设置值会与此概念相冲突。

现在你似乎又回到了 `initonly` 字段只能在编译时初始化，而字面量字段无论如何都能胜任的情况；然而，你有另一种在运行时初始化静态 `initonly` 字段的方法——通过静态构造函数。

