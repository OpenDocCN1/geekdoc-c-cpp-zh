
## 空合并运算符 (??)

**空合并运算符**是一种简洁的表达方式，用于表示“如果此值为 null，则使用其他值”。其形式如下：

*expression1 ?? expression2*

空合并运算符也使用一种短路求值形式。如果 *expression1* 不为 null，其值即为运算结果，另一个表达式不会被求值。如果 *expression1* 求值为 null，则 *expression2* 的值即为运算结果。与条件运算符不同，空合并运算符是一个二元运算符。

示例 4.36 说明了空合并运算符的用法。

### 示例 4.36：空合并运算符

```csharp
string fileName = GetFileName();
// ...
string fullName = fileName ?? "default.txt";
// ...
```

在此示例中，我们使用空合并运算符，如果 `fileName` 为 null，则设置 `fullName` 为 "default.txt"。如果 `fileName` 不为 null，`fullName` 将直接被赋值为 `fileName` 的值。

空合并运算符可以很好地“串联”使用。例如，形式为 `x ?? y ?? z` 的表达式，如果 `x` 不为 null，则结果为 `x`；否则，如果 `y` 不为 null，则结果为 `y`；否则，结果为 `z`。也就是说，它从左到右选择第一个非 null 表达式，如果之前所有表达式都为 null，则使用最后一个表达式。

空合并运算符在 C# 2.0 版本中引入，与可空值类型同时出现。该运算符适用于可空值类型和引用类型的操作数。

- 6.0 入门

## 空条件运算符 (?.)

每当你对 null 值调用方法时，运行时将抛出 `System.NullReferenceException`，这几乎总是表明编程逻辑中存在错误。鉴于此模式的频率（即在调用成员之前检查是否为 null），C# 6.0 引入了 `?.` 运算符，即空条件运算符，如示例 4.37 所示。

### 示例 4.37：空条件运算符

```csharp
class Program
{
    static void Main(string[] args)
    {
        if (args?.Length == 0)
        {
            System.Console.WriteLine(
                "ERROR: File missing. "
                + "Use:\n\tfind.exe file:<filename>");
        }
        else
        {
            if (args[0]?.ToLower().StartsWith("file:")?
                false)
            {
                string fileName = args[0]?.Remove(0, 5);
                // ...
            }
        }
    }
}
```

空条件运算符在调用方法或属性之前（在示例 4.37 中是第一个 `args`，在本示例的第一个例子中是 `Length`），检查操作数是否为 null。逻辑上等价的显式代码如下（虽然在 C# 6.0 语法中，`args` 的值只会被求值一次）：

```csharp
(args != null) ? (int?)args.Length : null
```

空条件运算符特别方便的地方在于它可以串联。例如，如果你调用 `args[0]?.ToLower().StartsWith("file:")`，只有当 `args[0]` 不为 null 时，`ToLower()` 和 `StartsWith()` 才会被调用。当表达式串联时，如果第一个操作数为 null，表达式求值会被短路，调用链中后续的调用将不会发生。

但是，请小心，以免无意中遗漏额外的空条件运算符。例如，假设（在这种情况下是假设性的）`args[0]?.ToLower()` 也可能返回 null。在这种情况下，调用 `StartsWith()` 时会发生 `NullReferenceException`。这并不意味着你必须使用一连串的空条件运算符，而是你应该有意地处理逻辑。在此示例中，因为 `ToLower()` 永远不为 null，所以不需要额外的空条件运算符。

- 6.9

关于空条件运算符，需要重点注意的是，当它与返回值类型的成员一起使用时，它总是返回该类型的可空版本。例如，`args?.Length` 返回 `int?`，而不仅仅是 `int`。类似地，`args[0]?.ToLower().StartsWith("file:")` 返回 `bool?`（即 `Nullable<bool>`）。另外，由于 `if` 语句需要 `bool` 数据类型，因此必须在 `StartsWith()` 表达式后跟随空合并运算符（`??`）。

尽管这可能有点特别（与其他运算符的行为相比），但可空值类型的返回只在调用链的末端产生。因此，在 `Length` 上调用点（.）运算符允许调用 `int`（而不是 `int?`）的成员。然而，将 `args?.Length` 包裹在括号中——从而通过括号运算符优先级强制得到 `int?` 结果——将调用 `int?` 返回，并使 `Nullable<T>` 的特定成员（`HasValue` 和 `Value`）可用。

空条件运算符也可以与索引运算符结合使用，如示例 4.38 所示。

### 示例 4.38：与索引运算符一起使用的空条件运算符

```csharp
class Program
{
    public static void Main(string[] args)
    {
        // 注意：未验证 args?.Length
        string directoryPath = args?[0];
        string searchPattern = args?[1];
        // ...
    }
}
```

在此示例中，*args* 的第一个和第二个元素仅在其不为 null 时才被赋给相应的变量。如果为 null，则会被赋值为 null。

不幸的是，这个例子如果说不危险，至少也是天真的，因为空条件运算符给人一种虚假的安全感，暗示如果 *args* 不为 null，则元素必须存在。当然，事实并非如此：即使 *args* 不为 null，元素也可能不存在。此外，由于使用 *args*?.*Length* 检查元素数量可以验证 *args* 不为 null，因此在检查长度之后，你实际上从不需要在对集合进行索引时使用空条件运算符。

总之，如果索引运算符在索引不存在时抛出 *IndexOutOfRangeException*，你应该避免将空条件运算符与索引运算符结合使用。这样做会导致对代码有效性的虚假安全感。

## 进阶主题

### 结合委托利用空条件运算符

空条件运算符本身是一个很好的特性。然而，将其与委托调用结合使用，解决了自 C# 1.0 以来一直存在的 C# 痛点。请注意下面 *PropertyChanged* 事件处理程序在检查 null 值并最终触发事件之前，是如何被赋给局部副本 (*propertyChanged*) 的。这是在不运行风险的情况下调用事件的最简单的线程安全方式，即在检查 null 和触发事件之间发生事件取消订阅。不幸的是，这种方法不直观，开发人员经常忽略遵循此模式——结果是不一致地抛出 *NullPointerExceptions*。幸运的是，随着 C# 6.0 中引入空条件运算符，这个问题已经得到解决。

在 C# 6.0 中，委托值的检查从

```csharp
PropertyChangedEventHandler propertyChanged =
    PropertyChanged;
if (propertyChanged != null)
{
    propertyChanged(this,
        new PropertyChangedEventArgs(nameof(Name)));
}
```

变为简单地

```csharp
PropertyChanged?.Invoke(propertyChanged(
    this, new PropertyChangedEventArgs(nameof(Name))));
```

因为事件只是一个委托，所以通过空条件运算符和 `Invoke()` 调用委托的相同模式始终可行。

## 按位运算符 (`<<, >>, |, &, ^, ~`)

几乎所有编程语言都共用的一组额外运算符是用于操作二进制格式值的运算符：按位运算符。

### 初学者主题

### 位与字节

计算机内的所有值都表示为 1 和 0 的二进制格式，称为**二进制位（bits）**。位被分组为八个一组，称为**字节**。在一个字节中，每个后续位对应 $2$ 的幂次值，从右边的 $2^{0}$ 开始，向左移动到 $2^{7}$，如图 4.1 所示。

![](img/ef6a8a417630b222bfb3f3b949facff0_183_0.png)

在许多场景中，特别是处理低级或系统服务时，信息以二进制数据的形式检索。要操作这些设备和服务，你需要执行二进制数据操作。

