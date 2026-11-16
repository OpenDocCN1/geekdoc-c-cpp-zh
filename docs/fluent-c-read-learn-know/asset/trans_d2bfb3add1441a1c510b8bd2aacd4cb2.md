

## IS AND AS CASTS

C# 支持两个关键字，可在转换对象时避免异常。is 运算符返回一个布尔值，指示源类型是否为目标类型，或是否通过继承或接口继承从目标类型派生。

```csharp
if (sourceObject is DestinationType)
    destinationObject = (DestinationType)sourceObject;
    //do something
else
    throw new ArgumentException("Please pass a DestinationType.");
```

使用 is 关键字的常见模式如所示——先测试再转换。as 关键字是实现相同目标的一种稍微更高效的方式。如果源对象可以转换为目标对象，as 运算符会执行转换。如果不能，它不会抛出异常，而是返回 null 值，这是未引用任何对象的对象变量所赋的值：

```csharp
DestinationType destinationObject = sourceObject as DestinationType;
if (destinationObject != null)
    //do something
else
    throw new ArgumentException("Please pass a DestinationType.");
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_305_0.png)

## 你做得怎么样？

### Supplier 到 IPrintable:

```csharp
myIPrintable = mySupplier;
```

Supplier 实现了 IPrintable，因此这是一个安全的转换，可以隐式进行。（但显式转换也没错。）

### StockItem 到 IPrintable

```csharp
myIPrintable = myStockItem;
```

尽管 IPrintable 是由 StockItem 的基类实现的，而不是 StockItem 本身，但这仍然是一个安全的转换。

### Component 到 Ingredient

```csharp
myComponent = myIngredient;
```

Component 是 Ingredient 的基类，因此这也是一个安全的转换。但是 (Component)MyIngredient 也没错，并且可能使你的意图更清晰。

### Ingredient 到 Component

```csharp
myComponent = (Component)MyIngredient;
```
or
```csharp
myComponent as Component;
```

这是一个不安全的转换，因此必须显式进行。如果你绝对确定 MyIngredient 确实是一个 Component（通常这意味着你刚刚声明了它），则第一种版本是安全的。第二种始终是安全的，但在使用前你需要检查 MyComponent 是否为 null 值。

## 装箱与拆箱

你知道 C# 会将任何类型隐式转换为其祖先之一，或其或其祖先实现的接口。有时这意味着在值类型和引用类型之间进行转换，这个过程称为装箱（BOXING）和拆箱（UNBOXING）。每当你将值类型转换为接口或所有 .NET Framework 类型的基类 System.Object 时，都可能发生这种情况。

```csharp
Int32 x = 5;
```

Int32 是值类型，因此 x 在栈上创建和存储。

```csharp
x = 5
```

堆上没有任何操作。

```csharp
x.ToString();
```

ToString() 是 System.Object 声明的方法，因此 x 需要被装箱。

在栈上创建一个新的引用对象。

```csharp
x =
x = 5
```

在堆上分配内存以存储其值。

After the ToString() method has executed, the reference value is available for garbage collection.

```csharp
x =
5
```

```csharp
x = 5
```

> ### 独立练习
> 装箱是透明发生的，但这是你需要小心的事情。你认为为什么？(提示：重新阅读第 274 页关于值类型和引用类型的讨论。)

## 参数，再探

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_308_0.png)

让我们做一个小实验，探索值类型和引用类型之间的另一个区别。尝试仅根据说明构建项目，但如果遇到麻烦，我的版本在第 302 页。

- 创建一个新的 WPF 项目并向其中添加一个按钮。
- 在代码文件中，在 MainWindow 类中定义一个名为 Elephant 的类。（记住，类可以将类作为成员。）向 Elephant 添加一个名为 Name 的自动实现属性。
- 向 MainWindow 类（不是 Elephant 类）添加两个方法。两者都命名为 ChangeMe。第一个应接受一个 Int32，并在方法体中递增其值。第二个应接受一个 Elephant，并在方法体中将其 Name 属性更改为“Sally”。
- 在 button1_click 事件处理程序中，创建一个 Int32 变量和一个 Elephant 变量。将 Int32 设置为 5，将 Elephant.Name 属性设置为“George”。
- 仍在 button1_click 事件处理程序中，为你创建的每个变量调用 ChangeMe() 方法，并在 MessageBox 中显示结果。

## 动动脑筋

在运行应用程序之前，你认为 MessageBox 中显示的值会是什么？

Elephant.Name:

Int32:

5

现在运行应用程序并单击按钮。MessageBox 显示的结果是你预期的吗？

如果我告诉你，默认情况下，当你将变量作为参数传递给方法时，它是按值传递——方法实际接收的是栈上内容的副本，当方法结束时，传递给它的副本会被丢弃，这可能有助于你理解发生了什么。

那么我们的两个变量各自在栈上有什么呢？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_309_0.png)

## 演练代码

这是我编写的演练代码版本。你的代码不必完全匹配，只要基本元素到位即可。

```csharp
public partial class MainWindow : Window
{
    public class Elephant
    {
        public String Name { get; set; }
    }

    public MainWindow()
    {
        InitializeComponent();
    }

    private void button1_Click(object sender, RoutedEventArgs e)
    {
        Int32 MyInt;
        Elephant MyPet = new Elephant();

        MyInt = 5;
        MyPet.Name = "George";

        ChangeMe(MyInt);
        ChangeMe(MyPet);

        MessageBox.Show("My pet's name is " + MyPet.Name + " " +
            MyInt.ToString());
    }

    private void ChangeMe(Int32 x)
    {
        x++;
    }

    private void ChangeMe(Elephant x)
    {
        x.Name = "Sally";
    }
}
```

## 按引用传递

当你将变量作为参数传递给方法时，方法接收栈上值的副本。对于值类型，它接收值的副本。对于引用类型，它接收堆上值的引用的副本（换句话说，引用按引用传递，值按值传递）。

当方法退出时，参数会被丢弃，但通过引用所做的更改（即对堆上值的更改）会保留。这就是为什么对 Name 属性的更改被保留，而对 Int32 变量值的更改没有被保留。

### 按值传递

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_311_0.png)

### 按引用传递

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_311_1.png)

> ### 动动脑筋
> 
> 如果按值将引用类型传递给方法，你能让它引用另一个对象吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_312_0.png)

## 参数要点

你不需要过分担心堆和栈上发生的细节。以下是重要要点：

- 按值传递的值类型不能更改
- 按值传递的引用类型的属性可以更改
- 按值传递的引用类型所引用的对象不能更改
- 按引用传递的值类型的属性可以更改
- 按引用传递的引用类型所引用的对象可以更改

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_312_1.png)

## 你做得怎么样？

不，你不能。就像传递值类型一样，你对栈上内容（引用）所做的更改在方法退出时会被丢弃。

```csharp
void DoSomething(Elephant x)
{
    y = new Elephant();
    x = y;
}
```

这一行没有实际效果，因为传递给此方法的参数在方法退出时仍将引用原始对象。

## 引用语法

C# 中用于按引用传递值的关键字是 ref。方法定义和方法调用都必须使用该关键字：

```csharp
void DoSomething(ref Elephant x)
{
    y = new Elephant();
    x = y;
}
```

两者必须匹配。

```csharp
DoSomething(ref MyPet);
```

此行现在有效，因为更改将被保留。

### 做个笔记

ref 修饰符是签名的一部分，因此你可以声明两个版本的方法，它们仅在是否可以更改参数方面有所不同。但这似乎不是个好主意，是吧？不。我也不这么认为。

### 休息一下

目前关于创建 .NET Framework 类型的内容就到这里。随着我们继续阅读本书，我们将回到前几章讨论过的许多主题，特别是在“原则”部分，但目前，在回来完成最后的复习之前，先休息一下。

