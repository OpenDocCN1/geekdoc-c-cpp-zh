
> **埃里克·利珀特**  
> 如果你需要一个二元组、三元组等等，CLR 4 版框架中定义的泛型“元组”类型是很方便的类型。

当使用泛型类时，必须为每个类型参数提供类型实参：

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;   // TFirst is int
string s = pair.Second; // TSecond is string
```

像上面的 Pair<int,string> 这样提供了类型实参的泛型类型称为构造类型。

## 1.6.4 基类

类声明可以通过在类名和类型参数之后加上冒号和基类的名称来指定基类。省略基类指定与从类型 object 派生相同。在下面的示例中，Point3D 的基类是 Point，Point 的基类是 object：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

public class Point3D : Point
{
    public int z;
    public Point3D(int x, int y, int z): base(x, y)
    {
        this.z = z;
    }
}
```

类继承其基类的成员。继承意味着一个类隐式包含其基类的所有成员，但基类的实例构造函数、静态构造函数和析构函数除外。派生类可以向其继承的成员中添加新成员，但不能移除已继承成员的定义。在前面的示例中，Point3D 从 Point 继承 x 和 y 字段，每个 Point3D 实例都包含 x、y 和 z 三个字段。

> **杰西·利伯蒂**  
> 对于 C# 来说，没有什么比继承和多态更重要的概念需要理解了。这些概念是这门语言的核心，也是面向对象编程的灵魂。请阅读本节直到理解为止，或者寻求帮助，或用额外阅读来补充，但不要跳过它——这些内容是 C# 不可或缺的要素。

存在从类类型到其任何基类类型的隐式转换。因此，类类型的变量可以引用该类的实例或任何派生类的实例。例如，给定前面的类声明，Point 类型的变量既可以引用 Point，也可以引用 Point3D：

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

## 1.6.5 字段

字段是与类或类的实例关联的变量。

用 static 修饰符声明的字段定义*静态字段*。静态字段恰好标识一个存储位置。无论创建多少个类的实例，静态字段始终只有一份副本。

> **埃里克·利珀特**  
> 对于泛型类型，静态字段是按构造类型区分的。也就是说，如果你有
>
>     class Stack<T> {
>         public readonly static Stack<T> empty = whatever; ...
>     }
>
> 那么 Stack<int>.empty 与 Stack<string>.empty 是不同的字段。

不使用 static 修饰符声明的字段定义*实例字段*。类的每个实例都包含该类所有实例字段的单独副本。

在下面的示例中，Color 类的每个实例都有 r、g、b 实例字段的单独副本，但 Black、White、Red、Green 和 Blue 静态字段只有一份副本：

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte r, g, b;

    public Color(byte r, byte g, byte b)
    {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```

如前面的示例所示，*只读字段*可以用 readonly 修饰符声明。对 readonly 字段的赋值只能作为字段声明的一部分，或在同一个类的构造函数中进行。

> **布拉德·艾布拉姆斯**  
> readonly 保护字段的位置在类型构造函数之外不被更改，但不保护该位置上的值。例如，考虑以下类型：
>
> ```csharp
> public class Names
> {
>     public static readonly StringBuilder FirstBorn = new StringBuilder("Joe");
>     public static readonly StringBuilder SecondBorn = new StringBuilder("Sue");
> }
> ```
>
> 在构造函数之外，直接更改 FirstBorn 实例会导致编译器错误：
>
> ```csharp
> Names.FirstBorn = new StringBuilder("Biff");
> // Compile error
> ```
>
> 但是，我可以通过修改 StringBuilder 实例来实现完全相同的结果：
>
> ```csharp
> Names.FirstBorn.Remove(0,6).Append("Biff");
> Console.WriteLine(Names.FirstBorn);    // Outputs "Biff"
> ```
>
> 正是由于这个原因，我们强烈建议将只读字段限制为不可变类型。不可变类型没有任何公开暴露的 setter，例如 int、double 或 String。

> **比尔·瓦格纳**  
> 几种著名的设计模式利用了可变类型的只读字段。适配器（Adapter）、装饰器（Decorator）、外观（Façade）和代理（Proxy）模式是最明显的例子。当你通过组合较小的结构来创建较大的结构时，你经常会使用只读字段来表示这些较小结构的实例。可变类型的只读字段应表明正在使用这些结构模式之一。

## 1.6.6 方法

方法是一个成员，它实现可由对象或类执行的计算或操作。静态方法通过类访问。实例方法通过类的实例访问。

方法有一个（可能为空的）参数列表，这些参数表示传递给方法的值或变量引用；方法还有一个返回类型，它指定方法计算并返回的值的类型。如果方法不返回值，则其返回类型为 void。

与类型一样，方法也可以有一组类型参数；调用方法时，必须为这些类型参数指定类型实参。与类型不同，类型实参通常可以从方法调用的实参中推断出来，而不必显式给出。

方法的签名在其声明所在的类中必须唯一。方法的签名由方法名称、类型参数数目，以及参数数目、修饰符和类型组成。方法的签名不包括返回类型。

> **埃里克·利珀特**  
> 泛型类型的一个不幸后果是，构造类型可能有两个签名完全相同的方法。例如，class C<T> { void M(T t){} void M(int t){} ...} 完全合法，但 C<int> 有两个签名完全相同的 M 方法。正如我们稍后将看到的，这种可能性会导致一些涉及重载决策和显式接口实现的有趣场景。一条好的指导原则是：不要创建会以这种方式在构造时产生歧义的泛型类型；这样的类型极其令人困惑，并可能产生意外行为。

### 1.6.6.1 参数

参数用于将值或变量引用传递给方法。方法的参数从调用方法时指定的实参获取实际值。参数有四种：值参数、引用参数、输出参数和参数数组。

值参数用于输入参数传递。值参数对应于一个局部变量，该局部变量从为该参数传递的实参获取初始值。对值参数的修改不会影响为该参数传递的实参。

> **比尔·瓦格纳**  
> “对值参数的修改不会影响实参”这一说法可能会造成误解，因为变更器方法可能会更改引用类型参数的内容。值参数本身不会改变，但所引用对象的内容会改变。

值参数可以是可选的，方法是指定默认值，以便可以省略相应的实参。

引用参数用于输入和输出参数传递。为引用参数传递的实参必须是变量，并且在方法执行期间，引用参数表示与实参变量相同的存储位置。引用参数用 ref 修饰符声明。下面的示例展示了 ref 参数的用法。

```csharp
using System;
class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }

    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("{0} {1}", i, j); // Outputs "2 1"
    }
}
```

