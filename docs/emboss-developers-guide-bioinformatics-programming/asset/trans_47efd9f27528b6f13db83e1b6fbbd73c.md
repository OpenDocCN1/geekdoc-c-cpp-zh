

### 6.20.14 获取图表属性

获取图表属性的函数具有前缀 ajGraphGet：

```
ajGraphGetSubtitleC		/* Graph subtitle. */
ajGraphGetTitleC		/* Graph title. */
ajGraphGetXlabelC		/* x-axis title */
ajGraphGetYlabelC		/* y-axis title */
ajGraphicsGetFgcolour		/* Current foreground colour. */
ajGraphicsBasecolourNewNuc	/* Base colours array for nucleotide sequence. */
ajGraphicsBasecolourNewProt	/* Base colours array for protein sequence. */
ajGraphicsGetCharsize		/* Character size. */
ajGraphGetParamsPage		/* Output device parameters. */
```

返回图表标题的函数返回字符串对象本身（而非副本），因此必须小心，不要无意中更改或删除它。

ajGraphicsGetFgcolour 将当前前景颜色作为整数返回：

```
ajint ajGraphicsGetFgcolour (void);
```

ajGraphicsCheckColourC 接受一个表示颜色的字符串参数，并返回与该颜色对应的整数，如果未找到该颜色，则返回 -1。

```
ajint ajGraphicsCheckColourS (const AjPStr colour);
ajint* ajGraphicsBasecolourNewNuc (const AjPStr codes);
ajint* ajGraphicsBasecolourNewProt (const AjPStr codes);
```

下面的代码从 ACD 文件处理中获取用户指定为字符串的颜色。会调用 ajGraphicsCheckColourC 来获取颜色的整数值，然后将其传递给 ajGraphicsSetFgcolour 以设置前景颜色：

```
AjPStr colour = NULL;
ajint colouri;
colour = ajAcdGetString("colour");
colouri = ajGraphicsCheckColourC(colour);
if(colouri == -1)
    colouri = GREY;
ajGraphicsSetFgcolour(colouri);
```

ajGraphicsGetCharsize 检索默认和当前字符大小。在设置其他图形元素的大小时很有用：

```
void ajGraphicsGetCharsize (float *defheight, float *currentheight);
```

ajGraphicsGetParamsPage 获取在 PLplot 内部定义的输出设备参数。这些参数的用处可能不如人们预期的那样大，因为有些参数针对每个设备驱动程序是硬编码的，或者只是 PLplot 中被忽略的用户值副本。在需要绘图尺寸时，请使用 ajGraphOpenMm 并以毫米为单位工作。

### 6.20.15 图表的计算属性

以下函数返回从图表中派生的一些计算值（以用户坐标表示）：

```
ajGraphicsCalcCoord    /* coordinates of a point on a circle knowing the angle. */
ajGraphicsCalcDistance /* Distances between 2 points. */
ajGraphicsCalcTextlengthC /* Text length. */
ajGraphicsCalcTextheight /* Text height. */
ajGraphicsCalcCharsize /* Text size (mm) to needed for given text length and height. */
```

有关如何使用这些函数的说明，请参阅在线文档。

### 6.20.16 图表调试函数

用于调试图表对象的函数具有前缀 ajGraphDebug。有关更多信息，请参阅在线文档。

### 6.20.17 直方图

直方图是图形绘制的一种特殊情况。提供了一组专用函数来处理底层图表对象和函数调用，因此您无需自行处理。

要绘制直方图，您首先必须创建一个直方图对象。提供了两个构造函数，它们接受数据集的数量（numofsets），每个集合都必须具有相同数量的数据点（numofpoints）：

```
AjPHist ajHistNew (ajint numofsets, ajint numofpoints);
AjPHist ajHistNewG (ajint numofsets, ajint numofpoints, AjPGraph graph);
```

ajHistNewG 还会将图表对象（作为参数传递）分配给返回的直方图。若干（numofsets）个图表会被添加到图表对象中。还会设置图表设备以及输出文件的名称和扩展名。

要为单集直方图设置标题，请使用以下函数之一：

```
/* Title */
void ajHistSetTitleC (AjPHist hist, const char* string);

/* x-axis label */
void ajHistSetXlabelC (AjPHist hist, const char* string);

/* y-axis left label */
void ajHistSetYlabelC (AjPHist hist,const char* string);

/* y-axis right label */
void ajHistSetRlabelC (AjPHist hist, const char* string);
```

要为多集直方图设置标题，请使用以下函数之一。index 是集中要将其标题设置为 title 的直方图的编号：

```
/* Title for histogram with multiple sets */
void ajHistSetmultiTitleC (AjPHist hist, ajint index, const AjPStr title);
/* x-axis title */
void ajHistSetmultiXlabelC (AjPHist hist, ajint index, const AjPStr title);
/* y-axis title */
void ajHistSetmultiYlabelC (AjPHist hist, ajint index, const AjPStr title);
```

ajHistSetmultiColour 和 ajHistSetmultiPattern 将为指定集（index）设置颜色或线型：

```
/* Set colour for bars in histogram */
void ajHistSetmultiColour(AjPHist hist, ajint index, ajint colour);
/* Set linestyle for set of bars */
void ajHistSetmultiPattern (AjPHist hist, ajint index, ajint style);
```

ajHistSetMono 对于单色打印很有用：

```
/* Set patterns instead of colours */
void ajHistSetMono (AjPHist hist, AjBool set);
```

要显示直方图，请调用 ajHistDisplay：

```
void ajHistDisplay (const AjPHist hist);
```

使用完直方图后，必须关闭输出文件并删除直方图对象。相关函数如下：

```
void ajHistogramClose (void);
void ajHistDel (AjPHist* hist);
```

ajHistDataAdd 和 ajHistDataCopy 用于为集中指定的直方图（index）指定一组数据点：

```
void ajHistDataAdd (AjPHist hist, ajint index, PLFLT *data);
void ajHistDataCopy (AjPHist hist, ajint index, const PLFLT *data);
```

ajHistDataAdd 将直方图设置为指向传递的数据，而 ajHistDataCopy 则复制数据。

下面的示例展示了一个函数，用于将整数数组（results）中保存的一组数据复制到直方图（hist）中。使用 ajHistDataCopy 来复制数据数组，因此可以删除 farray。如果改用 ajHistDataAdd，则不会调用 AJFREE：

```
void func(AjPHist hist, const ajint * results, ajint npts, ajint hist_num)
{
    ajint i;

    float *farray;

    AJCNEW(farray, npts);
    for(i=0; i<npts; i++)
        farray[i] = (float) results[i];

    ajHistDataCopy(hist, hist_num, farray);
    AJFREE(farray);
}
```

## 6.21 处理数学

### 6.21.1 简介

EMBOSS 提供了一个基本数学库，包括用于数据类型转换、随机数生成、舍入和其他基础功能的函数。

### 6.21.2 AJAX 库文件

用于处理数学的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整描述）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajmath | 通用数学函数 |
| ajvector | 用于处理向量的函数 |

ajmath.h/c。用于数字舍入、坐标转换、随机数生成等的通用数学函数。

ajvector.h/c。用于处理 3D 空间中向量的数据结构和函数。本文未对该库进行描述，有关更多信息，请参阅在线库文档。

### 6.21.3 ACD 数据类型

没有专门用于数学的 ACD 数据类型。

### 6.21.4 AJAX 数据类型

没有专门用于数学的 AJAX 数据类型。

### 6.21.5 转换函数

提供了用于在一种数据类型与另一种数据类型之间转换的函数。这些函数都具有前缀 ajCvt。要在极坐标和笛卡尔坐标之间相互转换、将弧度转换为角度，或根据高斯分布返回概率，请使用：

```
float ajCvtDegToRad (float degrees);
void ajCvtPolToRec (float radius, float angle, float* Px, float* Py);
float ajCvtRadToDeg (float radians);
void ajCvtRecToPol (float x, float y, float* Pradius, float* Pangle);
double ajCvtGaussToProb (float mean, float sd, float score);
```

序列位置通常由用户在命令行中指定。EMBOSS 支持序列位置的负值，这些值被解释为从序列 _末尾_ 开始的偏移量。提供了两个函数，用于将 EMBOSS 序列位置转换为真实位置（例如，可用于对序列本身进行索引）。这些函数返回 0（序列起始位置）到序列长度减 1 之间的整数：

```
ajint ajCvtSposToPos (ajint len, ajint ipos);
ajint ajCvtSposToPosStart (ajint len, ajint imin, ajint ipos);
```

在这两种情况下，len 是序列的长度，ipos 是位置。值 0 表示序列的起始位置，而负数表示从序列末尾开始的偏移量。可以指定最小相对位置（imin）。

### 6.21.6 随机数函数

有三个用于随机数生成的函数。这些函数基于 dprand 和 sdprand，并经 N. M. Maclaren（版权所有，剑桥大学）许可使用。ajRandomSeed 初始化随机数生成，必须在 ajRandomNumber（返回 0 到 32767 之间的随机整数）和 ajRandomDouble（返回 0.0 到 1.0 之间的随机双精度值）之前调用：

```
void ajRandomSeed (void);
double ajRandomNumber (void);
double ajRandomDouble (void);
```

### 6.21.7 舍入

有两个函数用于对数字进行舍入，要么将 float 舍入为 int，要么将 float 舍入为 float，并为累加指定保留的位数：

```
ajint ajRound (ajint i, ajint round);
float ajRoundFloat (float f, ajint nbits);
```

