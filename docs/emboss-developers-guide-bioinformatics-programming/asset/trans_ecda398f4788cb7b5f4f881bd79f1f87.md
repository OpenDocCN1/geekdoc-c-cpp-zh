

seqoutall: outseq
[
    parameter: "Y"
    features: "$(feature)"
]

相比之下，boolean: feature 是一个控制定义，如果由用户设置，将导致 **seqret** 读取输入文件中的序列特征信息（如果可用）。

boolean: firstonly 是另一个控制定义，如果设置，将导致只读取单个序列：

```
boolean: feature
[
    information: "Use feature information"
]
boolean: firstonly
[
    information: "Read one sequence and stop"
]
```

在实践中，有多种不同的 ACD 数据类型（第 A.2 节，“数据类型”）可用。对这些数据定义的编程在第 5.5 节“使用对象编程”中有更详细的介绍。

## 9.1.4 属性

每个 ACD 定义都有属性，属性是名称：值对。属性有两种基本类型。_全局属性_ 可用于所有数据类型，而 _特定于数据类型的属性_ 可用于单个或一组相关数据类型。

考虑 `feature` 和 `sequence` 的定义：

```
boolean: feature
[
    information: "Use feature information"
]
seqall: sequence
[
    parameter: "Y"
    type: "gapany"
    features: "$(feature)"
]
```

`parameter:` 和 `information:` 是全局属性，而 `type:` 和 `features:` 是特定于数据类型的属性。

`parameter:` "Y" 将数据定义定义为 _参数_，而不是某种 _限定符_。如上所述，参数的值可以在命令行上带或不带标志（参数名称）给出。应用程序需要所有参数，如果命令行上未给出值，将提示输入值。

布尔定义未给出 parameter: "Y"，这意味着，在没有 standard: "Y" 或 additional: "Y" 属性的情况下，它们将默认为高级限定符。高级限定符永远不会提示输入。如果已定义 standard: "Y" 或 additional: "Y"，则数据定义将是标准或附加限定符。有关限定符和参数行为的更多信息可用（第 4.1 节，“ACD 文件开发简介”）。

information: 为数据定义提供非常简洁的描述。该文本用于 Web 表单和其他 GUI。它也是用于在命令行上提示用户输入值的文本。您会注意到，序列输入和输出未定义 information:。EMBOSS 为这些数据类型提供默认提示。所有 boolean: 数据类型的默认值均为 False，这意味着无需在 ACD 文件中显式定义默认值。

type: 属性特定于序列数据类型。type: "gapany" 表示输入序列可以是任何类型，并可能包含间隙字符。在实践中，支持多种不同的序列类型（第 A.7 节，“序列类型”）。

features: 属性也是特定于序列的。属性定义看起来有点奇怪：

```
features: "$(feature)"
```

$ 语法的意思是“检索……的值”，在此情况下是“检索 feature ACD 定义的值”，因此 outseq 的 features: 属性将设置为该值。换句话说，如果用户通过在命令行上给出它（例如 secret -feature）打开了 feature 高级限定符，则输入序列将包含特征。虽然严格来说不需要 features: "$(feature)"（毕竟信息在 boolean: feature 中已指定），但这使应用程序源代码更加整洁。

除了全局属性和特定于数据类型的属性之外，ACD 文件中还可能出现另外两种属性。计算属性在处理 ACD 文件并读取应用程序输入文件后接收值。最后，还有特定于数据类型的命令行限定符，它们为单个或一组 ACD 数据类型定义，并可以作为属性硬编码在 ACD 文件中。参见第 A.4 节（“全局属性”）、第 A.5 节（“特定于数据类型的属性”）和第 A.6 节（“计算属性”）。

## 9.2 C 源代码 (secret.c)

应用程序 C 源代码（见下文）非常简单。其基本功能包括：

- 声明用于保存来自 ACD 文件的值的变量（AjP* 类型声明）
- 处理 ACD 文件和命令行（embInit）
- 将值（输入和输出序列流）从 ACD 文件读入内存（ajAcdGet 函数系列）
- 遍历输入序列并将序列加载到内存中（ajSeqallNext）
- 写出序列（ajSeqoutWriteSeq）
- 关闭输出文件
- 干净退出（embExit）

源代码如下：

/*@source secret application
**
** Return a sequence
**
** @author Copyright (C) Peter Rice
** @@
**
** This program is free software; you can redistribute it and/or
** modify it under the terms of the GNU General Public License
** as published by the Free Software Foundation; either version 2
** of the License, or (at your option) any later version.
**
** This program is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
** GNU General Public License for more details.
**
** You should have received a copy of the GNU General Public License
** along with this program; if not, write to the Free Software
** Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
******************************************************************************/

#include "emboss.h"

/* @prog secret **************************************************************
**
** Reads and writes (returns) sequences
**
******************************************************************************/

int main(int argc, char **argv)
{
    AjPSeqall seqall;
    AjPSeqout seqout;
    AjPSeq seq = NULL;
    AjBool firstonly;

    embInit("secret", argc, argv);

    seqout = ajAcdGetSeqoutall("outseq");
    seqall = ajAcdGetSeqall("sequence");
    firstonly = ajAcdGetBoolean("firstonly");

    while(ajSeqallNext(seqall, &seq))
    {
        ajSeqoutWriteSeq(seqout, seq);
        if(firstonly)
            break;
    }

    ajSeqoutClose(seqout);

    embExit();

    return 0;
}
```

### 9.2.1 变量声明

`main()` 中的第一个代码块声明用于保存来自 ACD 文件的值的变量：

```c
AjPSeqall seqall=NULL;
AjPSeqout seqout=NULL;
AjPSeq seq = NULL;
AjBool firstonly;
```

以 `AjP` 开头的变量都是指向 EMBOSS 对象（相应类型的 C 数据结构）的 C 指针。这些包括 `AjPSeqall`、`AjPSeqout` 和 `AjPSeq`。许多 EMBOSS 对象（包括复杂生物类型和其他类型）定义在 AJAX 和 NUCLEUS 编程库中。相比之下，`AjBool` 是 EMBOSS 用于简单布尔变量的数据类型。您会注意到指针变量初始化为 `NULL`。在首次定义指针时始终将其初始化为 `NULL` 是良好做法。有关原因的解释以及使用对象编程的详细信息，请参见第 5.3 节“对象（C 数据结构）”。

`AjPSeq` 用于单个序列输入，`AjPSeqall` 用于多个序列输入，`AjPSeqout` 用于单个序列输出。对于 **seqret** 应用程序，`AjPSeqall seqall` 用于输入序列流，`AjPSeq seq` 用于保存该流中单个序列的数据，`AjPSeqout seqout` 用于输出序列流。`AjBool firstonly` 用于保存来自 ACD 文件的 `firstonly` 控制属性的值。

您会注意到，`feature` 数据定义不需要变量。此选项的值在输入序列流上设置，在 ACD 文件本身中，通过 ACD 代码 `features: "$(feature)"`。换句话说，是否将特征信息与序列一起包含是在 ACD 文件中设置并存储在 `seqall` 对象中的，因此 C 代码中不需要为它添加其他变量。

### 9.2.2 ACD 文件和命令行处理

以下代码：

```c
embInit("secret", argc, argv);
```

用于处理 ACD 文件和命令行。它处理所有用户输入处理，这就是为什么它首先被调用。`embInit` 读取本地数据库定义，找到要使用的正确 ACD 文件（第一个参数是 "secret"，因此它在 ACD 目录中查找 `secret.acd`），读取 ACD 文件，并使用 `main` 中的 `argc` 和 `argv` 处理命令行。

当 `embInit` 返回时，输入序列流（`sequence`）将打开以供读取，第一个序列将读入内存，布尔变量 `feature` 和 `firstonly` 将接收值（可能是默认值），并且将为 `outseq` 打开输出文件。为这些对象分配内存并可供程序使用。

`embInit` 处理提示用户输入未在命令行上输入的值，包括重新提示用户输入超出范围的值等功能。

