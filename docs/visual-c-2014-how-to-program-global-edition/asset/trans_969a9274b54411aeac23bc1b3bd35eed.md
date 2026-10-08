

# 440 第 10 章 类与对象：深入观察

10.3 演示了私有类成员无法在类外部直接访问。在本文应用程序中，我们使用了 `Time1` 类的修改版本，它声明了私有实例变量 `hour`、`minute` 和 `second`，而不是公共属性 `Hour`、`Minute` 和 `Second`。第 9–11 行尝试访问 `Time1 time` 的私有实例变量 `hour`、`minute` 和 `second`。当编译代码时，编译器会生成错误信息，指出这些私有成员不可访问。

```csharp
// 图 10.3: MemberAccessTest.cs
// 私有成员在类外部不可访问。
class MemberAccessTest {
    static void Main() {
        var time = new Time1(); // 创建并初始化 Time1 对象
        time.hour = 7; // 错误：hour 在 Time1 中私有访问
        time.minute = 15; // 错误：minute 在 Time1 中私有访问
        time.second = 30; // 错误：second 在 Time1 中私有访问
    }
}
```

| 代码 | 描述 | 项目 | 文件 | 行号 |
|---|---|---|---|---|
| CS0122 | 'Time.hour' 因其保护级别无法访问 | MemberAccessTest | MemberAccessTest.cs | 9 |
| CS0122 | 'Time.minute' 因其保护级别无法访问 | MemberAccessTest | MemberAccessTest.cs | 10 |
| CS0122 | 'Time.second' 因其保护级别无法访问 | MemberAccessTest | MemberAccessTest.cs | 11 |

图 10.3 `Time1` 类的私有成员在类外部不可访问。

# 10.4 使用引用访问当前对象的成员

每个对象都可以通过 `this` 关键字（也称为 `this` 引用）访问自身的引用。当为特定对象调用非静态方法（或属性）时，方法体会隐式地使用 `this` 关键字来引用对象的实例变量和非静态类成员。正如图 10.4 所示，你也可以在非静态方法体中显式地使用 `this` 关键字。第 10.5 节解释了为什么这不能在静态方法中使用。

```csharp
// 图 10.4: ThisTest.cs
// this 被隐式和显式地用于引用对象的成员。
using System;
class ThisTest {
```

图 10.4 `this` 被隐式和显式地用于引用对象的成员。（2 部分中的第 1 部分）

# 10.4 使用 this 引用访问当前对象的成员 441

```csharp
static void Main() {
    var time = new SimpleTime(15, 30, 19);
    Console.WriteLine(time.BuildString());
}
// class SimpleTime 类演示演示了 "this" 引用
public class SimpleTime {
    private int hour; // 0-23
    private int minute; // 0-59
    private int second; // 0-59

    // 如果构造函数使用的参数名称与变量名相同，则需要
    // "this" 引用来区分这些名称
    public SimpleTime(int hour, int minute, int second) {
        this.hour = hour; // 设置 "this" 对象的 hour 实例变量
        this.minute = minute; // 设置 "this" 对象的 minute
        this.second = second; // 设置 "this" 对象的 second
    }

    // 使用显式隐式的 "this" 调用 ToUniversalString
    public string ToString() {
        return ToUniversalString();
    }
}
```

15:30:19

图 10.4 | `this` 被隐式和显式地用于引用对象的成员。（2 部分中的第 2 部分。）

 10.4 演示了 `this` 的隐式和显式使用，以使 `ThisTest` 类的方法能够显示 `SimpleTime` 对象的私有数据。为了简洁起见，我们将它们声明在两个文件中——`class ThisTest` 声明在第 5–52 行，`class SimpleTime` 声明在第 15–42 行。

`Class SimpleTime` 声明了私有实例变量——`hour`、`minute` 和 `second`（第 17–19 行）。构造函数（第 24–29 行）接收三个 `int` 参数来初始化 `SimpleTime` 对象（为了简单，未进行验证）。我们使用了与类实例变量名称相同的参数名称（第 17–19 行）。我们故意这样做是为了突出相应的实例变量，以便说明对 `this` 引用的显式使用。如果方法中有一个与实例变量同名的局部变量，则该局部变量在方法体中被称为“遮蔽（shadow）”。然而，你可以使用 `this` 来显式地访问被隐藏的实例变量，如第 26–28 行中 `SimpleTime` 隐藏的实例变量所示。

# 软件工程观察 10.4

在整个类中通过属性来访问类的实例变量通常会消除遮蔽问题，因为属性名称使用驼峰命名法（首字母大写），而参数名称使用驼峰命名法（首字母小写）。

`BuildString`（第 32–34 行）返回由显式和隐式使用 `this` 引用的语句创建的字符串。第 33 行显式使用 `this` 引用调用 `UniversalToString()` 方法。第 34 行隐式使用该引用调用相同的方法。程序员通常不会显式使用 `this` 引用来引用当前对象中的其他方法。此外，这里没有必要访问每个实例变量，因为方法没有任何与类实例变量同名的局部变量。
`ClassTest`（第 5–12 行）演示了 `SimpleTime`。第 9 行创建 `SimpleTime` 实例，第 10 行调用其 `BuildString` 方法并显示结果。

# 10.5 Time 类研究：重载构造函数

接下来，我们演示一个具有多个重载构造函数的类，允许以不同的方式初始化对象。要重载构造函数，只需具有不同签名的多个构造函数声明。

# 10.5.1 Time2 类

默认情况下，`Time1`（图 10.1）的 `Hour`、`Minute` 和 `Second` 属性初始化为默认值 0（午夜），这不允许客户端使用特定的非零值初始化类。`Time2`（图 10.5）包含了重载构造函数。在此应用程序中，一个构造函数反过来调用 `SetTime` 来设置私有变量 `hour`、`minute` 和 `second`。构造函数通过匹配每个构造函数声明中指定的参数数量和类型。

```csharp
// 10.5: Time2.cs
// 带有重载构造函数的 Time2 类
using System;
public class Time2 {
    private int hour; // 0-23
    private int minute; // 0-59
    private int second; // 0-59
```

图 10.5 `Time2` 类带有重载构造函数的声明。（3 部分中的第 1 部分）

# 10.5 Time 类研究：重载构造函数 443

```csharp
// 构造函数可以使用零、一个或三个参数调用
public Time2(int hour = 0, int minute = 0, int second = 0)
{
    SetTime(hour, minute, second); // 调用 SetTime 以验证时间
}

// Time2 构造函数：提供另一个 Time2 对象作为参数
public Time2(Time2 time)
    : this(time.Hour, time.Minute, time.Second) {
```

```csharp
// 使用通用时间设置新值；无效值
public void SetTime(int hour, int minute, int second)
{
    Hour = hour; // 设置 Hour 属性
    Minute = minute; // 设置 Minute 属性
    Second = second; // 设置 Second 属性
}
```

```csharp
// 获取和设置 hour 的属性
public int Hour
{
    get
    {
        return hour;
    }
    set
    {
        if (value < 0 || value > 23)
            throw new ArgumentOutOfRangeException(nameof(value),
                value, $"{nameof(Hour)} 必须是 0-23");
    }
}
```

```csharp
hour = value;
}

// 获取和设置 minute 的属性
public int Minute
{
    get
    {
        return minute;
    }
    set
    {
        if (value < 0 || value > 59)
            throw new ArgumentOutOfRangeException(nameof(value),
                value, $"{nameof(Minute)} 必须是 0-59");
    }
}
```

minute = value;
}

