
U 是构造的类、结构体、接口或委托类型 C<U1, ..., Un>，而 V 是类、结构体、接口或委托类型，其与唯一类型 C<V1, ..., Vn> 相同、继承自（直接或间接）或实现（直接或间接）该类型。

（“唯一性”限制意味着如果我们有接口 C<T>{} 类 V<Z>: C<X<Z>>, C<V<Z>>{}，则在从 C<U> 推断到 V<Q> 时不进行推断。不会从 U1 推断到 X<Q> 或 V<Q>。）

如果适用上述任一情况，则按如下方式从每个 Ui 推断到对应的 Vi：

- 如果不知道 Ui 是引用类型，则进行精确推断。
- 否则，如果 V 是数组类型，则进行上界推断。
- 否则，如果 U 是 C<U1, ..., Un>，则推断取决于 C 的第 i 个类型参数：
  - 如果它是协变的，则进行上界推断。
  - 如果它是逆变的，则进行下界推断。
  - 如果它是不可变的，则进行精确推断。
- 否则，不进行推断。

> **VLADIMIR RESHETNIKOV** 因此，对于在泛型方法参数类型中未出现的 方法类型参数，永远不会进行推断。例如，对于仅出现在约束中的参数，不会进行推断：
> 
> ```csharp
> using System.Collections.Generic;
> 
> class C
> {
>     static void Foo<T,U>(T x) where T : IEnumerable<U> { }
> 
>     static void Main()
>     {
>         Foo(new List<int>());
>         // Error CS0411: The type arguments for method
>         // 'C.Foo<T,U>(T)' cannot be inferred from the
>         // usage.
>     }
> }
> ```

## 7.5.2.11 Fixing

未固定的类型变量 Xi 及其一组边界的固定方式如下：

- 候选类型 Uj 的集合最初为 Xi 边界集合中的所有类型的集合。

> **ERIC LIPPERT**  此条件说明了 C# 的一个微妙设计点。面对给定一组类型时需要选择“最佳类型”的情况，我们总是从该集合中选择一种类型。也就是说，如果要求在 `{Cat, Dog, Goldfish}` 中选择最佳类型，我们将找不到最佳类型；我们永远不会说，“鉴于这三个选择，公共基类型 Animal 是我们能做到的最好”，因为 Animal 首先就不是选择之一。

- 然后我们依次检查 xᵢ 的每个边界：对于每个边界 U of xᵢ，所有不与 U 相同的类型 Uⱼ 都从候选集合中移除。对于每个下界 U of xᵢ，所有不存在从 U 到 Uⱼ 的隐式转换的类型 Uⱼ 都从候选集合中移除。对于每个上界 U of xᵢ，所有不存在从 Uⱼ 到 U 的隐式转换的类型 Uⱼ 都从候选集合中移除。
- 如果在剩余的候选类型 Uⱼ 中存在唯一的类型 V，可以隐式转换为所有其他候选类型，则将 xᵢ 固定为 V。
- 否则，类型推断失败。

> **ERIC LIPPERT**  在 C# 2.0 中，如果为同一类型参数计算出两个不同的边界，则泛型方法类型推断算法会失败。在 C# 3.0 中，我们有 Join 方法等情况，必须推断两个集合连接的“键”的类型。如果一个集合中的键是， say， `int`，而另一个集合中对应的键是 `int?`，则我们有两个不同的类型。然而，由于每个 int 都可以转换为 int?，我们可以允许这种歧义并通过选择两者中更通用的类型来解决它。C# 4.0 支持泛型协变，这进一步复杂化了情况；现在我们可能对类型参数具有上界、下界和精确边界。

## 7.5.2.12 Inferred Return Type

匿名函数 F 的 *推断返回类型* 在类型推断和重载解析期间使用。推断返回类型只能针对所有参数类型已知的匿名函数确定，这些参数类型要么是显式给出的，要么是通过匿名函数转换提供的，要么是在封闭泛型方法调用的类型推断期间推断出来的。推断返回类型按如下方式确定：

- 如果 F 的主体是 *表达式*，则 F 的推断返回类型为该表达式的类型。
- 如果 F 的主体是 *块* 并且块的 return 语句中表达式集合具有最佳公共类型 T (§7.5.2.14)，则 F 的推断返回类型为 T。

![](img/04b421b044b1254de966ab5335775a89_284_0.png)

> > **VLADIMIR RESHETNIKOV** 即使不可达代码中的 return 语句也被包含在集合中并参与推断返回类型的计算。这有一个令人惊讶的后果，即删除不可达代码可能会改变程序行为。

- 否则，无法为 F 推断返回类型。

作为涉及匿名函数的类型推断的示例，请考虑在 `System.Linq.Enumerable` 类中声明的 `Select` 扩展方法：

```
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource, TResult>(
            this IEnumerable<TSource> source,
            Func<TSource, TResult> selector)
        {
            foreach (TSource element in source)
                yield return selector(element);
        }
    }
}
```

假设已通过 using 子句导入 `System.Linq` 命名空间，并且给定一个 Name 属性类型为 string 的 Customer 类，则可以使用 Select 方法选择客户列表的名称：

```
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

Select 的扩展方法调用 (§7.6.5.2) 通过重写调用为静态方法调用来处理：

```
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

由于未显式指定类型参数，因此使用类型推断来推断类型参数。首先，将 customers 参数与 source 参数关联，推断 T 为 Customer。然后，使用上面描述的匿名函数类型推断过程，c 被赋予 Customer 类型，并且表达式 c.Name 与 selector 参数的返回类型关联，推断 S 为 string。因此，该调用等价于

```
Enumerable.Select<Customer,string>(customers, (Customer c) => c.Name)
```

并且结果的类型为 `IEnumerable<string>`。

以下示例演示了匿名函数类型推断如何允许类型信息在泛型方法调用的参数之间“流动”。给定方法

```
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

对调用的类型推断

```
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```

进行如下：首先，将参数 “1:15:30” 与 value 参数关联，推断 X 为 string。然后，将第一个匿名函数的参数 s 赋予推断出的 string 类型，并且表达式 TimeSpan.Parse(s) 与 f1 的返回类型关联，推断 Y 为 System.TimeSpan。最后，将第二个匿名函数的参数 t 赋予推断出的 System.TimeSpan 类型，并且表达式 t.TotalSeconds 与 f2 的返回类型关联，推断 Z 为 double。因此，该调用的结果类型为 double。

## 7.5.2.13 Type Inference for Conversion of Method Groups

与泛型方法调用类似，当包含泛型方法的 方法组 M 转换为给定的委托类型 D (§6.6) 时，也必须应用类型推断。给定方法

T_r M<X_1...X_n>(T_1 x_1 ... T_n x_n)

并且方法组 M 被赋给委托类型 D，类型推断的任务是找到类型参数 S_1...S_n，使得表达式

M<S_1...S_n>

与 D 兼容 (§15.1)。

与泛型方法调用的类型推断算法不同，在这种情况下只有参数类型——没有参数表达式。特别是，没有匿名函数，因此不需要多阶段推断。

相反，所有 X_i 都被视为未固定，并且从 D 的每个参数类型 U_i 到 M 的对应参数类型 T_i 进行下界推断。如果对于任何 X_i 未找到边界，则类型推断失败。否则，所有 X_i 都被固定为对应的 S_i，即类型推断的结果。
