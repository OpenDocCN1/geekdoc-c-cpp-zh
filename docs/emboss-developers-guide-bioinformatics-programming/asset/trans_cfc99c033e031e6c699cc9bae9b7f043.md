

## 4.6.2 使用实用程序

实用程序本身没有选项。它们的调用方式相同，即指定要测试的应用程序名称，并在实用程序应用程序名称之后指定任何命令行选项：

```
UtilityName ApplicationName Options
```

例如，这将测试名为 helloworld 的应用程序的 ACD 文件：

```
acdc helloworld
```

acdc、acdtrace 和 acdlog 将通过读取其 ACD 文件，并以与真正运行程序时完全相同的方式处理命令行和用户响应，来运行任何 EMBOSS 程序的命令行界面。用户将被提示输入应用程序参数所需的任何值，并读取任何输入文件。不会运行应用程序本身，只读取 ACD 文件。

可以指定任何命令行选项。在以下示例中，seqret 被调用以从序列（sequence.in）中检索区域 50 – 100，并将片段写入输出文件（sequence.out）：

```
acdc seqret sequence.in sequence.out -sbegin 50 -send 100
```

> 注意
> 所有 EMBOSS 应用程序都会调用 NUCLEUS 函数 embInit（对于 EMBASSY 应用程序则为 embInitP），该函数会进一步调用 ACD 文件处理函数。实用程序应用程序将任何参数（即要测试的应用程序的命令行）传递给 embInit 或 embInitP，因此运行方式与原生应用程序完全相同。可以以任何可用格式指定输出文件；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

## 4.6.3 全局限定符

实用程序可以使用所有全局限定符（参见 EMBOSS 用户指南）：

- -auto 关闭任何用户提示。使用 -auto 选项测试应用程序总是很有用，因为这模拟了应用程序由脚本或其他不涉及交互式用户输入的方式调用的情况。
- -debug 打开调试。这将输出与调用 AJAX 函数 ajDebug 相关的参数。
- -filter 从 stdin 读取并写入 stdout，并隐含 -auto。
- -stdout 默认写入 stdout，但仍会提示用户。
- -help 将提供实用程序的用法信息。
- -verbose 与 -help 连用时，还会提供相关限定符和全局限定符。
- -warning 如果需要，程序将生成警告消息。
- -error 如果需要，程序将生成错误消息。
- -fatal 如果需要，程序将生成致命错误（终止）消息。

实用程序本身都不会生成调试、警告、错误或致命消息。但是，由于可以读取输入文件，输入函数所做的任何调试调用或消息 *将* 被报告。

## 4.6.4 实用程序说明

### 4.6.4.1 acdc

acdc 读取并处理 ACD 文件，在必要时提示用户，方式与应用程序运行时完全相同。如果遇到错误，它将终止。这允许在不同条件下测试命令行界面的行为，即使应用程序本身尚未编写。它是使用最广泛的实用程序，是测试 ACD 文件是否正确工作的基本工具。

acdc 没有自己的选项，但接受一个参数，即正在测试的 EMBOSS 应用程序的名称。它通过指定要测试的应用程序名称，并在实用程序应用程序名称之后指定任何命令行选项来调用：

```
acdc ApplicationName Options
```

可以为应用程序指定任何命令行选项。用户将被提示输入应用程序参数所需的任何值，并读取任何输入文件。不会运行应用程序本身，只读取 ACD 文件。

acdc 将使用指定程序的 ACD 文件中指定的任何数据文件，但会忽略仅由程序代码直接使用的任何数据文件。EMBOSS 数据文件随应用程序分发，并存储在标准 EMBOSS 数据目录中（参见 *EMBOSS 用户指南*）。

可以以任何可用格式指定输出文件；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

以下是 **acdc** 的示例会话：

```
% acdc antigenic
Finds antigenic sites in proteins
Input protein sequence(s) : tsw:act1_fgru
Minimum length of antigenic region [6]:
Output report [act1_fgru.antigenic]:
```

### 4.6.4.2 acdtrace

acdtrace 的工作方式与 acdc 相同，但会报告 ACD 文件中行的处理情况。它还会打印评估 ACD 文件中任何变量和操作的结果（参见第 4.4 节，“操作”）。

调用方式如下：

```
acdtrace ApplicationName Options
```

acdtrace 将通过读取其 ACD 文件，并以与真正运行程序时完全相同的方式处理命令行和用户响应，来运行任何 EMBOSS 程序的命令行界面。可以为被调用的应用程序指定任何命令行选项。用户将被提示输入应用程序参数所需的任何值，并读取任何输入文件。不会运行应用程序本身，只读取 ACD 文件。

可以以任何可用格式指定输出文件，但它们将为空（不会调用应用程序代码，因此不会有输出）。

acdtrace 将使用指定程序的 ACD 文件中指定的任何数据文件，但会忽略仅由程序代码直接使用的任何数据文件。EMBOSS 数据文件随应用程序分发，并存储在标准 EMBOSS 数据目录中（参见 EMBOSS 用户指南）。

以下是 acdtrace 的示例会话：

```
% acdtrace antigenic
Finds antigenic sites in proteins
Input protein sequence(s) : tsw:act1_fgru
Minimum length of antigenic region [6]:
Output report [act1_fgru.antigenic]:
```

屏幕上的输出（未显示）可能看起来有点令人困惑，但这是查看变量和操作在 ACD 文件中如何工作的最佳方式。

### 4.6.4.3 acdvalid

acdvalid 处理 ACD 文件，并报告由不正确、已弃用或已过时的语法引起的任何错误或警告。测试内容超出了 acdc 和 acdtrace 的范围。它会突出显示可能导致包装 EMBOSS 应用程序的第三方解析软件出现问题的 ACD 语法。

acdvalid 验证 ACD 文件，测试许多功能，这些功能不会阻止应用程序运行，但可能会为任何用户界面（无论是命令行还是通过包装器）创建问题。acdvalid 的大多数消息都是警告，不会阻止程序运行。

调用方式如下：

```
acdvalid ApplicationName Options
```

acdvalid 将像 acdtrace 一样，以与真正运行程序时完全相同的方式运行命令行界面。

它将使用指定程序的 ACD 文件中指定的任何数据文件，但会忽略仅由程序代码直接使用的任何数据文件。EMBOSS 数据文件随应用程序分发，并存储在标准 EMBOSS 数据目录中（参见 EMBOSS 用户指南）。

可以以任何可用格式指定输出文件；但是，它们将为空（不会调用应用程序代码，因此不会有输出）。

以下是 acdvalid 的示例会话：

```
% acdvalid antigenic
```

acdvalid 会生成错误和警告消息。如果消息是“错误”，则 ACD 文件将无法工作并需要修复。如果消息是“警告”，则 ACD 文件将能工作，但值得尝试修复问题。

> **注意**
> 警告消息仅供参考，但主发布版本中的任何应用程序都会尽可能修复尽多的警告。
>
> 值得在每个新版本的 EMBOSS 中对所有本地 ACD 文件运行 acdvalid。因为每个新版本都会添加额外的验证测试。

### 4.6.4.3.1 acdvalid 测试的功能

这些包括：

- 各部分的顺序正确，为“input”、“required”、“additional”、“advanced”和“output”。
- 部分和子部分名称（第 4.1.5 节，“ACD 文件部分”）在 EMBOSS 系统文件 sections.standard 中定义。
  - 这确保了在使用部分对应用程序参数进行分组时，界面包装器将具有一致的描述。
- 所有数据定义都包含在一个部分或子部分中。
- 限制在一个部分中的参数位于正确的部分。
  - 所有输入 ACD 数据类型（第 A.2.2 节，“输入 ACD 数据类型描述”）必须位于“input”部分，所有输出 ACD 数据类型（第 A.2.3 节，“输出 ACD 数据类型描述”）位于“output”部分。
- 其他参数在其出现的部分中是有效的。

