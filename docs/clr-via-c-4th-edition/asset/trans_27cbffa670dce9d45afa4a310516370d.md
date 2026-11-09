
```csharp
Device        = 0x00040,
Normal        = 0x00080,
Temporary     = 0x00100,
SparseFile    = 0x00200,
ReparsePoint  = 0x00400,
Compressed    = 0x00800,
Offline       = 0x01000,
NotContentIndexed = 0x02000,
Encrypted     = 0x04000,
IntegrityStream = 0x08000,
NoScrubData   = 0x20000
}
```

要判断文件是否隐藏，可执行如下代码。

```csharp
String file = Assembly.GetEntryAssembly().Location;
FileAttributes attributes = File.GetAttributes(file);
Console.WriteLine("Is {0} hidden? {1}", file, (attributes & FileAttributes.Hidden) != 0);
```

> **注意** Enum 类定义了一个 HasFlag 方法，如下所示。
>
> `public Boolean HasFlag(Enum flag);`
>
> 使用此方法，你可以像下面这样重写对 Console.WriteLine 的调用。
>
> `Console.WriteLine("Is {0} hidden? {1}", file, attributes.HasFlag(FileAttributes.Hidden));`
>
> 然而，由于以下原因，我建议你避免使用 HasFlag 方法：因为它接受一个 Enum 类型的参数，所以你传递给它的任何值都必须装箱，从而需要内存分配。

下面的代码演示如何将文件属性更改为只读和隐藏。

```csharp
File.SetAttributes(file, FileAttributes.ReadOnly | FileAttributes.Hidden);
```

正如 FileAttributes 类型所示，使用枚举类型来表示可组合的位标志集合很常见。然而，尽管枚举类型和位标志相似，但它们并不具有完全相同的语义。例如，枚举类型表示单个数值，而位标志表示一组位，其中一些位为开，一些位为关。

当定义用于标识位标志的枚举类型时，当然应为每个符号显式分配一个数值。通常，每个符号都会有一个单独的位被打开。也常见到名为 None 的符号被定义为值 0，你还可以定义表示常用组合的符号（参见下面的 ReadWrite 符号）。还强烈建议将 System.FlagsAttribute 自定义特性类型应用于该枚举类型，如下所示：

```csharp
[Flags]      // The C# compiler allows either "Flags" or "FlagsAttribute".
internal enum Actions {
    None      = 0,
    Read      = 0x0001,
    Write     = 0x0002,
    ReadWrite = Actions.Read | Actions.Write,
    Delete    = 0x0004,
    Query     = 0x0008,
    Sync      = 0x0010
}
```

因为 Actions 是枚举类型，所以在处理位标志枚举类型时，你可以使用上一节中描述的所有方法。然而，如果其中一些函数的行为稍有不同，那会更好。例如，假设你有以下代码。

```csharp
Actions actions = Actions.Read | Actions.Delete;   // 0x0005
Console.WriteLine(actions.ToString());              // "Read, Delete"
```

调用 ToString 时，它会尝试将数值转换为其对应的符号表示。该数值为 0x0005，没有对应的符号表示。然而，ToString 方法检测到 Actions 类型上存在 [Flags] 特性，现在 ToString 不再将该数值视为单个值，而是视为一组位标志。由于 0x0001 和 0x0004 位已设置，ToString 生成以下字符串：“Read, Delete”。如果从 Actions 类型中移除 [Flags] 特性，ToString 将返回“5”。

我在上一节讨论了 ToString 方法，并展示了它提供三种格式化输出的方式：“G”（常规）、“D”（十进制）和“X”（十六进制）。当你使用常规格式格式化枚举类型的实例时，首先会检查该类型是否应用了 [Flags] 特性。如果未应用此特性，则会查找并返回与数值匹配的符号。如果应用了 [Flags] 特性，ToString 的工作方式如下：

- 1. 获取枚举类型定义的一组数值，并按降序对这些数字排序。
- 2. 将每个数值与枚举实例中的值进行按位与运算；如果结果等于该数值，则将与该数值关联的字符串追加到输出字符串，并认为这些位已处理并将其关闭。重复此步骤，直到所有数值都已检查，或直到枚举实例的所有位都已关闭。
- 3. 如果检查完所有数值后，枚举实例仍不为 0，则说明该枚举实例有一些已打开的位不对应任何已定义符号。在这种情况下，ToString 会将枚举实例中的原始数字作为字符串返回。
- 4. 如果枚举实例的原始值不为 0，则返回包含逗号分隔符号集合的字符串。
- 5. 如果枚举实例的原始值为 0，且该枚举类型定义了对应值为 0 的符号，则返回该符号。
- 6. 如果执行到这一步，则返回“0”。

如果你愿意，也可以在不使用 [Flags] 特性的情况下定义 Actions 类型，并通过使用“F”格式仍然获得正确的字符串。

```csharp
// [Flags]    // Commented out now
internal enum Actions {
    None        = 0,
    Read        = 0x0001,
    Write       = 0x0002,
    ReadWrite = Actions.Read | Actions.Write,
    Delete      = 0x0004,
    Query       = 0x0008,
    Sync        = 0x0010
}

Actions actions = Actions.Read | Actions.Delete; // 0x0005
Console.WriteLine(actions.ToString("F"));       // "Read, Delete"
```

如果数值中有某一位无法映射到符号，则返回的字符串将仅包含一个表示原始数值的十进制数字；字符串中不会出现任何符号。

请注意，你在枚举类型中定义的符号不必是纯 2 的幂。例如，Actions 类型可以定义一个名为 All 的符号，其值为 0x001F。如果 Actions 类型的某个实例的值为 0x001F，格式化该实例将生成包含“All”的字符串。其他符号字符串不会出现。

到目前为止，我已经讨论了如何将数值转换为标志字符串。还可以通过调用 Enum 的静态 Parse 和 TryParse 方法，将逗号分隔的符号字符串转换为数值。下面是一些演示如何使用该方法的代码。

```csharp
// Because Query is defined as 8, 'a' is initialized to 8.
Actions a = (Actions) Enum.Parse(typeof(Actions), "Query", true);
Console.WriteLine(a.ToString());   // "Query"

// Because Query and Read are defined, 'a' is initialized to 9.
Enum.TryParse<Actions>("Query, Read", false, out a);
Console.WriteLine(a.ToString());   // "Read, Query"

// Creates an instance of the Actions enum with a value of 28
a = (Actions) Enum.Parse(typeof(Actions), "28", false);
Console.WriteLine(a.ToString());   // "Delete, Query, Sync"
```

调用 Parse 和 TryParse 时，内部会执行以下操作：

- 1. 移除字符串开头和末尾的所有空白字符。
- 2. 如果字符串的第一个字符是数字、加号（+）或减号（-），则假定该字符串是数字，并返回一个枚举实例，其数值等于将该字符串转换后的数值。
- 3. 将传入的字符串拆分为一组标记（以逗号分隔），并去除每个标记中的所有空白。

Nat. Commun. 14, 1234 (2023)

## 基于数据增强知识蒸馏的细粒度场景图生成

Yuyu Guo, Lianli Gao, Xuanhan Wang, Yuxuan Zhai, Xing Xu, Heng Tao Shen

电子科技大学计算机科学与工程学院

**摘要。** 场景图生成（SGG）旨在识别图像中的对象及其关系。尽管近期的 SGG 模型已取得显著进展，但其性能仍受谓词类别长尾问题的限制。为缓解该问题，我们提出了一种新颖的数据增强知识蒸馏框架。具体而言，我们首先通过从训练数据中提取高置信度关系三元组来构建知识库。然后，我们设计了一种知识引导的数据增强策略，为稀有谓词类别生成额外的训练样本。最后，我们采用教师-学生框架，将知识从复杂的教师模型迁移到轻量级学生模型。在 Visual Genome 数据集上的大量实验证明了我们方法的有效性，并达到了最先进的性能。

**关键词：** 场景图生成、知识蒸馏、数据增强、长尾问题

### 1 引言

近年来，场景图生成因其在图像描述、视觉问答和图像检索中的广泛应用而受到越来越多的关注。场景图提供了图像的结构化表示，其中节点对应对象边界框，边表示对象之间的成对关系。尽管取得了显著进展，现有 SGG 方法仍常常受到关系类别长尾分布的困扰：少数常见谓词主导训练数据，而许多其他谓词仅很少出现。

为应对这一挑战，一些工作尝试通过重采样或重加权策略重新平衡数据分布。然而，这些方法可能引入偏差或丢失重要信息。另一类研究侧重于利用外部知识源或引入语言先验，以提供额外的语义信息。尽管如此，这些方法通常需要额外标注或外部数据，限制了其适用性。

本文提出了一种新颖框架，结合数据增强与知识蒸馏来解决 SGG 中的长尾问题。我们的主要贡献可总结如下：

- 我们从训练集构建高置信度知识库，并设计知识引导的数据增强策略，为稀有谓词生成有效的训练样本。
- 我们提出教师-学生知识蒸馏框架，将增强后的知识迁移到紧凑的学生模型，在性能与效率之间取得良好平衡。
- 我们在 Visual Genome 数据集上进行大量实验，证明我们的方法显著优于现有 SGG 方法，尤其是在稀有谓词类别上。

### 2 相关工作

**场景图生成。** 早期 SGG 方法通常采用两阶段流程：先进行目标检测，再进行关系分类。近期工作引入了更复杂的架构，如图神经网络和基于 Transformer 的模型，以捕获上下文信息。然而，由于长尾分布，这些模型往往偏向于频繁谓词。

**知识蒸馏。** 知识蒸馏（KD）是一种有效的模型压缩技术，可将知识从大型教师模型迁移到小型学生模型。KD 已成功应用于多种任务，包括图像分类、目标检测和场景图生成。与现有基于 KD 的 SGG 方法不同，我们侧重于利用蒸馏知识增强训练数据本身，而不仅仅是对齐输出。

**数据增强。** 数据增强是一种广泛用于缓解数据稀缺的技术。在 SGG 背景下，少数工作探索了生成合成关系样本。然而，这些方法往往忽略对象与谓词之间的语义关联。我们的数据增强策略明确结合知识库，以生成更合理、更多样的样本。

### 参考文献

- [1] J. Johnson, R. Krishna, M. Stark 等. 使用场景图的图像检索. 载于 CVPR, 2015.
- [2] R. Krishna, Y. Zhu, O. Groth 等. Visual Genome：使用众包密集图像标注连接语言与视觉. 载于 IJCV, 2017.
- [3] D. Xu, Y. Zhu, C. B. Choy 等. 通过迭代消息传递进行场景图生成. 载于 CVPR, 2017.
- [4] G. Hinton, O. Vinyals, and J. Dean. 在神经网络中蒸馏知识. 载于 NeurIPS Workshop, 2014.

