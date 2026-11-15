

ajarr.h/c. 定义了用于处理动态数组的各种数组对象和函数。它还包含用于在低级别处理它们的静态函数。除非您计划扩展库的核心功能，否则不太可能需要这些。

ajsort.h/c. 用于对数组进行排序的函数（第 6.17.10 节，“对数组进行排序”）。

## 6.17.3 AJAX 数据类型

用于处理在 ACD 文件中定义的输入数组，请使用：

AjPFloat 浮点数数组（用于数组 ACD 数据类型）

AJAX 为基本 C 数据类型（第 5.1 节，“基本数据类型”）提供了以下动态数组对象。

## 6.17.3.1 char 数组

- AjPChar 一维字符数组

## 6.17.3.2 short 数组

- AjPShort 一维 short 数组
- AjPShort2d 二维 short 数组
- AjPShort3d 三维 short 数组

## 6.17.3.3 unsigned int 数组

- AjPUint 一维无符号整数数组
- AjPUint2d 二维无符号整数数组
- AjPUint3d 三维无符号整数数组

## 6.17.3.4 int 数组

- AjPInt 一维整数数组
- AjPInt2d 二维整数数组
- AjPInt3d 三维整数数组

## 6.17.3.5 float 数组

- AjPFloat 一维 float 数组
- AjPFloat2d 二维 float 数组
- AjPFloat3d 三维 float 数组

## 6.17.3.6 long 数组

- AjPLong 一维 long 数组
- AjPLong2d 二维 long 数组
- AjPLong3d 三维 long 数组

## 6.17.3.7 double 数组

- AjPDouble 一维 double 数组
- AjPDouble2d 二维 double 数组
- AjPDouble3d 三维 double 数组

## 6.17.4 ACD 数据类型

用于处理数组输入的 ACD 数据类型是：

- array 整数或浮点数列表

## 6.17.5 ACD 数据定义

数组输入的典型 ACD 定义：

```
array: thresholds
[
  information: "Values to represent 'identical', 'similar' and 'related'"
  default: "-1.5,0.0,1.5"
  minimum: "0.0"
  size: "3"
  sum: "0"
  sumtest: "Y"
]
```

## 6.17.5.1 参数名称

所有数组输入的数据定义都应具有直观的名称（附录 A.1.3，“参数命名约定”），尽管不强制执行标准命名方案。

## 6.17.5.2 常用属性

通常指定的属性摘要如下。除非它们被指示为全局属性（附录 A.4，“全局属性”），否则它们都是特定于数据类型的（附录 A.5，“特定于数据类型的属性”）。

- default：一个全局属性，用于指定默认值。

- minimum：指定允许的最小值。

size: 指定数组数据定义中允许的元素数量。

sum: 指定数组数据定义中所有值的总和，除非 sumtest 属性为 false，否则会对其进行测试。

sumtest: 一个布尔属性，如果关闭，则会关闭对数组数据定义的 sum: 属性的测试。

## 6.17.6 ACD 文件处理

通过 ACD 文件处理数组的数据类型和函数如下所示。

| 标题 | 读取数组 |
| :--- | :--- |
| ACD 数据类型 | array |
| AJAX 数据类型 | AjPFloat |
| 从 ACD 检索 | ajAcdGetArray |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并在必要时打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，该系列函数返回指向相应对象的指针。

## 6.17.6.1 输入数组检索

要检索输入数组，需声明一个对象指针，然后使用 ajAcdGetArray 进行初始化：

```
AjPFloat thresholds=NULL;
thresholds = ajAcdGetArray("thresholds");
```

## 6.17.6.2 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

## 6.17.6.3 内存管理

在程序结束时释放内存是您的责任。您必须对 ajAcdGetArray 调用返回的任何数组对象调用默认析构函数（见下文）。

## 6.17.7 函数名称

处理数组的函数名称具有一致的前缀，其一般形式如下：

```
ajTypeDim
```

Type 是数组的类型，为以下之一：

- Chararr（字符数组）
- Short（ajshort 数组）
- Uint（ajuint 整数数组）
- Int（ajint 数组）
- Float（float 数组）
- Long（ajlong 数组）
- Double（double 数组）

Dim 是数组的维度。对于一维数组，*不*给出：

- 2d（二维数组）
- 3d（三维数组）。

例如，所有处理无符号整数二维数组的函数都具有前缀 ajUint2d，而所有处理 float 一维数组的函数都具有前缀 ajFloat。提供了用于处理一维、二维和三维数组的函数；但是，仅支持一维字符数组。

## 6.17.8 数组对象内存管理

### 6.17.8.1 默认对象构造

要使用未在 ACD 文件中定义的数组对象，必须首先实例化相应的对象指针。默认构造函数的后缀为 New：

```
AjPChar		 ajCharrNew (void);
AjPShort		 ajShortNew (void);
AjPShort2d	 ajShort2dNew (void);
AjPShort3d	 ajShort3dNew (void);
AjPUint		 ajUintNew (void);
AjPUint2d	 ajUint2dNew (void);
AjPUint3d	 ajUint3dNew (void);
AjPInt		 ajIntNew (void);
AjPInt2d	 ajInt2dNew (void);
AjPInt3d	 ajInt3dNew (void);
AjPFloat		 ajFloatNew (void);
AjPFloat2d	 ajFloat2dNew (void);
AjPFloat3d	 ajFloat3dNew (void);
AjPLong		 ajLongNew (void);
AjPLong2d	 ajLong2dNew (void);
AjPLong3d	 ajLong3dNew (void);
AjPDouble		 ajDoubleNew (void);
AjPDouble2d	 ajDouble2dNew (void);
AjPDouble3d	 ajDouble3dNew (void);
```

所有构造函数都返回新对象的地址。指针不需要事先初始化为 NULL，但这样做是良好的实践。上述所有函数的使用方式相同：

```
AjPShort2d shorts = NULL;
shorts = ajShort2dNew();
/* The objects are instantiated and ready for use */
```

### 6.17.8.2 默认对象销毁

在使用完对象后，必须释放其内存。默认析构函数的后缀为 Del，并以相应对象的地址作为参数：

```
void ajCharrDel (AjPChar* Parr);
void ajShortDel (AjPShort* Parr);
void ajShort2dDel (AjPShort2d* Parr);
void ajShort3dDel (AjPShort3d* Parr);
void ajUintDel (AjPUint* Parr);
void ajUint2dDel (AjPUint2d* Parr);
void ajUint3dDel (AjPUint3d* Parr);
void ajIntDel (AjPInt* Parr);
void ajInt2dDel (AjPInt2d* Parr);
void ajInt3dDel (AjPInt3d* Parr);
void ajFloatDel (AjPFloat* Parr);
void ajFloat2dDel (AjPFloat2d* Parr);
void ajFloat3dDel (AjPFloat3d* Parr);
void ajLongDel (AjPLong* Parr);
void ajLong2dDel (AjPLong2d* Parr);
void ajLong3dDel (AjPLong3d* Parr);
void ajDoubleDel (AjPDouble* Parr);
void ajDouble2dDel (AjPDouble2d* Parr);
void ajDouble3dDel (AjPDouble3d* Parr);
```

例如，要释放由 ACD 文件中的数组输入分配的内存，请使用：

```
void ajFloatDel (AjPFloat* Parr);
```

其用法如下：

```
AjPFloat thresholds=NULL;
thresholds = ajAcdGetArray("thresholds");
/* Do something with the array */
ajFloatDel(&thresholds);
```

调用函数有责任在使用完对象后将其销毁：

```
AjPShort2d shorts = NULL;
shorts = ajShort2dNew();
/* The object is instantiated and ready for use */
/* Do something with the instantiated objects */
ajShort2dDel(&shorts);
/* The memory is freed and the pointers reset to NULL, ready for re-use. */
shorts = ajShort2dNew();
/* Do something else with the new objects. The pointer variable is reallocated. */
```

```
ajShort2dDel(&shorts);
/* The objects are done with so the memory is freed. */
```

### 6.17.8.3 替代对象构造和加载

可以使用后缀为 NewRes 的函数构造具有固定预留大小的数组。此类函数接受一个整数参数（size）作为预留大小，但其余部分与默认构造函数相同。以下仅显示部分可用函数：

```
AjPChar ajCharrNewRes (ajint size);
AjPShort ajShortNewRes (ajint size);
AjPShort2d ajShort2dNewRes (ajint size);
AjPShort3d ajShort3dNewRes (ajint size);
AjPUint ajUintNewRes (ajint size);
AjPUint2d ajUint2dNewRes (ajint size);
...
```

## 6.17.9 获取和设置数组元素

如果您将值分配给超出当前数组大小的数组元素，则数组将动态重新分配到足够大的大小以容纳新元素。如果您尝试检索超出当前数组大小的数组元素，将生成错误。

因此，预先知道数组的大小很有用。用于检索数组大小的函数具有后缀 Len，对于一维数组，它们返回数组长度；对于二维和三维数组，它们通过参数写入长度。同样，此处仅显示部分函数：

```
ajint ajCharrLen (const AjPChar arr);
ajint ajShortLen (const AjPShort arr);
void ajShort2dLen (const AjPShort2d arr, ajint* Pn1, ajint* Pn2);
void ajShort3dLen (const AjPShort3d arr,ajint* Pn1, ajint* Pn2, ajint* Pn3);
ajint ajUintLen (const AjPUint arr);
void ajUint2dLen (const AjPUint2d arr, ajint* Pn1, ajint* Pn2);
...
```

例如，要获取三维 double 数组的大小：

```
AjPDouble3d arr = NULL;
ajint dim1;
ajint dim2;
ajint dim3;
/* Allocate array */
ajDouble3dLen(arr, &dim1, &dim2, &dim3);
```

用于检索数组元素的函数具有后缀 Get。它们接受要检索的元素的索引并返回相应的数据类型：

