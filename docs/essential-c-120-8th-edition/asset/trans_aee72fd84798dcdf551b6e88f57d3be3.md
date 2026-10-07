

# 第 14 章：事件

带有 `event` 关键字修饰符的变量会将委托声明为私有类型。此外，它还会添加几个方法和两个特殊的事件块。本质上，`event` 关键字是生成相应封装逻辑的 C# 简写。请考虑列表 14.15 所示事件声明中的示例。

列表 14.15：声明 OnTemperatureChange 事件

```cs
public class Thermostat
// ...
    public event EventHandler<TemperatureArgs>? OnTemperatureChange;
}
```

当 C# 编译器遇到 `event` 关键字时，它会生成等同于列表 14.16 所示 C# 代码的 CIL 代码。

列表 14.16：编译器生成的事件 CIL 代码的 C# 上等代码

```cs
public class Thermostat
// ...
    // 委托字段以保存
    // 订阅者列表
    private EventHandler<TemperatureArgs>? _OnTemperatureChange;

    public void add_OnTemperatureChange(EventHandler<TemperatureArgs> handler)
    {
        System.Delegate.Combine(_OnTemperatureChange, handler);
    }

    public void remove_OnTemperatureChange(EventHandler<TemperatureArgs> handler)
    {
        System.Delegate.Remove(_OnTemperatureChange, handler);
    }

#if ConceptualEquivalentCode
public event EventHandler<TemperatureArgs> OnTemperatureChange
{
    // 会导致编译器错误
    add
    {
        add_OnTemperatureChange(value);
    }
    // 会导致编译器错误
remove{
  remove_OnTemperatureChange(value);
}
#endif // ConceptualEquivalentCode
```

换句话说，列表 14.15 所示的代码是（概念上）编译器用于触发列表 14.16 所示代码展开的 C# 简写。（需要“概念上”这一修饰符是因为为了说明起见，消除了某些关于线程同步的细节。）

C# 编译器首先解析原始事件定义，并在其位置定义一个私有委托。结果是该委托对任何外部类（即使是派生类）都是不可用的。

接下来，C# 编译器定义了两个方法 `add_OnTemperatureChange()` 和 `remove_OnTemperatureChange()`，其中 `OnTemperature` 后缀取自事件的原始名称。这些方法负责实现 `+=` 和 `-=` 赋值运算符。如列表 14.16 所示，这些方法是使用在本章之前讨论的静态 `System.Delegate.Combine()` 和 `System.Delegate.Remove()` 方法实现的。传递给这些方法的第一个参数是私有的 `EventHandler<TemperatureArgs>` 委托实例 `OnTemperatureChange`。

`event` 关键字生成的代码中最奇特的部分可能是最后一段。其语法与属性的 getter 和 setter 方法非常相似，只是方法分别被命名为 `add` 和 `remove`。`add` 块通过将调用传递给 `add_OnTemperatureChange()` 来处理 `+=` 运算符。同样，`remove` 块通过将调用传递给 `remove_OnTemperatureChange` 来处理 `-=` 运算符。

仔细注意此代码与属性生成的代码之间的相似之处。记得 C# 中属性的实现是创建 `get_<propertyName>` 和 `set_<propertyName>`，然后将调用传递到这些方法上的 `get` 和 `set` 块。显然，在这种情况下语法非常相似。

生成的 CIL 代码另一个需要注意的重要特征是，`event` 关键字的 CIL 等价项保留在 CIL 中。换句话说，事件是 CIL 代码显式识别的内容；它不仅仅是 C# 构造。通过在 CIL 代码中保留等效的事件 `event`，所有语言和编辑器都可以提供特殊功能，因为它们可以将事件识别为一种特殊的类成员。

# 自定义事件实现

你可以自定义编译器为 `+=` 和 `-=` 生成的范围。例如，更改 `OnTemperatureChange` 委托的范围，使其成为 `protected` 而不是 `private`。这允许派生自 `Thermostat` 的类直接访问委托，而不是受到相同限制。为了实现此行为，C# 允许使用与列表 14.17 相同的属性语法。换句话说，C# 允许你定义自定义的 `add` 和 `remove` 块，为事件封装的每个方面提供独特的实现。

列表 14.17：自定义 add 和 remove Handler

```cs
public class Thermostat
{
    public class TemperatureArgs : System.EventArgs
    //...
    // 定义事件发布者
    public event EventHandler<TemperatureArgs> OnTemperatureChange
    {
        add
        {
            _OnTemperatureChange = (EventHandler<TemperatureArgs>)
System.Delegate.Combine(value, _OnTemperatureChange);
        }
        remove
        {
            _OnTemperatureChange = (EventHandler<TemperatureArgs>)?
System.Delegate.Remove(_OnTemperatureChange, value);
        }
    }
}

protected EventHandler<TemperatureArgs>? _OnTemperatureChange;
public float CurrentTemperature
// ...
private float _CurrentTemperature;
```

在这里，委托存储了每个订阅者 `_OnTemperatureChange`。此外，`add` 块的实现切换了委托的存储，使得最后添加到链链中的委托是第一个接收通知的委托。然而，代码不应依赖这种实现。

# 总结

现在我们已经描述了事件，我们注意到，通常情况下，只有在方法引用的情况下才建议在事件上下文之外处理委托变量。鉴于事件的额外封装功能以及必要时自定义实现的能力，最佳实践始终是使用事件来实现发布-订阅模式。

在能够不参考示例代码就从零编写事件之前，可能需要一些练习。然而，事件是本书后续章节中描述的异步、多线程编码的关键基础。

# 15 章：带有标准查询运算符的集合接口

通过一组扩展方法和 lambda 表达式，称为语言集成查询（LINQ）的编程 API 为处理集合提供了了优越多的 API¹。事实上，在本书的早期版本中，集合章节紧随泛型章节之后，并在委托章节之前。然而，lambda 表达式对 LINQ 来说是如此基础，以至于如果不先涵盖委托（lambda 表达式的基础），就无法涵盖集合。现在你已经通过前两个章节建立了 lambda 表达式的坚实基础，我们可以深入集合的细节——这是一个跨越三个章节的话题。在本章中，重点从**标准查询运算符**开始——这通过直接调用扩展方法来利用 LINQ 的手段。

在引入集合初始化器后，本章涵盖了各种集合接口，并探索了它们之间的相互关系。这是理解集合的基础，因此你应该勤奋地学习这些材料。集合接口部分包含了实现标准查询运算符的 `IEnumerable<T>` 扩展方法²。

集合相关的类和接口分为两类：支持泛型的和不支持泛型的。本章主要讨论泛型

# 第 15 章：带有标准查询运算符的集合接口

![](img/ffe0f34eac7523830420733690014d7_790_0.png)

集合接口。只有当你编写需要与旧版本的运行时一起操作的组件时，才应该使用不支持泛型的集合类。这是因为非泛型形式中可用的一切都有一个强类型的泛型替代品。尽管这些概念仍然适用于两种形式，但我们没有显式讨论非泛型版本³。

本章以对匿名类型的深入讨论结束——我们在第 3 章的几个高级主题章节中简要涵盖过这些。匿名类型的有趣之处在于，它们已经被元组⁴所掩盖，我们将在章末尾进一步讨论这一话题。

# 集合初始化器

¹ C# 3.0 在集合中添加的归因于 LINQ 的显著特性。
² 在 C# 3.0 中添加。
³ 实际上，NET Standards 和 .NET Core 甚至不包含非泛型集合。
⁴ 从 C# 7.0 开始。

