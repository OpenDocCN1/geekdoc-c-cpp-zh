

minseqs: "integer" ("1") 要读取的最小序列数。默认情况下，最少可接受一个序列。

maxseqs: "integer" ("INT_MAX") 要读取的最大序列数。默认情况下，没有最大值。

### A.5.2.18.1 关联限定符

seqset 数据类型具有以下关联限定符，这些限定符可作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 限定符 | 类型/默认值 | 描述 |
|---|---|---|
| sbegin | "integer" ("0") | 要使用的序列起始位置 |
| send | "integer" ("0") | 要使用的序列结束位置 |
| sreverse | "boolean" ("N") | 反向（如果是 DNA） |
| sask | "boolean" ("N") | 询问起始/结束/反向 |
| snucleotide | "boolean" ("N") | 序列为核苷酸 |
| sprotein | "boolean" ("N") | 序列为蛋白质 |
| slower | "boolean" ("N") | 转换为小写 |
| supper | "boolean" ("N") | 转换为大写 |
| sformat | "string" ("") | 输入序列格式 |
| sdbname | "string" ("") | 数据库名称 |
| sid | "string" ("") | 条目名 |
| ufo | "string" ("") | UFO 特征 |
| fformat | "string" ("") | 特征格式 |
| fopenfile | "string" ("") | 特征文件名 |

## A.5.2.19 seqsetall

type: "string" ("") 强制序列集为给定类型。默认情况下接受任何序列类型。理想情况下应设置 type: 属性，以明确接受的输入序列类型。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。

aligned: "boolean" ("N") 如果为 true，则指定输入中的所有序列预期已比对。如果为 false，则假设序列未比对，并简单地一起读入内存进行处理。理想情况下应始终设置 aligned: 属性，以明确定义序列集的性质。

features: "boolean" ("N") 如果设置，序列输入将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

entry: "boolean" ("N") 如果设置，序列输入将包含输入序列或数据库条目的完整原始文本。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在没有序列输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无序列输入）作为仅偶尔需要序列输入的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并可从命令行打开。

minsets: "integer" ("1") 要读取的最小序列集数。默认情况下，最少可接受一个序列集。

maxsets: "integer" ("INT_MAX") 要读取的最大序列集数。默认情况下，没有最大值（整数大小的系统限制除外）。

minseqs: "integer" ("1") 要读取的最小序列数。默认情况下，最少可接受一个序列。

maxseqs: "integer" ("INT_MAX") 要读取的最大序列数。默认情况下，没有最大值。

### A.5.2.19.1 关联限定符

seqsetall 数据类型具有以下关联限定符，这些限定符可作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
|---|---|
| sbegin: "integer" ("0") | 要使用的序列起始位置 |
| send: "integer" ("0") | 要使用的序列结束位置 |
| sreverse: "boolean" ("N") | 反向（如果是 DNA） |
| sask: "boolean" ("N") | 询问起始/结束/反向 |
| snucleotide: "boolean" ("N") | 序列为核苷酸 |
| sprotein: "boolean" ("N") | 序列为蛋白质 |
| slower: "boolean" ("N") | 转换为小写 |
| supper: "boolean" ("N") | 转换为大写 |
| sformat: "string" ("") | 输入序列格式 |
| sdbname: "string" ("") | 数据库名称 |
| sid: "string" ("") | 条目名 |
| ufo: "string" ("") | UFO 特征 |
| fformat: "string" ("") | 特征格式 |
| fopenfile: "string" ("") | 特征文件名 |

## A.5.2.20 tree

size: "integer" ("0") 输入文件中的树的数量。有些只能接受单棵树，因此对于这些，值应设置为 "1"。值为 "0" 表示可接受任意数量的树。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在没有树输入的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

### A.5.2.20.1 关联限定符

tree 数据类型没有关联限定符。

## A.5.3 输出属性描述

### A.5.3.1 align

minseqs: "integer" ("1") 输出比对中预期的最小序列数。

minseqs: 和 maxseqs: 属性可用于验证应用程序输出，例如，在命令行上使用 -aformat 限定符选择格式时。

maxseqs: "integer" ("INT_MAX") 输出比对中预期的最大序列数。

minseqs: 和 maxseqs: 属性可用于验证应用程序输出，例如，在命令行上使用 -aformat 限定符选择格式时。

multiple: "boolean" ("N") 如果输出可以包含来自同一输入的多个比对，则应设置为 "Y"。

type: 序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以明确输出序列类型。

taglist: "string" ("") 定义要为比对序列从内部特征表中报告的其他标记。标记名称和类型必须与应用程序源代码匹配。每个标记的格式为 type:tagname[=columnname]，例如 int:length 或 string:gc=GC%。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在不生成比对输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无比对文件）作为仅偶尔需要比对文件的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。

#### A.5.3.1.1 关联限定符

align 数据类型具有以下关联限定符，这些限定符可作为属性硬编码在 ACD 文件中。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
|---|---|
| aformat: "string" ("") | 比对格式 |
| aextension: "string" ("") | 文件名扩展名 |
| adirectory: "string" ("") | 输出目录 |
| aname: "string" ("") | 基础文件名 |
| awidth: "integer" ("0") | 比对宽度 |
| aaccshow: "boolean" ("N") | 在标题中显示登录号 |
| adesshow: "boolean" ("N") | 在标题中显示描述 |
| ausashow: "boolean" ("N") | 在比对中显示完整 USA |
| aglobal: "boolean" ("N") | 在比对中显示完整序列 |

align 数据类型有两个关联限定符（-aformat 和 -aglobal），这些限定符通常作为属性硬编码在 ACD 文件中（参见 EMBOSS 用户指南）。aformat: 定义 -aformat 限定符的默认值，即默认比对格式。aglobal: 定义 -aglobal 限定符的默认值，对于生成全局比对的程序，应将其设置为 "Y"。

### A.5.3.2 featout

- name: "string" ("") 输出文件的基本名称。优先使用 -ofname（见下文）。
- extension: "string" ("") 输出文件的扩展名。优先使用 -oformat（见下文）。
- type: "string" ("") 定义特征输出是 "protein" 还是 "nucleotide"。基于任何输入序列的类型有一个默认值，但应始终指定一个值。
- multiple: "boolean" ("N") 如果特征注释针对多个序列，则应设置为 "Y"。
- nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值且可以在不生成特征输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。
- nulldefault: "boolean" ("N") nulldefault: 属性会覆盖默认名称生成，并将空字符串（无特征输出）作为仅偶尔需要特征输出的程序的默认值。如果在命令行上指定空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并可从命令行打开。

