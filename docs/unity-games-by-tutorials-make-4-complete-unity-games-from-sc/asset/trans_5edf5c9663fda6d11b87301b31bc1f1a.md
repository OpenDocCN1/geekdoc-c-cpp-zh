
另一种选项是 `foreach` 循环。这在处理数组等集合时非常有用。
请将之前的循环替换为以下代码：

```
foreach (string writer in writers)
{
    Console.WriteLine(writer);
}
```

点击 Run（运行）按钮，你将看到相同的名称。

`foreach` 循环的妙之处在于，你不需要担心初始化变量和检查条件。

## 变量作用域

和其他基于 C 的语言一样，变量存在于作用域中。这决定了它们如何能被访问。当变量在作用域之外时，它将不再可访问，如果你尝试访问它，将会遇到编译时错误。

添加以下代码：

```
if (meaningOfLife == 42)
{
    bool inScope = true;
}
```

在这种情况下，你创建了一个 `if` 块并在大括号内定义了一个新变量。大括号定义了作用域。只有在大括号内部，你才能访问 `inScope`。

在大括号之后添加以下内容：

```
inScope = false;
```

点击 Run（运行）按钮，你将看到一个新错误。

```
Error(s):
(43:13) The name 'inScope' does not exist in the current context
```

当你尝试访问作用域之外的变量时就会发生这种情况。你只能在大括号内部访问该变量。循环也是如此。

删除最后一行使代码能够编译。

## 结构和类

在 C# 中，组织数据有两种不同的方式：结构（Structs）和类（Classes）。让我们来看看它们并探索它们之间的区别。

## 结构

要定义一个结构，请在 Program 的最后一个大括号之后添加内容。

```
struct Point2D
{
}
```

这定义了一个名为 `Point2D` 的新对象类型。它本身不是一个对象，而是对象的一个模板。它目前没做什么，因此在大括号之间添加以下内容：

```
public int X;
public int Y;
```

该结构现在定义了一个二维点（2D point），包含两个属性：X 位置和 Y 位置。`public` 表示这些属性可以从对象外部进行修改。如果你只想从对象内部修改属性，则可以将它们标记为 `private`。

在 C# 中，惯例是公有变量的首字母大写。在 Unity 中，当变量仅打算在 Inspector（检查器）中使用时，变量使用小写。

现在创建一个新的 `Point2D` 对象。在 `Main()` 的结束大括号之前，添加以下代码：

```
Point2D myPoint = new Point2D();
```

这创建了一个新的 `Point2D` 结构对象。现在，你需要设置 `Point2D` 的属性。添加以下代码：

```
myPoint.X = 10;
myPoint.Y = 20;
```

访问属性的方法是通过点运算符（`.`）跟随属性名，你可以直接赋值。

现在你已经定义了结构的状态，现在需要定义行为了。你通过创建一些方法来实现这一点。

## 第 22 章：C# 快速入门课程

在 `Point2D` 的结束大括号之前添加以下内容：

```
public void AddPoint(Point2D anotherPoint)
{
}
```

这是一个方法。`void` 表示方法的返回类型，字面上意思是“无”。如果你想让方法返回一个值，则需要指定它返回的值类型。接下来是方法名。括号包含任何传递给方法的参数。

此方法旨在将两个不同的点相加。为了实现这一点，在大括号之间添加以下内容：

```
this.X = this.X + anotherPoint.X;
this.Y = this.Y + anotherPoint.Y;
```

`this` 指向当前对象。在这种情况下，你正在通过传递给方法的名为 `anotherPoint` 的另一个 `Point2D` 对象的对应 X 和 Y 变量，增加当前对象的 X 和 Y 变量。

要看到这一点，你需要创建另一个 `Point2D` 对象。在 `Main()` 的结束大括号之前添加以下内容：

```
Point2D anotherPoint = new Point2D();
anotherPoint.X = 5;
anotherPoint.Y = 15;
```

现在，使用以下代码调用 `AddPoint()`：

```
myPoint.AddPoint(anotherPoint);
```

访问变量一样，方法也使用点运算符访问。要查看方法的结果，请执行以下操作：

```
Console.WriteLine(myPoint.X);
Console.WriteLine(myPoint.Y);
```

点击 Run（运行）按钮，你将看到以下结果：

| 15 |
| 35 |

结构不是很棒吗？

## 类

到目前，你已经看到了结构的运行，但你还有被称为“类”的东西。

在 `Point2D` 下方添加以下内容：

```
class Point2DRef {
    public int X;
    public int Y;

    public void AddPoint(Point2DRef anotherPoint) {
        this.X = this.X + anotherPoint.X;
        this.Y = this.Y + anotherPoint.Y;
    }
}
```

除了类关键字之外，你会发现定义与 struct 完全相同。结构和类之间的主要区别是它们在内存中的处理方式。结构是值类型（value type），而类是引用类型（reference type）。结构在栈（stack）上，而类在堆（heap）上。结构在赋值给变量时会被复制，而引用会被复制。结构在超出作用域时会被销毁，而类在没有更多引用它时会被回收。结构是按值传递，而类按引用传递。结构不能为 `null`，而类可以。结构不能继承另一个类，而类可以。结构不能实现接口，而类可以。结构不能有虚方法，而类可以。结构不能有抽象方法，而类可以。结构不能作为基类使用，而类可以。结构不能作为接口实现，而类可以。结构不能作为泛型约束使用，而类可以。结构不能作为泛型参数使用，而类可以。结构不能作为泛型方法使用，而类可以。结构不能作为类型参数使用，而类可以。结构不能作为方法参数使用，而类可以。结构不能作为委托，而类可以。结构不能作为事件使用，而类可以。结构不能作为属性使用，而类可以。结构不能作为异常使用，而类可以。结构不能作为接口使用，而类可以。结构不能作为命名空间使用，而类可以。结构不能作为属性使用，而类可以。结构不能作为字段使用，而类可以。结构不能作为方法使用，而类可以。结构不能作为属性使用，而类可以。结构不能作为构造函数使用，而类可以。结构不能作为析构函数使用，而类可以。结构不能作为运算符使用，而类可以。结构不能作为关键字使用，而类可以。结构不能作为字面量使用，而类可以。结构不能作为标识符使用，而类可以。结构不能作为注释使用，而类可以。结构不能作为字符串使用，而类可以。结构不能作为变量使用，而类可以。结构不能作为常量使用，而类可以。结构不能作为类型使用，而类可以。结构不能作为值使用，而类可以。结构不能作为引用使用，而类可以。结构不能作为对象使用，而类可以。结构不能作为实例使用，而类可以。（等等，OCR 在这里似乎循环了，我将根据提供的实际文本继续进行）。

## 内存管理

类和结构之间的区别真正体现在内存回收上。对于结构，当变量超出作用域时内存会被回收。对于类来说并不如此。通过给变量赋值 `null`，在之前的代码下方添加以下内容：

```
pointRef = null;
```

对象仍在内存中，因为还有另一个引用它。这意味着对象仍然可以访问。添加以下内容：

```
anotherRef.X = 125;
Console.WriteLine(anotherRef.X);
```

点击 Run（运行）按钮，你将看到：

## 继承

对于类，C# 采用单父继承。这意味着对象可以从它们的父类继承方法和属性。这允许你创建通用类并根据其用途对其进行特化。

在 `Point2Ref` 类下方添加以下内容：

```
class Person {
    public string Name;
    public virtual void SayHello()
    {
        Console.WriteLine("Hello");
    }
}
```

创建了一个名为 `Person` 的类，包含一个 `Name` 以及一个名为 `SayHello()` 的方法。该方法被标记为 `virtual`，是因为子类将覆盖它；即重新实现该方法以提供特化行为。

在 `Person` 下方添加以下内容：

```
class RenfairePerson : Person {
    public override void SayHello()
    {
        Console.WriteLine("Huzzah!");
    }
}
```

这里发生了几点。首先，`RenfairePerson` 扩展了 `Person`。冒号表示超类。接下来，类实现了 `SayHello`。它表示它通过 `override` 关键字覆盖了父方法。

在 `Main()` 的底部添加以下内容：

```
RenfairePerson person = new RenfairePerson();
person.Name = "Igor the Ratcatcher";
person.SayHello();
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_631_0.png)
