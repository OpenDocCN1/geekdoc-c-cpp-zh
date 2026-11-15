

### 4.1.5.4 其他部分

用户偶尔设置的其他限定符。

### 4.1.5.5 高级部分

可以设置值但从不提示输入的高级限定符。它们由以下属性的缺失定义：

```
parameter: "Y"
standard: "Y"
additional: "Y"
```

### 4.1.5.6 输出部分

与输出相关的输出数据类型和其他参数。参见第 A.2.3 节，“输出 ACD 数据类型的描述”。

### 4.1.5.7 示例

wossname 应用程序的搜索输入字符串包含在输入部分中。输出部分包含与输出相关的所有参数和限定符，还包含一个名为 htmlsection 的子部分：

```
section: input
[
  information: "Input section"
  type: "page"
]

string: search
[
  parameter: "Y"
  default: ""
  information: "Text to search for, or blank to list all
  programs"

  help:"Enter a word or words here and a case-independent search
  for it will be made in the one-line documentation, group names and
  keywords of all of the EMBOSS programs. If no keyword is
  specified, all programs will be listed."
  knowntype: "emboss keyword"
]

endsection: input
.
.
section: output
[
  information: "Output section"
  type: "page"
]

outfile: outfile
[
additional: "Y"
default: "stdout"
knowntype: "wossname output"
]
section: htmlsection
[
information: "Html section"
type: "frame"
]
toggle: html
[
additional: "Y"
default: "N"
information: "Format the output for HTML"
help: "If you are sending the output to a file, this will format
it for displaying as a table in a WWW document."
outputmodifier: "Y"
]
boolean: groups
[
additional: "Y"
default: "N"
information: "Output only the group names"
help: "If you use this option, then only the group names will
output to the file"
outputmodifier: "Y"
]
boolean: alphabetic
[
additional: "Y"
default: "N"
information: "Output an alphabetic list of programs"
help: "If you use this option, then you will get a single list of
the program names and descriptions instead of the programs being
listed in their functional groups."
outputmodifier: "Y"
]
endsection: output
```

### 4.1.5.8 标准文件部分（sections.standard 文件）

所有部分和子部分都定义在 sections.standard 文件中，该文件存储在 EMBOSS 应用程序 ACD 文件目录中，例如：

```
../emboss/emboss/emboss/acd/sections.standard
```

此文件的摘录如下所示：

```
#
# ACD sections
#
# top level (page) sections
# =========================
additional page Additional section
advanced page Advanced section
input page Input section
output page Output section
required page Required section
#
#
# sub level (frame) sections
# ==========================
afeaturesection input First feature options
bfeaturesection input Second feature options
consensussection additional Consensus section
datasection output Data output section
fastalignsection additional Fast align options
```

该文件定义了顶级（页面）部分（‘输入’、‘必需’、‘其他’等）的允许顺序。该文件还定义了允许的子部分（在“# 子级（框架）部分”下给出），这些子部分已根据需要为各个应用程序定义和使用。行上的第一个标记是子部分名称。第二个标记是子部分所属的顶级部分：子部分不能出现在列出的任何其他部分中。行上的其余文本是对该部分的描述。

## 4 ACD 文件开发

## 4.2 应用程序定义

## 4.2.1 应用程序定义格式

ACD 文件中的第一个定义必须是应用程序定义。它由 application: 标记、与此 ACD 文件关联的应用程序名称以及方括号中的应用程序属性块组成。每个属性都是一个 name: value 对：

```
application: ApplicationName
[
    ApplicationAttribute1Name: "ApplicationAttribute1Value"
    ApplicationAttribute2Name: "ApplicationAttribute2Value"
]
```

例如，wossname 应用程序定义具有两个属性（documentation: 和 groups:）：

```
application: wossname
[
    documentation: "Finds programs by keywords"
    groups: "Display"
]
```

应用程序名称（ApplicationName）是任意的，但通常与 ACD 文件名相同。在程序初始化期间（参见第 6.3 节，“处理 ACD 文件”），将调用 embInit 函数以将 C 源代码与 ACD 文件关联并调用 ACD 文件处理。embInit 会传递要解析的 ACD 文件名，例如：

```
embInit("ApplicationName", argc, argv)
```

这使得可以为单个应用程序 C 源代码文件开发多个 ACD 文件（因此也可以开发多个命令行界面）。

> **注意**
> 
> embInit *不* 将 ApplicationName 与应用程序定义中 application: 标记后给出的字符串进行比较。

## 4.2.2 应用程序属性

应用程序属性用于描述应用程序本身的元数据。它们允许你设置诸如文档文本和应用程序所属组等内容。参见第 A.3 节，“应用程序属性”。

> **注意**
> 
> documentation:、keywords: 和 groups: 属性值得特别提及。wossname 程序会搜索它们的字符串值，给定一个关键字，将返回在 groups:、keywords: 或 documentation: 文本中包含该关键字的所有应用程序。
> groups: 字符串也由 seealso 应用程序使用，该应用程序获取 EMBOSS 程序的名称并返回与其共享某些功能的程序列表。

## 4.2.3 应用程序文档

documentation: 属性文本是对应用程序功能的简要描述，在运行程序或显示帮助时（当程序使用 -help 限定符运行时）打印到屏幕上。以下是 seqret 的应用程序定义：

```
application: seqret
[
    documentation: "Reads and writes (returns) a sequence"
    groups: "Edit"
]
```

上述 ACD 文件将在命令行中产生以下行为：

```
% seqret
Reads and writes (returns) a sequence
Input sequence :
```

如果缺少 documentation: 属性，则运行程序时会发出警告。字符串值必须符合某些约定（第 A.3 节，“应用程序属性”）。

### 4.2.3.1 应用程序关键字文件（keywords.standard）

keywords: 属性用于将关键字附加到属性。可给出的允许关键字定义在 keywords.standard 文件中，该文件安装在与 ACD 文件相同的目录中，例如：

```
../emboss/emboss/emboss/acd/Keywords.standard
```

文件如下所示：

```
#
# Application keywords
#
# Keywords are additional search terms to locate applications
# Valid group and subgroup names are not allowed. Keyword searches are
# expected to include the groups . Keywords defined here and in the
# application keywords: attribute are a few terms to be used where the
# short documentation string is not sufficient to identify an
# application by function.
```

你会发现当前未定义任何关键字。如果添加任何关键字，请在注释块之后每行给出一个关键字。

## 4.2.4 应用程序组

groups: 属性根据其功能将应用程序放入组或子组中。同一子组中的程序通常执行类似的操作或在同一常规区域内运行。groups: 属性的字符串值必须遵守某些约定（第 A.3 节，“应用程序属性”）。

一般格式如下：

```
application: ApplicationName
[
   groups: "GroupName1, GroupName2, ... : SubgroupName1, SubgroupName2, ... "
]
```

例如：

```
application: syco
[
   documentation: "Synonymous codon usage Gribsov statistic
   plot"
   groups: "Nucleic:Codon usage, Nucleic:Gene finding"
]
```

通常只指定一个组和子组。例如，以下 ACD 文件指示应用程序 pscan 属于 Protein 组和 Motifs 子组：

```
application: pscan
[
   documentation: "Scans proteins using PRINTS"
   groups: "Protein:Motifs"
]
```

通常只指定一个组也足够了，例如：

```
application: trimest
[
   documentation: "Trim poly-A tails off EST sequences"
   groups: "Edit"
]
```

### 4.2.4.1 应用程序组名称文件（groups.standard）

应用程序组已在其他地方广泛使用，因此 EMBOSS 现在使用一组标准组名称，ACD 文件中的所有组名称都将根据该组名称进行验证。该标准定义在 groups.standard 文件中，该文件安装在与 ACD 文件相同的目录中，例如：

```
.../emboss/emboss/emboss/acd/groups.standard
```

groups.standard 文件为每个有效的 group : 属性值包含一行。组和子组（如果指定）用 ':'（冒号）字符分隔，组或子组名称中的空格将替换为下划线字符 ('_')。还有一个简短的描述，说明可能会放置在组中的内容。文件摘录如下所示：

