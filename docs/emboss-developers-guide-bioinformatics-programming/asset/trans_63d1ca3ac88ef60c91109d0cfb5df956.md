

/* Convert single letter to three letter amino acid code. */
AJBool ajResidueToTriplet (char c, AjPStr *Paa3);

/* Convert three letter to single letter amino acid code. */
AJBool ajResidueFromTriplet (char *aa3, char *Pc);

### 6.7.17 DNA 计算

ajdan.h/c 中提供了各种用于计算核苷酸序列属性的函数。这些函数使用 DNA 熔解对象（AjPMelt），但这对应用程序员是透明的，您永远不需要直接实例化或使用该对象：

| 对象 | 描述 |
|---|---|
| AjPMelt | 用于 DNA 熔解 |

### 6.7.17.1 DNA 熔解的通用函数

AjPMeltInit 和 AjPMeltExit 函数在内部用于初始化和清理内存。无需直接调用它们。AjPMeltGC 函数是一个用于计算 G+C 含量的实用工具：

```
/* Initialises melt entropies, enthalpies and energies. Different data files are
read for DNA or RNA heteroduplex. Also sets optional flag for array saving of the
above. */
void ajMeltInit (AJBool isDNA, ajint savesize);

/* Cleans up DNA melting processing internal memory */
void ajMeltExit (void);

/* Calculates GC fraction of a sequence allowing for ambiguity */
float ajMeltGC (const AjPStr strand, ajint len);
```

### 6.7.17.2 计算 DNA 熔解和退火温度及能量

AjPMeltEnergy 计算序列字符串的熔解能和焓/熵。AjPMeltEnergy2 是一个替代接口，它初始化一组“保存”数组，通过仅检查序列一次来使后续调用更高效。AjPMeltTemp 计算寡核苷酸的熔解温度，并有一个使用“保存”数组以提高效率的 AjPMeltTempSave 版本。AjPMeltTempProd 在给定盐浓度下计算寡核苷酸产物的熔解温度。AjPMeltTemp 在给定各自的熔解温度时，计算产物和引物的退火温度。

```
/* Calculate melt energy and enthalpy/entropy for a sequence */
float ajMeltEnergy(const AjPStr strand, ajint len,
                ajint shift, AJBool isDNA,
                AJBool maySave, float *enthalpy, float *entropy);

/* Calculate melt energy for programs like prima */
float ajMeltEnergy2(const char *strand, ajint pos, ajint len,
AJBool isDNA,
float *enthalpy, float *entropy,
float **saveentr, float **saveenth, float **saveener);

/* Calculate melt temperature of DNA or RNA */
float ajMeltTemp (const AjPStr strand, ajint len, ajint shift, float saltconc,
float DNAconc, AJBool isDNA);

/* Calculate melt temperature of DNA or RNA */
float ajMeltTempSave(const char *strand, ajint pos,
ajint len, float saltconc,
float DNAconc, AJBool isDNA,
float **saveentr, float **saveenth, float **saveener);

/* Calculate product melt temperature of DNA */
float ajMeltTempProd (float gc, float saltconc, ajint len);

/* Calculate annealing temperature of product and primer */
float ajAnneal (float tmprimer, float tmproduct);
```

## 6.8 处理序列翻译

### 6.8.1 简介

将核苷酸序列翻译成蛋白质序列是一项常见任务。AJAX 提供了您所期望的所有基本功能。核苷酸序列可以采用多种形式（AJAX 字符串 (AjPStr)、C 类型字符串 (char *) 或 AJAX 序列对象 (AjPSeq)），并可以在所有阅读框中进行翻译。序列的反向互补链也可以被翻译。

### 6.8.2 AJAX 库文件

用于处理序列翻译的 AJAX 库文件在下表中列出。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajtranslate | 序列翻译 |

ajtranslate.h/c。定义序列翻译对象 (AjPTrn) 并包含用于处理序列翻译的函数。

### 6.8.3 ACD 数据类型

没有专门用于处理翻译的 ACD 数据类型。此类操作在核苷酸序列上执行，因此需要适当类型的序列输入。还需要遗传代码，其选择通常通过由 list ACD 数据类型实现的菜单提供给用户。因此，您需要的 ACD 数据类型如下：

| 数据类型 | 描述 |
|---|---|
| list | 带有文本标签的选项列表（文本描述）。用户会看到一个有限的选项列表，可从中进行选择。选项可以由任意文本标签标记。 |
| sequence | 单个输入序列。 |

注意 有关菜单和序列处理的一般信息，请参见：第 6.19 节（'处理菜单'）和第 6.7 节（'处理序列'）。

### 6.8.4 ACD 数据定义

单个序列输入的典型 ACD 定义如下：

```
sequence: sequence
[
    parameter: "Y"
    type: "nucleotide"
]
```

可用的遗传代码必须在 ACD 文件中定义，并可为此使用 list 数据类型。EMBOSS 支持一组标准遗传代码，如下所示：

```
list: table
[
    additional: "Y"
    default: "0"
    minimum: "1"
    maximum: "1"
    header: "Genetic codes"
    values: "0:Standard; 1:Standard (with alternative initiation codons); 2:Vertebrate Mitochondrial; 3:Yeast Mitochondrial;
    4:Mold, Protozoan, Coelenterate Mitochondrial and
    Mycoplasma/Spiroplasma; 5:Invertebrate Mitochondrial; 6:Ciliate
    Macronuclear and Dasycladacean; 9:Echinoderm Mitochondrial;
    10:Euplotid Nuclear; 11:Bacterial; 12:Alternative Yeast Nuclear;
    13:Ascidian Mitochondrial; 14:Flatworm Mitochondrial;
    15:Blepharisma Macronuclear; 16:Chlorophycean Mitochondrial;
    21:Trematode Mitochondrial; 22:Scenedesmus obliquus;
    23:Thraustochytrium Mitochondrial"
    delimiter: ";"
    codedelimiter: ":"
    information: "Code to use"
]
```

代码的顺序目前很重要；列表必须按上述确切顺序给出。

### 6.8.5 AJAX 数据类型

为处理需要序列和菜单输入的序列翻译，请使用：

- AjPTrn 用于序列翻译
- AjPSeq 单个输入序列（用于 sequence ACD 数据类型）
- AjPStr 来自菜单的单个选择（用于 list ACD 数据类型）

### 6.8.6 ACD 文件处理

下表显示了通过 ACD 文件处理翻译的数据类型和函数。这里从列表中检索单个选择，但也可以使用其他类型的菜单、输入序列或访问方法。

| 标题 | 读取序列 | 从列表读取单个选择 |
|---|---|---|
| ACD 数据类型 | sequence | list |
| 对象 | AjPSeq | AjPStr |
| 从 ACD 检索 | ajAcdGetSeq | ajAcdGetListSingle |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节（'处理 ACD 文件'））。ACD 文件中的所有值都读入内存。您可以通过 ajAcdGet* 函数系列来控制内存，该系列函数返回指向相应对象的指针。

### 6.8.6.1 序列或菜单选择检索

要检索序列或菜单选择对象指针，需先声明指针，然后使用相应的 ajAcdGet* 函数进行初始化。

### 6.8.6.1.1 输入序列

要检索输入序列：

```
AjPSeq seq=NULL;
seq = ajAcdGetSeq("sequence");
```

### 6.8.6.1.2 菜单选择

从遗传代码列表中选择的选项需要作为整数。

ajAcdGetListSingle 将选择作为字符串返回，其初始部分使用 ajStrToInt 转换为整数。此整数传递给 ajTrnNewI 以创建翻译表对象。这就是为什么 ACD 文件中的列表顺序很重要！您还必须声明翻译对象指针：

```
AjPTrn trnTable = NULL; /* Translation object pointer */
AjPStr gcode = NULL; /* Genetic code (selection from list) */
ajint n = 0; /* Selection */
gcode = ajAcdGetListSingle("table");
ajStrToInt(gcode, &n);
trnTable = ajTrnNewI(n);
```

### 6.8.6.2 内存管理

在程序结束时释放内存是您的责任。必须为用于 ACD 数据定义的翻译、序列和字符串对象调用默认析构函数：

```
/* Deletes a translation table object */
void ajTrnDel(AjPTrn* pthis);
/* Delete a string object. */
void ajStrDel (AjPStr *Pstr);
/* Delete a sequence object. */
void ajSeqDel (AjPSeq* Pseq);
```

函数 ajTrnExit 在退出时自动调用，以清理翻译处理内部管家所用的内存：

```
void ajTrnExit(void);
```

### 6.8.7 翻译对象内存管理

### 6.8.7.1 默认对象构造

要使用翻译对象，必须首先实例化相应的对象指针。提供了默认构造函数。它们将从 EMBOSS 数据搜索目录（参见 EMBOSS 用户指南）中读取名为 EGC.n 的翻译数据文件，其中 n 是要使用的遗传代码编号。此编号可以显式提供给 ajTrnNewI。或者，可以通过调用 ajTrnNew 或 ajTrnNewC 按文件名打开文件：

```
/* Reads EGC.trnFileNameInt where trnFileNameInt is supplied as a parameter. */
AjPTrn ajTrnNewI (ajint trnFileNameInt);
/* Reads trnFileName. */
AjPTrn ajTrnNew (const AjPStr trnFileName);
/* Reads trnFileName. */
AjPTrn ajTrnNewC (const char *trnFileName);
```

所有构造函数都返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好的实践：

