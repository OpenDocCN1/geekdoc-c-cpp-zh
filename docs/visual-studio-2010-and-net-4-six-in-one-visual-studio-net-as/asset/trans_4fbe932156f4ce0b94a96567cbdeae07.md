
`OrdinaryClassificationDefinition` 类是一个非功能性类型定义，它仅用于表示分类类型的元数据。该类被定义为静态，正如其唯一的字段 `OrdinaryClassificationType` 一样，该字段装饰了 MEF 属性，这些属性定义了“普通”分类。

```
[Export(typeof(ClassificationDefinition))]
[Name("ordinary")]
```

`Export` 属性使用 `ClassificationDefinition` 类型作为其参数，用于标记符合分类类型契约的相应成员。当与编辑器组合扩展时，这是编辑器识别分类类型的契约。`Name` 属性是一个 MEF 元数据属性，它的值显然被视为分类类型的名称考虑在内。

> 如果该类是可实例化的且不是静态的，上述代码将可以工作，因为在这种情况下 MEF 也能发现分类类型契约。然而，将类设为静态传达了意图：“这是一个元数据类，请勿实例化它。”

# 分类器提供程序（Classifier Provider）与分类器（Classifier）

分类的核心元素是承担了大部分工作的分类器。分类器负责分析编辑器提供的文本跨度（text span），以识别其能够识别的任何分类类型。编辑器使用工厂模式通过分类器提供程序创建分类器的工作实例。这种模式使得分类器的实例化变得非常灵活，因为合适的分类器类型不是硬编码的，而可以在运行时决定，从而避免了分类器的必要的实例化。

这两个类都可以在列表 6-6所示的 `Classifier.cs` 文件中找到。

列表 6-6：Classifier.cs

```
using System;
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Windows.Media;
using Microsoft.VisualStudio.Text;
using Microsoft.VisualStudio.Text.Classification;
using Microsoft.VisualStudio.Utilities;

namespace FileAssocClassifier
{
    #region Provider definition
    <summary>
```

# 列表 6-6（续）

```
/// 此类导致分类器被添加到分类器集合中。由于
/// 内容类型被设置为 "text"，因此该分类器适用于所有文本文件
/// </summary>
[Export(typeof(IClassifierProvider))]
[ContentType("text")]
internal class OrdinaryClassifierProvider : IClassifierProvider
{
    /// <summary>
    /// 导入分类注册表，以便稍后获取自定义分类类型的引用
    /// </summary>
    [Import]
    internal IClassificationRegistryService ClassificationRegistry = null;
    /// 返回分类器的实例
    public IClassifier GetClassifier(ITextBuffer buffer)
    {
        return buffer.Properties.GetOrCreateSingletonProperty<IOrdinaryClassifier>(
            delegate { return new OrdinaryClassifier(ClassificationRegistry); });
    }
}
#endregion provider def

#region Classifier
/// <summary>
/// 将所有文本分类为 OrdinaryClassifierType 实例实例的分类器
/// </summary>
class OrdinaryClassifier : IClassifier
{
    #pragma warning disable 67
    // 此事件在当非文本更改会以某种方式影响分类时触发。
    // 例如，在 C# 中输入 / 会导致分类发生变化，
    // 而不会直接影响该跨度。
    public event EventHandler<ClassificationChangedArgs> ClassificationChanged;
    #pragma warning restore 67

    IClassificationType _classificationType;
    internal OrdinaryClassifier(IClassificationRegistryService registry)
    {
        _classificationType = registry.GetClassificationType("ordinary");
    }

    /// <summary>
    /// 此方法扫描给定的快照跨度（SnapshotSpan），以查找此分类的潜在匹配
    /// 在此实例，它分类所有内容并将每个跨度作为一个新的
    /// ClassificationSpan 返回
    /// </summary>
    /// <param name="trackingSpan">当前正在分类的跨度</param>
```

```
/// <returns>
/// 一个表示被识别为此类分类的跨度的 ClassificationSpan 列表
/// </returns>
public IList<ClassificationSpan> GetClassificationSpans(SnapshotSpan span)
{
    // 创建一个列表来存储结果
List<ClassificationSpan> classifications = new List<ClassificationSpan>();
classifications.Add(new ClassificationSpan(new SnapshotSpan(span.Snapshot,
new Span(span.Start, span.Length)),
    _classificationType));

    return classifications;
}

#endregion //Classifier
```

代码文件 `[Classifier.cs]` 可在 Wrox.com 下载。

`OrdinaryClassifierProvider` 扮演着分类器提供程序的角色，正如其名称所暗示。编辑器根据其定义将其识别为一个提供程序：

```
[Export(typeof(IClassifierProvider))]
[ContentType("*")]
internal class OrdinaryClassifierProvider : IClassifierProvider
{
    // ...
```

契约是由 `IClassifierProvider` 类型作为 `Export` 属性的参数定义的，类必须实现此接口，因为它包含了分类器提供程序的职责。`ContentType` 属性指定该提供程序到 "text" 内容类型。由于 "text" 是分类的根，它可以应用于 C#、XML 等等。

编辑器使用分类注册表，因为分类器将使用该服务。以下声明提供了该服务的访问方式：

```
[Import]
internal IClassificationRegistryService ClassificationRegistry = null;
```

正如你所见，这在实例化时初始化。这是 MEF 再次出现的地方。在组合阶段，MEF 将实例化 `OrdinaryClassifier` 并使用相应的实例初始化 `ClassificationRegistry` 字段。当需要使用分类器时，编辑器首先通过调用 `GetClassifier` 方法转向分类器提供程序，并将文本缓冲区传递给该方法。缓冲区跟踪其 `Properties`，其中以 `OrdinaryClassifier` 为键存储了实例，`GetClassifier` 方法体只需查询缓冲区中的该实例，如果找不到，则使用指定的委托进行实例化。

```
return buffer.Properties.GetOrCreateSingletonProperty<OrdinaryClassifier>(delegate => return new OrdinaryClassifier(ClassificationRegistry));
```

第一次调用 `GetOrCreateSingletonProperty` 执行实例化，并将分类器实例存储在属性中。任何后续调用都将从属性中返回分类器。

> 注意，分类注册表实例被传递给分类器的构造函数。

现在，让我们关注负责分类跨度的 `OrdinaryClassifier` 类。该类实现 `IClassifier` 接口，定义了 `ClassificationChanged` 事件和 `GetClassificationSpans` 方法。实现的核心是该接收一个不可变的文本跨度（作为 SnapshotSpan 实例）并提供描述可以如何分类的 ClassificationSpan 对象列表。

模板的默认实现在结果列表中创建一个输入文本的全跨度，声明为“普通”分类：

```
public IList<ClassificationSpan> GetClassificationSpans(SnapshotSpan span)
{
    classifications = new List<ClassificationSpan>();
    classifications.Add(new ClassificationSpan(new SnapshotSpan(span.Snapshot), new Span(span.Start, span.Length)), _classificationType);
    return classifications;
}
```

“普通”分类由类构造函数中的 `ClassificationType` 字段表示。构造函数使用了你传递提供程序的分类注册表实例。

```
internal OrdinaryClassifier(IClassificationRegistryService registry)
{
    _classificationType = registry.GetClassificationType("ordinary");
}
```

正如你看到的，分类器非常简单。另一个尚未提到的细节是 `ClassificationChanged` 事件。当某些文本跨度外的更改可能会影响该文本跨度的分类时，就会触发此事件。一个很好的例子是使用 C# 注释块标记（/*）。该标记之后的所有文本可能会更改语言元素，如
