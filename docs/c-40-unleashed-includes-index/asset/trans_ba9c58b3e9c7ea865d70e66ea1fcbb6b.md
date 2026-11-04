

```
return (int)a + (int)b; // from Figure 22.14
return site.Update(site, a, b);
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1167_0.png)

图22.14 C#绑定器生成的用于将两个Int32对象相加的代码。

这正是调用点需要在调用时传递自身的原因；通过这种方式，DLR才能获取Target委托字段，并在每次对调用目标有了更多了解时，用更专用的委托替换它。

有了这个新委托后，任何后续以两个Int32对象作为输入的调用都将执行这段专用代码片段。这会绕过C#绑定器中的所有逻辑。这些逻辑并不简单；您应当理解，Microsoft.CSharp.dll中的绑定器掌握着针对重载解析、隐式转换等的语言特定规则。例如，如果我们向绑定器传入一个int和一个long，它会应用C#规则：Int32可以隐式转换为Int64，这样就可以在两个Int64之间执行加法：

```
if (a is long && b is int)
    return (long)a + (long)b;
```

当然，这种操作解析还包含了诸如运算符重载之类的查找，如图22.15所示，该图展示了C#运行时绑定器在遇到DateTime和TimeSpan对象时返回的部分表达式树。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1167_1.png)

图22.15 用于将DateTime和TimeSpan相加的运算符重载。

从这个角度来看，DLR的本质是为通过语言特定绑定器传递给它的表达式树片段提供树拼接服务。这也解释了为什么表达式树API被增强以支持语句树节点——因为类似这样的调用点需要条件逻辑。

## 表达式树：新一代瑞士军刀

随着.NET Framework的每次发布，表达式树的使用变得越来越明显。最初，表达式树是LINQ提供程序理解用户意图的一种方式，现在它们已成为运行时各种编译任务的通用后端。IronPython和IronRuby等语言总是将代码转换为表达式树，以便通过IL高效执行代码。

图22.16展示了我们的调用点背后的Target委托代码在使用不同参数类型组合调用时所经历的状态。至于绘制用于表示这些代码的相应表达式/语句树（在动态语言运行时编译之前），则留给读者作为练习。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1168_0.png)

图22.16 调用点在传入新输入类型时被更新。

WriteLine调用的调用点以类似方式工作。在这种情况下，第一个参数在静态上被确定为typeof(Console)，因为我们在原始C#代码中指定了这一点（Console.WriteLine）。然而，从运行时类型的角度来看，方法参数会变化，因此会调用Console.WriteLine的不同重载。我把它留作练习：基于我们运行示例的生成代码，为InvokeMember操作创建一个C#绑定器，并用各种参数（如int和DateTime对象）调用绑定器的Bind方法。生成的表达式树大致应如下所示：

```
(CallSite site, Type t, object a) =>
{
    // t will always be typeof(Console); see the CSharpArgumentInfo flags
    if (a is int)
        Console.WriteLine((int)a);
    if (a is DateTime)
        Console.WriteLine(a); // System.Object argument overload
    site.Update(site, a, b);
}
```

## 使用DynamicObject自定义动态对象

到目前为止，我们还没有机会控制在对象上调用动态操作时发生在运行时的任何绑定逻辑。DLR的灵活基础设施提供了一种创建参与这些操作的对象的方式。要实现这一点，最简单的途径是使用System.Dynamic.DynamicObject，如图22.17所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1169_0.png)

图22.17 查看DynamicObject和IDynamicMetaObjectProvider。

如您所见，这个基类包含DLR所支持的每个动态操作的Try方法。作为第一个参数传递的Binder对象与这些操作相对应，并根据前端编译器发出的代码，包含有关所执行操作的信息。

当DLR遇到从DynamicObject派生的对象时，绑定信息将首先传递给该对象的方法，使其有机会为这些操作提供一些非标准语义。作为示例，考虑bag类型的概念，我们将其视为将字符串键映射到对象值的字典。字典对象的典型用法是在索引器上处理字符串。然而，我们的bag实现将允许我们使用C#语法“点入”对象。以下代码示例对比了两种方法：

```csharp
// Classic dictionary
var d = new Dictionary<string, object>();
d["Name"] = "Bart";
d["Age"] = 27;
Console.WriteLine(d["Name"].ToString() + " is " + d["Age"].ToString());

// Bag using dynamic
dynamic bag = new Bag();
bag.Name = "Bart";
bag.Age = 27;
Console.WriteLine(bag.Name + " is " + bag.Age);
```

显然，我们不会提供一个预定义了Name和Age属性的Bag对象，因为我们希望将bag用于任何键值对集合（重新）使用。

为了实现这种效果，我们从DynamicObject派生Bag，并重写其中一些成员来拦截对bag实例执行的操作。具体来说，我们想要参与成员获取和设置操作的动态调用，因此我们重写TryGetMember和TrySetMember：

```csharp
class Bag : DynamicObject
{
    private Dictionary<string, object> _bag = new Dictionary<string,object>();

    public override bool TryGetMember(GetMemberBinder binder, out object res)
    {
        return _bag.TryGetValue(binder.Name, out res);
    }

    public override bool TrySetMember(SetMemberBinder binder, object value)
    {
        _bag[binder.Name] = value;
        return true;
    }
}
```

bag的私有状态由一个经典字典组成，我们为其提供更简单的访问模式。在binder对象上，我们可以找出用户目标成员的名称（例如Name或Age），以及其他信息，例如语言的大小写敏感性（这里我们忽略）。图22.18展示了`TryGetMember`被命中时的调用栈。注意栈上的先前帧：

- `Program.Main`中从站点容器获取生成的调用点对象，并调用Target委托。
- Target委托本身调用Update委托，指向一个DLR函数，用于更新调用点并执行操作。`arg0`参数将是对Bag对象的引用。
- Lightweight Function包含针对`DynamicObject`的类型检查以及随后对`TryGetMember`的调用。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1171_0.png)

**图22.18** 通过DLR代码路径调用`TryGetMember`。

`DynamicObject`上各个Try方法的布尔返回值用于指示动态操作的成功或失败。当返回false时，后备行为将启动，在运行时绑定器（此处是C#的绑定器）中循环，该绑定器将在Bag实例本身上查找目标操作。例如：

```
public int Count { get { return _bag.Keys.Count; } }

public override bool TryGetMember(GetMemberBinder binder, out object result)
{
    // Count is never in the bag, so hand over to the C# binder (return false).
    return _bag.TryGetValue(binder.Name, out result);
}

public override bool TrySetMember(SetMemberBinder binder, object value)
{
    if (binder.Name == "Count")
        return false; // Attempt to set Count via the C# binder (will fail).
    _bag[binder.Name] = value;
    return true;
}
```

## 扩展对象

事实上，对象可以在运行时获取成员的概念并不新鲜；毕竟，JavaScript等动态语言非常依赖这一点。在这种语言中，甚至每个对象都具备这些能力。

这个概念被称为expando对象（扩展对象），因为它们可以在运行时扩展其表面。我们刚刚构建的Bag实际上以（一种更复杂的方式）存在于System.Dynamic命名空间中，名为ExpandoObject。附加功能包括实现INotifyPropertyChanged，以及直接的字典访问，因为该类型实现了IDictionary<string, object>，因此它既可以作为字典使用（带更改通知），也可以通过新的动态功能使用：

```
var exp = new ExpandoObject();

// Use as generic dictionary
var dct = (IDictionary<string, object>)exp;
dct["Name"] = "Bart";

// Use as dynamic bag
var bag = (dynamic)exp;
bag.Age = 27;

// Use as enumerable for KeyValuePair<string, object>
foreach (var item in dct)
    Console.WriteLine(item);
```

熟悉经典COM编程的人们会认出IDispatchEx接口的这些能力。难怪这个接口在很久以前就被引入，用于支持VBScript和Jscript等脚本语言。

