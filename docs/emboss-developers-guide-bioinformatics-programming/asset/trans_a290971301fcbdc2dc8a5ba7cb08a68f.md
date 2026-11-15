

extension: "string" ("") 输出文件扩展名。

features: "boolean" ("N") 如果设置，序列输出将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

type: "string" ("") 输出序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以使输出序列类型清晰。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。

minseqs: "integer" ("1") 输出文件中预期的最小序列数。

maxseqs: "integer" ("INT_MAX") 输出文件中预期的最大序列数。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成序列输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无序列输出）作为仅偶尔需要序列输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.19.1 关联限定符

seqoutall 数据类型具有以下可能在 ACD 文件中作为属性硬编码的关联限定符。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
| :--- | :--- |
| osformat: "string" ("") | 输出序列格式 |
| osextension: "string" ("") | 文件扩展名 |
| osname: "string" ("") | 基础文件名 |
| osdirectory: "string" ("") | 输出目录 |
| osdbname: "string" ("") | 要添加的数据库名称 |
| ossingle: "boolean" ("N") | 每个条目单独文件 |
| oufo: "string" ("") | UFO 特征 |
| oformat: "string" ("") | 特征格式 |
| ofname: "string" ("") | 特征文件名 |
| ofdirectory: "string" ("") | 输出目录 |

seqoutall 数据类型具有一个数据类型关联的命令行限定符 (-ossingle)，它通常在 ACD 文件中作为属性硬编码（参见 EMBOSS 用户指南）。ossingle: 定义 -ossingle 限定符的默认值，并可以设置为 "Y" 以将输出定向到多个序列文件。例如，EMBOSS 程序 seqretsplit 使用此属性将输入序列拆分为多个文件。

## A.5.3.20 seqoutset

name: "string" ("") 输出文件的基本名称。

extension: "string" ("") 输出文件扩展名。

features: "boolean" ("N") 如果设置，序列输出将包含特征信息，要么在同一文件中（如果序列格式支持），要么在单独的文件中（默认为 GFF 格式）。

type: "string" ("") 输出序列类型。虽然这将默认为第一个输出序列的类型，但建议始终定义一个值以使输出序列类型清晰。序列类型必须是标准序列类型（第 A.7 节，“序列类型”）。

minseqs: "integer" ("1") 输出文件中预期的最小序列数。

maxseqs: "integer" ("INT_MAX") 输出文件中预期的最大序列数。

aligned: "boolean" ("N") 如果为 true，则指定输出中的所有序列预期是已比对的。如果为 false，则假设序列未比对。我们建议始终定义 aligned: 属性，以便明确定义序列集的性质。

nullok: "boolean" ("N") 如果应用程序可以接受此定义的空值，并且可以在不生成序列输出的情况下运行，则必须将 nullok: 属性设置为 "Y"。这允许省略默认值，或在命令行上使用 -noFlag 运行应用程序（其中 Flag 是数据定义标志）。

nulldefault: "boolean" ("N") nulldefault: 属性覆盖默认名称生成，并将空字符串（无序列输出）作为仅偶尔需要序列输出的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。与 nullok: 和 missing: 属性结合使用，这允许限定符默认为空，并从命令行打开。

### A.5.3.20.1 关联限定符

seqoutset 数据类型具有以下可能在 ACD 文件中作为属性硬编码的关联限定符。这些限定符在 EMBOSS 用户指南中有描述：

| 属性 | 描述 |
| :--- | :--- |
| osformat: "string" ("") | 输出序列格式 |
| osextension: "string" ("") | 文件扩展名 |
| osname: "string" ("") | 基础文件名 |
| osdirectory: "string" ("") | 输出目录 |
| osdbname: "string" ("") | 要添加的数据库名称 |
| ossingle: "boolean" ("N") | 每个条目单独文件 |
| oufo: "string" ("") | UFO 特征 |
| oformat: "string" ("") | 特征格式 |
| ofname: "string" ("") | 特征文件名 |
| ofdirectory: "string" ("") | 输出目录 |

## A.5.4 选择属性描述

### A.5.4.1 列表

values: "string" ("") 包含选项标签和描述列表的字符串，这些标签和描述定义了用户可以选择的选项。delimiter: 和 codedelimiter: 属性指定如何将此字符串解析为单个列表项。

delimiter: "string" (";") values: 字符串中用于分隔列表项的字符。默认为分号 (;)。

codedelimiter: "string" (":") values: 字符串中用于将选项标签与其描述分开的字符。默认为冒号 :。

minimum: "integer" ("1") 所需的最小选择数。默认需要一个选择。

maximum: "integer" ("1") 允许的最大选择数。默认正好需要一个选择。较高的值允许多个选择。

header: "string" ("") 显示在选项列表上方的文本。

button: "boolean" ("N") 为界面开发人员提供。它有一个布尔值，用于建议列表在界面中最好表示为复选框或单选按钮（值为 "Y"），还是应使用文本框来输入值（"N"）。

casesensitive: "boolean" ("N") 定义用户输入是否必须匹配列表项的精确大小写。无论用户使用何种大小写，参数的值都将完全是相应列表值的内容。

### A.5.4.1.1 关联限定符

列表数据类型没有关联限定符。

### A.5.4.2 选择

values: "string" ("") 包含选项描述列表的字符串，这些描述定义了用户可以选择的选项。delimiter: 属性指定如何将此字符串解析为单个选择列表项。

delimiter: "string" (":") values: 字符串中用于分隔列表项的字符。默认为分号 (;)。

minimum: "integer" ("1") 所需的最小选择数。默认需要一个选择。

maximum: "integer" ("1") 允许的最大选择数。默认正好需要一个选择。较高的值允许多个选择。

header: "string" ("") 显示在选项列表上方的文本。

button: "boolean" ("N") 为界面开发人员提供。它有一个布尔值，用于建议列表在界面中最好表示为复选框或单选按钮（值为 "Y"），还是应使用文本框来输入值（"N"）。

casesensitive: "boolean" ("N") 定义输入是否必须匹配列表项的精确大小写。无论用户使用何种大小写，参数的值都将完全是相应列表值的内容。

**注意**
所有数据类型定义的 information: 属性定义在列表或选择类型列表后用作提示的文本。

### A.5.4.2.1 关联限定符

选择数据类型没有关联限定符。

## A.5.5 图形属性描述

### A.5.5.1 图表

`nullok: "boolean" ("N")` 如果应用程序可以接受此定义的空值，并且可以在不生成图形输出的情况下运行，则必须将 `nullok:` 属性设置为 `"Y"`。这允许省略默认值，或在命令行上使用 `-noFlag` 运行应用程序（其中 `Flag` 是数据定义标志）。

`nulldefault: "boolean" ("N")` 覆盖默认名称生成，并将空字符串（无图表）作为仅偶尔需要图表的程序的默认值。如果在命令行上指定了空字符串，则将生成标准默认值。

### A.5.5.1.1 关联限定符

`graph` 数据类型具有以下可能在 ACD 文件中作为属性硬编码的关联限定符。这些限定符在 *EMBOSS 用户指南* 中有描述：

| 属性 | 描述 |
| :--- | :--- |
| `gprompt: "boolean" ("N")` | 图表提示 |
| `gdesc: "string" ("")` | 图表描述 |
| `gtitle: "string" ("")` | 图表标题 |
| `gsubtitle: "string" ("")` | 图表副标题 |
| `gxtitle: "string" ("")` | 图表 x 轴标题 |
| `gytitle: "string" ("")` | 图表 y 轴标题 |
| `goutfile: "string" ("")` | 非交互式显示的输出文件 |
| `gdirectory: "string" ("")` | 输出目录 |

`graph` 数据类型有四个关联限定符，通常在 ACD 文件中作为属性硬编码（参见 *EMBOSS 用户指南*）。`-gtitle`、`-gxtitle` 和 `-gytitle` 用于控制图表及其轴的标题，并通过属性 `gtitle:`、`gxtitle:` 和 `gytitle:` 设置。`goutfile:` 属性指定输出的基本文件名。例如，EMBOSS 程序 **tmap** 使用它将输出定向到命名文件，而不是默认名称（即读取的第一个输入序列的名称，如果有的话）。

