

EMBOSS 已知类型（第 4.3.5.3.1 节，“应用程序数据已知类型文件（knowntypes.standard）”）然后 ApplicationName 输出是推荐值。

name: 数据文件通常具有硬编码的文件名。您可以使用 name: 属性来定义此项。

default: 数据文件通常具有硬编码的文件名。为 outdata: 定义了默认文件名，使用 default: 全局属性（如您所期望的，没有 name: 属性可用）。

## 6.14.5 AJAX 数据类型

用于处理 ACD 文件中定义的输入文件和目录，请使用：

- AjPFile: 非缓冲文件，可用于输入或输出（用于 infile 和 datafile ACD 数据类型）
- AjPList: 通用列表（用于 filelist 和 dirlist ACD 数据类型的文件列表）
- AjPDir: 可用于输入或输出的目录（用于 directory ACD 数据类型）

用于处理 ACD 文件中定义的输出文件和目录，请使用：

- AjPFile: 通用文件（用于 outfile ACD 数据类型）
- AjPDir: 目录（用于 outdir 和 directory ACD 数据类型）

用于处理 ACD 文件中定义的包括输出数据文件在内的通用输出文件，请使用：

- AjPOutfile: 非缓冲输出文件

用于处理缓冲文件，请使用：

- AjPFilebuff: 缓冲文件对象，保存缓冲输入文件的信息
- AjPFilebufflist: 文件缓冲区，保存缓冲行的简单链表。这是 AjPFilebuff 对象的子结构

## 6.14.6 ACD 文件处理

通过 ACD 文件处理文件的数据类型和函数如下所示。

| ACD 数据类型 | AJAX 数据类型 | 从 ACD 检索 |
|---|---|---|
| 文件输入 | | |
| infile | AjPFile | ajAcdGetInfile |
| filelist | AjPList | ajAcdGetFilelist |
| datafile | AjPFile | ajAcdGetDatafile |
| dirlist | AjPList | ajAcdGetDirlist |
| directory | AjPDir | ajAcdGetDirectory |
| 文件输出 | | |
| outfile | AjPFile | ajAcdGetOutfile |
| outdata | AjPOutfile | ajAcdGetOutdata |
| outdir | AjPDir | ajAcdGetOutdir |
| directory | AjPDir | ajAcdGetDirectory |

您的应用程序代码将调用 embInit 来处理 ACD 文件和命令行（参见第 6.3 节，“处理 ACD 文件”）。ACD 文件中的所有值都将读入内存，并根据需要打开文件。您可以通过 ajAcdGet* 函数系列对文件和内存进行控制，该系列函数返回指向相应对象的指针。

### 6.14.6.1 输入文件检索

要检索输入文件、文件列表等，需声明对象指针，然后使用相应的 ajAcdGet* 函数进行初始化。

### 6.14.6.1.1 输入文件

```
AjPFile pepstatsfile = NULL;
pepstatsfile = ajAcdGetInfile("pepstatsfile");
```

### 6.14.6.1.2 输入文件列表

```
AjPList files= NULL;
files = ajAcdGetFilelist("files");
```

### 6.14.6.1.3 输入数据文件

```
AjPFile aaproperties = NULL;
aaproperties = ajAcdGetDatafile("aaproperties");
```

### 6.14.6.1.4 从目录输入文件列表

```
AjPList filelist = NULL;
filelist = ajAcdGetDirlist("directory");
```

### 6.14.6.1.5 目录（输入或输出）

```
AjPDir directory = NULL;
directory = ajAcdGetDirectory("directory");
```

### 6.14.6.2 输出文件检索

要检索输出文件流、目录等，需声明对象指针并使用相应的 ajAcdGet* 函数进行初始化。

### 6.14.6.2.1 输出文件

```
AjPFile outfile = NULL;
outfile = ajAcdGetOutfile("outfile");
```

### 6.14.6.2.2 输出数据文件

```
AjPOutfile outfile = NULL;
outfile = ajAcdGetOutdata("outfile");
```

### 6.14.6.2.3 输出目录

```
AjPDir indexoutdir = NULL;
indexoutdir = ajAcdGetOutdir("indexoutdir");
```

### 6.14.6.2.4 目录（输入或输出）

```
AjPDir directory = NULL;
directory = ajAcdGetDirectory("directory");
```

### 6.14.6.3 替代 ACD 检索函数

要检索目录名而非目录本身，请调用 ajAcdGetDirectoryName（directory ACD 对象）或 ajAcdGetOutdirName（outdir ACD 对象）。这两个函数都将目录名作为字符串对象返回。目录和名称字符串由调用方所有，应在应用程序退出时释放。例如：

```
AjPDir directory  = NULL;
AjPDir indexoutdir = NULL;
AjPStr indir      = NULL;
AjPStr outdir     = NULL;

directory  = ajAcdGetDirectory("directory");
indexoutdir = ajAcdGetOutdir("indexoutdir");

indir  = ajAcdGetDirectoryName("directory");
outdir = ajAcdGetOutdirName("indexoutdir");

/* ... */

ajStrDel(&indir);
ajStrDel(&outdir);
ajDirDel(&indexoutdir);
```

### 6.14.6.4 处理命令行选项和 ACD 属性

目前没有用于此目的的函数。

### 6.14.6.5 内存和文件管理

在程序结束时，关闭任何文件并释放内存是您的责任。

### 6.14.6.5.1 关闭文件

要关闭输入文件或输入数据文件，请使用输入文件的地址调用 ajFileClose。要关闭输出文件，请使用输出文件的地址调用 ajOutfileClose。根据上述示例：

```
AjPFile pepstatsfile = NULL;
AjPFile outfile = NULL;

pepstatsfile = ajAcdGetInfile("pepstatsfile");
outfile = ajAcdGetOutfile("outfile");

/* Do something with files */

ajFileClose (&pepstatsfile);
ajOutfileClose(&outfile);
ajOutfileClose(&outfile);
```

在两种情况下，文件都会被关闭，文件对象的内存会被释放。

### 6.14.6.5.2 释放内存

您必须调用析构函数（见下文）来释放 ajAcdGet* 调用返回的任何对象所使用的内存。

## 6.14.7 文件和目录对象内存管理

### 6.14.7.1 默认对象构造

要使用未在 ACD 文件中定义的文件或目录对象，必须首先实例化相应的对象指针。下面描述的默认构造函数接受要打开的文件或目录的名称。

### 6.14.7.1.1 通用输入和输出文件

通用输入和输出文件的基本构造函数如下：

```
/* Input file */
AjPFile ajFileNewInNameS (const AjPStr name);
/* Input file */
AjPFile ajFileNewInNameC (const char* name);

/* Output file */
AjPFile ajFileNewOutNameS (const AjPStr name);

/* Output file */
AjPFile ajFileNewOutNameC (const char* name);

/* Perl-style Pipe. */
AjPFile ajFileNewInPipe (const AjPStr str);

/* Output file */
AjPOutfile ajOutfileNewNameS (const AjPStr name);
```

通常，您会将 AjPFile 用于输入，将 AjPOutfile 用于输出，因此应优先使用 ajOutfileNewNameS，而不是 ajFileNewOutNameS 或 ajFileNewOutNameC。

### 6.14.7.1.2 数据文件

输入数据文件的默认构造函数如下：

```
/* Input data file */
AjPFile ajDatafileNewInNameS (const AjPStr name);

/* Input data file */
AjPFile ajDatafileNewInNameC (const char* name);
```

这些函数将文件名作为 C 类型（char *）或字符串对象（AjPStr）接受，其余方面相同。如果在以下按所示顺序搜索的路径之一中存在指定文件，则它们将打开该文件：

1. .（当前工作目录）
2. ./.embossdata（EMBOSS 数据目录）
3. ~/(用户主目录）
4. ~/.embossdata（EMBOSS 数据目录）
5. $EMBOSS_DATA（EMBOSS 数据目录）

输出数据文件的默认构造函数如下：

```
AjPFile ajDatafileNewOutNameS (const AjPStr name);
```

ajDatafileNewOutNameS 将返回指向 EMBOSS 数据目录 ($EMBOSS_DATA) 中文件的文件对象指针。

### 6.14.7.1.3 缓冲输入文件

缓冲文件没有 ACD 数据类型，尽管有 AJAX 数据类型 (AjPFilebuff)。要使用缓冲文件，必须首先使用文件名、打开的文件或缓冲的数据行来实例化对象指针。基本构造函数如下：

```
/* Named buffered input file */
AjPFilebuff ajFilebuffNewNameS (const AjPStr name);

/* Named buffered input file and directory */
AjPFilebuff ajFilebuffNewNamePathS (const AjPStr name, const AjPStr path)

/* Named directory and wildcard filename to read all matching files */
AjPFilebuff ajFilebuffNewPathWild (const AjPStr path,
    const AjPStr wildname);

/* Named directory and wildcard filename to read all matching files with exceptions */
AjPFilebuff ajFilebuffNewPathWildExclude(const AjPStr path,
    const AjPStr wildname,
    const AjPStr exclude)

/* no file - to be loaded with data for re-reading */
AjPFilebuff ajFilebuffNewNofile (void);
```

ajFilebuffNewNofile 是一个原始构造函数，用于创建对象但不创建文件流，在 EMBOSS 的多个位置中使用，其中缓冲区将加载数据记录。示例可在处理序列数据库中找到。常用的构造函数是 ajFilebuffNewNameS，它将打开指定文件。

### 6.14.7.1.4 目录

为输入和输出提供了默认构造函数：

```
/* Directory for input */
AjPDir ajDirNewPath (const AjPStr path);

/* Directory for output */
AjPDir ajDiroutNewPath (const AjPStr path);
```

构造函数返回新对象的地址。指针不需要初始化为 NULL，但这样做是良好实践：

```
AjPFile    filein   = NULL;
AjPFilebuff buffin  = NULL;
AjPFile    datain   = NULL;

AjPOutfile fileout  = NULL;

AjPDir     dirin    = NULL;
AjPDir     dirout   = NULL;

AjPStr     fileout_name = NULL;
AjPStr     buffin_name  = NULL;
AjPStr     dirin_name   = NULL;
AjPStr     dirout_name  = NULL;
```

