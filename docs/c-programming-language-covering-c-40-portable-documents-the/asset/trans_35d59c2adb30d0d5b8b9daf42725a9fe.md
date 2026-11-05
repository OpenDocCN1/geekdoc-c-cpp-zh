
前两个实例构造函数仅为缺失的参数提供默认值。两者都使用 `this(...)` 构造函数初始值设定项来调用第三个实例构造函数，后者实际执行初始化新实例的工作。其效果等同于可选的构造函数参数：

```
Text t1 = new Text();            // Same as Text(5, 0, null)
Text t2 = new Text(5, 10);       // Same as Text(5, 10, null)
Text t3 = new Text(5, 20, "Hello");
```

## 10.12 静态构造函数

一个 *静态构造函数* 是实现初始化封闭类类型所需操作的成员。静态构造函数使用 *静态构造函数声明* 声明：

```
static-constructor-declaration:
    attributes? static-constructor-modifiers identifier ( ) static-constructor-body

static-constructor-modifiers:
    extern? static
    static extern?

static-constructor-body:
    block
    ;
```

一个 *静态构造函数声明* 可以包含一组属性 (§17) 和一个 extern 修饰符 (§10.6.7)。

*静态构造函数声明* 的标识符必须命名声明静态构造函数的类。如果指定了其他名称，则会发生编译时错误。

当静态构造函数声明包含 extern 修饰符时，该静态构造函数被称为 *外部静态构造函数*。由于外部静态构造函数声明不提供实际实现，其 *静态构造函数体* 由分号组成。对于所有其他静态构造函数声明，*静态构造函数体* 由一个块组成，该块指定用于初始化类的语句要执行的语句。这与返回类型为 void 的静态方法的 *方法体* 完全对应 (§10.6.10)。

静态构造函数不会被继承，也不能直接调用。

封闭类类型的静态构造函数在给定的应用程序域中最多执行一次。静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 创建了该类类型的实例。
- 引用了该类类型的任何静态成员。

> JON SKEET 空静态构造函数的存在非常可能影响代码的行为，因为它可以改变静态字段初始值设定项执行的时机。如果你选择利用这种行为，我强烈建议你至少在静态构造函数中包含一条注释，解释为什么以及如何依赖其存在，以避免日后被急于求成的维护者移除。

如果一个类包含执行开始的 Main 方法 (§3.1)，则该类的静态构造函数在调用 Main 方法之前执行。

为了初始化新的封闭类类型，首先为该特定封闭类型创建一组新的静态字段 (§10.5.1)。每个静态字段都初始化为其默认值 (§5.2)。接下来，为这些静态字段执行静态字段初始值设定项 (§10.4.5.1)。最后，执行静态构造函数。

### 示例

```
using System;
class Test
{
    static void Main()
    {
        A.F();
        B.F();
    }
}
class A
{
    static A()
    {
        Console.WriteLine("Init A");
    }
    public static void F()
    {
        Console.WriteLine("A.F");
    }
}
class B
{
    static B()
    {
        Console.WriteLine("Init B");
    }
}
public static void F()
{
    Console.WriteLine("B.F");
}
```

必须产生输出

```
Init A
A.F
Init B
B.F
```

因为 A 的静态构造函数的执行由对 A.F 的调用触发，而 B 的静态构造函数的执行由对 B.F 的调用触发。

可以构造循环依赖，使得具有变量初始值设定项的静态字段在其默认值状态下被观察到。

### 示例

```
using System;

class A
{
    public static int X;
    static A()
    {
        X = B.Y + 1;
    }
}

class B
{
    public static int Y = A.X + 1;
    static B() { }
    static void Main()
    {
        Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
    }
}
```

产生以下输出：

```
X = 1, Y = 2
```

为了执行 Main 方法，系统首先在类 B 的静态构造函数之前运行 B.Y 的初始值设定项。Y 的初始值设定项导致 A 的静态构造函数被运行，因为引用了 A.X 的值。A 的静态构造函数随后继续计算 X 的值，在此过程中获取 Y 的默认值，即零。因此 A.X 被初始化为 1。运行 A 的静态字段初始值设定项和静态构造函数的过程随后完成，返回到 Y 初始值的计算，其结果变为 2。

由于静态构造函数对每个封闭构造类类型恰好执行一次，因此它是强制执行在编译时无法通过约束 (§10.1.5) 检查的类型参数运行时检查的方便位置。例如，以下类型使用静态构造函数来强制类型参数为枚举：

```
class Gen<T> where T : struct
{
    static Gen()
    {
        if (typeof(T).IsEnum)
        {
            throw new ArgumentException("T must be an enum");
        }
    }
}
```

## 10.13 析构函数

析构函数是实现销毁类实例所需操作的成员。析构函数使用 *析构函数声明* 声明：

```
destructor-declaration:
    attributes_opt extern_opt ~ identifier ( ) destructor-body

destructor-body:
    block
    ;
```

*析构函数声明* 可以包含一组属性 (§17)。

*析构函数声明* 的标识符必须命名声明析构函数的类。如果指定了其他名称，则会发生编译时错误。

当析构函数声明包含 extern 修饰符时，该析构函数被称为外部析构函数。由于外部析构函数声明不提供实际实现，其 destructor-body 由分号组成。对于所有其他析构函数，destructor-body 由一个块组成，该块指定用于销毁类实例的语句要执行的语句。destructor-body 与返回类型为 void 的实例方法的 *方法体* 完全对应 (§10.6.10)。

析构函数不会被继承。因此，一个类没有除其自身声明的析构函数之外的其他析构函数。

由于析构函数要求没有参数，因此它不能被重载，所以一个类最多只能有一个析构函数。

析构函数会自动调用，不能显式调用。当不再可能有任何代码使用该实例时，实例变得有资格被销毁。实例有资格被销毁后，其析构函数的执行可能在任何时间发生。当一个实例被销毁时，该实例继承链中的析构函数会按顺序调用，从最派生到最不派生。析构函数可能在任何线程上执行。有关管理析构函数何时以及如何执行的规则的进一步讨论，请参阅 §3.9。

> ERIC LIPPERT 显然，在析构函数中运行的代码与程序中其他任何地方的代码运行的环境可能非常不同。在析构函数中做任何复杂、危险、产生副作用或冗长的操作都是一个非常糟糕的主意。特别是，以下代码会产生向控制台写入的复杂副作用，仅用于教学目的，并不是你在实际析构函数中应该做的事情的例子。

### 示例

```
using System;
class A
{
    ~A()
    {
        Console.WriteLine("A's destructor");
    }
}
class B : A
{
    ~B()
    {
        Console.WriteLine("B's destructor");
    }
}
class Test
{
    static void Main()
    {
        B b = new B();
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

产生输出

B's destructor
A's destructor

因为继承链中的析构函数按顺序调用，从最派生到最不派生。

> ERIC LIPPERT 传统上，“析构函数”一词指的是确定性的清理方法，而“终结器”指的是由垃圾收集器调用的非确定性清理方法。“析构函数”在 C# 中有点不幸的误称；理想情况下，这些方法应称为“终结器”，而 IDisposable 的 Dispose 方法应称为“析构函数”。

析构函数通过重写 System.Object 上的虚方法 Finalize 来实现。C# 程序不允许重写此方法或直接调用它（或它的重写）。例如，程序

```
class A
{
    override protected void Finalize() { }    // Error
    public void F()
    {
        this.Finalize();    // Error
    }
}
```

包含两个错误。

编译器表现得好像此方法及其重写根本不存在。因此程序

```
class A
{
    void Finalize() { }    // Permitted
}
```

是有效的，并且所示方法隐藏了 System.Object 的 Finalize 方法。

有关从析构函数抛出异常时的行为讨论，请参阅 §16.3。
