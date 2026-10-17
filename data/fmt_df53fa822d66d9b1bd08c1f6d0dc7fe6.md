
动态语言编译器实现在 DLR 之上并生成语法树，该树由 DLR 库使用。DLR 为 CLR 的服务类似于表达式树、调用缓存和 DOI。表达式树用于表示语言语义。这些树帮助绑定器（`binders`）封装语言语义，并定义在调用中执行的操作。调用站点（`call site`）是代码对动态对象进行数学和逻辑操作（如 `x=y` 或 `a.b(i)`）的特定区域。

图 7.2 显示了 DLR 的架构：

| IronRuby | IronPython | C# | Visual Basic | Microsoft .NET Framework |
| :--- | :--- | :--- | :--- | :--- |
| | 动态语言运行时 | Microsoft Silverlight | | |
| | 表达式树 | 调用缓存 | 动态对象互操作 | Microsoft Office |

图 7.2：DLR 架构

- DLR 为 CLR 提供的服务用于支持动态语言。这些服务包括：
- 表达式树——表达式树是随着集成查询 (`LINQ`) 的引入而引入的。任何用户代码首先被转换为表达式树，然后这些树被转换为中间语言 (`IL`)。表达式树通过通过自己分析、转换和组合代码来帮助编译器优化代码。表达式树通过提供未类型和已绑定的节点支持了动态语言的概念。
- 调用站点缓存利用了委托和泛型。由于动态对象的创建，任何变量都不是固定的数据类型，可以在遇到时由调用站点进行更新。
- 动态对象缓存——调用站点缓存利用了委托和泛型。由于动态对象的创建，任何变量都不是固定的数据类型，可以在遇到时由调用站点进行更新。
- 动态对象互操作 (`DOI`)—`DOI` 是为了允许 DLR 创建动态对象的类。

# 第7章：动态数据类型与动态语言运行时 (DLR)

## 理解 ExpandObject 和 DynamicObject

`System` 命名空间包含了如 `ExpandObject` 和 `DynamicObject` 等类。这些类是可扩展的。这意味着类的属性、方法和事件可以添加或删除。该对象可以在运行时初始化。`DynamicObject` 类定义了可以在运行时执行的操作。此基类无法直接实例化；因此，要实现动态行为，必须继承 `DynamicObject` 并重写必要的方法。

在详细讨论了 C# 的增强后，现在让我们学习如何在应用程序中使用这些增强。

## 解决方案

### 使用动态数据类型

正如我们在深度解析部分讨论的，动态数据类型是在运行时而不是编译时解析。让我们创建一个名为 `DynamicDataType` 的控制台应用程序来理解数据类型的实现。

列表 7.2 显示了 `DynamicDataType` 应用的代码：

**列表 7.2：DynamicDataType 应用程序的代码**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DynamicDataType
{
    class Program
    {
        static dynamic dyn = 5.56;
        public void Method1(string str, int b)
        {
            Console.WriteLine(str);
            Console.WriteLine(b);
        }
        static void Main(string[] args)
        {
            Program p = new Program();
            ///此方法可以成功编译并运行。
            p.Method1("Hello", 45);
            ///以下行代码编译成功，但在运行时会显示错误。
            ///dynamic dyn 变量的值为 float。
            p.Method1("Hello", dyn); //需要一个整数值作为第二个参数；
            p.Method1(dyn, dyn); //需要字符串和整数值作为第一个和第二个参数；
            Console.Read();
        }
    }
}
```

列表 7.2 的输出如图 7.3 所示：

![](img/17af790174c480761404624aeed9b30b_300_0.png)

在打印了图 7.3 中的结果后，`DynamicDataType` 应用在运行时抛出了异常，如图 7.4 所示：

```csharp
p.Method("Hello", 45);
// 以下行可以成功编译，但在运行时显示错误。
dynamic var = float;
p.Method("Hello", dyn);
// 第二个参数需要 int 值
// 字符串和整数值分别作为第一个和第二个值生成
Console.WriteLine();
// DynamicDataType.Method 的最佳重载方法
// 没有涉及的参数
p.Method(dyn);
// 获取异常的帮助。
```

图 7.4：运行时异常的错误消息

编译器在编译时不会检查 `dynamic` 类型的 `dyn` 变量。`DynamicDataType` 能够成功编译，并且在以下行在编译时不会显示任何错误：

```csharp
p.Method("Hello", dyn);
p.Method(dyn, dyn);
```

让我们学习如何将动态数据类型转换为其他数据类型。

### 转换数据类型

有时，你需要从动态数据类型获取其他数据类型的值。为了做到这一点，你需要将动态类型变量的值转换为其他数据类型。`DynamicConversion` 控制台应用程序展示了将动态变量转换为动态类型的示例。列表 7.3 显示了 `DynamicConversion` 应用的代码：

列表 7.3：DynamicConversion 应用的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DynamicConversion
{
    class Program
    {
        dynamic dynDouble = 5.46;
        dynamic dynString = "test string";
        dynamic dynbool = true;
        dynamic dynDate = System.DateTime.Today;

        public void Method1()
        {
            // 打印动态类型变量的数据类型
            Console.WriteLine(dynDouble.GetType());
            Console.WriteLine(dynString.GetType());
            Console.WriteLine(dynbool.GetType());
            Console.WriteLine(dynDate.GetType());
        }

        public void Method2()
        {
            // 从相应的动态变量获取不同变量的值
            double d = dynDouble;
            string str = dynString;
        }
    }
}
```

## 立即解决方案

```csharp
bool check = dynBool;
DateTime date = dynDate;

// 打印值
Console.WriteLine("double: " + d);
Console.WriteLine("String: " + str);
Console.WriteLine("Boolean: " + check);
Console.WriteLine("DateTime: " + date);

static void Main(string[] args)
{
    Program p = new Program();
    p.Method1();
    p.Method2();
    Console.WriteLine("\n");
    Console.WriteLine("Press Enter to quit...");
    Console.read();
}
}
```

在列表 7.3 中，我们声明并为四个动态数据类型分配了值。`p` 对象调用 `Method` 方法，该方法使用变量的类型。动态类型选择分配给它们的值并在屏幕上打印这些值。接下来，`p` 对象调用 `Method2` 方法，该方法获取不同动态变量的值并打印这些值。

列表 7.3 的输出如图 7.5 所示：

![](img/17af790174c480761404624aeed9b30b_302_0.png)

图 7.5：DynamicConversion 应用的输出

让我们了解如何使用 `ExpandoObject` 类。

### 使用 ExpandoObject 类

作为参数传递的 `ExpandoObject` 类的实例在 C# 中被视为动态对象。这意味着 IntelliSense 对对象成员不起作用；当调用不存在的成员时，编译器不会产生任何错误。然而，当在运行时调用不存在的成员时会发生异常。让我们创建一个名为 `UsingandoObject` 的控制台应用程序，使用一个方法打印不同属性的名称和值。列表 7.4 显示了 `UsingandoObject` 应用的代码。

列表 7.4：UsingandoObject 应用的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Dynamic;

namespace UsingandoObject
{
    class Program
    {
        static void Main(string[] args)
        {
            // 动态类型变量
            dynamic son, father;

            // 初始化 ExpandoObject 对象
            son = new ExpandoObject();
            son.Name = "Son";
            son.Age = 20;

            father = new ExpandoObject();
            father.Name = "Father";
            father.Age = 48;
            father.Children = 3;

            writeFamily(son);
            writeFamily(father);
            Console.WriteLine("Press Enter to quit...");
            Console.Read();
        }

        private static void writeFamily(dynamic member)
        {
            Console.WriteLine("{0} is {1} years old.", member.Name, member.Age);
            // 如果传递 father 对象，以下语句会导致异常
            Console.WriteLine("{0} has {1}", member.Name, member.Children);
        }
    }
}
```

列表 7.4 的输出如图 7.6 所示：

![](img/17af790174c480761404624aeed9b30b_303_0.png)

图 7.6：UsingandoObject 应用的输出

让我们了解如何使用 `DynamicObject` 类。

### DynamicObject 类

作为参数传递的 `ExpandoObject` 类的实例在 C# 中被视为动态对象。这意味着 IntelliSense 对对象成员不起作用；当调用不存在的成员时，编译器不会产生任何错误。然而，当在运行时调用不存在的成员时会发生异常。让我们创建一个 `UsingDynamicObject` 的控制台应用程序，使用一个方法打印不同属性的名称和值。列表 7.4 显示了 `UsingandoObject` 应用。

列表 7.5：DynamicObject 应用的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Dynamic;

namespace UsingDynamicObject
{
    public class Dynamicword : DynamicObject
    {
        Dictionary<string, object> dict = new Dictionary<string, object>();

        // 在类中定义 cnt 属性
        public int cnt
        {
            return dict.Count;
        }

        public override bool TryGetMember(dynamic binder, out object result)
        {
            // 当尝试获取值时调用此方法
            string name = binder.Name;
            if (dict.TryGetValue(name, out result))
            {
                return true;
            }
            result = null;
            return false;
        }

        public override bool TrySetMember(dynamic binder, object value)
        {
            // 当尝试设置值时调用此方法
            dict[binder.Name] = value;
            return true;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 创建动态字典
            dynamic dyn = new Dynamicword();

            // 向对象添加新的动态属性
            // 因此默认调用 TrySetMember 方法
            dyn.text = "C#";
            dyn.description = "A programming language";

            // 获取动态属性的值。默认调用 TryGetMember 方法
            Console.WriteLine(dyn.text + " " + dyn.description);

            // 获取 count 属性的值
            // cnt 属性在类中定义
            // 因此没有调用 TryGetMember
            Console.WriteLine("Number of dynamic properties: " + dyn.cnt);
            Console.WriteLine("\n");
            Console.WriteLine("Press Enter to quit...");
            Console.read();

            Console.WriteLine(dyn.definition);
            // 前一个语句在运行时抛出异常
            // 没有 "definition" 属性
            // 所以 GetMember 方法返回 false，这导致了
            // RuntimeBinderException
        }
    }
}
```

列表 7.5 的输出如图 7.7 所示：

![](img/17af790174c480761404624aeed9b30b_305_0.png)

图 7.7：DynamicObject 应用的输出

## 总结

在本章，你学习了动态数据类型。你还学习了将动态数据类型转换为非动态数据类型以及反之。接下来，你学习了 DLR 及其架构和优势。你还学习了 C# 应用程序中的 `ExpandoObject` 和 `DynamicObject` 类。

## 介绍 Windows Presentation Foundation
