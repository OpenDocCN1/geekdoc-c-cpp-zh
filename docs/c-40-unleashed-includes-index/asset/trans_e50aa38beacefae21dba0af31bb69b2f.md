
让我们来看一个综合示例：

```
[AttributeUsage(AttributeTargets.Class)]
public class ExtensionAttribute : Attribute
{
    public ExtensionAttribute(string name)
    {
        Name = name;
    }
    public string Name { get; private set; }
}
```

特性的声明有多种模式。由于特性上的某些参数可能是可选的，常见的做法是定义一个构造函数，它接收所有必需的参数，同时组合一组可设置的属性用于可选参数。必需参数也称为“位置参数”，因为它们是按构造函数中出现的顺序指定的，而可选参数则称为“命名参数”，因为你是通过属性名来指定的。

为了简化特性的声明，Visual Studio 提供了一个名为 Attribute 的代码片段。要插入它，请输入 Attribute 并按两次 Tab 键。此操作的结果如图 21.10 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1106_0.png)

图 21.10 用于声明自定义特性的代码片段。

## 使用特性

在适用目标上使用自定义特性，是通过前面展示的方括号语法完成的。在方括号内，指定特性的名称，其中类型名上的 Attribute 前缀可以省略，后跟括号内的参数。位置参数在前，以逗号分隔，而命名参数可以在后面使用 name = value 语法指定。

例如，考虑 AttributeUsage 特性本身，它在 Visual Studio 中显示的 IntelliSense 辅助如图 21.11 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1107_0.png)

图 21.11 将特性应用于类定义的使用示例。

## 命名参数语法

编程语言的演进总会带来有趣的挑战。其中之一是让现有程序能在更新版本的语言下继续编译。命名参数也不例外。首先是特性，在括号内使用 name-value 对来指定可选参数：

```
Bar(42, Optional = "Hi")
```

在 C# 3.0 中，添加了对象初始化器表达式，其语法略有不同，因为前面的形式会产生歧义。（你是想将 Optional 初始化为 Bar 实例上的一个属性，还是想调用一个接受整数和字符串的构造函数，并顺便将 Optional 赋值？）

```
new Foo(42) { Optional = "Hi" }
```

最后，在 C# 4.0 中，可选参数和命名参数被引入到各种调用语法形式（构造函数、方法、委托）中，如果要调用的构造函数有一个名为 optional 的参数，你可以编写如下代码：

```
new Foo(42, optional: "Hi")
```

同样，需要使用带有冒号标记的专用语法，以区别于该语言早期版本中已有的赋值表达式。

尽管事后看来，为相关概念提供如此多的语法并不理想，但这就是语言演进（面临高度兼容性需求）所带来的。

## 自定义特性是如何存储的？

自定义特性定义在代码块之外（代码块会表示为中间语言 IL），你可能想知道自定义特性在程序集中是如何存储的，以及存储在哪里。同样，答案可以在 ILDASM 中找到，它也解释了围绕自定义特性数据的一些限制。例如，为什么只有常量表达式才能用于自定义特性中的数据？让我们基于以下代码来看一看：

```
[My("Hello", NamedInt=42)]
class Program
{
    ...
}
```

查看 ILDASM，你首先会看到自定义特性是如何隐藏在某个 .custom 结构后面的，如图 21.12 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1108_0.png)

图 21.12 在 ILDASM 中显示的自定义特性。

从中你已可以看到自定义特性是如何由一个字节序列表示的，该序列包含其常量数据。换句话说，自定义特性不可能依赖代码执行来计算其数据值，因为所有数据都被序列化为一个字节序列。你可以进一步深入，进入 View、MetaInfo、Show (Ctrl+M) 以文本格式显示类型定义等内容。在那里，Program 的类型定义会显示以下特性：

```
TypeDef #2 (02000003)
....................................................
TypDefName: Program  (02000003)
...
CustomAttribute #1 (0c000006)
....................................................
    CustomAttribute Type: 06000001
    CustomAttributeName: MyAttribute :: instance void .ctor(class String)
    Length: 25
    Value : 01 00 05 48 65 6c 6c 6f 01 00 54 08 08 4e 61 6d ...
    ctor args: ("Hello_")
```

## 发现自定义特性

尽管大多数读者可能只需要使用自定义特性来使用框架的某些部分（如 MEF、WCF 等）或使用外部库，但了解如何声明和发现自定义特性仍然很有用。你已经看到了如何声明它们，但你的代码现在如何检查给定的程序集、类型或成员，并确定是否应用了特性？答案同样在于反射。

为了将理论付诸实践，让我们在 Extensibility 程序集中引入以下自定义特性，从而扩展 ExtensiCalc 应用程序：

```
[AttributeUsage(AttributeTargets.Class)]
public class CalculationOperationAttribute : Attribute
{
    public CalculationOperationAttribute(string name, string infix)
    {
        Name = name;
        Infix = infix;
    }

    public string Name { get; private set; }
    public string Infix { get; private set; }
}
```

该特性的目的是为计算操作提供友好的名称，并提供中缀运算符表示法以实现美观打印。例如，Addition 类可以像下面这样使用该特性进行修饰：

```
[CalculationOperation("Add", "+")]
class Addition : ICalculation
{
    public int Calculate(int a, int b)
    {
        return a + b;
    }
}
```

有了这些信息，宿主应用程序现在可以查看操作的类型，并判断是否存在此自定义特性。如果存在，就可以进行额外的“美观打印”。检测自定义特性并检索其中定义的信息的要点如下所示：

```
var add = typeof(Addition);
var opa = (CalculationOperationAttribute)Attribute.GetCustomAttribute(
    add, typeof(CalculationOperationAttribute));
if (opa != null)
{
    Console.WriteLine("Extension: {0}", add);
    Console.WriteLine("Name: {0}", opa.Name);
    Console.WriteLine("Notation: a {0} b", opa.Infix);
}
```

给定操作类型，第二行使用 System.Attribute 上的 GetCustomAttribute 静态方法在 add 类型上检测 CalculationOperationAttribute。或者，你可以使用 System.Type（或反射的其他成员，如 MethodInfo）上的 GetCustomAttributes（复数）方法来检测给定类型的自定义特性（同样是复数）。LINQ 运算符在这种情况下也很有用：

```
var opa = add.GetCustomAttributes(false /* inherit */)
    .OfType<CalculationOperationAttribute>()
    .SingleOrDefault();
```

这里我们找到所有自定义特性，筛除指定类型之外的，最后获取唯一的那个，如果没有则返回 null。不管怎样，有了自定义特性对象，我们现在就可以检查它的属性，即本例中的 Name 和 Infix。

我将把以下内容留作练习：请你用附加代码改造整个 ExtensiCalc 示例，以查找此自定义特性，并使用所发现操作的 Name 属性呈现自定义菜单。图 21.13 显示了程序改造版本输出的截图。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1110_0.png)

图 21.13 用于美观打印运算符名称和中缀表示法的自定义特性。

## 自定义特性还是更丰富的接口？

从 ExtensiCalc 示例可以清楚地看到，有多种方式可以暴露与类相关联的丰富元数据。除了使用自定义特性，我们也可以使用额外属性来丰富 ICalculationOperation 接口。虽然这样也行，但接口往往会在使用者和提供者之间造成紧张关系。丰富的接口意味着实现者需要做更多工作，这可能并不是人们所期望的。使用抽象类来摆脱这个问题是一种可能，但由于单一继承模型，它又会带来其他限制。

此外，自定义特性为元数据提供了更丰富的支持，而且不仅限于类，因为它们可以应用于各种成员，甚至整个程序集。因此，请扪心自问：在你的特定用例中，元数据意味着什么？你如何处理其存在或缺失？最终的解决方案是什么？
