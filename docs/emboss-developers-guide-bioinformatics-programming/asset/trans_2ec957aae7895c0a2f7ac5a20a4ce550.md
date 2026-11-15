

- discretestates: 离散状态文件
- distances: 距离矩阵
- frequencies: 频率值
- properties: 属性值
- tree: 系统发育树

用于处理系统发育数据输出的数据类型如下：

- outdiscrete: 系统发育离散特征数据输出文件
- outdistances: 系统发育距离矩阵数据输出文件
- outfreq: 系统发育字符频率数据输出文件
- outproperties: 系统发育属性数据输出文件
- outtree: 系统发育树数据输出文件

## 6.12.5 ACD 数据定义

系统发育数据输入和输出的典型 ACD 定义如下。

### 6.12.5.1 discretestates

离散状态数据输入：

```
discretestates: discretestatesfile
[
   parameter: "Y"
   characters: "01PB?"
   knowntype: "discrete states"
   information: "Phylip discrete states file"
]
```

### 6.12.5.2 distances

距离数据输入：

```
distances: distancesfile
[
   parameter: "Y"
   knowntype: "distance matrix"
   information: "Phylip distance matrix file"
]
```

### 6.12.5.3 frequencies

频率数据输入：

```
frequencies: frequenciesfile
[
  parameter: "Y"
]
```

### 6.12.5.4 properties

属性数据输入：

```
properties: propertiesfile
[
  characters: "01"
  length: "$(infile.discretelength)"
  knowntype: "ancestral states"
  information: "Phylip ancestral states file"
]
```

### 6.12.5.5 tree

树数据输入：

```
tree: treefile
[
  parameter: "Y"
  knowntype: "newick"
  information: "Phylip tree file (optional)"
]
```

### 6.12.5.6 outdiscrete

离散状态数据输出：

```
outdiscrete: outdiscretefile
[
  parameter: "Y"
]
```

### 6.12.5.7 outdistance

距离数据输出：

```
outdistance: outdistancefile
[
  parameter: "Y"
]
```

### 6.12.5.8 outfreq

频率数据输出：

```
outfreq: outfreqfile
[
   parameter: "Y"
]
```

### 6.12.5.9 outproperties

属性数据输出：

```
outproperties: outpropertiesfile
[
   parameter: "Y"
]
```

### 6.12.5.10 outtree

树数据输出：

```
outtree: outtreefile
[
   parameter: "Y"
]
```

### 6.12.5.11 参数名

系统发育数据输入和输出的所有数据定义都应具有直观的名称。

有一些一般性指导原则，但目前未强制执行具体的命名规则。参见
附录 A，ACD 语法参考。

### 6.12.5.12 常用属性

下表汇总了通常指定的属性。除非它们被指示为全局属性（第 A.4 节，“全局属性”），否则它们均为数据类型特定属性（第 A.5 节，“数据类型特定属性”）。

parameter：如果系统发育数据是 EMBOSS 应用程序的主要输入或输出，则应使用全局属性
parameter: "Y" 将其定义为参数。

characters：分别指定 discretestates 或 properties 对象允许的离散状态或属性字符。

knowntype：此全局属性通常用于所有系统发育输入和输出类型。

information：用于用户提示和应用程序文档的全局属性。

length：指定每组的属性值数量（properties 数据类型）或每组的频率位点/值数量（frequencies 数据类型）。

size：指定离散状态集数量（discretestates 数据类型）、频率集数量（frequencies 数据类型）或树的数量（tree 数据类型）。

**注意**

各种计算属性（第 A.6 节，“计算属性”）在 ACD 文件级别可用。

## 6.12.6 ACD 文件处理

通过 ACD 文件处理系统发育数据的数据类型和函数如下。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
| :--- | :--- | :--- |
| *系统发育数据输入* | | |
| discretestates | AjPPhyloState* | ajAcdGetDiscretestates |
| distances | AjPPhyloDist | ajAcdGetDistances |
| frequencies | AjPPhyloFreq | ajAcdGetFrequencies |
| properties | AjPPhyloProp | ajAcdGetProperties |
| tree | AjPPhyloTree* | ajAcdGetTree |
| *系统发育数据输出* | | |
| outdiscrete | AjPOutfile | ajAcdGetOutdiscrete |
| outdistance | AjPOutfile | ajAcdGetOutdistance |
| outfreq | AjPOutfile | ajAcdGetOutfreq |
| outproperties | AjPOutfile | ajAcdGetOutproperties |
| outtree | AjPOutfile | ajAcdGetOuttree |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.12.6.1 系统发育数据检索

#### 6.12.6.1.1 输入系统发育数据

要检索输入系统发育数据，需声明对象指针，然后使用相应的 ajAcdGet* 函数对其进行初始化。

#### discretestates

```
AjPPhyloState *data=NULL;
data = ajAcdGetDiscretestates("discretestatesfile");
```

#### distances

```
AjPPhyloDist data=NULL;
data = ajAcdGetDistances("distancesfile");
```

#### frequencies

```
AjPPhyloFreq data=NULL;
data = ajAcdGetFrequencies("frequenciesfile");
```

#### properties

```
AjPPhyloProp data=NULL;
data = ajAcdGetProperties("propertiesfile");
```

#### tree

```
AjPPhyloTree* data=NULL;
data = ajAcdGetTree("treefile");
```

#### 6.12.6.1.2 输出系统发育数据

要检索输出系统发育数据流，需声明对象指针，并使用相应的 ajAcdGet* 函数对其进行初始化。

#### outdiscrete

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutdiscrete("outdiscretefile");
```

#### outdistance

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutdistance("outdistancefile");
```

#### outfreq

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutfreq("outfreqfile");
```

#### outproperties

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOutproperties("outpropertiesfile");
```

#### outtree

```
AjPOutfile outfile=NULL;
outfile = ajAcdGetOuttree("outtreefile");
```

#### 6.12.6.1.3 替代 ACD 检索函数

存在用于从文件中检索单个（第一个）状态或树对象的函数：

```
AjPPhyloState ajAcdGetDiscretestatesSingle (const char *token);
AjPPhyloTree ajAcdGetTreeSingle (const char *token);
```

使用这些函数时，仍然需要调用相应的析构函数（见下文），以确保释放在 ACD 文件处理期间分配的状态或树对象数组。

### 6.12.6.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.12.6.3 内存和文件管理

程序结束时，关闭所有文件并释放内存是您的责任。

#### 6.12.6.3.1 关闭输出系统发育数据文件

要关闭输出系统发育数据流，请使用输出文件的地址调用 ajOutfileClose：

```
ajOutfileClose(&outfile);
```

#### 6.12.6.3.2 释放内存

您必须对 ajAcdGet* 调用返回的任何系统发育数据对象调用相应的析构函数（见下文）。

此外，您必须调用 ajPhyloExit 以释放内部用于管家工作的内存：

```
void ajPhyloExit (void);
```

## 6.12.7 系统发育对象内存管理

### 6.12.7.1 默认对象构造

要使用未在 ACD 文件中定义的系统发育数据对象，必须首先实例化相应的对象指针。默认构造函数如下：

```
AjPPhyloDist ajPhyloDistNew (void);
AjPPhyloFreq ajPhyloFreqNew (void);
AjPPhyloProp ajPhyloPropNew (void);
AjPPhyloState ajPhyloStateNew (void);
AjPPhyloTree ajPhyloTreeNew (void);
```

### 6.12.7.2 默认对象销毁

使用完对象后，必须释放其内存。默认析构函数如下：

```
void ajPhyloDistDel (AjPPhyloDist* pthis);
void ajPhyloFreqDel (AjPPhyloFreq* pthis);
void ajPhyloPropDel (AjPPhyloProp* pthis);
void ajPhyloStateDel (AjPPhyloState* pthis);
void ajPhyloTreeDel (AjPPhyloTree* pthis);
```

默认构造函数和析构函数的用法如下：

```
AjPPhyloDist dist = NULL;
AjPPhyloFreq freq = NULL;
AjPPhyloProp prop = NULL;
AjPPhyloState state = NULL;
AjPPhyloTree tree = NULL;

/* Call constructor functions */
dist = ajPhyloDistNew();
freq = ajPhyloFreqNew();
prop = ajPhyloPropNew();
state = ajPhyloStateNew();
tree = ajPhyloTreeNew();

/* Do something with instantiated objects */
...

/* Call destructor functions */
ajPhyloDistDel (&dist);
ajPhyloFreqDel (&freq);
ajPhyloPropDel (&prop);
ajPhyloStateDel (&state);
ajPhyloTreeDel (&tree);
```

有两个替代析构函数用于释放状态和树对象数组：

```
void ajPhyloStateDelarray(AjPPhyloState** pthis);
void ajPhyloTreeDelarray(AjPPhyloTree** pthis);
```

它们用于状态和树对象，而非默认析构函数，以释放 ACD 文件处理产生的内存：

