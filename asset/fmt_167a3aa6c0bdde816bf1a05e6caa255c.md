
```
struct ScreenPosition
{
    ...
    public int GetX()
    {
        return this.x;
    }

    public void SetX(int newX)
    {
        this.x = rangeCheckedX(newX);
    }
    ...
    private static int rangeCheckedX(int x) { ... }
    private static int rangeCheckedY(int y) { ... }
    private int x, y;
}
```

代码现在成功地强制执行了范围约束，这很好。然而，为了获得这种有价值的保证，需要付出代价——`ScreenPosition` 不再具有自然的字段式语法；它改用笨拙的方法式语法。下面的示例将 `X` 的值增加 10。为此，它必须使用 `GetX` 访问器方法读取 `X` 的值，然后使用 `SetX` 修改器方法写入 `X` 的值。

```
int xpos = origin.GetX();
origin.SetX(xpos + 10);
```

将其与 `X` 字段为 `public` 时的等效代码进行比较：

```
origin.X += 10;
```

毫无疑问，在这种情况下，使用 `public` 字段在语法上更简洁、更短、更容易。不幸的是，使用 `public` 字段会破坏封装。通过使用属性，你可以结合两者（字段和方法）的优点，在保留封装的同时提供类似字段的语法。

## What are properties?

属性是字段和方法之间的混合体——它看起来像字段，但像方法一样工作。你访问属性时使用的语法与访问字段时完全相同。然而，编译器会自动将这种类似字段的语法翻译成对访问器方法的调用（有时称为属性 getter 和属性 setter）。

属性声明的语法如下所示：

```
AccessModifier Type PropertyName
{
    get
    {
        // read accessor code
    }
    set
    {
        // write accessor code
    }
}
```

属性可以包含两个以 `get` 和 `set` 关键字开头的代码块。`get` 块包含在读取属性时执行的语句，而 `set` 块包含在写入属性时运行的语句。属性的类型指定了 `get` 和 `set` 访问器读取和写入的数据类型。

下面的代码示例展示了使用属性重写的 `ScreenPosition` 结构。查看此代码时，请注意以下几点：

- 小写 `_x` 和 `_y` 是私有字段。
- 大写 `X` 和 `Y` 是公共属性。
- 所有 `set` 访问器都使用名为 `value` 的隐藏内置参数传递要写入的数据。

```
struct ScreenPosition
{
    private int _x, _y;

    public ScreenPosition(int X, int Y)
    {
        this._x = rangeCheckedX(X);
        this._y = rangeCheckedY(Y);
    }

    public int X
    {
        get { return this._x; }
        set { this._x = rangeCheckedX(value); }
    }

    public int Y
    {
        get { return this._y; }
        set { this._y = rangeCheckedY(value); }
    }

    private static int rangeCheckedX(int x) { ... }
    private static int rangeCheckedY(int y) { ... }
}
```

在此示例中，私有字段直接实现每个属性，但这只是实现属性的一种方式。唯一的要求是 `get` 访问器返回指定类型的值。这样的值可以很容易地动态计算，而不是简单地从存储的数据中检索，在这种情况下，就不需要物理字段。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_401_0.png)

## Note

尽管本章中的示例展示了如何为结构定义属性，但它们同样适用于类；语法相同。

## Properties and field names: A warning

第 2 章“Working with variables, operators, and expressions”中“Naming variables”部分描述了一些命名变量的建议。特别是，它指出你应避免以下划线开头标识符。然而，你可以看到 `ScreenPosition` 结构并未完全遵循此指导；它包含名为 `_x` 和 `_y` 的字段。这反常是有充分理由的。第 7 章“Creating and managing classes and objects”中侧边栏“Naming and accessibility”描述了使用以大写字母开头的标识符用于公共可访问的方法和字段，以及使用以小写字母开头的标识符用于私有方法和字段的做法是常见的。把这两种做法结合起来，你可能会给属性和私有字段赋予仅在首字母大小写上不同的名称，许多组织正是这样做的。

如果你的组织遵循这种方法，你应该注意一个重要的缺点。检查以下代码，该代码实现了一个名为 `Employee` 的类。`employeeID` 字段是私有的，但 `EmployeeID` 属性提供了对该字段的公共访问。

```
class Employee
{
    private int employeeID;

    public int EmployeeID
    {
        get { return this.EmployeeID; }
        set { this.EmployeeID = value; }
    }
}
```

此代码将完美编译，但它会导致程序在访问 `EmployeeID` 属性时引发 `StackOverflowException` 异常。异常发生的原因是 `get` 和 `set` 访问器引用的是属性（大写 E）而不是私有字段（小写 e），这会导致无休止的递归循环，最终导致进程耗尽可用内存。这种类型的错误很难发现！因此，本书中的示例使用前导下划线命名为属性提供数据的私有字段；这样它们更容易与属性名称区分。所有其他私有字段将继续使用不带前导下划线的 `camelCase` 标识符。

## Using properties

当你在表达式中使用属性时，你可以在读取上下文中使用它（当你检索其值时）和在写入上下文中使用它（当你修改其值时）。下面的示例展示了如何从 `ScreenPosition` 结构的 `X` 和 `Y` 属性读取值：

```
ScreenPosition origin = new ScreenPosition(0, 0);
int xpos = origin.X;    // calls origin.X.get
int ypos = origin.Y;    // calls origin.Y.get
```

请注意，你使用相同的语法访问属性和字段。当你在读取上下文中使用属性时，编译器会自动将你的类似字段代码翻译成对该属性的 `get` 访问器的调用。同样，如果你在写入上下文中使用属性，编译器会自动将你的类似字段代码翻译成对该属性的 `set` 访问器的调用。

```
origin.X = 40;    // calls origin.X.set, with value set to 40
origin.Y = 100;   // calls origin.Y.Set, with value set to 100
```

要赋的值会使用 `value` 变量传递给 `set` 访问器，如前一节所述。运行时会自动执行此操作。

也可以在读写上下文中使用属性。在这种情况下，`get` 访问器和 `set` 访问器都会被使用。例如，编译器会自动将以下语句翻译成对 `get` 和 `set` 访问器的调用：

```
origin.X += 10;
```

## Tip

你可以以声明静态字段和方法相同的方式声明静态属性。你可以通过使用类或结构的名字而不是类或结构的实例来访问静态属性。

## Read-only properties

你可以声明仅包含 `get` 访问器的属性。在这种情况下，你只能在读取上下文中使用该属性。例如，这里是 `ScreenPosition` 结构的 `X` 属性声明为只读属性：

```
struct ScreenPosition
{
    private int _x;
    ...
    public int X
    {
        get { return this._x; }
    }
}
```

`X` 属性不包含 `set` 访问器；因此，任何尝试在写入上下文中使用 `X` 的尝试都将失败，如以下示例所示：

```
origin.X = 140; // compile-time error
```

## Write-only properties

同样，你可以声明仅包含 `set` 访问器的属性。在这种情况下，你只能在写入上下文中使用该属性。例如，这里是 `ScreenPosition` 结构的 `X` 属性声明为只写属性：

```
struct ScreenPosition
{
    private int _x;
    ...
    public int X
    {
        set { this._x = rangeCheckedX(value); }
    }
}
```

`X` 属性不包含 `get` 访问器；任何尝试在读取上下文中使用 `X` 的尝试都将失败，如下所示：

```
Console.WriteLine(origin.X);      // compile-time error
origin.X = 200;                  // compiles OK
origin.X += 10;                  // compile-time error
```

## Note

只写属性对于密码等安全数据很有用。理想情况下，实现安全性的应用程序应允许你设置密码，但永远不允许你读取它。当用户尝试登录时，用户可以提供密码。登录方法可以将此密码与存储的密码进行比较，并仅返回它们是否匹配的指示。

## 属性可访问性

你可以在声明属性时使用 `public`、`private` 或 `protected` 等关键字来指定属性的可访问性。然而，在属性声明中，可以为 `get` 和 `set` 访问器覆盖属性的可访问性。例如，下面的代码中显示的 `ScreenPosition` 结构版本将 `X` 和 `Y` 属性的 `set` 访问器定义为 `private`。（`get` 访问器是 `public`，因为属性是 `public`。）

```
struct ScreenPosition
{
    private int _x, _y;
    ...
    public int X
    {
        get { return this._x; }
        private set { this._x = rangeCheckedX(value); }
    }

    public int Y
    {
        get { return this._y; }
        private set { this._y = rangeCheckedY(value); }
    }
    ...
}
```

在定义可访问性彼此不同的访问器时，必须遵守一些规则：

- 你只能在定义时更改其中一个访问器的可访问性。无论如何，将属性定义为 `public` 只是为了将两个访问器的可访问性都更改为 `private` 都没有多大意义。
- 修饰符不得指定比属性本身更宽松的可访问性。例如，如果属性声明为 `private`，则不能将读访问器指定为 `public`。（相反，你应将属性设为 `public` 并将写访问器设为 `private`。）

## 理解属性限制

当你使用它们读取或写入数据时，属性看起来、表现和感觉都像字段。然而，它们不是真正的字段，并且对其有某些限制：

- 只有在结构或类已被初始化后，才能通过结构或类的属性为其赋值。以下代码示例是非法的，因为 `location` 变量尚未初始化（使用 `new`）：

```
ScreenPosition location;
location.X = 40; // compile-time error, location not assigned
```

### Note

这可能看起来很微不足道，但如果 `X` 是一个字段而不是属性，则代码将是合法的。因此，你应该从一开始就使用属性而不是字段来定义结构和类，而不是后来将字段迁移为属性。在你将字段更改为属性后，使用你的类和结构体的代码可能不再工作。你将在本章后面的“生成自动属性”部分再次讨论此事。

- 你不能将属性用作方法的 `ref` 或 `out` 参数（尽管你可以使用可写的字段作为 `ref` 或 `out` 参数）。这是有道理的，因为属性实际上并不指向内存位置；相反，它指向访问器方法，如以下示例所示：

```
MyMethod(ref location.X); // compile-time error
```

- 一个属性最多可以包含一个 `get` 访问器和一个 `set` 访问器。属性不能包含其他方法、字段或属性。
- `get` 和 `set` 访问器不能接受任何参数。被赋值的数据会通过 `value` 变量自动传递给 `set` 访问器。
- 你不能使用 `const` 声明属性，如下所示：

```
const int X { get { ... } set { ... } } // compile-time error
```

## 适当使用属性

属性是一个强大的功能，如果使用正确，可以帮助使代码更易于理解和维护。然而，它们不能替代以对象的行为而非对象的属性为重点的仔细面向对象设计。通过常规方法或通过属性访问私有字段本身并不能使你的代码设计良好。例如，银行账户保存一个余额，表示账户中可用的资金。因此，你可能会被诱惑在 `BankAccount` 类上创建一个 `Balance` 属性，如下所示：

```
class BankAccount
{
    private decimal _balance;
    ...
    public decimal Balance
    {
        get { return this._balance; }
        set { this._balance = value; }
    }
}
```

这是一个糟糕的设计，因为它未能表示从账户中取款或存款时所需的功能。（如果你知道有一家银行允许你直接更改账户余额而无需将钱实际存入账户，请告诉我！）在编程时，尝试在解决方案中表达你正在解决的问题，不要迷失在大量低级语法中。如以下示例所示，为 `BankAccount` 类提供 `Deposit` 和 `Withdraw` 方法，而不是属性 setter：

```
class BankAccount
{
    private decimal _balance;
    ...
    public decimal Balance { get { return this._balance; } }
    public void Deposit(decimal amount) { ... }
    public bool Withdraw(decimal amount) { ... }
}
```

## 声明接口属性

你在第 13 章“创建接口和定义抽象类”中遇到了接口。接口可以定义属性以及方法。要做到这一点，你指定 `get` 或 `set` 关键字或两者，但用分号替换 `get` 或 `set` 访问器的主体，如下所示：

```
interface IScreenPosition
{
    int X { get; set; }
    int Y { get; set; }
}
```

任何实现此接口的类或结构都必须使用 `get` 和 `set` 访问器方法实现 `X` 和 `Y` 属性。

```
struct ScreenPosition : IScreenPosition
{
    ...
    public int X
    {
        get { ... }
        set { ... }
    }

    public int Y
    {
        get { ... }
        set { ... }
    }
    ...
}
```

如果你在类中实现接口属性，可以将属性实现声明为 `virtual`，从而使派生类能够覆盖实现。
