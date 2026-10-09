

当指定条件为真时，你也可以重新抛出异常，如下面的示例所示。

```csharp
catch (InvalidCastException e)
{
    if (e.Data == null)
    {
        throw;
    }
    else
    {
        // 执行某些操作。
    }
}
```

![](img/25af69ec45b3c0b589a8dccd0c2a88be_557_0.png)

也可以使用异常过滤器来以通常更简洁的方式获得类似的结果（以及如本文档前文所述，不修改调用堆栈）。以下示例对于调用者的行为与上一个示例类似。当 `e.Data` 为 null 时，该函数将 `InvalidCastException` 抛回给调用者。

```csharp
catch (InvalidCastException e) when (e.Data != null)
{
    // 执行某些操作。
}
```

在 `try` 块内部，仅初始化在该块中声明的变量。否则，在执行完成之前可能会发生异常。例如，在以下代码示例中，变量 `n` 在 `try` 块内被初始化。尝试在 `try` 块外部通过 `Write(n)` 语句使用此变量将产生编译器错误。

```csharp
static void Main()
{
    int n;
    try
    {
        // 不要在这里初始化此变量。
        n = 123;
    }
    catch
    {
    }
    // 错误：使用未赋值的局部变量 'n'。
    Console.Write(n);
}
```

## async 方法中的异常

async 方法由 async 修饰符标记，通常包含一个或多个 await 表达式或语句。await 表达式将 await 运算符应用于 System.Threading.Tasks.Task 或 System.Threading.Tasks.Task<T>。

当控制流到达 async 方法中的 await 时，方法的进度将暂停，直到被等待的任务完成。当任务完成时，执行可以在方法中恢复。

应用 await 的已完成任务可能处于故障状态，因为返回该任务的方法中发生了未处理的异常。等待该任务会抛出异常。如果返回该任务的异步过程被取消，任务也可能最终处于取消状态。等待已取消的任务会抛出 OperationCanceledException。

要捕获异常，请在 try 块中等待任务，并在关联的 catch 块中捕获该异常。

任务可能处于故障状态，因为在被等待的 async 方法中发生了多个异常。例如，该任务可能是对 `System.Threading.Tasks.Task.WhenAll` 调用的结果。当你等待此类任务时，只能捕获其中一个异常，并且无法预测将捕获哪个异常。

### 两个 catch 块示例

在以下示例中，使用了两个 catch 块，并且首先捕获最具体的异常。

要捕获最不具体的异常，你可以将 `ProcessString` 中的 throw 语句替换为以下语句：`throw new Exception();`。

如果在示例中将最不具体的 catch 块放在前面，则会出现以下错误消息：`前一个 catch 子句已捕获此类型或其超类型 ('System.Exception') 的所有异常。`

## Using 指令 (using, using static)

using 指令有三种用途：

- 允许使用命名空间中的类型，从而无需限定该命名空间中类型的使用：

```csharp
using System.Text;
```

- 允许你访问类型的静态成员和嵌套类型，而无需使用类型名限定访问。

```csharp
using static System.Math;
```

- 为命名空间或类型创建别名。这被称为 *using 别名指令*。

```csharp
using Project = PC.MyCompany.Project;
```

`using` 关键字也用于创建 *using 语句*，这有助于确保像文件和字体这样的 `System.IDisposable` 对象得到正确处理。

### Using static 类型

你可以访问类型的静态成员，而无需使用类型名限定访问：

```csharp
using static System.Console;
using static System.Math;

class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```

### 备注

`using` 指令的范围限于其出现的文件。

`using` 指令可以出现在：

- 源代码文件的开头，在任何命名空间或类型定义之前。
- 任何命名空间中，但在该命名空间中声明的任何命名空间或类型之前。

否则，将生成编译器错误 [CS1529]。

创建 `using` 别名指令以便于将标识符限定于命名空间或类型。在任何 using 指令中，无论其之前有哪些 using 指令，都必须使用完全限定的命名空间或类型。不能在使用指令的声明中使用 using 别名。例如，以下代码将生成编译器错误：

```csharp
using s = System.Text;
using s.RegularExpressions; // 生成编译器错误。
```

创建 using 指令以使用命名空间中的类型，而无需指定命名空间。using 指令不会授予你访问指定命名空间内嵌套命名空间的权限。

命名空间分为两类：用户定义的和系统定义的。用户定义的命名空间是在你的代码中定义的命名空间。

using static 指令指定一个类型，你可以访问该类型的静态成员和嵌套类型而无需指定类型名称。其语法为：

```csharp
using static <fully-qualified-type-name>;
```

其中 fully-qualified-type-name 是类型名称，可以引用其静态成员和嵌套类型而无需指定类型名称。如果你不提供完全限定的类型名称（完整的命名空间名称加上类型名称），C# 将生成编译器错误 CS0246：找不到类型或命名空间名称 `type/namespace`（是否缺少 using 指令或程序集引用？）。

using static 指令适用于具有静态成员（或嵌套类型）的任何类型，即使它也有实例成员。然而，实例成员只能通过类型实例调用。

## Virtual 修饰符 (virtual)

`virtual` 关键字用于修饰方法、属性、索引器或事件声明，并允许在派生类中重写它。例如，任何继承此方法的类都可以重写该方法：

```csharp
public virtual double Area()
{
    return x * y;
}
```

虚成员的实现可以通过派生类中的重写成员更改。

### 备注

当调用虚方法时，将检查对象的运行时类型以查找重写成员。将调用最派生类中的重写成员，如果没有派生类重写该成员，则可能是原始成员。

默认情况下，方法是非虚的。你不能重写非虚方法。

不能将 `virtual` 修饰符与 `static`、`abstract`、`private` 或 `override` 修饰符一起使用。

虚属性类似于虚方法，除了声明和调用语法的差异外。

- 在静态属性上使用 `virtual` 修饰符是一个错误。
- 可以通过包含使用 `override` 修饰符的属性声明，在派生类中重写继承的虚属性。

## Void 关键字 (void)

使用 `void` 作为方法（或局部函数）的返回类型，以指定该方法不返回值。

你不能将 `void` 用作变量的类型。

## While 语句 (`while`)

`while` 语句执行语句或语句块，直到指定的布尔表达式求值为 `true`。由于该表达式在每次循环执行之前求值，`while` 循环执行零次或多次。这与 `do` 循环不同，后者执行一次或多次。

在 `while` 语句块内的任何位置，你都可以通过使用 `break` 语句退出循环。

你可以使用 `continue` 语句直接跳转到 `while` 表达式的求值处。如果表达式求值为 `true`，执行从循环中的第一个语句继续。否则，执行从循环后的第一个语句继续。

你还可以使用 `goto`、`return` 或 `throw` 语句退出 `while` 循环。

