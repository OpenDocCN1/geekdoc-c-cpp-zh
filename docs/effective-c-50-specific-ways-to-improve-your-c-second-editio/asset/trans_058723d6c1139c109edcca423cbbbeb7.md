
# 条款 10：使用可选参数以最小化方法重载

用途。命名参数与可选参数配合使用，可减少许多 API 周围的噪音，尤其是在 Microsoft Office 的 COM API 中。这段小代码片段创建了一个 Word 文档并插入少量文本，使用经典的 COM 方法：

```
var wasted = Type.Missing;
var wordApp = new Microsoft.Office.Interop.Word.Application();
wordApp.Visible = true;
Documents docs = wordApp.Documents;

Document doc = docs.Add(ref wasted, ref wasted, ref wasted, ref wasted);

Range range = doc.Range(0, 0);

range.InsertAfter("Testing, testing, testing. . .");
```

这段小而可以说无用的片段使用了四次 Type.Missing 对象。任何 Office Interop 应用程序在应用程序中都会使用更多数量的 Type.Missing 对象。这些实例会 clutter 你的应用程序并隐藏你正在构建的软件的实际逻辑。

这种额外的噪音是 C# 语言中添加可选和命名参数的主要驱动因素。可选参数意味着这些 Office API 可以为所有使用 Type.Missing 的位置创建默认值。这简化了甚至这段小片段：

```
var wordApp = new Microsoft.Office.Interop.Word.Application();
wordApp.Visible = true;
Documents docs = wordApp.Documents;

Document doc = docs.Add();

Range range = doc.Range(0, 0);

range.InsertAfter("Testing, testing, testing. . .");
```

即使是这种小的改动也提高了这段片段的可读性。当然，你可能并不总是想使用所有默认值。而且，你仍然不想在中间添加所有 Type.Missing 参数。假设你想创建一个新的网页而不是新的 Word 文档。那是 Add() 方法中四个参数中的最后一个。使用命名参数，你可以只指定最后一个参数：

```
var wordApp = new
    Microsoft.Office.Interop.Word.Application();
wordApp.Visible = true;
Documents docs = wordApp.Documents;

object docType = WdNewDocumentType.wdNewWebPage;
Document doc = docs.Add(DocumentType : ref docType);

Range range = doc.Range(0, 0);

range.InsertAfter("Testing, testing, testing. . .");
```

命名参数意味着在任何具有默认参数的 API 中，你只需要指定你打算使用的那些参数。它比多个重载更简单。事实上，对于四个不同的参数，你需要创建 15 个不同的 Add() 方法重载才能达到命名和可选参数提供的同等灵活性。请记住，其中一些 Office API 拥有多达 16 个参数，可选和命名参数是很大的帮助。

我在参数列表中保留了 ref 装饰器，但在 COM 场景中，C# 4.0 中的另一个更改使它成为可选的。这是因为 COM 通常按引用传递对象，因此几乎所有参数都按引用传递，即使它们没有被调用的方法修改。事实上，Range() 调用按引用传递值 (0,0)。我没有在那里包含 ref 修饰符，因为那样会明显具有误导性。事实上，在大多数生产代码中，我也不会在对 Add() 的调用上包含 ref 修饰符。我在上面这样做是为了让你可以看到实际的 API 签名。

当然，仅仅因为命名和可选参数的理由是 COM 和 Office API，并不意味着你应该将它们的使用限制在 Office 互操作应用程序中。事实上，你不能。调用你 API 的开发人员可以使用命名参数装饰调用位置，无论你是否希望他们这样做。

这个方法：

```
private void SetName(string lastName, string firstName)
{
```

// elided
}
```

可以使用命名参数调用以避免对顺序的任何混淆：

```
SetName(lastName: "Wagner", firstName: "Bill");
```

注释参数名称可确保以后阅读此代码的人不会怀疑参数是否按正确顺序排列。开发人员在添加名称会提高某人试图阅读的代码的清晰度时，就会使用命名参数。只要你使用包含多个相同类型参数的方法，在调用站点命名参数就会使你的代码更具可读性。

更改参数名称以一种有趣的方式表现为破坏性更改。参数名称仅在调用站点存储在 MSIL 中，而不在调用站点存储。你可以更改参数名称并发布组件，而不会破坏现场的任何组件用户。在客户端程序集将继续正确运行。参数名称已更改。

更改默认值也需要调用者重新编译以获取这些更改。如果你编译你的程序集并将其作为补丁发布，所有现有调用者将继续使用之前的默认参数。

当然，你也不想惹使用你组件的开发人员生气。为此原因，你必须将参数名称视为组件公共接口的一部分。更改参数名称将在编译时破坏客户端代码。

此外，添加参数（即使它们具有默认值）将在运行时破坏。 可选参数以与命名参数类似的方式实现。调用站点将包含 MSIL 中的注释，反映默认值的存在，以及这些默认值是什么。调用站点将这些值替换为调用者未明确指定的任何可选参数。

因此，添加参数，即使它们是可选参数，也是运行时破坏性更改。如果它们具有默认值，则不是编译时破坏性更改。

现在，经过那番解释，指导应该更清晰了。对于你的初始发布，使用可选和命名参数来创建用户可能想要使用的任何组合重载。然而，一旦你开始创建未来版本，你必须为额外参数创建重载。这样，现有客户端应用程序仍将正常运行。此外，在任何未来版本中，避免更改参数名称。它们现在是你的公共接口的一部分。

# 条款 11：理解小函数的吸引力

作为经验丰富的程序员，无论我们在 C# 之前偏爱哪种语言，我们都内化了几种用于开发更高效代码的实践。有时在我们之前的环境中有效的做法在 .NET 环境中会适得其反。当你尝试为 C# 编译器手工优化算法时，这一点非常正确。你的操作通常会阻止 JIT 编译器进行更有效的优化。你以性能为名所做的额外工作实际上会生成更慢的代码。你最好编写你能创建的最清晰的代码。让 JIT 编译器做其余的工作。过早优化导致问题的最常见例子之一是当你创建更长、更复杂的函数以期避免函数调用时。诸如将函数逻辑提升到循环体中之类的实践实际上会损害你的 .NET 应用程序的性能。这违反直觉，所以让我们回顾所有细节。

.NET 运行时调用 JIT 编译器将 C# 编译器生成的 IL 翻译成机器代码。此任务在你的程序执行生命周期中摊销。不是 JIT 编译你的整个应用-

