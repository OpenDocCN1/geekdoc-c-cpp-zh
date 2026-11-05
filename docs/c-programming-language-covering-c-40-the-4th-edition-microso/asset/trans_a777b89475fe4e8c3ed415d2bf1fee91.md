
> **埃里克·利珀特** 这种语法应有助于消除两个都称为“按引用传递”的事物之间的混淆。在 C# 中，引用类型之所以被称为这个名字，是因为它们是“按引用传递”的；你将一个对象实例传递给方法，方法获得对该对象实例的引用。其他一些代码也可能持有对同一对象的引用。

> 引用参数是“按引用传递”的一种略有不同的形式。在这种情况下，引用指向变量本身，而不是某个对象实例。如果该变量恰好包含值类型（如前面的示例所示），那完全合法。按引用传递的不是值，而是保存该值的变量。

> 理解引用参数的一个好方法是：引用参数成为作为实参传递的变量的别名。在前面的示例中，x 和 z 本质上是同一个变量。它们指向同一个存储位置。

*输出参数*用于输出参数传递。输出参数与引用参数类似，不同之处在于调用方提供的实参的初始值无关紧要。输出参数使用 out 修饰符声明。下面的示例展示了 out 参数的用法。

```
using System;
class Test
{
    static void Divide(int x, int y, out int result, out int remainder) {
        result = x / y;
        remainder = x % y;
    }
    static void Main() {
        int res, rem;
        Divide(10, 3, out res, out rem);
        Console.WriteLine("{0} {1}", res, rem);    // Outputs "3 1"
    }
}
```

> **埃里克·利珀特** CLR 直接只支持 ref 参数。out 参数在元数据中表示为带有特殊特性的 ref 参数，该特性向 C# 编译器表明此 ref 参数应被视为 out 参数。这解释了为什么不能有两个仅在“out/ref 性”上不同的方法；从 CLR 的角度来看，它们将是两个完全相同的方法。

*参数数组*允许将可变数量的实参传递给方法。参数数组使用 `params` 修饰符声明。只有方法的最后一个参数可以是参数数组，并且参数数组的类型必须是一维数组类型。`System.Console` 类的 `Write` 和 `WriteLine` 方法是参数数组用法的良好示例。它们的声明如下。

```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```

在使用参数数组的方法内部，参数数组的行为完全像数组类型的常规参数。然而，在调用带有参数数组的方法时，既可以传递参数数组类型的单个实参，也可以传递任意数量的参数数组元素类型的实参。在后一种情况下，会自动创建一个数组实例，并用给定的实参初始化它。这个示例

```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```

等价于编写以下代码。

```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

> > **布拉德·艾布拉姆斯** 你可能会注意到 `params` 与 C 编程语言中的 `varargs` 概念之间的相似性。为了保持让 C# 非常易于理解的目标，`params` 修饰符不需要特殊的调用约定或特殊的库支持。因此，事实证明它比 `varargs` 更不容易出错。
> >
> > 但请注意，C# 模型确实会在每次调用时隐式地创建一个额外的对象分配（即包含参数的数组）。这很少成为问题，但在内循环类型的场景中，它可能会变得低效，我们建议为主流情况提供重载，并仅对边缘情况使用 `params` 重载。一个例子是 `StringBuilder.AppendFormat()` 系列重载：

```csharp
public static StringBuilder AppendFormat(string format, object arg0);
public static StringBuilder AppendFormat(string format, object arg0, object arg1);
public static StringBuilder AppendFormat(string format, object arg0, object arg1, object arg2);
public static StringBuilder AppendFormat(string format, params object[] args);
```

**克里斯·塞尔斯** params 实际上只是一个可选快捷方式，这一事实的一个良好副作用是，我不必编写像下面这样疯狂的东西：

```csharp
static object[] GetArgs() { ... }

static void Main() {
    object[] args = GetArgs();
    object x = args[0];
    object y = args[1];
    object z = args[2];
    Console.WriteLine("x={0} y={1} z={2}", x, y, z);
}
```

在这里，我调用方法并把参数拆出来，只是为了编译器能再次在它们周围创建一个数组。当然，我其实应该只这样写：

```csharp
static object[] GetArgs() { ... }

static void Main() {
    Console.WriteLine("x={0} y={1} z={2}", GetArgs());
}
```

然而，如今在 .NET 中，返回数组的方法越来越少，因为大多数人更喜欢使用 IEnumerable<T> 的灵活性。这意味着你可能要编写如下代码：

```csharp
static IEnumerable<object> GetArgs() { ... }

static void Main() {
    Console.WriteLine("x={0} y={1} z={2}", GetArgs().ToArray());
}
```

如果 params 能直接“理解” IEnumerable，那会很方便。也许下次吧。

## 1.6.6.2 方法体和局部变量

方法体指定调用方法时要执行的语句。

方法体可以声明特定于该方法调用的变量。此类变量称为局部变量。局部变量声明指定类型名、变量名，并可能指定初始值。下面的示例声明一个初始值为零的局部变量 i 和一个没有初始值的局部变量 j。

![](img/04b421b044b1254de966ab5335775a89_50_0.png)

```csharp
using System;
class Squares
{
    static void Main() {
        int i = 0;
        int j;
        while (i < 10) {
            j = i * i;
            Console.WriteLine("{0} x {0} = {1}", i, j);
            i = i + 1;
        }
    }
}
```

C# 要求局部变量在获取其值之前必须被*明确赋值*。例如，如果前面 `i` 的声明没有包含初始值，编译器会对后续使用 `i` 的地方报告错误，因为在程序中的那些位置它没有被明确赋值。

方法可以使用 return 语句将控制权返回给调用方。在返回 `void` 的方法中，return 语句不能指定表达式。在返回非 void 的方法中，return 语句必须包含计算返回值的表达式。

## 1.6.6.3 *静态方法和实例方法*

使用 static 修饰符声明的方法是*静态方法*。静态方法不作用于特定实例，并且只能直接访问静态成员。

> > **埃里克·利珀特** 当然，如果静态方法碰巧手边有一个实例，那么它访问实例成员是完全合法的。

不使用 static 修饰符声明的方法是*实例方法*。实例方法作用于特定实例，并且可以访问静态成员和实例成员。调用实例方法时所针对的实例可以通过 `this` 显式访问。在静态方法中引用 `this` 是错误的。

下面的 Entity 类同时具有静态成员和实例成员。

```csharp
class Entity
{
    static int nextSerialNo;
    int serialNo;
    public Entity()
    {
    serialNo = nextSerialNo++;
    }
    public int GetSerialNo()
    {
        return serialNo;
    }
    public static int GetNextSerialNo()
    {
        return nextSerialNo;
    }
    public static void SetNextSerialNo(int value)
    {
        nextSerialNo = value;
    }
}
```

每个 Entity 实例都包含一个序列号（并且大概还包含此处未显示的其他一些信息）。Entity 构造函数（类似于实例方法）用下一个可用的序列号初始化新实例。由于构造函数是实例成员，因此允许它访问 serialNo 实例字段和 nextSerialNo 静态字段。

GetNextSerialNo 和 SetNextSerialNo 静态方法可以访问 nextSerialNo 静态字段，但它们直接访问 serialNo 实例字段会出错。

下面的示例展示了 Entity 类的用法。

```csharp
using System;
class Test
{
    static void Main() {
        Entity.SetNextSerialNo(1000);

        Entity e1 = new Entity();
        Entity e2 = new Entity();

        Console.WriteLine(e1.GetSerialNo());          // Outputs "1000"
        Console.WriteLine(e2.GetSerialNo());          // Outputs "1001"
        Console.WriteLine(Entity.GetNextSerialNo());  // Outputs "1002"
    }
}
```

请注意，SetNextSerialNo 和 GetNextSerialNo 静态方法是在类上调用的，而 GetSerialNo 实例方法是在类的实例上调用的。

