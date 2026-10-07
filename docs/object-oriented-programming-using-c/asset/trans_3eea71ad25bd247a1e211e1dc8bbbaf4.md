
# 使用 C# 的面向对象编程

## 继承与方法重写

```csharp
private double price;
public double Price
{
    get { return price; }
    set { price = value; }
}
private int copies;
public int Copies
{
    get { return copies; }
    set { copies = value; }
}
```

因此，当我们引用 'copies' 时，我们指的是一个在类外部无法访问的私有变量。当我们引用大写字母 的 'Copies' 时，我们指的是公共属性……由于它是公共的，我们可以从任何类中使用它来获取或更改 'copies' 的值。

在上面的代码中，属性的定义方式使得它们可以获取和设置相应变量的值……且没有任何限制。我们可以修改这一点以施加限制，或者移除 'get' 或 'set' 方法。

通过使用 'Copies = orderQty'，我们实际上是在调用一个设置器方法（setter method），但我们是通过使用属性来实现此点的。这与之前显示的使用设置器方法设置新值实际上是相同的……'Copies(orderQty);'

使用属性，我们可以将上面显示的方法替换为下面的方法。

```csharp
// 在 Book 中
public void OrderCopies(int orderQty)
{
    Copies = Copies + orderQty;
}
```

```csharp
// 以及在 Magazine 中
public void RecNewIssue(String newIssue)
{
    Copies = orderQty;
    currIssue = newIssue;
}
```

使用属性在 C# 中是常见的。在其他面向对象的语言中，访问器方法（accessor methods）的作用是完全相同的。

使用 C# 的面向对象编程

继承与方法重写

## 3.8 抽象类

一个既不是书（Book）也不是杂志（Magazine）的出版物（Publication）是没有意义的，就像既不是男性（MalePerson）也不是女性（FemalePerson）的人一样。因此，虽然我们乐意创建 Book 或 Magazine 对象，但我们可能希望防止创建 Publication 类型的对象。

如果我们想处理一种真正的既书也不是杂志的新类型 Publication——例如报纸（Newspaper），它自然会成为 Publication 的另一个子类。

由于 Publication 永远不会被实例化，即我们永远不会创建这种类型的对象，该类存在的唯一目的是将其子类的泛化特征汇集在一起，供它们继承。

![](img/e143b38d00f95425fa4f3efca0527189_76_0.png)

请点击广告

在 bookboom.com 免费下载电子书

我们通过将其声明为 'abstract'（抽象）来强制执行 Publication 不可实例化：

```csharp
public abstract class Publication
{
  // 等等
```

## 3.9 方法重写

子类继承其父类的方法，因此必须始终提供至少与父类相同的方法，且通常更多。然而，方法的实现可以在子类中进行更改。

这就是方法重写（overriding）。

为了做到这一点，我们在子类中写一个新版本来替换继承而来的版本。

新方法本质上应该执行与它所替换的方法相同的功能，但通过更改功能，我们可以改进该方法，并使其功能更适用于特定的子类。

例如，想象一种特殊的杂志类别，每份杂志都附带了一张光盘——我们可以将其命名为 DiscMag，并创建一个 Magazine 的子类来处理 DiscMag。当一期 DiscMag 的新杂志到达时，我们不仅想要更新当前库存，还想要检查光盘是否正确连接。因此，我们希望在 RecNewIssue() 方法中加入额外的功能来提醒我们这样做。我们通过在 DiscMag 子类中重新定义 RecNewIssue() 来实现这一点。

注意，当一期 Magazine 新杂志到达时，由于它们没有光盘，我们想要调用 Magazine 类中定义的原始 RecNewIssue() 方法。

![](img/e143b38d00f95425fa4f3efca0527189_77_0.png)

- DiscMag 中 RecNewIssue() 的定义重写了继承的定义。
- Magazine 不受影响——它保留了原始的 RecNewIssue() 定义。
- 通过在 DiscMag 中显示 RecNewIssue()，我们表明继承的方法正在被重写（即被替换），因为我们不会在子类中显示继承的方法。

在 bookboom.com 免费下载电子书

# 使用 C# 的面向对象编程

当我们在 DiscMag 对象上调用 RecNewIssue() 方法时，CLR 引擎会自动选择重写版本——调用者不需要知道这一点，也不需要知道它是否是一个重写的方法。当我们在 Magazine 对象上调用 RecNewIssue() 方法时，调用的是父类中的方法。

## 实现 DiscMag

要实现 DiscMag，我们必须创建一个 Magazine 的子类。不需要额外的实例变量或方法，尽管如果我们有构造函数，也可以创建一些。DiscMag 仅将所有参数直接传递给父类，并在 DiscMag 中定义了 RecNewIssue() 的版本以重写从 Magazine 继承的版本（见下文）。

```csharp
public class DiscMag : Magazine {
    public DiscMag(String title, double price, int orderQty, String curr) : base(title, price, orderQty, curr) {

    public override void RecNewIssue(String newIssue) {
      base.RecNewIssue(newIssue);
      Console.WriteLine("Check discs are attached");
    }
}
```注意使用 base.RecNewIssue() 调用父类的方法，正如我们在构造函数中使用那样。

为了让方法被重写，必须由父类的作者授予 virtual 关键字。

因此，为了让上面的代码工作，Magazine 中的 RecNewIssue() 方法必须标记为 virtual。

```csharp
// 在 Magazine 中
public virtual void RecNewIssue(String newIssue)
{
    Copies = orderQty;
    currIssue = newIssue;
}
```

# 使用 C# 的面向对象编程

## 继承与方法重写

这种机制允许我们在子类中重写创建的方法。

## 操作

形式上，'RecNewIssue()' 是一个操作。该操作由两个不同的方法实现，一个在 Magazine 中，另一个重写后的。这种区别是多态（polymorphism）的重要部分，我们将在第四章遇到。

## 3.10 Object 类

在 C 中，所有类都是直接或间接地作为 'Object' 类的子类。Object 是 C# 继承层次结构的根。因此每个 C# 程序中都存在。

如果一个类没有声明继承另一个类，它就会隐式地继承自 Object。

Object 定义了自己的实例变量，但有几个方法。通常这些方法会被新类重写以使其变得有用。一个例子就是 ToString() 方法。

因此，当我们定义自己的类时，默认它们是 Object 的直接子类。

如果我们的类被组织成层次结构，那么层次结构中顶部的父类是 object 的直接子类，其他所有类都是间接子类。

![](img/e143b38d00f95425fa4f3efca0527189_79_0.png)

使用 C# 的面向对象编程

继承与方法重写

因此，直接或间接地，C# 中创建的所有类都继承 Object 类定义的 ToString() 方法。

![](img/e143b38d00f95425fa4f3efca0527189_80_0.png)

## 3.11 重写 Object 中定义的 ToString()

Object 类定义了一个 ToString() 方法，它是有用方法之一。

ToString() 的签名如下
public String ToString()

ToString 方法的目的是返回一个表示当前对象的字符串值。由 Object 类定义的 ToString 版本产生类似于："Book" 的输出。这是实例化对象的类名。然而，为了通常有用，我们需要重写它以给出一个更有意义的字符串。

# 在 Publication 中

```csharp
public override String ToString()
{
    return title;
}
```

# 在 Book 中

```csharp
public override String ToString()
{
    return base.ToString() + " by " + author;
}
```

在 bookboom.com 免费下载电子书

81
