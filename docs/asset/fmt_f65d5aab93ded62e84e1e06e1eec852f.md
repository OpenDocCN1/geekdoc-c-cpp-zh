
代码的逻辑显而易见，不需要任何注释。在这种情况下，仅需一句话描述特定方法的目的和概括想法就足够了。

为了编写有效的注释，尽可能使用伪代码。注释应该在编写代码时编写，而不是之后。效率（即快速编写代码）永远不是不写注释的良好理由。任何明显糟糕的内容都应该记录。编写过多不必要的注释同样糟糕。

坏代码无法通过增加注释来改进，而应该重写或重构。

# C# 中的 XML 文档

你可能已经注意到了代码中解释类或方法目的及其参数的特殊注释：

## C# 内置的计算机编程基础

这种内置在 C# 源代码中的特殊文档样式被称为 XML 文档。它被包含在三斜注释 `///` 中，并使用特殊的 XML 标签：用于记录类型/方法的摘要 `<summary>`、描述方法的返回值 `<returns>`、记录最终可能抛出的异常 `<exception cref="...">`、为链接的类型创建交叉引用链接 `<seealso cref=".../">`、描述某些备注 `<remarks>` 以及提供如何使用该类型/方法的示例 `<example>`。

在代码中使用 XML 文档样式有几个优点：

- `XML` 文档内置在源代码本身中。
- `XML` 文档由 `Visual Studio` 自动处理并在其自动补全功能中显示。
- 可以通过像 `Sandcastle` (`http://shfb.codplex.com`) 这样的专用工具将 `XML` 文档编译成 `MSDN` 风格的网站或电子书（`CHM` 格式）。

关于编写和使用文档的更多信息可以在 `MSDN` 库中找到：`http://msdn.microsoft.com/en-us/library/b2s063f7.aspx`。

## 代码重构

“重构”出现于 1993 年，并由 `Martin Fowler` 在他的同名书籍中普及。该书回顾了许多代码重构的技术（称为重构模式）。我们将提到其中一些。

当出现代码重复时，程序就需要进行重构。代码重复是危险的，因为一一处的更改需要所有其他重复的代码也随之更改。后者很容易出错，因此可能会产生不一致性。可以通过将特定的代码段放入方法中或通过将公共功能移动到基类来避免代码重复。

对于随着时间推移而变得复杂的方法，重构是必要的。方法过长是考虑在逻辑上将其拆分为几个更小、更简单的方法的好理由。

深度嵌套的结构是另一个重构的理由。可以通过将代码块提取到方法中消除它们。

没有提供足够抽象级别或执行无关任务（低内聚性）的类也是重构的候选对象。

长参数列表和公共字段也应该进入修复列表。紧密耦合的类也属于同一大类。

## 第 21 章 高质量编程代码

### 数据层面的重构

良好的做法是避免散落在整个代码中的魔数字。它们应该被命名的常量所取代。名称不清晰的变量应该重命名。长条件表达式可以重构为单独的方法。可以使用变量来保存表达式的中间结果。一组总是一起出现的数据可以重构为一个单独的类。相关的常量应该分组枚举。

### 方法和类层面的重构

在一个较长的方法中，所有与其主要目的无关的任务应该移动到单独的方法中。相似的任务应该在公共类中分组，相似的类放在公共包中。如果一组类具有公共功能，应移动到基类中。

类之间不应存在循环依赖，应该将其移除。在大多数情况下，更常见的类拥有更专门类的引用（父子关系）。

## 单元测试

单元测试意味着编写一个测试特定方法或类的程序。典型的单元测试执行被测试的方法，传递示例数据（参数和对象状态），并检查方法的结果对于该示例数据是否正确，即方法是否执行了它应该执行的操作以及是否执行得正确。

一个方法通常由多个单元测试测试，每个测试实现一个不同的测试场景。首先检查典型情况。边界情况是可能需要特殊处理的特殊情况，例如最大或最小值、第一个或最后一个元素。最后，使用错误数据对方法进行测试，并预期会抛出异常。有时可能涉及性能测试，以检查方法是否足够快。

## 单元测试 – 示例

让我们来看一个简单的示例——一个对数字数组的方法：

```csharp
static int Sum(int[] numbers)
{
    int sum = numbers[0];
    for (int i = 1; i < numbers.Length; i++) {
        sum += numbers[i];
    }
    return sum;
}
```

上面的方法看起来可能是正确的，但它内部有几个可以通过单元测试发现的 bug。让我们测试典型情况：

```csharp
if (Sum(new int[] {1, 2}) != 3)
    throw new Exception("1 + 2 != 3");
```

看来 `Sum(...)` 方法在它的典型情况下运行正常：`1+2` 的之和为 `3`（符合预期），且代码没有输出。单元测试针对测试场景对特定方法、类或其他功能进行测试，并在代码出现异常行为时通知。如果测试通过，代码不会产生输出。

现在我们来测试边界情况。如果我们只加一个数字会发生什么？让我们尝试：

```csharp
if (Sum(new int[] {1}) != 1)
    throw new Exception("Sum of 1 != 1");
```

看来我们的方法仍然正常工作。让我们尝试对空数字列表求和。应该是 `0` 对吧？让我们尝试这个：

```csharp
if (Sum(new int[] {}) != 0)
    throw new Exception("Sum of 0 numbers != 0");
```

上面的代码在 `Sum(...)` 方法中产生了意外之外的异常：`System.IndexOutOfRangeException: Index was out of bounds of the array`。

我们发现了一个 bug，让我们修复它。我们可以从 `0` 开始而不是从第一个元素开始。以下是修复代码：

```csharp
static int Sum(int[] numbers)
{
    int sum = 0;
    for (int i = 0; i < numbers.Length; i++)
    {
        sum += numbers[i];
    }
    return sum;
}
```

## 第 21 章 高质量代码

单元测试允许在重构代码时无需担心某些功能损坏。可能会出现这种情况：你在重构代码以提高其质量时，意外导致代码在所有情况下都无法正常工作。所有严肃的软件开发公司和软件产品都会使用单元测试。例如，如果你下载 `Firefox` 的源代码，你会发现一半的代码是用于执行单元测试的。在实践中，如果没有单元测试，编写复杂的产品（例如 `MS Word`、`Android` 或 `Firefox` 浏览器）是不可能的。

## 单元测试的优势

让我们来看看单元测试的优势之一：能够更改方法的内部实现并重新测试以确保新实现正常工作。考虑以下使用 `System` 的 `Sum` 方法的新实现：

```csharp
using System;
using System.Linq;
static long Sum(int[] numbers)
{
    return numbers.Sum();
}
```

我们将在下一章“Lambda 表达式和 LINQ”中解释上述代码的工作原理。现在来测试以确保这段代码的行为符合预期。如果我们运行上面讨论的相同组测试，我们会发现问题：有两个测试无法工作。第一个失败的测试是：

```csharp
if (Sum(new[] { 2000000000, 2000000000 }) != 4000000000)
    throw new Exception("4000000000");
```

我们在 `Sum` 方法的新实现中发现了一个 错误：它没有返回正确的结果，而是产生了 `System.OverflowException`。我们无法为这个问题找到简单的解决方案，要么可以假设不支持大数求和并修改测试以期望 `Overflow`，要么可以使用新的实现重写 `Sum` 方法。

如果我们继续进行，还会发现另一个测试失败了：当我们尝试求和一个空数组时，我们将得到 `System.ArgumentNullException` 而不是 `NullReferenceException`。通过修改单元测试可以很容易修复：

```csharp
try
{
    Sum(null);
    // 预期产生异常 -> 测试失败
    throw new Exception("Null array cannot be summed.");
}
catch (ArgumentNullException)
{
    // 预期 NullReferenceException -> 测试失败
}
```

现在所有单元测试都正常工作了。上述经验得出的结论是：当我们修改代码且单元测试失败时，要么是被测试的代码是不正确的，要么是单元测试是不正确的。在两种情况下，我们都收到了新代码行为与旧代码不同的通知。这在软件工程过程中非常重要。当我们开发复杂的软件产品时，我们希望当前版本中正常的功能在所有后续版本中继续有效。例如，如果我们开发 `MS Word` 并为下一个版本添加 `PDF` 导出功能，我们希望在引入 `PDF` 导出后保存 `DOCX` 格式依然可用。

## 单元测试框架和工具

为了简化测试编写，许多单元测试框架和工具应运而生。在 `C#` 中，我们可以使用 `Visual Studio Test` (`VSTST`) 或 `JUnit` 框架来简化编写测试、断言测试条件以及执行测试用例集的过程。

## 使用 Visual Studio Test (VSTST) 进行单元测试

如果你安装了支持单元测试的 `Visual Studio 2010` 版本（例如 `Visual Studio 2010 Ultimate`），当你右键点击 `C#` 代码中的某个方法时，会在弹出菜单中看到 [ 创建单元测试 ... ]：

```csharp
public class Sumator
{
    static long Sum(int[] numbers)
    {
        long sum = 0;
        for (int i = 0; i < numbers.Length; i++)
        {
            sum += numbers[i];
        }
        return sum;
    }
}
```

上述功能在 `VS 2010` 中引入，但由于未知原因在 `VS 2012` 中缺失了。因此，如果你在使用 `Visual Studio 2012`，你需要手动创建一个单元测试项目（文件 -> 新项目 -> 单元测试项目）。`Visual Studio Test` 中的单元测试如下：

```csharp
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class SumatorTest
{
    [TestMethod]
    public void SumTestTypicalCase()
    {
        int[] numbers = new int[] { 1, 2 };
        long expected = 3;
        long actual = Sumator_Accessor.Sum(numbers);
        Assert.AreEqual(expected, actual);
    }

    [TestMethod]
    public void TestOverflow()
    {
        int[] numbers = new int[] { 2000000000, 2000000000 };
        long expected = 4000000000;
        long actual = Sumator_Accessor.Sum(numbers);
        Assert.AreEqual(expected, actual);
    }

    [TestMethod]
    [ExpectedException(typeof(NullReferenceException))]
    public void SumTestNullArray()
    {
        Sumator_Accessor.Sum(null);
    }
}
```
