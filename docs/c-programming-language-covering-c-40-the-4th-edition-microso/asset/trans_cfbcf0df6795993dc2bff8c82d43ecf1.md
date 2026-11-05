

声明为分部方法（§10.2.7）或迭代器（§10.14）的方法不能有输出参数。

输出参数通常用于产生多个返回值的方法。

> BILL WAGNER 当然，你可以创建一个结构或类来返回多个值，这样就不需要输出参数了。此外，新的 Tuple<> 泛型类可用于返回多个值。

> JON SKEET Bill 观点的一个例子可以是 .NET Framework 中的 int.TryParse。它实际上返回两个值：解析后的整数，以及一个指示操作是否成功的布尔标志。C# 中的可空值类型已经恰好提供了这种组合，因此当前的方法签名：
>
> bool TryParse(string s, out int result)
>
> 本可以改为：
>
> int? TryParse(string s)
>
> 对于类似的调用（例如 decimal.TryParse 等），情况也是如此。

例如：

```csharp
using System;
class Test { static void SplitPath(string path, out string dir, out string name) { int i = path.Length; while (i > 0) { char ch = path[i - 1]; if (ch == '/' || ch == ':') break; i--; } dir = path.Substring(0, i); name = path.Substring(i); } static void Main() { string dir, name; SplitPath("c:\\Windows\\System\\hello.txt", out dir, out name); Console.WriteLine(dir); Console.WriteLine(name); } }
```

该示例产生以下输出：

```
c:\Windows\System\
hello.txt
```

注意，`dir` 和 `name` 变量在传递给 `SplitPath` 之前可以未赋值，并且在调用之后它们被视为明确赋值。

### 10.6.1.4 参数数组

使用 `params` 修饰符声明的参数是参数数组。如果形参列表包含参数数组，则它必须是列表中的最后一个参数，并且必须是一维数组类型。例如，类型 `string[]` 和 `string[][]` 可以用作参数数组的类型，但类型 `string[,]` 不能。不能将 `params` 修饰符与 `ref` 和 `out` 修饰符组合使用。

参数数组允许在方法调用中以两种方式之一指定实参：

- 为参数数组提供的实参可以是单个表达式，该表达式可隐式转换（§6.1）为参数数组类型。在这种情况下，参数数组的行为完全类似于值参数。
- 或者，调用可以为参数数组指定零个或多个实参，其中每个实参都是可隐式转换（§6.1）为参数数组元素类型的表达式。在这种情况下，调用会创建一个长度与实参数量相对应的参数数组类型实例，使用给定的实参值初始化该数组实例的元素，并将新创建的数组实例用作实际实参。

除了允许调用中使用可变数量的实参外，参数数组完全等价于同一类型的值参数（§10.6.1.1）。

示例

```csharp
using System;

class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args)
            Console.Write(" {0}", i);
        Console.WriteLine();
    }
}
```

```csharp
static void Main() {
    int[] arr = {1, 2, 3};
    F(arr);
    F(10, 20, 30, 40);
    F();
}
```

产生以下输出：

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

对 F 的第一次调用只是将数组作为值参数传递。对 F 的第二次调用会自动创建一个包含给定元素值的四元素 int[]，并将该数组实例作为值参数传递。同样，对 F 的第三次调用会创建一个零元素 int[]，并将该实例作为值参数传递。第二次和第三次调用完全等价于编写

```
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

在执行重载决策时，带参数数组的方法可能以其正常形式或其展开形式（§7.5.3.1）适用。仅当方法的正常形式不适用，并且同一类型中尚未声明与展开形式具有相同签名的方法时，方法的展开形式才可用。

示例

```csharp
using System;

class Test
{
    static void F(params object[] a) {
        Console.WriteLine("F(object[])");
    }

    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object a0, object a1) {
        Console.WriteLine("F(object,object)");
    }

    static void Main() {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
        F(1, 2, 3, 4);
    }
}
```

产生以下输出：

```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

> **BILL WAGNER** 你创建的可能是合适方法的方法越多，给用户带来的麻烦就越多。更多的编译器歧义也会给客户端开发人员带来更多歧义。

在示例中，带参数数组的方法的两种可能的展开形式已经作为常规方法包含在类中。因此，在执行重载决策时不考虑这些展开形式，第一次和第三次方法调用会选择常规方法。当类声明带参数数组的方法时，还包含一些展开形式作为常规方法并不罕见。这样做可以避免在调用带参数数组的方法的展开形式时发生的数组实例分配。

当参数数组的类型为 object[] 时，在方法的正常形式与单个 object 参数的展开形式之间会产生潜在歧义。产生歧义的原因是 object[] 本身可隐式转换为类型 object。然而，这种歧义不会造成问题，因为如果需要，可以通过插入强制转换来解决。

示例

```csharp
using System;
class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }

    static void Main() {
        object[] a = {1, "Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```

产生以下输出：

```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

在对 F 的第一次和最后一次调用中，F 的正常形式适用，因为存在从实参类型到参数类型的隐式转换（两者都是 object[] 类型）。因此，重载决策会选择 F 的正常形式，并且实参作为常规值参数传递。在第二次和第三次调用中，F 的正常形式不适用，因为不存在从实参类型到参数类型的隐式转换（类型 object 不能隐式转换为类型 object[]）。但是，F 的展开形式适用，因此它被重载决策选中。结果，调用会创建一个单元素 object[]，并且该数组的单个元素会用给定的实参值（该值本身是对 object[] 的引用）初始化。

## 10.6.2 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法称为静态方法。当不存在 static 修饰符时，该方法称为实例方法。

静态方法不针对特定实例进行操作，在静态方法中引用 this 是编译时错误。

实例方法针对类的给定实例进行操作，并且该实例可作为 this（§7.6.7）访问。

当在形式为 *E.M* 的*成员访问*（§7.6.4）中引用方法时，如果 *M* 是静态方法，则 *E* 必须表示包含 *M* 的类型；如果 *M* 是实例方法，则 *E* 必须表示包含 *M* 的类型的实例。

静态成员和实例成员之间的差异将在 §10.3.7 中进一步讨论。

