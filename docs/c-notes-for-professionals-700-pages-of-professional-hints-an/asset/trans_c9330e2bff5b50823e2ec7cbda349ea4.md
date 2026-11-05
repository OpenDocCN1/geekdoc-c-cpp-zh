
查看演示

调用基类的另一个构造函数的方式是，在构造函数签名与其主体之间放置 : base(args)：

```csharp
public class Mammal : Animal
{
    public Mammal(string name) : base(name)
    {
        Console.WriteLine(name + " is a mammal.");
    }
}
```

调用 new Mammal("George the Cat") 现在将输出：

> George the Cat 出生了。
> George the Cat 是哺乳动物。

查看演示

### 第 39.7 节：派生类的终结器

当对象图被终结时，顺序与构造顺序相反。例如，如下代码所示，超类型先于基类型被终结：

```csharp
class TheBaseClass
{
    ~TheBaseClass()
    {
        Console.WriteLine("Base class finalized!");
    }
}

class TheDerivedClass : TheBaseClass
{
    ~TheDerivedClass()
    {
        Console.WriteLine("Derived class finalized!");
    }
}

//Don't assign to a variable
//to make the object unreachable
new TheDerivedClass();

//Just to make the example work;
//this is otherwise NOT recommended!
GC.Collect();

//Derived class finalized!
//Base class finalized!
```

### 第 39.8 节：静态构造函数中的异常

如果静态构造函数抛出异常，则永远不会重试。在该 AppDomain 的生存期内，该类型不可用。对该类型的任何进一步使用都将引发一个包装了原始异常的 TypeInitializationException。

```csharp
public class Animal
{
    static Animal()
    {
        Console.WriteLine("Static ctor");
        throw new Exception();
    }

    public static void Yawn() {}
}
try
{
    Animal.Yawn();
}
catch (Exception e)
{
    Console.WriteLine(e.ToString());
}
try
{
    Animal.Yawn();
}
catch (Exception e)
{
    Console.WriteLine(e.ToString());
}
```

这将输出：

> 静态构造函数
> 
> System.TypeInitializationException: “Animal”的类型初始值设定项引发了异常。 --->
> System.Exception: 引发了“System.Exception”类型的异常。

[...]

> System.TypeInitializationException: “Animal”的类型初始值设定项引发了异常。 --->
> System.Exception: 引发了“System.Exception”类型的异常。

由此可以看到，实际的构造函数只执行了一次，而异常被重复使用。

### 第 39.9 节：构造函数与属性初始化

属性值的赋值应在类构造函数之前还是之后执行？

```csharp
public class TestClass
{
    public int TestProperty { get; set; } = 2;

    public TestClass()
    {
        if (TestProperty == 1)
        {
            Console.WriteLine("Shall this be executed?");
        }
        if (TestProperty == 2)
        {
            Console.WriteLine("Or shall this be executed");
        }
    }
}
var testInstance = new TestClass() { TestProperty = 1 };
```

在上面的示例中，TestProperty 的值在类构造函数中应为 1，还是在类构造函数之后为 1？

像这样在实例创建时分配属性值：

```csharp
var testInstance = new TestClass() { TestProperty = 1 };
```

将在构造函数运行之后执行。然而，在 C# 6.0 中像这样在类的属性中初始化属性值：

```csharp
public class TestClass
{
    public int TestProperty { get; set; } = 2;

    public TestClass()
    {
    }
}
```

将在构造函数运行之前完成。

将上述两个概念合并到一个示例中：

```csharp
public class TestClass
{
    public int TestProperty { get; set; } = 2;

    public TestClass()
    {
        if (TestProperty == 1)
        {
            Console.WriteLine("Shall this be executed?");
        }

        if (TestProperty == 2)
        {
            Console.WriteLine("Or shall this be executed");
        }
    }
}

static void Main(string[] args)
{
    var testInstance = new TestClass() { TestProperty = 1 };
    Console.WriteLine(testInstance.TestProperty); //resulting in 1
}
```

最终结果：

```
"Or shall this be executed"
"1"
```

解释：

TestProperty 的值将首先被赋值为 2，然后运行 TestClass 构造函数，从而打印出

```
"Or shall this be executed"
```

然后，由于 new TestClass() { TestProperty = 1 }，TestProperty 将被赋值为 1，使得 Console.WriteLine(testInstance.TestProperty) 打印的 TestProperty 最终值为

```
"1"
```

### 第 39.10 节：泛型静态构造函数

如果声明静态构造函数的类型是泛型，则对于每一种唯一的泛型参数组合，静态构造函数都会被调用一次。

```csharp
class Animal<T>
{
    static Animal()
    {
        Console.WriteLine(typeof(T).FullName);
    }
    public static void Yawn() { }
}
Animal<Object>.Yawn();
Animal<String>.Yawn();
```

这将输出：

System.Object
System.String

另请参阅：泛型类型的静态构造函数如何工作？

### 第 39.11 节：在构造函数中调用虚方法

与 C++ 不同，在 C# 中可以从类构造函数调用虚方法（好吧，在 C++ 中也可以，但其行为起初令人惊讶）。例如：

```csharp
abstract class Base
{
    protected Base()
    {
        _obj = CreateAnother();
    }

    protected virtual AnotherBase CreateAnother()
    {
        return new AnotherBase();
    }

    private readonly AnotherBase _obj;
}

sealed class Derived : Base
{
    public Derived() { }

    protected override AnotherBase CreateAnother()
    {
        return new AnotherDerived();
    }
}

var test = new Derived();
// test._obj is AnotherDerived
```

如果你有 C++ 背景，这会令人惊讶：基类构造函数已经能看到派生类的虚方法表！

**注意：** 派生类可能尚未完全初始化（其构造函数将在基类构造函数之后执行），并且此技术很危险（对此还有一个 StyleCop 警告）。通常这被视为不良做法。

## 第 40 章：访问修饰符

### 第 40.1 节：访问修饰符示意图

以下是维恩图中的所有访问修饰符，按限制性从强到可访问性从高排列：

| 访问修饰符 | 示意图 |
|---|---|
| private | 维恩图，Derived 和 Same Assembly 圆圈重叠，Me 位于重叠区域，private 区域高亮显示 |
| internal | 维恩图，Derived 和 Same Assembly 圆圈重叠，Me 位于重叠区域，Same Assembly 区域高亮显示 |
| protected | 维恩图，Derived 和 Same Assembly 圆圈重叠，Me 位于重叠区域，Derived 区域高亮显示 |
| protected internal | 维恩图，Derived 和 Same Assembly 圆圈重叠，Me 位于重叠区域，Derived 和 Same Assembly 区域高亮显示 |

![](img/5da9b5c72747b887ec63f57c832400bf_184_0.png)

![](img/5da9b5c72747b887ec63f57c832400bf_184_1.png)

![](img/5da9b5c72747b887ec63f57c832400bf_184_2.png)

![](img/5da9b5c72747b887ec63f57c832400bf_184_3.png)

![](img/5da9b5c72747b887ec63f57c832400bf_185_0.png)

你可以在下面找到更多信息。

### 第 40.2 节：public

public 关键字使类（包括嵌套类）、属性、方法或字段可供每个使用者访问：

```csharp
public class Foo
{
    public string SomeProperty { get; set; }

    public class Baz
    {
        public int Value { get; set; }
    }
}

public class Bar
{
    public Bar()
    {
        var myInstance = new Foo();
        var someValue = foo.SomeProperty;
        var myNestedInstance = new Foo.Baz();
        var otherValue = myNestedInstance.Value;
    }
}
```

### 第 40.3 节：private

private 关键字将属性、方法、字段和嵌套类标记为仅在类内部使用：

```csharp
public class Foo
{
    private string someProperty { get; set; }

    private class Baz
    {
        public string Value { get; set; }
    }

    public void Do()
    {
        var baz = new Baz { Value = 42 };
    }
}
```

```csharp
public class Bar
{
    public Bar()
    {
        var myInstance = new Foo();

        // Compile Error - not accessible due to private modifier
        var someValue = foo.someProperty;
        // Compile Error - not accessible due to private modifier
        var baz = new Foo.Baz();
    }
}
```

### 第 40.4 节：protected internal

`protected internal` 关键字将字段、方法、属性和嵌套类标记为可在同一程序集内或另一程序集中的派生类中使用。

> > 程序集 1

```csharp
public class Foo
{
    public string MyPublicProperty { get; set; }
    protected internal string MyProtectedInternalProperty { get; set; }

    protected internal class MyProtectedInternalNestedClass
    {
        private string blah;
        public int N { get; set; }
    }
}

public class Bar
{
    void MyMethod1()
    {
        Foo foo = new Foo();
        var myPublicProperty = foo.MyPublicProperty;
        var myProtectedInternalProperty = foo.MyProtectedInternalProperty;
        var myProtectedInternalNestedInstance =
            new Foo.MyProtectedInternalNestedClass();
    }
}
```

> > 程序集 2

```csharp
public class Baz : Foo
{
    void MyMethod1()
    {
        var myPublicProperty = MyPublicProperty;
        var myProtectedInternalProperty = MyProtectedInternalProperty;
        var thing = new MyProtectedInternalNestedClass();
    }

    void MyMethod2()
```
