

## 4.5 控制提示

由于您现在只有一个参数，以下两个命令行都是有效的：

```
helloworld -message "Hello World!" message.dat
helloworld message.dat -message "Hello World!"
```

现在如果您在命令行中未指定消息文本，即您只输入：

```
helloworld message.dat
```

那么 message.dat 将被视为一个参数，并被当作输出文件名。程序随后会提示您输入要打印的字符串。这接近我们想要的，但仍不完全是期望的行为。我们希望它能直接使用默认字符串运行。

### 4.5.4 默认值

您可以使用 default: 属性为大多数数据定义关联默认值。ACD 可以修改如下：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]
string: message
[
    standard: "Y"
    default: "Hello World!"
]
outfile: outfile
[
    parameter: "Y"
]
```

现在如果您输入：

```
helloworld message.dat
```

那么，尽管您指定了默认值，它仍在提示输入值。请记住，标准数据定义的所有值始终会被提示输入，无论是否指定了默认值。您需要将 message 指定为“附加”或“高级”限定符，这些通常不会被提示输入。

ACD 文件将如下所示：

```
application: helloworld
[
    documentation: "Prints something arguably uninteresting"
]
string: message
[
  additional: "Y"
  default: "Hello World!"
]
outfile: outfile
[
  parameter: "Y"
]
```

这个 ACD 终于实现了所需功能。输入：

```
helloworld message.dat
```

将把 Hello World! 打印到文件 message.dat 中，即期望的行为。
当然，您也可以通过在命令行中指定消息来覆盖默认消息：

```
helloworld -message "Goodbye World!" message.dat
```

这将向输出文件打印一条相当令人不快的消息。对于附加和高级 ACD 数据定义，您通常应提供默认值，因为如果您未在命令行中指定值，EMBOSS 不会提示您输入。如果您尝试在 C 源代码中访问未指定数据项的值，EMBOSS 会生成错误。相比之下，标准和参数数据定义的值如果未在命令行中指定，始终会被提示输入，因此默认值有用但非必需。

### 注意

请注意，某些数据类型（如 boolean）具有内置默认值。

### 4.5.5 最大值和最小值

为 ACD 数据类型定义设置最大值和/或最小值限制通常很有用，甚至至关重要。这是通过使用 minimum 和 maximum 属性以直观的方式完成的：

```
integer: window
[
  standard: "Y"
  default: "10"
  minimum: "5"
  maximum: "100"
]
```

### 4.5.6 设置提示

EMBOSS 始终会提供默认提示文本。请考虑以下 ACD 文件：

```
integer: window
[
 standard: "Y"
 default: "10"
 minimum: "5"
 maximum: "100"
]
```

用户将按以下方式被提示：

```
-window : Enter a number [10] :
```

虽然足够，但这并不十分友好。您可以使用 information: 属性为数据类型定义设置提示。ACD 文件将如下所示：

```
integer: window
[
 standard: "Y"
 default: "10"
 minimum: "5"
 maximum: "100"
 information: "Window size"
]
```

这将给出以下提示。

```
Window size [10]:
```

这要有意义得多。

### 4.5.7 否定

迄今为止，您只在参数或限定符定义后描述了值 "Y"。然而，否定（间接指定值 "N"）在 ACD 文件中常有用处。举个简单的例子：

```
sequence: sequence
[
 parameter: "Y"
]
```

```
integer: n
[
    standard: "@($(sequence.length) > 100)"
]
```

如果序列长度大于 100，standard: 属性将被设置为 "Y"，否则设置为 "N"。虽然值 "N" 不应在 parameter:、standard: 或 additional: 后显式指定，但计算结果为 "N" 的计算值实际上对限定符（而非参数）是支持的。在这种情况下，"N" 会覆盖属性的默认行为，使得提示输入值被关闭。这在某些情况下很有用。在此示例中，计算仅在序列长度大于 100 时才会打开提示。

现在假设您的应用程序可以生成图形和文本输出。进一步假设，您只有在用户未选择图形输出时才希望获得文本输出。首先，您将按如下方式设置一个切换 ACD 数据类型定义：

```
toggle: plot
[
    standard: "Y"
    default: "N"
    information: "Plot a graph"
]
```

如果用户在命令行中添加 -plot，$(plot) 的值将为 "Y"。如果用户未在命令行中添加任何内容，或者用户添加了 -noplot，则值为 N。

输出文件现在可以定义为：

```
outfile: outfile
[
    standard: "@(!$plot)"
]
```

仅当 plot 为假时，这才等同于 standard: "Y"。否定运算符 (!) 是一个计算，因此该项必须用 @() 包围。

这唯一令人遗憾的是，它按原样写无法工作，但这与逻辑无关。原因是 EMBOSS 处理文件输入/输出操作的方式与其他数据类型不同。如果它看到文件（例如 outfile）或序列（例如 seqout）定义，它将始终尝试打开它。

如果该项等同于 standard: "N"，且命令行或默认值中未指定文件名（您通常不会为输出文件指定默认名称），则 ACD 解析将尝试打开一个无名文件。这将导致错误。

绕过此问题的方法是使用 nullok: 属性。因此，一个可行的 outfile 定义是：

```
outfile: outfile
[
  standard: "@(!$plot)"
  nullok: "Y"
]
```

上面的 nullok: 属性表示，如果未给出文件名，则可以继续（不生成错误）。

> **注意**
> 
> 如果您运行一个 ACD 文件（例如，使用 acdc（第 4.6.4.1 节，‘acdc’）进行测试，并为 standard: 使用计算值），您将看到一条警告消息。以这种方式使用计算是受支持的，但仅在绝对必要时才推荐。这是因为这可能会使 ACD 文件的理解变得混乱，例如，第三方界面可能会感到困惑。

> **警告**
> 
> 计算 *不应* 用于设置参数的值：如果这样做，在 ACD 处理期间将生成错误。参数被视为应用程序的必要输入。相比之下，计算可以用于控制限定符（无论是标准、附加还是高级）的提示输入。

### 4.5.8 布尔数据类型

ACD 语法提供了两种具有布尔值的数据类型（boolean 和 toggle）。boolean 是标准布尔数据类型，而 toggle 是一种特殊的布尔数据类型，专门用于控制其他属性的提示输入。

以下 ACD 文件展示了一个带有两个参数和一个高级限定符（abool，布尔数据类型）的应用程序。abool 可能会被用来设置输出文件中的详细或简洁文本，尽管它会被赋予一个更直观的名称。

```
application: seqdemo
[
  documentation: "Demo application."
]

sequence: asequence
[
  parameter: "Y"
]

boolean: abool
[
  default: "Y"
]

outfile: outfile
[
  parameter: "Y"
]
```

应用程序可以以以下任一方式调用：

```
seqdemo filename.seq filename.out -abool
seqdemo filename.seq filename.out -noabool
```

在第一个示例中，布尔限定符 abool 被设置为 True。实际上，该值无需显式设置，因为默认值为 True。在第二个命令行中，abool 通过前缀 no 被设置为 False。

### 4.5.8.1 提示布尔值

为布尔数据类型定义 information: 和 help: 全局属性时应小心。这些属性用于提示用户（交互式或通过 GUI）并提供帮助文本。每种情况下提供的文本都应反映布尔选项的预期默认值，这可能与名称所暗示的相反。例如，如果默认设置为 “Y”，则命令行选项通常为 -noFlag，其中 Flag 是限定符。如果默认设置为 “N”，则默认操作可能与信息或帮助文本所暗示的相反。如果值是计算得出的，用户可能需要一些额外指导。

## 4.6 ACD 实用程序

### 4.6.1 简介

EMBOSS 包含六个实用程序，用于运行、测试和记录 ACD 文件，而无需为程序本身编写 C 源代码：

- **acdc** 读取并处理 ACD 文件，按必要提示用户，方式与应用程序运行时完全相同。如果遇到错误，它将终止。这允许在不同条件下测试命令行界面的行为，即使应用程序本身尚未编写。它是使用最广泛的实用程序，也是测试 ACD 文件是否正确工作的基本工具。

- **acdtrace** 的工作方式与 **acdc** 相同，但会报告 ACD 文件中行的处理情况。它还会打印评估任何变量和操作的结果（参见第 4.4 节，‘Operations’）。

- **acdvalid** 处理 ACD 文件并报告由不正确、弃用或过时的语法引起的任何错误或警告。测试超出了 **acdc** 和 **acdtrace** 的范围。它强制执行参数和限定符命名的建议，并突出显示可能对第三方解析软件造成问题的 ACD 语法。

- **acdlog** 处理 ACD 文件和用户输入，同时记录内部数据结构的内容。目前其使用已弃用，应改用 **entrails** 应用程序（见下文）。

- **acdpretty** 从可解析但部分或格式不正确的 ACD 文件生成格式正确的 ACD 文件。

- **acdtable** 创建参数、允许值和默认值的表，用于应用程序文档和提供用户帮助。

