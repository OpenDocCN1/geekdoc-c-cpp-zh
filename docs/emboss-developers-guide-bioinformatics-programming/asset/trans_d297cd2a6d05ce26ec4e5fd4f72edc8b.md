

存在返回集合中序列属性的‘Get’函数。这些函数的前缀为 ajSeqsetGetseq。需要指定所需序列的编号。例如，提供了三个函数来返回集合中给定的序列，可以作为序列对象指针、EMBOSS 字符串或 C 类型（char *）字符串。同样，应注意不要无意中以任何方式更改对象数据：

```
AjPSeq seqset = NULL;

AjPSeq seqPtr;
AjPStr seqS;
char * seqC;

seqset = ajAcdGetSeqset( "sequence" );

/* First sequence in call cases */
seqPtr = ajSeqsetGetseqSeq ( seqset, 1 );
seqS = ajSeqsetGetseqSeqS ( seqset, 1 );
seqC = ajSeqsetGetseqSeqC ( seqset, 1 );
```

返回流中序列属性的函数前缀为 ajSeqallGetseq，并返回流中*当前*序列的属性。例如，要获取当前序列的名称和长度：

```
AjPSeq seqall = NULL;
AjPStr name=NULL;
ajint len;

seqall = ajAcdGetSeqall( "sequences" );

name = ajSeqallGetseqName ( seqall );
len = ajSeqallGetseqLen(seqall);
```

## 6.7.9 测试序列属性

可以测试序列属性，例如序列是蛋白质还是核苷酸。此类函数返回 AjBool：

```
AjPSeq seq = NULL;
AjPSeqset seqset = NULL;

seq = ajAcdGetSeq( "sequence" );
seqset = ajAcdGetSeq( "sequences" );

if( ajSeqIsProt( seq ) )
    /* Protein sequence */;
else if( ajSeqIsNuc( seq ) )
    /* Nucleotide sequence */;
else
    /* Error handling */;

if( ajSeqsetIsNuc( seqset )
{
    if(ajSeqsetIsRna (seqset)
    /* Do something. */;
}
else if(ajSeqsetIsNuc(seqset)
{
    /* Do something else */
}
```

然而，此类测试很少需要，因为序列类型可以在 ACD 文件级别强制执行。

## 6.7.10 计算序列属性

可以计算序列的各种属性。例如，ajSeqCalcCount 将核苷酸序列中 A、C、G 和 T 核苷酸的数量写入数组，而 ajSeqCalcMolwt 计算蛋白质序列的分子量：

```
AjPSeq seq = NULL;
ajint nbases[5];
float molwt;

seq = ajAcdGetSeq("sequence");

if(ajSeqIsNuc(seq))
    ajSeqCalcCount(seq, *nbases);
else if(ajSeqIsProt(seq))
    molwt = ajSeqCalcMolwt(seq);
```

> **注意**
>
> 请注意，序列的各种计算属性（第 A.6 节，‘计算属性’），例如长度和类型，可在 ACD 文件级别使用。

## 6.7.11 序列字符串函数

有两个函数可将序列复制到字符串中，目标可以是 EMBOSS 字符串或 C 类型（char *）字符串：

```
char* ajSeqGetSeqCopyC (const AjPSeq seq) ;
AjPStr ajSeqGetSeqCopyS (const AjPSeq seq) ;
```

有几个函数用于处理使用 AjPStr 对象作为字符串保存的序列。这些函数的前缀为 ajSeqstr。这里首先使用 ajSeqGetSeqCopyS 将序列复制到字符串中。计算蛋白质序列的分子量，或核苷酸序列的反向互补：

```
AjPSeq seq = NULL;
AjPStr str = NULL;
float molwt;

seq = ajAcdGetSeq("sequence");
str = ajSeqGetSeqCopyS(seq);

if(ajSeqIsNuc(seq))
    ajSeqstrReverse(&str);
else if(ajSeqIsProt(seq))
    molwt = ajSeqCalcMolwt(str);
```

## 6.7.12 处理序列

提供了各种用于处理序列的函数。您已经接触过 ajSeqTrim 和 ajSeqsetTrim，用于将序列修剪到其起始和结束区域，但也可以进行其他操作。例如，可以使用以下函数处理间隙字符：

```
void ajSeqGapFill (AjPSeq seq, ajuint len);
void ajSeqGapStandard(AjPSeq seq, char gapchar);
void ajSeqGapLen (AjPSeq thys, char gapc, char padc, ajuint ilen);
```

ajSeqGapFill 将间隙字符追加到序列，直到达到指定的最大序列长度。ajSeqGapStandard 使字符串中的所有间隙都使用提供的标准间隙字符。字符串中的任何破折号、波浪号、句号、问号或空格字符（- . ? ）都会被转换。ajSeqGapLen 将任何非序列字符设置为有效的间隙字符，并在必要时用额外的间隙填充到指定长度。

要计算序列中的间隙数（计算任何可能的间隙字符），请调用 ajSeqCountGaps：

```
ajuint ajSeqCountGaps (const AjPSeq seq);
```

如果尚未从 ACD 或命令行处理中完成，则可用函数对核苷酸序列进行互补，或反向互补：

```
void ajSeqComplement (AjPSeq seq);
void ajSeqReverseDo (AjPSeq seq);
```

有几个函数可将序列或集合中所有序列转换为小写或大写：

```
void ajSeqsetFmtLower (AjPSeqset seq);
void ajSeqsetFmtUpper (AjPSeqset seq);
void ajSeqFmtLower (AjPSeq thys);
void ajSeqFmtUpper (AjPSeq thys);
```

ajSeqsetFill 可用于通过在任何短序列的末尾放置间隙来填充序列集：

```
ajint ajSeqsetFill(AjPSeqset seq);
```

## 6.7.13 序列类型验证

在大多数情况下，序列类型的验证（参见第 A.7 节，‘序列类型’），例如序列是用于蛋白质还是核酸，是否包含间隙等，是在 ACD 文件级别处理的。这意味着应用程序始终接收（通过调用 ajAcdGet*）与 ACD 文件中指定的精确类型相符的序列。

AJAX 中提供了几个函数用于直接处理序列类型。可以通过调用 ajSeqType 自动设置序列的类型，即从序列本身确定。否则，可以使用以下函数直接为序列或序列集设置为核苷酸或蛋白质之一：

```
void ajSeqType (AjPSeq thys);
void ajSeqSetNuc (AjPSeq thys);
void ajSeqSetProt (AjPSeq thys);
void ajSeqsetSetNuc (AjPSeqset thys);
void ajSeqsetSetProt (AjPSeqset thys);
```

## 6.7.14 序列转换

有时有必要将序列转换为数值形式以便于处理。AJAX 用于此目的的数据类型是：

- AjPSeqCvt 用于将序列转换为数值形式

常见用例是为评分矩阵生成序列字符转换表，例如氨基酸替换评分矩阵（参见第 6.10 节，‘处理比较矩阵’）。

## 6.7.15 处理序列翻译

将遗传序列翻译为蛋白质是一项常见任务，并在其他地方介绍（第 6.8 节，‘处理序列翻译’）。

## 6.7.16 处理 IUB 碱基代码

EMBOSS 支持下面所示的官方 IUB 碱基代码，还支持 X 表示未知碱基。

### 6.7.16.1 无歧义代码

无歧义碱基代码为：

- A（腺嘌呤）
- C（胞嘧啶）
- G（鸟嘌呤）
- T（胸腺嘧啶）或 U（尿嘧啶）

### 6.7.16.2 歧义代码

两种碱基之一：

- M（A 或 C）
- R（A 或 G）
- W（A 或 T/U）
- S（C 或 G）
- Y（C 或 T/U）
- K（G 或 T/U）

三种碱基之一：

- B（C、G 或 T/U）
- D（A、G 或 T/U）
- H（A、C 或 T/U）
- V（A、C 或 G）

四种碱基之一：

- N（A、C、G 或 T/U）

未知（或非标准）碱基：

- X（不是 A、C、G 或 T/U）

### 6.7.16.3 处理 IUB 碱基代码

标准 IUB 碱基代码有四种可能性，可以表示为 4 位二进制，以便快速比较，包括测试歧义代码。提供了用于碱基代码字符和二进制表示的函数。

歧义代码及其数值表示从本地数据文件 Ebases.iub 中读取。

```
/* Sets up binary OR representation of all IUB bases in
a table aj_base_table where A=1,
C=2, G=4 and T=8. Also sets up a match probability array aj_base_prob holding the
probability of one IUB base matching any other. Uses the Ebases.iub file. Is
initialised if necessary from other AJAX functions. *\/
/* Complements a nucleotide base. *\/
char ajBaseAlphacharComp(char base);
/* Returns an element of the base match probability array *\/
float ajBaseAlphaCompare(ajint base1, ajint base2);
```

要清理用于序列碱基处理内部维护的内存，请调用 ajBaseExit：

```
void ajBaseExit (void);
```

这由 embExit 自动调用。

### 6.7.16.4 碱基和氨基酸代码的转换

用于将碱基代码的整数表示转换为其他形式的函数：

```
/* Convert to string of matching base code(s). *\/
const AjPStr ajBaseGetCodes (ajint ibase);
/* Convert to base code: 0 to 'A', 1 to 'B' ... 25 to 'Z'. Returns an integer. *\/
ajint ajBasecodeFromInt (ajint n);
```

要将碱基代码转换为其他形式：

```
/*Convert to integer: 'A' to 0, 'B' to 1, ... 'Z' to 25. Returns an integer.*\/
ajint ajBasecodeToInt (ajint c);
/* Convert to binary OR representation of an IUB base. *\/
ajint ajBaseAlphaToBin (ajint c);
/* Convert to binary OR representation of an IUB base. *\/
char ajBaseAlphacharToBin (char c);
```

ajBaseAlphaToBin 和 ajBaseAlphacharToBin 返回 IUB 碱基的二进制 OR 表示，其中 A = 1、C = 2、G = 4 和 T = 8。这些函数使用内部碱基表。

要将 IUB 碱基的二进制 OR 表示转换为其他形式：

```
/* Converts a binary OR representation of an IUB base to an ambiguous DNA base code. *\/
char ajBaseBinToAlpha (ajint c);
```

ajBaseBinToAlpha 将 IUB 碱基的二进制 OR 表示（其中 A = 1、C = 2、G = 4 和 T = 8）转换为歧义 DNA 碱基代码（使用 T 而不是 U）。它使用内部碱基表。

要在单字母和三字母氨基酸代码之间相互转换：

