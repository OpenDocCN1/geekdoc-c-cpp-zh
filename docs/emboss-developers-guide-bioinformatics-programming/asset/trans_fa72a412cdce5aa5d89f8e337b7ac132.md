

## 6.12.7.3 替代对象构建和加载

### 6.12.7.3.1 系统发育数据输入

目前没有用于此的函数。

### 6.12.7.3.2 系统发育数据输出

目前没有用于此的函数。

### 6.12.8 从文件读取系统发育数据

用于此的函数如下：

```
AjPPhyloDist* ajPhyloDistRead (const AjPStr filename, ajint size, AjBool missing);
AjPPhyloFreq ajPhyloFreqRead (const AjPStr filename, AjBool contchar, AjBool genedata, AjBool indiv);
AjPPhyloProp ajPhyloPropRead (const AjPStr filename, const AjPStr propchars, ajint len, ajint size);
AjPPhyloState* ajPhyloStateRead (const AjPStr filename, const AjPStr statechars);
AjPPhyloTree* ajPhyloTreeRead (const AjPStr filename, ajint size);
```

这些函数的提供是为了在ACD文件处理上下文之外处理系统发育数据时使用。有关更多信息，请参阅在线文档。

### 6.12.9 获取系统发育对象的元素

目前只有一个用于此的函数。它返回属性对象的大小：

```
ajint ajPhyloPropGetSize (const AjPPhyloProp thys);
```

### 6.12.10 调试函数

这些函数将每个对象的元素报告到调试文件。函数如下：

```
void ajPhyloDistTrace (const AjPPhyloDist thys);
void ajPhyloFreqTrace (const AjPPhyloFreq thys);
void ajPhyloPropTrace (const AjPPhyloProp thys);
void ajPhyloStateTrace (const AjPPhyloState thys);
void ajPhyloTreeTrace (const AjPPhyloTree thys);
```

## 6.13 处理密码子使用表

### 6.13.1 简介

EMBOSS提供一个密码子使用表对象，用于存储描述核苷酸序列中密码子使用情况的数组。

输入和输出的密码子使用表通常在ACD文件中定义，但如果需要，也可以直接创建。提供了用于读写数据、获取和设置对象元素、计算密码子使用表属性以及反向翻译的函数。还有一些杂项函数，主要用于三联体碱基代码与密码子索引之间的相互转换。

创建密码子使用表的代码需要先创建一个输出对象，然后用编码序列中的密码子使用数据填充它，计算密码子频率的统计信息，并写入使用用户选定格式的文件。

### 6.13.2 AJAX库文件

下表列出了用于处理密码子使用表的AJAX库文件。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajcod | 密码子使用表处理 |

ajcod.h/c. 定义了AjPCod对象和用于处理密码子使用表的函数。它还包含用于在低级别处理它们的静态数据结构和函数。除非您打算扩展库的核心功能，否则不太可能需要这些。

### 6.13.3 ACD数据类型

用于处理密码子使用表的ACD数据类型是：

- codon 密码子使用表文件

### 6.13.4 ACD数据定义

密码子使用表输入的典型ACD定义：

```
codon: infile
[
  parameter: "y"
]
```

密码子使用表输出的典型ACD定义：

```
outcodon: outfile
[
  parameter: "Y"
]
```

### 6.13.4.1 参数名称

密码子使用表输入和输出的所有数据定义都应具有直观的名称：目前未定义标准名称。

### 6.13.4.2 常用属性

通常指定的属性总结如下。

parameter: 如果密码子使用表是EMBOSS应用程序的主要输入或输出，则应使用parameter: "Y"将其定义为参数（参见第A.4节“全局属性”）。

### 6.13.5 AJAX数据类型

用于处理密码子使用表（包括在ACD文件中定义的输入密码子使用表），请使用：

- AjPCod 密码子使用表对象（用于codon ACD数据类型）

用于处理在ACD文件中定义的输出密码子使用表，请使用：

- AjPOutfile 通用输出文件（用于outcodon ACD数据类型）

### 6.13.6 ACD文件处理

通过ACD文件处理密码子使用表的数据类型和函数如下所示。

| | 读取密码子使用表 | 写入密码子使用表 |
|---|---|---|
| ACD数据类型 | codon | outcodon |
| AJAX数据类型 | AjPCod | AjPOutfile |
| 从ACD检索 | ajAcdGetCodon | ajAcdGetOutcodon |

您的应用程序代码将调用embInit来处理ACD文件和命令行（参见第6.3节“处理ACD文件”）。ACD文件中的所有值都将读入内存，并根据需要打开文件。您可以通过ajAcdGet*函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.13.6.1 输入密码子使用表检索

要检索输入密码子使用表，需声明一个对象指针，然后使用ajAcdGetCodon对其进行初始化：

```
AjPCod cod = NULL;
cod = ajAcdGetCodon("infile");
```

### 6.13.6.2 输出密码子使用表检索

要检索输出密码子使用表流，需声明一个对象指针，并使用ajAcdGetOutcodon对其进行初始化：

```
AjPOutfile codout = NULL;
codout = ajAcdGetOutcodon("outfile");
```

### 6.13.6.3 处理命令行选项和ACD属性

目前没有用于此的函数。

### 6.13.6.4 内存和文件管理

程序结束时，关闭任何文件并释放内存是您的责任。

#### 6.13.6.4.1 关闭输出密码子使用表文件

要关闭输出密码子使用表，请使用ajOutfileClose：

```
ajOutfileClose(&codout);
```

#### 6.13.6.4.2 释放内存

您必须对通过ajAcdGetCodon或ajAcdGetOutcodon调用返回的任何对象调用默认析构函数（见下文）。

此外，您必须调用ajCodExit以清理为密码子使用处理内部管理分配的内存：

```
ajCodExit();
```

### 6.13.7 密码子使用表对象内存管理

#### 6.13.7.1 默认对象构建

要使用未在ACD文件中定义的密码子使用表对象，必须首先实例化相应的对象指针。默认构造函数是：

```
AjPCod ajCodNew(void);
```

所有构造函数都返回新对象的地址。在以下代码中，指针不需要初始化为NULL，但这样做是良好的做法：

```c
AjPCod cod = NULL;
cod = ajCodNew();
/* 对象已实例化并可供使用 */
```

#### 6.13.7.2 默认对象销毁

使用完对象后，必须释放其内存。默认析构函数是：

```c
void ajCodDel (AjPCod *pthys) ;
```

使用方法如下：

```c
AjPCod cod = NULL;
AjPOutfile codout = NULL;
cod = ajAcdGetCodon("infile");
codout = ajAcdGetOutcodon("outfile");
...
ajCodDel(&cod);
ajOutfileClose(&codout);
```

#### 6.13.7.3 替代对象构建和加载

有两个替代构造函数。ajCodNewCodenum使用标准遗传代码中的氨基酸分配创建密码子使用对象。相比之下，ajCodNewCod将复制现有的密码子对象并返回指向新对象的指针：

```c
AjPCod ajCodNewCodenum (ajint code) ;
AjPCod ajCodNewCod (const AjPCod thys) ;
```

### 6.13.8 读写密码子使用表

#### 6.13.8.1 读取密码子使用表

要使用直接创建的密码子使用表（即未在ACD文件中定义的表），有必要为其分配一个密码子索引。ajCodRead将从文件读取密码子使用数据

```
AjBool ajCodRead (AjPCod thys, const AjPStr fn, const AjPStr format);
```

密码子输入和输出格式由entrails实用程序使用ajCodPrintFormat函数打印。

#### 6.13.8.2 写入密码子使用表

有两个类似的函数用于将密码子使用表信息写入文件，它们的区别在于传递的文件对象类型（AjPFile和AjPOutfile）：

```
void ajCodWrite (AjPCod thys, AjPFile outf);
void ajCodWriteOut (const AjPCod thys, AjPOutfile outf);
```

通常，密码子使用表输出文件（AjPOutfile）是从ACD文件处理加载的（见上文）。因此，对于与outcodon：ACD数据定义对应的此类AjPOutfile，将调用ajCodWriteOut：

```
AjPCod cod = NULL;
AjPOutfile codout = NULL;

cod = ajAcdGetCodon("infile");
codout = ajAcdGetOutcodon("outfile");

ajCodWriteOut(cod, codout);
```

使用ajCodWrite时，需要手动处理输出文件的创建。使用ajFileNewOutNameC（或其他函数）来执行此操作：

```
AjPCod cod = NULL;
AjPFile codout = NULL;

/* Open a file called "OutputFileName" */
codout = ajFileNewOutNameC ("OutputFileName");

ajCodWrite(cod, codout);
```

### 6.13.9 获取和设置元素

密码子使用表的以下元素可以检索或设置：

- 名称
- 发行版
- 描述
- 分区

