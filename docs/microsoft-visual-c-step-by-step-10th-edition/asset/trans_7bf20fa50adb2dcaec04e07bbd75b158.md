

-   属性最多包含一个 `get` 访问器和一个 `set` 访问器。属性不能包含其他方法、字段或属性。
-   `get` 和 `set` 访问器不能接受任何参数。赋值的数据通过 `value` 变量自动传递给 `set` 访问器。
-   你不能使用 `const` 声明属性，如下：

```cs
const int X
{
    get => ...
    set => ...
} // 编译错误
```

## 恰当使用属性

属性是一个强大的功能。如果使用正确，它们可以帮助代码更易理解和维护。然而，它们并不适用于细致的面向对象设计，因为这种设计关注的是对象的行为而非对象的属性。

通过普通方法或属性访问私有字段本身并不会让你的代码设计得良好。例如，银行账户持有一个余额（balance），表示账户中的可用资金。你可能诱于在 `BankAccount` 类上创建一个 `Balance` 属性，如下所示：

点击此处查看代码图像

```csharp
class BankAccount
{
    private decimal _balance;
    ...
    public decimal Balance
    {
        get => this.balance;
        set => this.balance = value;
    }
}
```

这是一种糟糕的设计，因为它没有体现当有人向账户取款或存款时所需的功能。（如果你知道哪家银行允许你在不物理向账户存钱的情况下直接增加账户余额，请告诉我！）

在编程时，请尝试在解决方案中表达你正在解决的问题，不要迷失在大量的低级语法中。如下例所示，为 `BankAccount` 类提供 `Deposit` 和 `Withdraw` 方法，而不是使用属性set器器：

点击此处查看代码图像

```csharp
class BankAccount {
  private decimal _balance;

  public decimal Balance { get => this._balance; }
  public void Deposit(decimal amount) { ... }
  public bool Withdraw(decimal amount) { ... }
}
```

## 声明接口属性

你已经在第 13 章“创建接口和定义抽象类”中遇到过接口。你可以使用接口来定义属性，也可以用来定义方法。要这样做，请指定 `get` 或 `set` 关键字（或两者兼有），但要像所示将 `get` 或 `set` 访问器的正体替换为分号：

```cs
interface IScreenPosition {
  int X { get; set; }
  int Y { get; set; }
}
```

任何实现此接口的类或结构必须使用 `get` 和 `set` 访问器方法（或表达式体成员）实现 x 和 y 属性。

点击此处查看代码图像

```cs
struct ScreenPosition : IScreenPosition {
  public int X {
    get { ... } // 或 get =>
    set { ... } // 或 set =>
  }
  public int Y
  {
    get { ... }
    set { ... }
  }
  ...
}
```

如果你在类中实现接口属性，可以将属性实现声明为 `virtual`，这允许派生类重写这些实现。

点击此处查看代码图像

```csharp
class ScreenPosition : IScreenPosition
{
    ...
    public virtual int X
    {
        get { ... }
        set { ... }
    }
    public virtual int Y
    {
        get { ... }
        set { ... }
    }
    ...
}
```

> 注意：此示例展示了一个类。记住，在创建结构体时 `virtual` 关键字是无效的，因为结构体不支持继承。

你也可以选择使用第 13 章涵盖的显式接口实现语法来实现属性。属性的显式实现是非最终（nonfinal）且非虚拟（nonvirtual）的（无法重写）。

```cs
struct ScreenPosition : IScreenPosition
{
  ...
  int IScreenPosition.X
{
    get { ... }
    set { ... }
  }
  int IScreenPosition.Y
{
    get { ... }
    set { ... }
  }
  ...
}
```

## 用属性替换方法

第 13 章教了你如何创建一个应用程序，用户可以在窗口画布上放置圆形和正方形。在该章的练习中，你将 `Circle` 和 `Square` 类的公共功能提取到抽象类 `DrawingShape` 中。`DrawingShape` 类提供了 `SetLocation` 和 `SetColor` 方法，应用程序使用这些方法指定屏幕上形状的位置和颜色。在下面的练习中，你将修改 `DrawingShape` 类，将形状的位置和颜色暴露为属性。

## 使用属性

-   1. 启动 Visual Studio 2022，如果它尚未运行。
2. 打开 `Drawing` 解决方案，它位于文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 15\Drawing Using Properties` 文件夹中。
3. 在代码和文本编辑器中显示 `DrawingShape.cs` 文件。该文件包含了第 13 章中的 `DrawingShape` 类，但根据本章之前描述的建议，`size` 字段已重命名为 `_size`，`locX` 和 `locY` 字段已重命名为 `_x` 和 `_y`。

点击此处查看代码图像

```csharp
abstract class DrawingShape
{
    protected int size;
    protected int _x = 0, _y = 0;
    ...
}
```

-   4. 在代码和文本编辑器窗口中打开 `Drawing` 项目的 `IDraw.cs` 文件。此接口指定了 `SetLocation` 方法，如下：

点击此处查看代码图像

```cs
interface IDraw
{
    void SetLocation(int xCoord, int yCoord);
}
```

此接口指定 `SetLocation` 方法，如下：

点击此处查看代码图像

```cs
interface IDraw
{
    void SetLocation(int xCoord, int yCoord);
}
```

通过普通方法或属性访问私有字段本身并不会让你的代码设计得良好。

5. 删除此方法并将其替换为 `x` 和 `y` 属性对，如下：

```cs
interface IDraw
{
    int X { get; set; }
    int Y { get; set; }
}
```

6. 在 `DrawingShape` 类中删除 `SetLocation` 方法，将其替换为 `x` 和 `y` 属性的实现，如下：

```csharp
public int X
{
    get => this._x;
    set => this._x = value;
}

public int Y
{
    get => this._y;
    set => this._y = value;
}
```

7. 在代码和文本编辑器中显示 `DrawingPad.cs` 文件并找到 `Tapped` 方法。该方法在用户点击左左键时运行。

8. 找到调用 `SetLocation` 方法的语句，以设置屏幕上正方形的位置，如下：

```csharp
if (mySquare is IDraw)
{
    IDraw drawSquare = mySquare;
    drawSquare.SetLocation((int)mouseLocation.X, (int)mouseLocation.Y);
    drawSquare.Draw(drawingCanvas);
}
```

9. 将此语句替换为设置 `x` 和 `y` 属性的代码，如下所示：

```csharp
if (mySquare is IDraw)
{
    IDraw drawSquare = mySquare;
    drawSquare.X = (int)mouseLocation.X;
    drawSquare.Y = (int)mouseLocation.Y;
    drawSquare.Draw(drawingCanvas);
}
```

10. 找到 `RightTapped` 方法。该方法在用户按住屏幕或点击右键时运行。它在用户按住或右键点击的位置绘制圆形。

11. 在此方法中，替换调用圆形对象 `SetLocation` 方法的语句，转而使用 `x` 和 `y` 属性，如下所示：

```csharp
if (myCircle is IDraw)
{
    IDraw drawCircle = myCircle;
    drawCircle.X = (int)mouseLocation.X;
    drawCircle.Y = (int)mouseLocation.Y;
    drawCircle.Draw(drawingCanvas);
}
```

12. 在代码和文本编辑器窗口中打开 `Drawing` 项目的 `Color.cs` 文件。此接口指定 `SetColor` 方法，如下：

```cs
interface IColor {
    void SetColor(Color color);
}
```

13. 删除此方法并将其替换为名为 `Color` 的属性定义，如下所示：

```cs
interface IColor {
    Color Color { set; }
}
```

