

void embExit (void);
void embExitBad (void);

这些函数定义在 embExit.h/c 中。embExit 返回成功代码 (0)，而 embExitBad 返回失败代码 (0)。
因此，大多数 EMBOSS 应用程序的最后两行是：

embExit();
return 0;

## 6.4 处理简单 ACD 数据类型

### 6.4.1 简介

本节介绍“简单”ACD 数据类型（第 A.2.1 节，“简单 ACD 数据类型描述”）的 ACD 文件处理：

- 整数 (integer)
- 浮点数 (float)
- 布尔值 (boolean)
- 切换 (toggle)
- 字符串 (string)
- 数组 (array)
- 范围 (range)

通过调用 ajAcdGet* 函数来检索值，这些函数返回相应类型的 AJAX 数据类型：对于 integer、float、boolean 和 toggle 返回基本类型，对于其他类型返回 EMBOSS 对象。处理范围的函数包括：

- 获取和设置范围对象的元素
- 查询范围对象的属性
- 根据范围对象中的规范处理字符串 (AjPStr) 和序列 (AjPSeq)

有关正则表达式（regexp ACD 数据类型）和序列模式（pattern ACD 数据类型），请参见第 6.6 节，“处理序列模式”。数组处理（第 6.17 节，“处理数组”）和字符串处理（第 6.5 节，“处理字符串”）在其他地方有详细描述。

### 6.4.2 AJAX 库文件

下表列出了用于处理简单 ACD 数据类型的 AJAX 库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
| --- | --- |
| ajrange | AJAX 范围表达式的处理 |
| ajstr | 字符串处理 |
| ajarr | 数组处理 |

ajrange.h/c. 定义范围规范对象 (AjPRange) 并包含处理范围规范的函数（参见第 A.2.1.5 节，“range”）。

ajstr.h/c. 定义用于处理来自 ACD 文件的字符串的字符串对象 (AjPStr)。它们包含您进行一般字符串处理所需的大部分函数（第 6.5 节，“处理字符串”）。

ajarr.h/c. 包含您进行一般数组处理所需的大部分函数（第 6.17 节，“处理数组”）。它们定义了用于处理来自 ACD 文件的数组的 AjPFloat 对象。它们包含用于低级处理数组的静态数据结构和函数。

### 6.4.3 ACD 数据类型

简单 ACD 数据类型用于应用程序输入：

- integer 简单整数
- float 简单浮点数
- boolean 简单布尔值
- toggle 简单布尔值
- string 简单字符串
- array 整数或浮点数列表
- range 序列位置范围

### 6.4.4 ACD 数据定义

典型的 ACD 定义如下所示。

#### 6.4.4.1 integer

用于整数输入：

integer: wordsize
[
   default: "4"
   minimum: "2"
   maximum: "20"
   information: "Word size"
]

#### 6.4.4.2 float

用于浮点数输入：

float: minscore
[
    default: "0.0"
    minimum: "0.0"
    information: "Minimum score of feature to display"
]

#### 6.4.4.3 boolean

用于布尔输入：

boolean: feature
[
    default: "N"
    information: "Use feature information"
]

#### 6.4.4.4 toggle

用于切换输入：

toggle: tolower
[
    default: "N"
    information: "Change masked region to lower case"
]

#### 6.4.4.5 string

用于字符串输入：

string: delimiter
[
    default: "|"
    information: "Delimiter of records in text output file"
    knowntype: "output delimiter"
]

#### 6.4.4.6 array

用于数组输入：

array: thresholds
[
    information: "Values to represent 'identical', 'similar' and 'related'"
    default: "-1.5,0.0,1.5"
    minimum: "0.0"
    size: "3"
    sum: "0"
    sumtest: "y"
]

#### 6.4.4.7 range

用于范围输入：

range: regions
[
    information: "Regions to put in uppercase (eg: 4-57,78-94)"
    default: ""
    help: "Regions to put in uppercase. If this is left blank, the sequence case is
left alone. A set of regions is specified by a set of pairs of integer positions
separated by any non-digit, non-alpha character. For example: \
24-45, 56-78 \
1:45, 67=99;765..888 \
1,5,8,10,23,45,57,99"
]

#### 6.4.4.8 参数名称

根据数据定义的特定用例，可能会提供标准参数名称；例如，用于定义间隙罚分的任何浮点输入的间隙罚分。请参见附录 A，ACD 语法参考。

#### 6.4.4.9 常见属性

通常指定的属性摘要如下。除非它们被指示为全局属性（第 A.4 节，“全局属性”），否则它们是特定于数据类型的（第 A.5 节，“特定于数据类型的属性”）。

- **默认：** 全局属性，指定默认值。
- **最小值：** 指定允许的最小值。
- **最大值：** 指定允许的最大值。
- **信息：** 全局属性，指定用户提示，也用于应用程序文档。
- **已知类型：** 此全局属性应始终为字符串输入指定。如果输出不是任何标准 EMBOSS 已知类型，则推荐使用 ApplicationName 输出。
- **大小：** 指定数组数据定义中允许的元素数量。
- **总和：** 指定数组数据定义中所有值的总和，除非 sumtest 属性为 false，否则会对其进行测试。
- **求和测试：** 布尔属性，如果设置为 false，则关闭对数组数据定义的 sum: 属性的测试。

### 6.4.5 AJAX 数据类型

用于处理 ACD 文件中定义的简单 ACD 数据类型，请使用：

- ajint 简单整数（用于 integer ACD 数据类型）。
- float 简单浮点数（用于 float ACD 数据类型）。
- AjBool 简单布尔值（用于 boolean 和 toggle ACD 数据类型）。
- AjPStr 字符串（用于 string ACD 数据类型）。
- AjPFloat 浮点数数组（用于 array ACD 数据类型）。
- AjPRange AJAX 序列范围规范（用于 range ACD 数据类型）。请参见第 A.2.1.5 节，“range”。

### 6.4.6 ACD 文件处理

通过 ACD 文件处理简单 ACD 数据类型的数据类型和函数如下所示。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
| --- | --- | --- |
| integer | ajint | ajAcdGetInt |
| float | float | ajAcdGetFloat |
| boolean | AjBool | ajAcdGetBoolean |
| toggle | AjBool | ajAcdGetToggle |
| string | AjPStr | ajAcdGetString |
| array | AjPFloat | ajAcdGetArray |
| range | AjPRange | ajAcdGetRange |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都读入内存。您可以通过 ajAcdGet* 函数系列来控制内存，该系列函数返回指向相应对象的指针。

> **注意**
>
> 您通常不会从 ACD 检索切换项，因为它们仅用于 ACD 文件内，通常用于控制对另一个参数的提示（参见第 4.5 节，“控制提示”）。

#### 6.4.6.1 简单 ACD 数据类型的检索

要从 ACD 文件检索数据，请按需要声明简单变量或对象指针，然后使用相应的 ajAcdGet* 函数对其进行初始化。

##### 6.4.6.1.1 integer

```c
ajint wordsize = 0;
wordsize = ajAcdGetInt("wordsize");
```

##### 6.4.6.1.2 float

```c
float minscore = 0.;
minscore = ajAcdGetFloat("minscore");
```

##### 6.4.6.1.3 boolean

```c
AjBool showall = ajFalse;
showall = ajAcdGetBoolean("showall");
```

##### 6.4.6.1.4 toggle

```c
AjBool tolower = ajFalse;
tolower = ajAcdGetToggle("tolower");
```

##### 6.4.6.1.5 string

```c
AjPStr delimiter = NULL;
delimiter = ajAcdGetString("delimiter");
```

##### 6.4.6.1.6 array

```c
AjPFloat thresholds = NULL;
thresholds = ajAcdGetArray("thresholds");
```

##### 6.4.6.1.7 range

```c
AjPRange regions = NULL;
regions = ajAcdGetRange("regions");
```

#### 6.4.6.2 处理命令行选项和 ACD 属性

##### 6.4.6.2.1 设置范围对象属性

设置范围对象属性的函数如下：

```c
/* Set the start and end values of a range element. */
AjBool ajRangeElementSet (AjPRange this, ajuint element, ajuint start, ajuint end);
/* Sets range values offset relative to a sequence -sbegin value */
AjBool ajRangeSetOffset (AjPRange this, ajuint begin);
```

ajRangeSetOffset 将把范围值设置为相对于指定位置 (begin) 的值，通常是命令行中通过 -sbegin 或序列的 USA 中指定的序列位置范围的起始位置（请参见 EMBOSS 用户指南）。例如，如果 begin 为 11 且范围为 11-12，则新范围将更改为 1-2。

#### 6.4.6.3 内存管理

在程序结束时释放内存是您的责任。您必须对 ajAcdGet* 调用返回的任何 AjPStr、AjPFloat 或 AjPRange 对象调用默认析构函数（见下文）。当然，对于基本数据类型，这不是必需的。

### 6.4.7 对象内存管理

#### 6.4.7.1 默认对象构造

要使用未在 ACD 文件中定义的字符串、数组或范围对象，您必须首先实例化相应的对象指针。默认构造函数如下：

```c
AjPStr ajStrNew (void);             /* String object. */
AjPFloat ajFloatNew (void);         /* Float array */
AjPRange ajRangeNewI (ajuint n);    /* Range object   */
```

ajRangeNewI 接受一个整数 (n)，即对象可以容纳的范围数量。所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好的做法：

```c
AjPStr    delimiter = NULL;
AjPFloat  thresholds = NULL;
AjPRange  regions   = NULL;

delimiter = ajStrNew();
```

