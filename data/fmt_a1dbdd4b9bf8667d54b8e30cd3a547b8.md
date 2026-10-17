
```csharp
return p*q;
}
static void Main(string[] args)
{
    FuncDelegate delegate1 = new FuncDelegate(AddNum);
    FuncDelegate delegate2 = new FuncDelegate(MultNum);
    Console.WriteLine("Sum of 10 and 20 is {0}", delegate1(10,20));
    Console.WriteLine("Multiplication of 10 and 20 is {0}", delegate2(10,20));
}
}
```

输出：
Sum of 10 and 20 is 30
Multiplication of 10 and 20 is 200

你可以看到通过创建名为 `delegate1` 和 `delegate2` 的实例实例化了 `FuncDelegate`。`delegate1` 和 `delegate2` 实例被设置为分别引用 `AddNum` 和 `MultNum` 方法。通过委托实例 `delegate1` 调用了 `AddNum` 方法，并传递了参数 10 和 20。同样，通过 `delegate2` 实例调用了 `MultNum` 方法，并传递了参数 10 和 20。两个方法返回的值显示在屏幕上。

委托类型之间是不兼容的，即使它们的签名相同。以下代码片段会导致编译错误：

```csharp
delegate delegate Calculate(int x, int y);
delegate int FuncDelegate(int m, int n);
```

## 委托与事件

即使委托的签名相同，它们也相等。在以下代码片段中，两个委托实例相等，因为它们指向同一个方法：

```csharp
delegate int FuncDelegate(int m, int n);
FuncDelegate delegate1 = AddNum;
FuncDelegate delegate2 = AddNum;
if (delegate1 == delegate2)
{
```

## 实例与静态方法目标

当实例方法分配给委托时，委托维护了该方法以及所属的实例。`System.Delegate` 类的 `Target` 属性表示该实例。当委托指向静态方法时，`System.Delegate` 类的 `Target` 属性设置为 null。列表 11.3 所示的 `Delegateb.cs` 程序演示了指向实例方法。该程序声明了一个名为 `Calculate` 的委托，它可以引用任何返回 `int` 并接受两个 `int` 类型参数的方法。定义了一个名为 `Shapes` 的类，它包含一个名为 `Rect` 的方法。`Calculate` 委托的签名与 `Rect` 方法匹配。创建了 `Shapes` 类的实例。委托实例 `r` 被设置为指向该实例的 `Rect` 方法。

列表 11.3 `Delegateb.cs` 中的程序代码

```csharp
using System;
delegate int Calculate(int x, int y);
class Shapes
{
    public int Rect(int x, int y)
    {
        return x * y;
    }
}
class Delegateb
{
    static void Main()
    {
        Shapes shp=new Shapes();
        Calculate r = new Calculate(shp.Rect);
        if(r.Target == shp)
        {
            Console.WriteLine("Method reference is: {0}",r.Method);
            Console.WriteLine("Area of rectangle is "+ r(5,8));
        }
    }
}
```

输出：
Method reference is: Int32(Int32, Int32)
Area of rectangle is 40

## 多路委托

多路委托代表可以同时调用多个方法的委托。所有委托实例都具有多路能力。换句话说，委托实例引用的不仅仅是一个方法，而是一个方法列表。委托还代表已分配的委托列表。相同类型的委托可以组合。多路委托基本上是委托的列表或具有相同签名的方法列表。使用多路委托的处是它可以调用一组方法，而不是单个方法。

你可以使用 `+` 和 `+=` 运算符将指定方法的引用添加到委托实例。你还可以使用这些运算符组合委托实例。例如，以下语句使 `Calculate` 委托实例 `r` 引用 `Rect` 和 `Sum` 方法：

```csharp
Calculate r = Rect
r+=Sum;
```

调用委托实例 `r` 现在会同时调用 `Rect` 和 `Sum` 方法。这些方法按照它们被添加到委托实例的顺序被调用。请记住，如果任一个方法抛出异常，委托调用将立即停止，列表中的其他方法将不再被调用。

与 `+=` 运算符一样，你也可以使用 `-=` 运算符从指定的委托实例中移除指定的委托操作数或方法。以下示例从委托实例中移除了 `Rect` 方法：

```
r -= Rect;
```

调用实例 `r` 只会触发 `Sum`。如果被移除的方法是最后一个方法，则委托实例将变为 `null`。请记住，调用 `null` 委托会导致运行时错误。

> `MulticastDelegate` 实现为委托的链表，添加和删除操作在列表末尾完成。

列表 11.4 显示的 `Delegate3.cs` 程序演示了多路委托。该程序声明了一个名为 `FunDelegate` 的委托，它可以引用任何返回 `int` 且接收两个 `int` 类型参数的方法。定义了两个与委托签名匹配的静态方法，命名为 `AddNum` 和 `MultNum`。`AddNum` 和 `MultNum` 分别返回所提供参数的加和乘积。定义了一个名为 `devar` 的 `FuncDelegate` 委托实例。`devar` 通过同时引用 `AddNum` 和 `MultNum` 实现了多路分发。

> 如果多路委托具有 `void` 返回类型，调用者将接收最后一个被调用方法的返回值。前面的方法会被调用，但它们的返回值会被丢弃。要处理每个返回值，请遍历委托列表并逐个调用每个委托。

# 列表 11.4 `Delegate3.cs` 文件中的程序代码

```
using System;
delegate int FuncDelegate(int m, int n);
class Delegate3{
    public static int AddNum(int p, int q)
    {
        return p+q;
    }
```

```
public static int MultNum(int p, int q)
{
    return p*q;
}
static void main(string[] args)
{
    FuncDelegate delegvar=AddNum;
    delegvar+=MultNum;
    Console.WriteLine("*Multiplication of 10 and 20 is {0}", delegvar(10,20));
    delegvar-=MultNum;
    Console.WriteLine("*Addition of 10 and 20 is {0}", delegvar(10,20));
    delegvar-=AddNum;
    if(delegvar!=null)
        Console.WriteLine("*Result of the method that is invoked by the delegate is {0}", delegvar(10,20));
    else
        Console.WriteLine("*Delegate is not pointing to any method*");
}
```

输出：
Multiplication of 10 and 20 is 200
Addition of 10 and 20 is 30
Delegate is not pointing to any method

在前面的程序中，你看到 `FuncDelegate` 实例 `delegvar` 被设置为引用 `AddNum`。然后将 `MultNum` 方法的引用添加到 `delegvar` 实例中，实现了多路委托。两个方法都通过 `delegvar` 实例被调用。方法按照它们添加到 `delegvar` 实例的顺序被调用（先调用 `AddNum`，后调用 `MultNum`）。如预期，`AddNum` 方法的返回值被丢弃，屏幕上只显示 `MultNum` 方法的返回值。

随后，`MultNum` 方法从调用列表中移除，使 `delegvar` 实例仅引用 `AddNum` 方法。再次使用 `delegvar` 实例调用 `AddNum` 方法以显示所提供参数的和。当你从 `delegvar` 实例中移除 `AddNum` 引用后，它变为 `null`，从而在屏幕上显示消息“Delegate is not pointing to any method”。

# 338 页 第 11 章 委托与事件

> 注意：委托是不可变的。当你调用 `+=` 或 `-=` 时，会创建一个新的委托实例来表示新的目标和方法列表，并赋值给现有变量。

回想所有委托类型都隐式派生自 `System.MulticastDelegate`，而后者继承自 `System.Delegate`。这意味着当你创建一个委托类型时，你间接接声明了一个派生自 `System.MulticastDelegate` 的类。该类除了某些方法外，还提供了一个调用列表（invocation list），其中包含委托对象要调用的方法的地址或指针。`System.MulticastDelegate`（或 `System.Delegate`）提供的方法可与调用列表交互。部分方法在表 11.1 中描述。

| 表 11.1 `System.MulticastDelegate` 类的方法 |
| 方法 | 说明 |
| :--- | :--- |
| Method | 返回一个 `System.Reflection.MethodInfo` 对象，表示由委托维护的静态方法的详细信息。 |
| Target | 如果调用的方法是实例方法（而非静态方法），`Target` 返回一个代表委托维护的方法的对象。如果调用的方法是静态的，`Target` 等于 `null`。 |
| Combine() | 向委托维护的列表添加一个方法。可以使用重载的 `+=` 运算符调用该方法。 |
| GetInvocationList() | 返回 `System.Delegate` 对象的数组，表示可能被调用的特定方法。 |
| Remove()/RemoveAll() | 从委托的调用列表中移除一个方法（或所有方法）。可以使用重载的 `-=` 运算符调用该方法。 |

© 2015 Cengage Learning®.

多路委托还涉及委托的组合。当调用组合时，所有由各个委托指向的方法都会被调用。请记住，只有相同类型的委托才能组合。

列表 11.5 显示的 `DelegateCompose.cs` 程序演示了两个委托实例的组合。该程序声明了一个名为 `FunDelegate` 的委托，它可以引用任何返回 `int` 且接收两个 `int` 类型参数的方法。定义了两个与委托签名匹配的静态方法，命名为 `AddNum` 和 `MultNum`。`AddNum` 和 `MultNum` 分别返回所提供参数的加和乘积。定义了一个名为 `devar` 的 `FuncDelegate` 委托实例。`devar` 通过同时引用 `AddNum` 和 `MultNum` 实现了多路分发。

## 多路委托

列表 11.5 显示的 `DelegateCompose.cs` 程序演示了两个委托实例的组合。该程序声明了一个名为 `FuncDelegate` 的委托，它可以引用任何返回 `int` 且接收两个 `int` 类型参数的方法。定义了两个与委托签名匹配的静态方法，命名为 `AddNum` 和 `MultNum`。`AddNum` 和 `MultNum` 分别返回所提供参数的加和乘积。定义了一个名为 `devar` 的 `FuncDelegate` 委托实例。`devar` 通过同时引用 `AddNum` 和 `MultNum` 实现了多路分发。

# 列表 11.5 `DelegateCompose.cs` 文件中的程序代码

```
using System;
delegate void FuncDelegate(int m, int n);
class DelegateCompose
{
    public static void AddNum(int p, int q)
    {
        Console.WriteLine("Sum of {0} and {1} is {2}", p, q, p+q);
    }
    public static void MultNum(int p, int q)
    {
        Console.WriteLine("Multiplication of {0} and {1} is {2}", p, q, p*q);
    }
    static void Main(string[] args)
    {
        FuncDelegate delegvar1 = new FuncDelegate(AddNum);
        FuncDelegate delegvar2 = new FuncDelegate(MultNum);
        FuncDelegate delegarg3 = delegvar1 + delegvar2;
        delegarg3(10, 20);
    }
}
```

输出：
Sum of 10 and 20 is 30
Multiplication of 10 and 20 is 200

# 357 页 第 11 章 委托与事件

两个委托实例使用加法运算符进行组合。同样，使用减法运算符移除委托实例。如果从组合中移除的委托未找到，将获得原始组合。

> 多路委托如果以相同的顺序引用方法则被认为是相等的。

# 多播委托 341

```sharp
FuncDelegate delegvar1 = new FuncDelegate(AddNum);
FuncDelegate delegvar2 = new FuncDelegate(MultNum);
FuncDelegate delegvar3=(FuncDelegate) Delegate.Combine(delegvar1, delegvar2);
if(delegvar3 != null )
{
    foreach(FuncDelegate delsingle in delegvar3.GetInvocationList())
    {
        try {
            delsingle(10,20);
        } catch {}
    }
    delegvar3 = (FuncDelegate) Delegate.Remove(delegvar3, delegvar2);
    delegvar3(10,20);
    delegvar3=(FuncDelegate) Delegate.RemoveAll(delegvar3, delegvar3);
if(delegvar3 != null)
    delegvar3(10,20);
else
    Console.WriteLine("Delegate is not pointing to any method");
```
