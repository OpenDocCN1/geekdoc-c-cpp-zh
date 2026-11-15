

| AJAX 数据类型 | AjPFeattable | AjPFeattabOut |
| --- | --- | --- |
| 从 ACD 检索 | ajAcdGetFeatures | ajAcdGetFeatout |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，这些函数返回指向相应对象的指针。

### 6.9.6.1 输入特征检索

要检索输入特征，需声明一个对象指针，然后使用 ajAcdGetFeatures 进行初始化：

```
AjPFeattable features=NULL;
features = ajAcdGetFeatures("features");
```

### 6.9.6.2 输出特征检索

要检索输出特征流，需声明并初始化一个对象指针，使用 ajAcdGetFeatout：

```
AjPFeattabOut outfeat=NULL;
outfeat = ajAcdGetFeatout("outfeat");
```

### 6.9.6.3 处理命令行选项和 ACD 属性

### 6.9.6.3.1 设置特征范围

特征输入数据类型包含多种内置命令行限定符，包括 -fbegin 和 -fend（用于指定特征的起始和结束位置），以及 -freverse（用于反转核苷酸特征的方向）。

读取特征表时，特征值将保存在相应的特征表对象中。无论范围值如何，整个表都会加载到内存中。函数 ajFeattableTrim 或 ajFeattableTrimOff 用于将特征修剪到 -fbegin 和 -fend 定义的区域：

```
AjFeattable ftable=NULL;
ftable = ajAcdGetFeatures("features");
ajFeattableTrim(ftable);
/* ajFeattableTrimOff(ftable,0,ajFeattableGetLen(ftable));*/
```

## 6.9 处理特征

读取序列时，特征值将保存在相应序列对象中的特征表里。无论序列范围值如何，整个序列都会加载到内存中。函数 ajSeqTrim（对于 AjPSeqset 对象则为 ajSeqsetTrim）用于将序列和特征修剪到 -sbegin 和 -send 定义的区域：

```
AjPSeq seq=NULL;

seq = ajAcdGetSeq("sequence");

ajSeqTrim(seq);
```

### 6.9.6.4 内存管理

在程序结束时释放内存是您的责任。必须对 ajAcdGet* 调用返回的任何对象调用默认析构函数（见下文）。

此外，您必须调用 embExit 来清理内部内存，包括为特征表管理分配的内存：

```
embExit();
```

### 6.9.7 内存管理

### 6.9.7.1 默认对象构造

要使用未在 ACD 文件中定义的特征表对象，必须首先实例化相应的对象指针。默认构造函数是 ajFeattableNew。
ajFeattableNew 会使特征表类型保持未初始化状态。当向表中添加特征时，会设置该类型。特定类型的函数 ajFeattableNewDna 和 ajFeattableNewProt 分别用于创建核苷酸和蛋白质特征表。函数 ajFeattableNewSeq 创建与序列对象类型和长度匹配的特征表。

特征表输出对象通常从 ACD 文件处理中加载（见上文）。在极少需要手动创建的情况下，可以使用默认构造函数 ajFeattabOutNew，或使用 ajFeattabOutNewCSF 和 ajFeattabOutNewSSF 函数（它们使用现有输出文件以及指定的类型和序列名称）。

要创建特征对象（通常存储在特征表中），可使用类似的一组函数。ajFeatNew 创建包含所有属性（包括类型）的特征。ajFeatNewProt 创建蛋白质特征所需的所有属性的特征（无链或框架）。
ajFeatNewII 和 ajFeatNewIIRev 是只需起始和结束值的通用构造函数。特征类型将默认为“杂项特征”或“多肽区域”值。
ajFeatNewFeat 是一个复制构造函数，用于从现有特征创建特征对象。

```
/* Constructor for feature which is added to table */
AjPFeature ajFeatNew (AjPFeattable thys,
                     const AjPStr source,
                     const AjPStr type,
                     ajint Start,
                     ajint End,
float score,
char strand,
ajint frame);
/* Constructor for protein feature */
AjPFeature ajFeatNewProt(AjPFeattable thys,
const AjPStr source,
const AjPStr type,
ajint Start, ajint End,
float score);
/* Simple constructor with only start and end positions */
AjPFeature ajFeatNewII (AjPFeattable thys,
ajint Start, ajint End);
/* Simple constructor, sets features to be on reverse strand */
AjPFeature ajFeatNewIIRev (AjPFeattable thys,
ajint Start, ajint End);
/* Copies a feature */
AjPFeature ajFeatNewFeat (const AjPFeature orig);
/* Feature Table Object Constructors */
AjPFeattable ajFeattableNew (const AjPStr name);
AjPFeattable ajFeattableNewDna (const AjPStr name);
AjPFeattable ajFeattableNewProt (const AjPStr name);
AjPFeattable ajFeattableNewSeq (const AjPSeq seq);
/* Output Feature Table Object constructors */
AjPFeattabOut ajFeattabOutNew (void);
AjPFeattabOut ajFeattabOutNewCSF (const char* fmt, const AjPStr name,
const char* type, AjPFile file);
AjPFeattabOut ajFeattabOutNewSSF (const AjPStr fmt, const AjPStr name,
const char* type, AjPFile file);
```

ajFeatNew 的参数如下：

- thys 指向添加新特征的特征表的指针
- source 特征的分析依据
- type 特征类型（例如 外显子）
- Start 特征的起始位置
- End 特征的结束位置
- score 特征的分析得分
- strand 特征的链
- frame 特征的框架

所有构造函数都返回新对象的地址。

### 6.9.7.2 默认对象销毁

使用完对象后，必须释放其内存。相关函数如下：

```
void ajFeatDel (AjPFeature *pthis);
void ajFeattableDel (AjPFeattable *pthis);
void ajFeattabOutDel (AjPFeattabOut* pthis);
```

### 示例

在以下示例中，特征表和单个特征是使用默认构造函数手动构建的。特征将写入从 ACD 处理中检索的特征表：

```
AjPFeattable feattable;
AjPStr name = NULL;
AjPStr source = NULL;
AjPStr type = NULL;
char strand = '+';
ajint frame = 0;
AjPFeature feature = NULL;
AjPFeattabOut output = NULL;
ajint i;
float score = 0.0;
embInit("demofeatures", argc, argv);

output = ajAcdGetFeatout("outfeat");

ajStrAssignC(&name,"seq1");

feattable = ajFeattableNew(name);

ajStrAssignC(&source,"demofeature");
score = 1.0;

for(i=1;i<11;i++)
{
    if(i & 1)
        ajStrAssignC(&type,"CDS");
    else
        ajStrAssignC(&type,"misc_feature");
    feature = ajFeatNew(feattable, source, type, i, i+10, score, strand,
                        frame);
}

ajFeattableWrite(output, feattable);

ajStrDel(&source);
ajStrDel(&name);
ajStrDel(&type);
ajFeattableDel(&feattable);
ajFeattabOutDel(&output);
```

### 6.9.7.4 替代对象构造和加载

### 6.9.7.4.1 单个特征

创建特征对象有多种替代方法。可以指定特征的起始和结束位置：

```
AjPFeature ajFeatNewII (AjPFeattable thys, ajint Start, ajint End);
AjPFeature ajFeatNewIIRev (AjPFeattable thys, ajint Start, ajint End);
```

```
AjPFeature ajFeatNewProt (AjPFeattable thys,
 const AjPStr source, const AjPStr type,
 ajint Start, ajint End, float score);
```

ajFeatNewIIRev 将特征设置为反向链，而 ajFeatNewProt 用于蛋白质特征。

在需要可安全修改和/或删除的特征副本的情况下，可以使用 ajFeatNewFeat：

```
AjPFeature ajFeatNewFeat (const AjPFeature orig);
```

### 6.9.7.4.2 特征表

创建特征表对象有多种替代方法，可以通过名称或从现有序列对象创建：

```
/* DNA feature table
 */
AjPFeattable ajFeattableNewDna (const AjPStr name);

/* Protein feature table */
AjPFeattable ajFeattableNewProt (const AjPStr name);

/* From existing sequence; type is determined by the sequence type. */
AjPFeattable ajFeattableNewSeq (const AjPSeq seq);
```

在需要可安全修改和/或删除的特征表副本的情况下，可以使用：

```
/* Copy whole feature table */
AjPFeattable ajFeattableNewFtable (const AjPFeattable orig);

/* Copy limited number of features */
AjPFeattable ajFeattableNewFtableLimit (const AjPFeattable orig, ajint limit);
```

可以使用以下函数从序列对象中检索特征表（定义在 ajseq.c 中）：

```
AjPFeattable ajSeqGetFeatCopy (const AjPSeq thys);
const AjPFeattable ajSeqGetFeat (const AjPSeq thys);
```

### 6.9.7.4.3 编辑特征表

要向特征表（AjPFeattable）添加新特征（AjPFeature），请调用：

```
void ajFeattableAdd (AjPFeattable thys, AjPFeature feature);
```

