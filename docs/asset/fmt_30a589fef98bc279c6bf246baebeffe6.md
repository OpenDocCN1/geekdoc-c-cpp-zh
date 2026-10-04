
只有当我们使用的对象（即`MyA`引用的对象）确实是一个`MyClassB`类型的对象时，这段代码才有效。如果不是，我们就是在尝试调用一个不存在的方法，结果会导致运行时错误。

你可以发现上转型并不是类型安全的，因为你无法轻松判断被转换的是否正确的类型。例如：

```csharp
Random R = new Random();
MyClassB myObject;
if (R.NextDouble() > 0.5)
{
    myObject = new MyClassB();
}
else
{
    myObject = (MyClassB) new MyClassA();
}
Console.WriteLine(myObject.property);
```

此程序没有产生编译错误或警告，但在 50% 的情况下，它会因为尝试将`MyClassA`类型对象转换为`MyClassB`类型而失败。在这种情况下，随机输入代表了真实程序由外部其他部分注入到程序中的可变性。

## is 和 as

有两个运算符可以帮助避免转换时的运行时异常。该运算符可以用于在应用转换之前测试引用的类型。例如：

```csharp
if (MyAnything is MyClassB)
{
    MyClassB MyB = (MyClassB)MyAnything;
};
```

这是`is`的基本形式，作为类型检查，它还可以测试更通用的模式——请参见第 2 章中的模式匹配（Pattern Matching）。

`as`运算符是编写转换的另一种方法，区别在于如果转换失败，引用将为`null`。例如：

`MyClassB MyB = Anything as MyClassB;`

这不会抛出异常，但你必须确保不会因为转换未没有而最终使用了`null`引用。

注意你可以使用它来整洁地编写转换方法调用：

`(Anything as ClassB).MethodB()`

但如果转换失败且`MethodB`不存在，你将产生运行时错误。为了避免这种情况，你可以使用空条件操作符：

`(Anything as ClassB)?.MethodB()`

现在，如果方法调用失败，结果就是`null`。

始终使用`as`代替显式转换。

## 重写与抽象类

继承因为方法可以被重写而变得复杂。也就是说你不仅可以为派生类添加完全新的方法和属性，还可以定义替换继承方法的方法。

在某种意义上，重写方法正是问题开始出现——或至少变得复杂的地方。如果面向对象代码的目的是代码复用，为什么要继承代码并将其重写为不同的内容呢？在极端情况下，你可以重写继承的每一个方法——这对代码复用意味着什么？

如果你认为重写每个方法是不可能的，你需要记住，抽象类可以包含没有实现细节且必须被重写的方法定义。由于抽象类的定义是不完全的，你无法创建该类的实例——它纯粹是为了继承而存在的。例如：

```csharp
abstract class MyClassA {

  abstract public void myMethod1();

  public void myMethod2()
  {
    Console.WriteLine("implemented");
  }
}
```

在这种情况下，你可以看到有两个方法：`myMethod1`是抽象的且没有实现，而`myMethod2`则有。

当你将`MyClassA`作为基类时，你必须重写`methodName`以提供实现：

```csharp
class MyClassB : MyClassA {
    public override void methodName()
    {
        throw new NotImplementedException();
    }
}
```

如所示的方法是由 Visual Studio 自动生成的，这很有帮助，但你仍然需要完成实现抽象方法的工作。那么抽象类到底是什么的？

显然，一个类可以是 100% 抽象的，它并不关乎代码复用，更多是关于定义让派生类遵循的契约。抽象类确保任何派生自它的类都具有某些方法，即使实现被留给子类处理。

## 重写 – 虚与晚绑定

初看之下，重写方法似乎简单直接。然而，存在一些复杂性，C# 提供的机制允许你处理这些复杂性。特别是它同时提供了晚绑定（Late Binding）和早期绑定（Early Binding）。在本节中，我们查看晚绑定。

如果你有一个继承自基类的类，且被继承的方法没有完成所需的工作，请用新方法重写它。但等一下，可能会出什么问题呢？

首先要注意，如果你将派生类作为另一个类的基类，使用的是新方法而不是基类方法。也就是说，一旦方法在某个类中被重写，该版本就会传递给其他类——它替换了基类方法。这有时是你需要的，有时又不是。唯一的解决方案是再次重写方法以获得你想要的行为。可以使用`base.myMethod()`调用直接基类中的方法，但无法使用类似`base.myMethod()`的表达式来调用更早基类的方法。

重写最大的复杂性在于如何处理转换。如前所述，我们可以使用基类型变量来引用派生类型对象——即向下转换。如果继承的方法被重写，这会导致对调用哪种方法产生歧义。

例如，我们在前面的章节中见过，如果`MyClass`继承了`MyClass`的`myMethod`并重写了它：

```csharp
MyClass MyA;
MyClass MyB;
MyB = new MyClass();
MyA = MyB;
MyA.myMethod();
```

使用的是哪个版本的`myMethod`？

初级程序员期望获得`MyB`的`myMethod`版本，即新版本以及属于所用实例的版本，但他们是错误的。默认情况下，你得到`MyA`的`myMethod`版本，即引用变量的类型决定了实际调用哪个版本的方法。

正如第 11 章详细解释的，这是一个早期绑定的例子，即调用方法在编译时确定，并且必须由变量的类型决定，而不是运行时变量引用的对象的类型决定。

如果你想使用显然更合理的晚期绑定（late binding），使得所调用的方法取决于运行时引用的对象的类型，你必须使用`virtual`关键字显式地请求它。例如：

```csharp
class MyClassA
{
    public virtual void myWeb()
    {
        Console.WriteLine("implemented A");
    }
}
```

现在，当`MyClassB`继承自`MyClassA`时，它可以以通常的方式重写方法：

```csharp
class MyClassB:MyClassA
{
    public override void myWeb()
    {
        Console.WriteLine("implemented B");
    }
}
```

注意新的修饰符是`override`。这两个关键字像括号一样协同工作。现有的方法必须声明为`virtual`，而新方法必须声明为`override`。漏掉其中任何一个声明都将产生编译器警告。如果你运行程序，漏掉`virtual`但使用`override`将产生运行时错误。漏掉`override`而反之使用`virtual`则会产生早期绑定（early binding）。

在有了`virtual`和`override`的情况下，示例：

```csharp
MyClass MyA;
MyClassB MyB;
MyB=new MyClassB();
MyA=MyB;
MyA.myMethod();
```

产生消息`implemented B`，因为调用的是`MyClassB`的方法，而不是`implemented A`。

准确地说，漏掉它还会得到另一个编译器警告。要使用早期绑定重写方法，你必须使用`new`关键字，这将在下一节中描述。

注意，无论运行哪个方法，它都是在其定义类的上下文中运行的。这意味着，如果`myMethod`指向属性或方法，那么这些是在方法所在的类（无论是`MyClassA`还是`MyClassB`）中定义的。因此，如果`MyClassB`类中的`webWeb`引用了`MyClassA`类中的的属性，当使用`MyClassA`引用运行时，它将访问`MyClassB`中的该属性，即就像它在`MyClassA`中一样。你不能直接引用该属性，但方法可以访问它。

例如，如果我们更改`MyClassB`的定义为：

```csharp
public class MyClassB : MyClassA
{
    public int myProperty=42;
    public override int myMethod()
    {
        Console.WriteLine("MyMethod "+myProperty.ToString());
        return 2;
    }
}
```

你可以看到，重写的`myMethod`现在访问了一个仅存在于`MyClassB`中的字段。如果你运行：

`MyClassA MyA = new MyClassB();`

`MyA.myMethod();`

如果你尝试直接访问该属性，将看到打印出 42：

`MyA.myProperty=43;`

你将看到编译时错误，因为`MyClassA`没有`myProperty`。

## 使用 New 隐藏方法

如果你不将方法声明为`virtual`，那么使用早期绑定进行重写并不像 C++ 和其他语言中那样简单。C# 并没有真正的默认的重写方法。你只需要漏掉任何额外的关键字并在派生类中重新定义该方法，但如果你这样做，将会得到一个编译器警告。它可以运行，但这不是完成该任务的正确方法。

也就是说，如果你这样声明一个类和方法：

```csharp
class MyClassA
{
    public void myMethod()
    {
        Console.WriteLine("implemented A");
    }
}
```

现在，当`MyClassB`继承自`MyClassA`时，它可以以通常的方式重写方法：

```csharp
class MyClassB:MyClassA
{
    public void myMethod()
    {
        Console.WriteLine("implemented B");
    }
}
```

这是可行的并导致早期绑定，这在其他语言中是重写方法的默认方式，但它会生成警告。

原因在于 C# 期望你在重新定义一个继承的函数时使用`new`关键字：

```csharp
class MyClassB:MyClassA
{
    public new void myMethod()
    {
        Console.WriteLine("implemented B");
    }
}
```

注意，无论运行哪个方法，它都是在其定义类的上下文中运行。这意味着，如果`myMethod`指向属性或方法，那么这些是在方法所在的类（无论是`MyClassA`还是`MyClassB`）中定义的。因此，如果`MyClassB`类中的`webWeb`引用了`MyClassA`类中不存在的属性，当使用`MyClassA`引用运行时，它将访问`MyClassB`中的该属性，即就像它在`MyClassA`中一样。你不能直接引用该属性，但方法可以访问它。

例如，如果我们更改`MyClassB`的定义为：

```csharp
public class MyClassB : MyClassA
{
    public int myProperty=42;
    public override int myMethod()
    {
        Console.WriteLine("MyMethod "+myProperty.ToString());
        return 2;
    }
}
```

你可以看到，重写的`myMethod`现在访问了一个仅存在于`MyClassB`中的字段。如果你运行：

`MyClassA MyA = new MyClassB();`

`MyA.myMethod();`

如果你尝试直接访问该属性，将看到打印出 42：

`MyA.myProperty=43;`

你将看到编译时错误，因为`MyClassA`没有`myProperty`。

## 隐藏方法与 New

如果你不将方法声明为`virtual`，使用早期绑定进行重写并不像 C++ 和其他语言中那样简单。C# 并没有真正的默认的重写方法。你只需要漏掉任何额外的关键字并在派生类中重新定义该方法，但如果你这样做，将会得到一个编译器警告。它可以运行，但这不是完成该任务的正确方法。

也就是说，如果你这样声明一个类和方法：

```csharp
class MyClassA
{
    public void myMethod()
    {
        Console.WriteLine("implemented A");
    }
}
```

现在，当`MyClassB`继承自`MyClassA`时，它可以以通常的方式重写方法：

```csharp
class MyClassB:MyClassA
{
    public void myMethod()
    {
        Console.WriteLine("implemented B");
    }
}
```

这是可行的并导致早期绑定，这在其他语言中是重写方法的默认方式，但它会生成警告。

原因在于 C# 期望你在重新定义一个继承的函数时使用`new`关键字：

```csharp
class MyClassB:MyClassA
{
    public new void myMethod()
    {
        Console.WriteLine("implemented B");
    }
}
```

注意，无论运行哪个方法，它都是在其定义类的上下文中运行。这意味着，如果`myMethod`指向属性或方法，那么这些是在方法所在的类（无论是`MyClassA`还是`MyClassB`）中定义的。因此，如果`MyClassB`类中的`webWeb`引用了`MyClassA`类中不存在的属性，当使用`MyClassA`引用运行时，它将访问`MyClassB`中的该属性，即就像它在`MyClassA`中一样。你不能直接引用该属性，但方法可以访问它。

例如，如果我们更改`MyClassB`的定义为：

```csharp
public class MyClassB : MyClassA
{
    public int myProperty=42;
    public override int myMethod()
    {
        Console.WriteLine("MyMethod "+myProperty.ToString());
        return 2;
    }
}
```

你可以看到，重写的`myMethod`现在访问了一个仅存在于`MyClassB`中的字段。如果你运行：

`MyClassA MyA = new MyClassB();`

`MyA.myMethod();`

如果你尝试直接访问该属性，将看到打印出 42：

`MyA.myProperty=43;`

你将看到编译时错误，因为`MyClassA`没有`myProperty`。

## Hiding Methods With New

如果你不将方法声明为`virtual`，使用早期绑定进行重写并不像 C++ 和其他语言中那样简单。C# 并没有真正的默认的重写方法。你只需要漏掉任何额外的关键字并在派生类中重新定义该方法，但如果你这样做，将会得到一个编译器警告。它可以运行，但这不是完成该任务的正确方法。

也就是说，如果你这样声明一个类和方法：

```csharp
class MyClassA
{
    public void myMethod()
    {
        Console.WriteLine("implemented A");
    }
}
```

现在，当`MyClassB`继承自`MyClassA`时，它可以以通常的方式重写方法：

```csharp
class MyClassB:MyClassA
{
    public void myMethod()
    {
        Console.WriteLine("implemented B");
    }
}
```

这是可行的并导致早期绑定，这在其他语言中是重写方法的默认方式，但它会生成警告。

原因在于 C# 期望你在重新定义一个继承的函数时使用`new`关键字：

```csharp
class MyClassB:MyClassA
{
    public new void myMethod()
    {
        Console.WriteLine("implemented B");
    }
}
```

注意，无论运行哪个方法，它都是在其定义类的上下文中运行。这意味着，如果`myMethod`指向属性或方法，那么这些是在方法所在的类（无论是`MyClassA`还是`MyClassB`）中定义的。因此，如果`MyClassB`类中的`webWeb`引用了`MyClassA`类中不存在的属性，当使用`MyClassA`引用运行时，它将访问`MyClassB`中的该属性，即就像它在`MyClassA`中一样。你不能直接引用该属性，但方法可以访问它。

例如，如果我们更改`MyClassB`的定义为：

```csharp
public class MyClassB : MyClassA
{
    public int myProperty=42;
    public override int myMethod()
    {
        Console.WriteLine("MyMethod "+myProperty.ToString());
        return 2;
    }
}
```
