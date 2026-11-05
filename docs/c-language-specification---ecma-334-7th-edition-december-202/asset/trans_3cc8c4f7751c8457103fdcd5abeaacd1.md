
- 如果 F 是异步的，并且具有推断出的有效返回类型 T，则推断的返回类型为 «TaskType»<T>（§15.15.1）。
- 如果 F 是非异步的，并且具有推断出的有效返回类型 T，则推断的返回类型为 T。
- 否则，无法为 F 推断返回类型。

*示例：* 作为涉及匿名函数的类型推断示例，请考虑在 System.Linq.Enumerable 类中声明的 Select 扩展方法：

```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source)
            {
                yield return selector(element);
            }
        }
    }
}
```

假设我们通过 using 命名空间指令导入了 System.Linq 命名空间，并且有一个包含 string 类型的 Name 属性的 Customer 类，那么可以使用 Select 方法来选择客户列表中的姓名：

```csharp
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

Select 的扩展方法调用（§12.8.9.3）通过将该调用重写为静态方法调用来处理：

```csharp
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

由于未显式指定类型实参，因此使用类型推断来推断类型实参。首先，将 customers 实参与 source 参数相关联，推断出 TSource 为 Customer。然后，使用上文描述的匿名函数类型推断过程，c 被赋予类型 Customer，并将表达式 c.Name 与 selector 参数的返回类型相关联，推断出 TResult 为 string。因此，该调用等价于 Enumerable.Select<Customer,string>(customers, (Customer c) => c.Name)，其结果类型为 IEnumerable<string>。

下面的示例演示了匿名函数类型推断如何使类型信息在泛型方法调用的实参之间“流动”。给定以下方法和调用：

```csharp
class A
{
    static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2)
    {
        return f2(f1(value));
    }
}

static void M()
{
    double hours = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalHours);
}
```

该调用的类型推断过程如下：首先，将实参 "1:15:30" 与 value 参数相关联，推断出 X 为 string。然后，第一个匿名函数的参数 s 被赋予推断出的类型 string，并将表达式 TimeSpan.Parse(s) 与 f1 的返回类型相关联，推断出 Y 为 System.TimeSpan。最后，第二个匿名函数的参数 t 被赋予推断出的类型 System.TimeSpan，并将表达式 t.TotalHours 与 f2 的返回类型相关联，推断出 Z 为 double。因此，该调用的结果类型为 double。示例结束

### 12.6.3.14 方法组转换的类型推断

与泛型方法的调用类似，当包含泛型方法的方法组 M 被转换为给定的委托类型 D（§10.8）时，也应应用类型推断。给定一个方法 Tₑ M<X₁...Xₙ>(T₁ x₁ ... Tₑ xₑ) 以及被赋值给委托类型 D 的方法组 M，类型推断的任务是找到类型实参 S₁...Sᵥ，使得表达式 M<S₁...Sᵥ> 与 D 兼容（§20.2）。

与泛型方法调用的类型推断算法不同，在这种情况下，只有实参类型，没有实参表达式。特别是，没有匿名函数，因此不需要多阶段推断。

相反，所有 Xᵢ 都被视为未固定，并从 D 的每个实参类型 Uᵢ 到 M 的相应参数类型 Tᵢ 执行下界推断。如果对于任何 Xᵢ 都没有找到界限，则类型推断失败。否则，所有 Xᵢ 都被固定为相应的 Sᵢ，即类型推断的结果。

### 12.6.3.15 查找一组表达式的最佳公共类型

在某些情况下，需要为一组表达式推断一个公共类型。特别是，隐式类型数组的元素类型和带块体的匿名函数的返回类型就是通过这种方式确定的。

对于一组表达式 E₁...Eᵥ，其最佳公共类型按如下方式确定：

- 引入一个新的未固定类型变量 X。
- 对于每个表达式 Eᵢ，从它到 X 执行一次输出类型推断（§12.6.3.7）。
- 如果可能，将 X 固定（§12.6.3.12），所得类型即最佳公共类型。
- 否则推断失败。
- 注意：直观上，此推断等价于调用一个方法 `void M<X>(X x₁ ... X xᵥ)`，将 Eᵢ 作为实参传入并推断 X。注释结束

## 12.6.4 重载决策

### 12.6.4.1 概述

重载决策是一种绑定期机制，用于在给定参数列表和一组候选函数成员的情况下，选择要调用的最佳函数成员。重载决策在 C# 中的以下不同上下文中选择要调用的函数成员：

- 调用 `invocation_expression`（§12.8.9）中命名的方法。
- 调用 `object_creation_expression`（§12.8.16.2）中命名的实例构造函数。
- 通过 `element_access`（§12.8.11）调用索引器访问器。
- 调用表达式中引用的预定义或用户定义运算符（§12.4.4 和 §12.4.5）。

这些上下文各自以独特的方式定义候选函数成员集合和参数列表。例如，方法调用的候选集不包含标记为 override 的方法（§12.5），并且如果派生类中有任何方法适用，则基类中的方法不作为候选（§12.8.9.2）。

一旦确定了候选函数成员和参数列表，最佳函数成员的选择在所有情况下都是相同的：

- 首先，将候选函数成员集合缩减为相对于给定参数列表适用的那些函数成员（§12.6.4.2）。如果缩减后的集合为空，则发生编译时错误。
- 然后，从适用的候选函数成员集合中找出最佳函数成员。如果该集合只包含一个函数成员，则该函数成员就是最佳函数成员。否则，最佳函数成员是相对于给定参数列表优于所有其他函数成员的那个函数成员，前提是每个函数成员都使用 §12.6.4.3 中的规则与其他所有函数成员进行比较。如果不存在恰好一个优于所有其他函数成员的函数成员，则函数成员调用具有歧义，并发生绑定期错误。

以下子条款定义了术语“适用的函数成员”和“更好的函数成员”的确切含义。

### 12.6.4.2 适用的函数成员

当以下所有条件都成立时，称函数成员相对于参数列表 A 是适用的函数成员：

- A 中的每个实参对应于函数成员声明中的一个参数，如 §12.6.2.2 所述，每个参数最多对应一个实参，且没有实参对应的任何参数均为可选参数。
- 对于 A 中的每个实参，该实参的参数传递模式与相应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，存在从实参表达式到相应参数类型的隐式转换（§10.2），或者
  - 对于 ref 或 out 参数，实参表达式（如果有）的类型与相应参数的类型之间存在恒等转换
  - 对于 in 参数，当相应实参具有 in 修饰符时，实参表达式（如果有）的类型与相应参数的类型之间存在恒等转换
  - 对于 in 参数，当相应实参省略 in 修饰符时，存在从实参表达式到相应参数类型的隐式转换（§10.2）。

对于包含参数数组的函数成员，如果该函数成员通过上述规则适用，则称其以其正常形式适用。如果包含参数数组的函数成员在其正常形式下不适用，则该函数成员可能以其展开形式适用：

- 展开形式是通过将函数成员声明中的参数数组替换为该参数数组元素类型的零个或多个值参数来构造的，以使参数列表 A 中的实参数量与参数总数匹配。如果 A 的实参数量少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个实参，以下条件之一成立，则展开形式适用：
  - 实参的参数传递模式与相应参数的参数传递模式相同，并且
    - 对于固定值参数或由展开创建的值参数，存在从实参表达式到相应参数类型的隐式转换（§10.2），或者
    - 对于 in、out 或 ref 参数，实参表达式的类型与相应参数的类型相同。
  - 实参的参数传递模式为 value，相应参数的参数传递模式为 input，并且存在从实参表达式到相应参数类型的隐式转换（§10.2）

当从实参类型到 in 参数类型的隐式转换为动态隐式转换（§10.2.10）时，结果未定义。

示例：给定以下声明和方法调用：

```csharp
public static void M1(int p1) { ... }
public static void M1(in int p1) { ... }
public static void M2(in int p1) { ... }
public static void Test()
{
    int i = 10; uint ui = 34U;

    M1(in i);    // M1(in int) is applicable
    M1(in ui);   // no exact type match, so M1(in int) is not applicable
    M1(i);       // M1(int) and M1(in int) are applicable
    M1(i + 5);   // M1(int) and M1(in int) are applicable
    M1(100u);    // no implicit conversion exists, so M1(int) is not applicable

    M2(in i);    // M2(in int) is applicable
    M2(i);       // M2(in int) is applicable
    M2(i + 5);   // M2(in int) is applicable
}
```

