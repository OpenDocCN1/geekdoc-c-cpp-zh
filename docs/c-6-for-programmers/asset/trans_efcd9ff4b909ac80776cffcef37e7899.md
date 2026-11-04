
第 41 行返回字符串 "value"，而第 42 行的表达式 `nameof(Hour)` 返回字符串 "Hour"。

## 良好的编程实践 10.1

*当需要在字符串字面量中包含标识符时，应使用 nameof 运算符，而不是在字符串中硬编码标识符的名称。如果在 Visual Studio 中右键单击某个标识符，然后使用 Rename... 选项在整个代码中更改该标识符的名称，那么 nameof 返回的字符串将自动更新为该标识符的新名称。*

## 关于 Time2 类的方法、属性和构造函数的说明

Time2 的属性在整个类体中被访问——SetTime 在第 25–27 行给 Hour、Minute 和 Second 赋值，而 ToUniversalString 和 ToString 分别在第 89 行以及第 93–94 行使用 Hour、Minute 和 Second 属性。这些方法可以直接访问类的私有数据。然而，可以考虑将时间的表示从三个 int 值（需要 12 字节内存）改为一个 int 值，该值表示自午夜以来经过的总秒数（只需要四个字节内存）。如果进行此更改，只有直接访问私有数据的代码需要更改——对于 Time2 类来说，就是 Hour、Minute 和 Second 属性的主体。无需修改 SetTime、ToUniversalString 或 ToString，因为它们通过 Hour、Minute 和 Second 间接访问私有数据。以这种方式设计类可以降低在更改类实现时出现编程错误的可能性。

同样，每个构造函数都可以包含来自 SetTime 方法的相应语句的副本。这样做可能稍微更高效，因为消除了额外的构造函数调用和对 SetTime 的调用。然而，在多个方法或构造函数中重复语句会使更改类的内部数据表示更加困难且更容易出错。让一个构造函数调用另一个构造函数，甚至直接调用 SetTime，可以使对 SetTime 实现的任何更改只需进行一次。

## 软件工程观察 10.7

*在实现类的方法时，使用类的属性来访问类的私有数据可以简化代码维护并降低出错的可能性。*

### 10.5.2 使用 Time2 类的重载构造函数

类 Time2Test（图 10.6）创建了六个 Time2 对象（第 9–13 行和第 41 行），以调用重载的 Time2 构造函数。

```csharp
1 // Fig. 10.6: Time2Test.cs
2 // Overloaded constructors used to initialize Time2 objects.
3 using System;
4
5 public class Time2Test
6 {
    static void Main()
    {
        var t1 = new Time2(); // 00:00:00
        var t2 = new Time2(2); // 02:00:00
        var t3 = new Time2(21, 34); // 21:34:00
        var t4 = new Time2(12, 25, 42); // 12:25:42
        var t5 = new Time2(t4); // 12:25:42

        Console.WriteLine("Constructed with:\n");
        Console.WriteLine("t1: all arguments defaulted");
        Console.WriteLine("{0}", t1.ToUniversalString()); // 00:00:00
        Console.WriteLine("{0}", t1.ToString()); // 12:00:00 AM

        Console.WriteLine(
            "t2: hour specified; minute and second defaulted");
        Console.WriteLine("{0}", t2.ToUniversalString()); // 02:00:00
        Console.WriteLine("{0}", t2.ToString()); // 2:00:00 AM

        Console.WriteLine(
            "t3: hour and minute specified; second defaulted");
        Console.WriteLine("{0}", t3.ToUniversalString()); // 21:34:00
        Console.WriteLine("{0}", t3.ToString()); // 9:34:00 PM

        Console.WriteLine("t4: hour, minute and second specified");
        Console.WriteLine("{0}", t4.ToUniversalString()); // 12:25:42
        Console.WriteLine("{0}", t4.ToString()); // 12:25:42 PM

        Console.WriteLine("t5: Time2 object t4 specified");
        Console.WriteLine("{0}", t5.ToUniversalString()); // 12:25:42
        Console.WriteLine("{0}", t5.ToString()); // 12:25:42 PM

        // attempt to initialize t6 with invalid values
        try
        {
            var t6 = new Time2(27, 74, 99); // invalid values
        }
        catch (ArgumentOutOfRangeException ex)
        {
            Console.WriteLine("\nException while initializing t6:");
            Console.WriteLine(ex.Message);
        }
    }
}
```

图 10.6 | 用于初始化 Time2 对象的重载构造函数。（第 1 部分，共 3 部分。）

```
Constructed with:
t1: all arguments defaulted
00:00:00
12:00:00 AM

t2: hour specified; minute and second defaulted
02:00:00
2:00:00 AM

t3: hour and minute specified; second defaulted
21:34:00
9:34:00 PM

t4: hour, minute and second specified
12:25:42
12:25:42 PM

t5: Time2 object t4 specified
12:25:42
12:25:42 PM

Exception while initializing t6:
Hour must be 0-23
Parameter name: value
Actual value was 27.
```

图 10.6 | 用于初始化 Time2 对象的重载构造函数。（第 3 部分，共 3 部分。）

第 9–13 行演示了向 Time2 构造函数传递参数。C# 通过将构造函数调用中的参数数量和类型与每个构造函数声明中的参数数量和类型进行匹配，来调用相应的重载构造函数。第 9–12 行分别调用图 10.5 第 12–15 行的构造函数：

- 图 10.6 的第 9 行调用无参构造函数——编译器为三个参数分别提供默认值 0。
- 第 10 行调用带一个表示小时的参数的构造函数——编译器为分钟和秒提供默认值 0。
- 第 11 行调用带两个分别表示小时和分钟的参数的构造函数——编译器为秒提供默认值 0。
- 第 12 行调用带小时、分钟和秒值的构造函数。

第 13 行调用图 10.5 第 18–19 行的构造函数。第 15–36 行（图 10.6）显示每个已初始化 Time2 对象的字符串表示，以确认每个对象都已正确初始化。

第 41 行尝试通过创建新的 Time2 对象并向构造函数传递三个无效值来初始化 t6。当构造函数尝试使用无效的小时值来初始化 Hour 属性时，会发生 ArgumentOutOfRangeException。我们在第 43 行捕获此异常并显示其 Message 属性，这会产生图 10.6 输出中的最后三行。由于在创建异常对象时使用了带三个参数的 ArgumentOutOfRangeException 构造函数，该异常的 Message 属性还包含有关超出范围值的信息。

### 10.6 默认构造函数和无参构造函数

每个类必须至少有一个构造函数——如果在类的声明中未提供任何构造函数，编译器会创建一个默认构造函数，该构造函数在被调用时不接受参数。在第 11.4.1 节中，你将了解到默认构造函数会隐式执行一项特殊任务。

对于显式声明了至少一个构造函数的类，编译器不会创建默认构造函数。在这种情况下，如果希望能够调用无参构造函数，则必须声明一个无参构造函数——即声明时没有参数的构造函数，或者所有参数都具有默认值的构造函数（例如，图 10.5 的第 12 行）。与默认构造函数一样，无参构造函数使用空括号调用。如果调用 Time2 类的三参数构造函数时不提供参数，编译器会显式向每个参数传递 0。如果从 Time2 类中省略可无参调用的构造函数，则该类的客户端将无法使用表达式 new Time2() 创建 Time2 对象。如果一个类同时提供无参构造函数和所有参数都具有默认值的构造函数，那么当你不向构造函数传递任何参数时，编译器将使用无参构造函数。

### 10.7 组合

一个类可以将值类型的对象或其他类的对象引用作为成员。这称为组合，有时也称为 has-a 关系。例如，AlarmClock 类的对象需要知道当前时间和应该响铃的时间，因此在 AlarmClock 对象中包含两个对 Time 对象的引用是合理的。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_315_0.png)

> **软件工程观察 10.8**
>
> 软件复用的一种形式是组合，即一个类包含对其他对象的引用。回想一下，类是引用类型。一个类可以具有自身类型的属性——例如，Person 类可以具有 Person 类型的 Mother 和 Father 属性，这些属性引用其他 Person 对象。

### 10.7.1 Date 类

我们的组合示例包含三个类——Date（图 10.7）、Employee（图 10.8）和 EmployeeTest（图 10.9）。类 Date（图 10.7）声明了 int 实例变量 month 和 day（第 7–8 行）以及自动实现的属性 Year（第 9 行），用于表示日期。

```csharp
// Fig. 10.7: Date.cs
// Date class declaration.
using System;

public class Date
{
    private int month; // 1-12
    private int day; // 1-31 based on month
    public int Year { get; private set; } // auto-implemented property Year

    // constructor: use property Month to confirm proper value for month;
    // use property Day to confirm proper value for day
    public Date(int month, int day, int year)
    {
        Month = month; // validates month
```

图 10.7 | Date 类声明。（第 1 部分，共 3 部分。）

