
一个参数。C 语言没有类型安全。你可以将任意函数传递给需要函数指针的方法。不幸的是，这种直接方式不仅会引发一些类型安全问题，还忽略了一个事实：在进行面向对象编程时，方法很少独立存在；它们通常需要与类实例关联后才能被调用。由于这些问题，.NET Framework 在语法上不允许这种直接方式。相反，如果你想传递方法，就必须将方法的细节包装到一种新型对象中，即委托（delegate）。简单来说，委托是一种特殊类型的对象——特殊之处在于，迄今为止定义的所有对象都包含数据，而委托包含的是方法的地址，或多个方法的地址。

## 声明委托

在 C# 中使用类时，需要分两个阶段进行。首先，需要定义类——也就是说，需要告诉编译器这个类由哪些字段和方法组成。然后（除非你只使用静态方法），实例化该类的一个对象。委托也是如此。首先声明要使用的委托。声明委托就是告诉编译器该类型的委托将表示哪种方法。然后，必须创建该委托的一个或多个实例。在幕后，编译器会创建一个表示该委托的类。

声明委托的语法如下所示：

```
delegate void IntMethodInvoker(int x);
```

这将声明一个名为 IntMethodInvoker 的委托，并指明该委托的每个实例都可以持有对一个方法的引用，该方法接受一个 int 参数并返回 void。关于委托，需要理解的关键点是它们是类型安全的。定义委托时，必须提供其所表示方法的签名和返回类型的完整细节。

> **注意** 理解委托的一个好方法是将委托视为给方法签名和返回类型命名的东西。

假设你想定义一个名为 TwoLongsOp 的委托，它表示一个接受两个 long 参数并返回 double 的方法。你可以这样做：

```
delegate double TwoLongsOp(long first, long second);
```

或者，要定义一个表示不带参数且返回字符串的方法的委托，可以这样写：

```
delegate string GetAString();
```

该语法与方法定义的语法相似，只是没有方法体，并且定义以关键字 delegate 开头。因为你在这里所做的基本上就是定义一个新类，所以你可以在定义类的任何地方定义委托——也就是说，可以在另一个类内部、任何类外部，或者在命名空间中作为顶级对象。根据你希望定义的可见性以及委托的作用域，你可以将任何常规访问修饰符应用于委托定义——public、private、protected 等：

```
public delegate string GetAString();
```

> **注意** 当我们把定义委托描述为定义一个新类时，我们确实是这个意思。委托是作为从 System.MulticastDelegate 类派生的类实现的，而 System.MulticastDelegate 又派生自基类 System.Delegate。C# 编译器知道这个类，并使用其委托语法来隐藏这个类操作的细节。这是 C# 与基类协同工作以尽可能简化编程的另一个好例子。

定义委托后，你可以创建它的一个实例，以便用它来存储有关特定方法的详细信息。

> **注意** 这里有一个不幸的术语问题。在讨论类时，有两个不同的术语：class（类），表示较宽泛的定义；object（对象），表示类的一个实例。不幸的是，对于委托，只有一个术语；delegate（委托）既可以指类，也可以指对象。当你创建委托的一个实例时，所创建的东西也被称为委托。在讨论委托时，你需要根据上下文来了解使用的是哪个含义。

## 使用委托

下面的代码片段演示了委托的使用。这是一种相当啰嗦的调用 int 的 ToString 方法的方式（代码文件 GetAStringDemo/Program.cs）：

```
private delegate string GetAString();

public static void Main()
{
    int x = 40;
    GetAString firstStringMethod = new GetAString(x.ToString);
    WriteLine($"String is {firstStringMethod()}");
    // With firstStringMethod initialized to x.ToString(),
    // the above statement is equivalent to saying
    // Console.WriteLine($"String is {x.ToString()}");
}
```

这段代码实例化了一个 `GetAString` 类型的委托，并对其进行初始化，使其引用整数变量 x 的 `ToString` 方法。在 C# 中，委托在语法上总是接受一个单参数构造函数，该参数就是委托所引用的方法。此方法必须与你最初定义委托时的签名匹配。在这种情况下，如果你试图用任何不带参数且不返回字符串的方法来初始化变量 `firstStringMethod`，就会收到编译错误。注意，由于 `int.ToString` 是一个实例方法（与静态方法相对），你需要同时指定实例 (x) 和方法名称，才能正确初始化委托。

下一行实际上使用委托来显示字符串。在任何代码中，提供委托实例的名称，后跟包含任何参数的括号，与调用该委托包装的方法具有完全相同的效果。因此，在前面的代码片段中，`Console.WriteLine` 语句与注释掉的那行完全等价。

实际上，给委托实例加上括号等同于调用委托类的 `Invoke` 方法。因为 `firstStringMethod` 是委托类型的变量，C# 编译器会将 `firstStringMethod` 替换为 `firstStringMethod.Invoke`：

```
firstStringMethod();
firstStringMethod.Invoke();
```

为了减少输入，在需要委托实例的任何地方，你都可以直接传递方法名称。这被称为 *委托推断*（delegate inference）。只要编译器能将委托实例解析为特定类型，这个 C# 功能就能正常工作。该示例使用委托 `GetAString` 的一个新实例初始化了类型为 `GetAString` 的变量 `firstStringMethod`：

```
GetAString firstStringMethod = new GetAString(x.ToString);
```

你可以只将方法名称与变量 x 一起传递给变量 `firstStringMethod`，实现同样的效果：

```
GetAString firstStringMethod = x.ToString;
```

C# 编译器生成的代码是相同的。编译器检测到 `firstStringMethod` 需要委托类型，因此它会创建委托类型 `GetAString` 的一个实例，并将方法地址与对象 x 一起传递给构造函数。

> **注意** 请注意，你不能在方法名后面加上括号，写成 `x.ToString()`，并将其传递给委托变量。那将是对方法的调用。`ToString` 方法的调用会返回一个字符串对象，不能赋值给委托变量。你只能将方法的地址赋给委托变量。

现在你可以如下使用 GetAString 实例（代码文件 GetAStringDemo/Program.cs）：

```
private delegate string GetAString();

public static void Main()
{
    int x = 40;
    GetAString firstStringMethod = x.ToString;
    WriteLine($"String is {firstStringMethod()}");

    var balance = new Currency(34, 50);

    // firstStringMethod references an instance method
    firstStringMethod = balance.ToString;
    WriteLine($"String is {firstStringMethod()}");

    // firstStringMethod references a static method
    firstStringMethod = new GetAString(Currency.GetCurrencyUnit);
    WriteLine($"String is {firstStringMethod()}");
}
```

这段代码演示了如何通过委托调用方法，并随后重新分配委托，使其引用不同类实例上的不同方法，甚至是静态方法或针对不同类型类实例的方法，前提是每个方法的签名都与委托定义匹配。

运行应用程序时，你会得到由委托引用的不同方法所返回的输出：

```
String is 40
String is $34.50
String is Dollar
```

然而，你还没有看到真正将委托传递给另一个方法的过程。而且，目前这还没有实现任何特别有用的功能。调用 int 和 Currency 对象的 ToString 方法，可以比使用委托更直接。遗憾的是，委托的本质决定了你需要一个相当复杂的示例才能真正体会到它们的用处。下一节将介绍两个委托示例。第一个示例只是使用委托来调用几个不同的操作。它说明了如何将委托传递给方法，以及如何使用委托数组——尽管可以说，它并没有做到不用委托也能更简单完成的事情。第二个示例要复杂得多，它介绍了一个 BubbleSorter 类，该类实现了一个将对象数组按升序排序的方法。如果不使用委托，这个类将很难编写。

## 简单的委托示例

这个示例定义了一个 MathOperations 类，该类使用几个静态方法对 double 执行两种操作。然后你使用委托来调用这些方法。MathOperations 类如下所示：

