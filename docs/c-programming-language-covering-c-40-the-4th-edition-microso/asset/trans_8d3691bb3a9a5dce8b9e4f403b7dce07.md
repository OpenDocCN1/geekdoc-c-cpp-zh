
> **CHRIS SELLS** 为了可读性，应优先使用 foreach 语句而不是 for 语句。

> **JON SKEET** 事实上只有一个迭代变量（它是只读的，却在每次迭代时神奇地改变其值）导致了捕获变量中最常见的问题之一。下面的代码看起来会打印“a”、“b”、“c”、“d”，但实际上会打印四次“d”。

```csharp
List<Action> actions = new List<Action>();
foreach (string value in new[] { "a", "b", "c", "d" })
{
    actions.Add(() => Console.WriteLine(value));
}
foreach (Action action in actions)
{
    action();
}
```

> 解决方案通常是在 foreach 语句的主体内部引入一个额外的变量，该变量获取迭代变量当前值的副本。这样每个委托将捕获不同的变量。在这种情况下，第一个循环将变为

```csharp
foreach (string value in new[] { "a", "b", "c", "d" })
{
    string copy = value;
    actions.Add(() => Console.WriteLine(copy));
}
```

> **PETER SESTOFT** foreach 语句本可以被定义为不同以避免 Jon Skeet 评论中讨论的变量捕获问题：只需将 try-while-finally 展开中稍后在本节所示的 while 循环内部移动声明 `v`。事实上，在原始 C# 语言规范中，声明出现在 while 循环内部，但在 C# 2.0 的标准化过程中，事实证明在 Microsoft 的实现中至少将 `v` 声明在循环外部更接近事实，因此标准据此进行了更改。

foreach 语句的编译时处理首先确定表达式的 *集合类型*、*枚举器类型* 和 *元素类型*。此确定按如下方式进行：

- 如果 *表达式* 的类型 X 是数组类型，则存在从 X 到 `System.Collections.IEnumerable` 接口的隐式引用转换（因为 `System.Array` 实现了该接口）。*集合类型* 是 `System.Collections.IEnumerable` 接口，*枚举器类型* 是 `System.Collections.IEnumerator` 接口，而 *元素类型* 是数组类型 X 的元素类型。
- 如果 *表达式* 的类型 X 是 *动态*，则存在从 *表达式* 到 `System.Collections.IEnumerable` 接口的隐式转换（§6.1.8）。*集合类型* 是 `System.Collections.IEnumerable` 接口，*枚举器类型* 是 `System.Collections.IEnumerator` 接口。如果 *局部变量类型* 给出 *var* 标识符，则 *元素类型* 为 *动态*；否则为 *object*。
- 否则，确定类型 X 是否具有适当的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且无类型参数执行成员查找。如果成员查找未产生匹配项，或产生歧义或不是方法组的匹配项，则按如下所述检查可枚举接口。建议如果成员查找产生除方法组或无匹配项之外的任何内容，则发出警告。

> > **ERIC LIPPERT** 这种基于“pattern”的方法被指定是为了在通用 `IEnumerable<T>` 可用之前的时代，集合作者能够为其枚举器对象提供更强的类型注释。
> >
> > 非通用 `IEnumerable` 的实现总是最终装箱整数集合的每个成员，因为 Current 属性的返回类型是 object。整数集合的提供者可以提供基于非接口的 GetEnumerator、MoveNext 和 Current 实现，使得 Current 返回未装箱的整数。
> >
> > 当然，在拥有通用 `IEnumerable<T>` 的世界里，所有这些努力都变得不必要了。大多数被迭代的集合将实现此接口。

- 使用 resulting 方法组和空参数列表执行重载解析。如果重载解析未产生适用方法、产生歧义，或产生单一最佳方法但该方法为静态或非公共，则按如下所述检查可枚举接口。建议如果重载解析产生除无歧义的公共实例方法或无适用方法之外的任何内容，则发出警告。
- 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误且不再进行后续步骤。

- 在 E 上使用标识符 Current 且无类型参数执行成员查找。如果成员查找未产生匹配项，结果为错误，或结果除允许读取的公共实例属性外为任何其他内容，则产生错误且不再进行后续步骤。
- 在 E 上使用标识符 MoveNext 且无类型参数执行成员查找。如果成员查找未产生匹配项，结果为错误，或结果除方法组外为任何其他内容，则产生错误且不再进行后续步骤。
- 对方法组使用空参数列表执行重载解析。如果重载解析未产生适用方法、产生歧义，或产生单一最佳方法但该方法为静态或非公共，或其返回类型不是 bool，则产生错误且不再进行后续步骤。
- *集合类型* 为 X，*枚举器类型* 为 E，*元素类型* 为 Current 属性的类型。
- 否则，检查可枚举接口：
  - 如果恰好存在一个类型 T，使得存在从 X 到接口 System.Collections.Generic.IEnumerable<T> 的隐式转换，则 *集合类型* 为此接口，*枚举器类型* 为接口 System.Collections.Generic.IEnumerator<T>，*元素类型* 为 T。
  - 否则，如果存在多个此类类型 T，则产生错误且不再进行后续步骤。
  - 否则，如果存在从 X 到 System.Collections.IEnumerable 接口的隐式转换，则 *集合类型* 为此接口，*枚举器类型* 为接口 System.Collections.IEnumerator，*元素类型* 为 object。
  - 否则，产生错误且不再进行后续步骤。

> > **PETER SESTOFT** 不幸的是，foreach 语句的编译时处理意味着它相当动态类型化。例如，对于任意非密封类 C 和接口 I，以下内容在类型上是正确的，并且不会产生任何编译器警告或错误：

```csharp
C[] xs = ...;
foreach (I x in xs)
...
```

> > 事实上，最近我就在移除一个看似无关的接口 I 从类 C 的接口列表时落入了这个陷阱。项目在构建阶段没有错误通过，但在运行时应用程序因 InvalidCastException 而崩溃，因为我忽略了几个 foreach 语句。实际上，这种行为是可以预期的，因为 C 的某个子类可能实现了接口 I。或许更令人惊讶的是，I 和 C 可以在前面的代码中互换而结果相同。

如果上述步骤成功，则会明确地产生 *集合类型* C、*枚举器类型* E 和 *元素类型* T。形式为的 foreach 语句

`foreach (V v in x) embedded-statement`

然后展开为：

```csharp
{
    E e = ((C)(x)).GetEnumerator();
    try {
        V v;
        while (e.MoveNext()) {
            v = (V)(T)e.Current;
            embedded-statement
        }
    }
    finally {
        ... // Dispose of e
    }
}
```

变量 e 不对表达式 x、嵌入语句或程序的任何其他源代码可见或可访问。变量 v 在嵌入语句中为只读。如果不存在从 T（*元素类型*）到 V（foreach 语句中的 *局部变量类型*）的显式转换（§6.2），则产生错误且不再进行后续步骤。如果 x 的值为 null，则在运行时抛出 System.NullReferenceException。

> > **MAREK SAFAR** foreach 语句是语言演进的经典示例。C# 1.0 没有通用的 IEnumerable<T>，必须从元素类型到局部变量使用显式转换。C# 2.0 引入了具有泛型元素类型的 foreach 语句的泛型版本。C# 3.0 通过引入 *隐式类型迭代变量* 将此结构带回了本应开始的地方，这使显式转换变为隐式，并避免了执行期间的任何 InvalidCastException。
