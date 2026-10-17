
```csharp
public static bool operator !=(Vector v1, Vector v2)
{
    return !(v1 == v2);
}
```

不要忘记 – 我之前提到过，当你重载关系运算符时，它们必须成对进行。所以，如果你重载了`==`，你也必须重载`!=`，就像上面的例子所示，虽然如果你愿意，也可以调用另一个运算符。

仔细看看这些重载，你应该能看出它们与普通方法的区别只在于`operator`关键字。C# 只是在代码的任何部分使用该运算符时将其转换为方法调用。说实话，这不过就是所谓的语法糖——它只是让代码看起来整洁美观。

现在，我们完整的类应该如下所示：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace OperatorOverloading
{
    public class Vector
    {
        public double X { get; set; }
        public double Y { get; set; }

        public Vector(double x, double y)
        {
            X = x;
            Y = y;
        }

        public static Vector operator +(Vector v1, Vector v2)
        {
            return new Vector(v1.X + v2.X, v1.Y + v2.Y);
        }

        public static Vector operator +(Vector v, double scalar)
        {
            return new Vector(v.X + scalar, v.Y + scalar);
        }

        public static Vector operator -(Vector v)
        {
            return new Vector(-v.X, -v.Y);
        }

        public static bool operator ==(Vector v1, Vector v2)
        {
            return ((v1.X == v2.X) && (v1.Y == v2.Y));
        }

        public static bool operator !=(Vector v1, Vector v2)
        {
            return !(v1 == v2);
        }
    }
}
```

现在运算符重载已经定义，它们可以像任何普通运算符一样使用：

```csharp
Vector a = new Vector(5, 2);
Vector b = new Vector(-3, 4);
Vector result = a + b; // 这里使用了运算符重载。
// 这里，结果是 <2, 6>。
```

### 快速入门

- 运算符重载是一种让我们能够定义传统运算符对我们创建的对象和类的工作方式的方法。

- 运算符重载适用于`=`、`-`、`/`、`*`、`%`、`++`、`==`、`--`、`!=`、`<`、`>`、`<=`和`>=`运算符，以及我们尚未讨论的另外几个运算符。

- 它不适用于赋值`==`、点号(`.`)、`new`、`&&`或`||`运算符。

- 重载`+`运算符可能看起来像这样：`public static Vector operator +(Vector v1, Vector v2) { return new Vector(v1.X +v2X, v1.Y + v2.Y; }`。

- 每个运算符都必须标记为`static`且`public`。

- 当关系运算符被重载时，必须成对进行，所以例如，如果`==`被重载，那么`!=`也必须被重载。

- `[`和`]`索引运算符也可以被重载，但这是以不同的方式完成的，我们稍后会看到。

#### 下一步是什么？

运算符重载是让你的代码更易读的最简单却最强大的方法之一。在下一节中，我们将研究索引器，这是一种非常相似的重载`[`和`]`运算符的方式。

### 索引器

我们在上一节讨论了运算符重载，在这一节中，我们将通过研究索引器来简要扩展它。索引器与重载索引运算符非常相似。就像运算符重载一样，仅因为你可以这样做，并不意味着你应该一直这样做。

### 创建索引器

当你定义一个索引器时，它很像属性和重载运算符的组合。做起来并不难，所以我们首先要做的就是看看让你做到这一点的代码片段。你可以将它添加到之前的`Vector`类中，但另一方面，如果你修改了`set`和`get`访问器的行为，你也可以把它放在任何类中：

```csharp
public double this[int index]
{
    get
    {
        if(index == 0) { return this.X; }
        else if(index == 1) { return this.Y; }
        else { throw new IndexOutOfRangeException(); }
    }
    set
    {
        if (index == 0) { this.X = value; }
        else if (index == 1) { this.Y = value; }
        else { throw new IndexOutOfRangeException(); }
    }
}
```

我们在这里指定了索引器的访问级别——我们使用了`public`——然后指定了返回类型。`this`关键字与`[]`方括号一起使用以表示索引。在方括号中，我们放置将在索引器中使用的索引变量类型和名称。

然后，与属性类似，我们有`get`和`set`代码块。同样像属性一样，如果你不想或不需要，你不必同时使用两者——只保留一个。在这些块内部，变量`index`可以与`setter`中的`value`关键字一起使用，引用将被赋予的值。

在这个例子中，我让向量`x`和`y`分量可以通过 0 索引访问`x`，1 索引访问`y`来被他人引用。有了所有这些，我们现在可以这样做：

```csharp
Vector v = new Vector(5, 2);
double xComponent = v[0]; // 现在我们可以使用索引运算符。
double yComponent = v[1];
```

这比替代方案更容易阅读和理解——替代方案会有一个名为`GetIndex`的方法，或类似的名称，并且会读作`xComponent = v.GetIndex(0);`。

但你不必只使用`int`作为索引。你也可以使用`double`、`string`或任何你想要的类型。事实上，想想我们谈论泛型时；`Dictionary`类就是这样做的。

这个例子展示了如何使用字符串进行索引：

```csharp
public double this[string component]
{
    get

if (component == "x") { return this.X; }
else if (component == "y") { return this.Y; }
else { throw new IndexOutOfRangeException(); }
}
set
{
if (component == "x") { this.X = value; }
else if (component == "y") { this.Y = value; }
else { throw new IndexOutOfRangeException(); }
}
}
```

这与我们之前使用的方法类似，但我们使用的是字符串而不是`int`进行索引。如果请求`x`，则返回`x`分量，如果请求`y`，则返回`y`分量。

所以现在我们可以这样做：

```csharp
Vector v = new Vector(5, 2);
double xComponent = v["x"]; // 现在我们可以使用索引运算符。
double yComponent = v["y"];
```

这变得更好，因为我们也可以使用多个索引进行索引。同样，你可能可以做到，但这并不意味着你应该这样做。只有在适当的情况下才这样做。

要添加多个索引，你只需在索引器定义处的方括号内列出它们。

```csharp
public double this[string component, int index]
{
    get

{
    // 我不太确定该如何处理这里的两个索引。
    // 我想我可能只是抛出一个异常。如果使用多个索引创建索引器是有意义的，你会在这里编写一些能够智能处理它的代码。
    throw new Exception();
}
set
{
    // 我不太确定该如何处理这里的两个索引。
    // 我想我可能只是抛出一个异常。如果使用多个索引创建索引器是有意义的，你会在这里编写一些能够智能处理它的代码。
    throw new Exception();
}
}
```

在这种情况下，这完全有意义，并且它向你展示了这是可以做到的；如果你能使用它，制作起来很容易。

### 快速入门

- 索引器是为类重载索引`[`和`]`运算符的一种方式。

- 定义索引器很像属性和运算符重载的组合：`public double this[int index] { get { /* get code goess here */ } set { /* set code goes here */ } }`。

- 你不局限于使用`int`；任何类型都可用于索引。

- 要使用多个索引，你只需在索引器定义处列出它们。

- 而不是使用`[ int index ]`，你可以使用`[ string someTextIndex, int numericIndex]`。

#### 下一步是什么？

我们讨论了运算符重载，这是一种让我们可以使运算符在自定义类中看起来和工作方式符合我们期望的方法，然后我们转向了索引器，这基本上是使用索引运算符的相同事情。接下来，我们将进行完全相同的事情，但使用用户定义的转换。这意味着我们可以指示一个类如何转换为另一种类型。

### 用户定义转换

使用运算符重载，我们可以让使用的运算符以特殊的方式与我们的类一起工作，并且我们也可以使用索引运算符做同样的事情。现在我们要看看如何自定义定义一种方式来确保我们的类可以被强制转换或转换为不同类型。你会发现强制转换和转换是可以互换使用的，因为它们的意思相同——从一种类型更改为另一种类型。

#### 隐式与显式转换

在讨论用户定义转换之前，我们应该解释转换是如何工作的。

作为示例，我们来看两种类型——`float`和`double`。假设我们有一个`float`；如果我们愿意，我们可以用它作为`double`，程序会自动将其转换为`double`。方法如下：

```csharp
float a = 3.5f;
```

然而，如果我们尝试反过来做，发生的所有事情都将是一个编译时错误：

```csharp
double b = 3.5;
float a = b; // 这将无法编译，因为你试图将 double 转换为 float。
```

为什么我们不能这样做？这归结于大小。你不能把一个`double`放入一个像`float`那样小的东西中，而`float`没有`double`的精度和准确度——你所能实现的就是信息丢失。

话虽如此，确实有一种转换方法；你需要明确说明这就是你想要做的：

```csharp
double b = 3.5;
float a = (float)b;
```

你在这里所做的是告知编译器你确实想要将`double`转换为`float`，即使你在过程中可能会丢失信息。

这就是隐式转换和显式转换之间的区别。当将`float`转换为`double`时，暗示它可以非常轻松地更改而无需做任何特殊操作。对于显式转换，你必须明确表示你确实知道自己在做什么，并且是的，你确实想要将此类型转换为另一种类型。这是通过使用强制转换运算符`(`和`)`完成的，将类型放在括号之间，如最后一个示例。

#### 创建用户定义转换

为了向你展示它是如何工作的，我们将回到之前创建的`MagicNumber`类：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace UserDefinedConversions
{
    public class MagicNumber
    {
        public int Number { get; set; }
        public bool IsMagic { get; set; }
    }
}
```

这个类很简单；一个数字以`int`存储，我们有一个`bool`告诉我们我们的数字是否‘神奇’，无论这对你的程序意味着什么。

你可能最能看到的是，可以想象如何将一个`int`转换为`MagicNumber`，反之亦然——将一个`MagicNumber`转换为`int`。做到这一点只需要一小段代码，以便转换可以发生。

要将`int`转换为`MagicNumber`，我们可以隐式地执行此操作，无需使用`(MagicNumber)`来强制转换它，只需传入`int`并使`IsMagic`评估为`false`：

```csharp
static public implicit operator MagicNumber(int value)
{
    return new MagicNumber() { Number = value, IsMagic = false };
}
```

与任何运算符一样，这个运算符必须标记为`static`和`public`。接下来，我们需要说明转换是隐式还是显式——我们为此示例选择了隐式。

接下来，我们指定转换发生的类型——`MagicNumber`——并且，在一组括号内，指定正在转换的类型。在转换体中，我们有执行转换的代码。

将此添加到`MagicNumber`类后，从`int`到`MagicNumber`的转换非常简单：

```csharp
int aNumber = 3;
MagicNumber magicNumber = aNumber;
```

创建显式强制转换的方式也差不多。我们现在将定义从`MagicNumber`到`int`的转换。顺便说一句，当转换过程中信息将被丢失时，要求强制转换是显式的是一个好主意。

使强制转换显式化就像在我们的类中添加类似这样的内容一样简单：

```csharp
static public explicit operator int(MagicNumber magicNumber)
{
    return magicNumber.Number;
}
```

与之前一样，它必须同时标记为`public`和`static`。`explicit`关键字用于指示这一点，并且为了使用它，必须明确说明你想要使用转换以及转换运算符。`operator`关键字被使用，并且，正如我们之前所做的那样，我们想要转换到的类型。在我们的括号内，我们说明我们正在转换的类型。

在转换块中是我们用于执行转换的代码，在此示例中，我们取`MagicNumber`的数字并留下`IsMagic`。发生的事情是我们丢失了告诉我们数字是否神奇的信息——`IsMagic`是否设置为`true`或`false`。

你可以在代码的其他地方使用此转换，但现在，我们需要明确我们正在从一种类型显式强制转换到另一种类型：

```csharp
MagicNumber magicNumber = new MagicNumber() { Number = 3, IsMagic = true };
int aNumber = (int)magicNumber;
```

### 快速入门

- 用户定义转换让你定义编译器和运行时如何转换到和从用户创建的类。

- 隐式强制转换是在无需转换运算符即可进行更改时。显式强制转换确实需要运算符。例如，从`float`隐式强制转换为`double`——`float a = 3; double b = a;`。分配给`a`的值会自动转换为`double`。

  然后，因为我们不能隐式地将`double`强制转换为`float`，所以我们需要显式地执行——`double a = 3; float b = (float)a;`。只要明确说明正在进行转换，`a`中的值就可以转换为`float`。

- 创建用户定义转换需要你遵循以下格式——`static public implicit operator MagicNumber(int value) { /* 在此处完成你的转换以返回一个 MagicNumber */ }`；

- 为了指示你正在进行的转换类型，你可以使用关键字`implicit`或`explicit`。

#### 下一步是什么？

用户定义转换是非常棒的功能，正确使用它们可以让你的代码变得易于阅读和整洁；它们也非常强大。

在下一节中，我们将介绍扩展方法，这是一个 C# 功能，让你可以向你从未创建过且无法直接修改或添加的类添加方法。这将为我们带来这一高级部分的结束。

### 扩展方法

直接进入主题，假设我们有一个类，但别人创建了它。它可能是 .NET 框架的一部分，例如`String`类，它相当于我们已经很好利用的类型——`string`类型。

现在假设我们有一个方法，我们想在`string`类型上使用它，但你没有类在那里进行修改。`String`类或`string`类型有两个方法称为`ToUpper()`和`ToLower()`，但如果我们想创建一个方法将其转换为另一种类型，例如使每个字母是小写还是大写随机，而不是一个或另一个？实际上创建该方法非常简单。我们想说类似`"Hello World!".ToRandomCase()`而不是说`ToUpper()`或`ToLower()`，并且，如果无法访问该类，我们通常不会能够添加新的`ToRandomCase()`方法。这是不正常的。

然而，C# 有一种方法让我们可以做到这一点，使用称为扩展方法的东西。我们所做的是在静态类中创建一个静态方法，并使用`this`关键字创建一个方法，可以像它属于原始类一样使用。

#### 创建扩展方法

创建扩展方法真的并不困难——首先，我们创建一个静态类，然后在其中放置一个静态方法来完全满足我们对扩展方法的要求。
