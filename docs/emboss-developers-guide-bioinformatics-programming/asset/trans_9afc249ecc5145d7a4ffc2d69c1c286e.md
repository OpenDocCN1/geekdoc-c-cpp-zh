

```c
AjPStr inputstring = NULL;
AjPStr token       = NULL;

inputstring = ajStrNewC(" First word in this string is 'First'");
token = ajStrParseWhite(inputstring);

/* Prints 'First' to the screen */
ajFmtPrint("token: %S\n", token);

/* Prints the rest of the words, one word at a time */
while(token = ajStrParseWhite(NULL))
    ajFmtPrint("token: %S\n", token);

ajStrDel(&inputstring);
```

要统计字符串中的标记数量，其中标记由空白字符或指定的分隔符集（strdelim）分隔，请使用：

```
/* Count tokens delimited by whitespace */
ajuint ajStrParseCount (const AjPStr line);

/* Count tokens delimited by set of delimiters */
ajuint ajStrParseCountS (const AjPStr line, const AjPStr strdelim);
```

## 6.5.22 处理 C 类型（char *）字符串

为方便起见，提供了多组用于处理 C 类型（char *）字符串的函数。它们都带有 ajChar 前缀，以便与其他函数区分。

### 6.5.22.1 C 类型字符串构造函数和析构函数

与 EMBOSS 字符串一样，C 类型字符串可以从起始的 C 类型（char *）或字符串对象创建，可以带有保留大小，也可以不带：

```
/* Create a string from a C-type string         */
char*   ajCharNewC (const char* txt);

/* Create a string from a string object         */
char*   ajCharNewS (const AjPStr this);

/* Create an empty string of reserved size.     */
char*   ajCharNewRes(ajuint size);

/* Create a string with reserved size from a C-type string */
char*   ajCharNewResC(const char* txt, ajuint size);

/* Create a string with reserved size from a string object */
char*   ajCharNewResS(const AjPStr str, ajuint size);

/* Create a string from a C-type string with specified length */
char*   ajCharNewResLenC(const char* txt, ajuint size, ajuint len);
```

在所有情况下，都会返回指向已分配内存的指针，使用完毕后必须释放它。要删除 C 类型字符串，请调用：

```
void ajCharDel (char** Ptxt);
```

示例：

```
char* string = NULL;
string = ajCharNewC("This is a text string");
ajCharDel(&string);
```

### 6.5.22.2 C 类型字符串比较函数

大多数字符串比较函数（第 6.5.17 节，“字符串比较函数”）也可用于 C 类型字符串：

```
AjBool ajCharMatchC (const char* txt1, const char* txt2);
AjBool ajCharMatchCaseC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildCaseC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildNextC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildWordC (const char* str, const char* txt);
AjBool ajCharMatchWildNextCaseC (const char* txt1, const char* txt2);
AjBool ajCharMatchWildWordCaseC (const char* str, const char* txt);
AjBool ajCharPrefixC (const char* txt, const char* pref);
AjBool ajCharPrefixCaseC (const char* txt, const char* pref);
AjBool ajCharSuffixC (const char* txt, const char* suff);
AjBool ajCharSuffixCaseC (const char* txt, const char* suff);
```

这些函数的变体版本（未显示）接受字符串对象作为第二个参数，其后缀为 S 而非 C。

## 6.5.23 处理字符串格式化

用于格式化和打印字符串的函数定义在库文件 ajfmt.h/c 中。所有 EMBOSS 基本数据类型（第 5.1 节，“基本数据类型”）都定义了转换字符，它们是基本 C 转换代码的扩展。它们如下：

- AJAX 字符串对象 `AjPStr` 由 `%S` 打印
- C 类型（`char*`）字符串由 `%s` 打印。如果指针为 `NULL`，则打印 `<null>`
- AJAX 文件对象 `AjPFile` 的文件名由 `%F` 打印
- 布尔变量 `AjBool` 由 `%b` 打印（输出为“Y/N”）或 `%B`（“Yes/No”）
- 日期和时间（`AjPDate`）由 `%D` 打印

带有 ajFmtScan 前缀的函数相当于 C 的 *scan* 函数：

```
ajint ajFmtScanS (const AjPStr str, const char* fmt, ...);
ajint ajFmtScanC (const char* txt, const char* fmt, ...);
ajint ajFmtScanF (AjPFile this, const char* fmt, ...);
```

带有 ajFmtPrint 前缀的函数相当于 C 的 *print* 函数：

```
/* format and emit the "..." arguments according to fmt; writes to stdout */
void ajFmtPrint (const char *fmt, ...);

/* format and emit the "..." arguments according to fmt; writes to a file object */
void ajFmtPrintF (AjPFile file,
    const char *fmt, ...);

/* format and emit the "..." arguments according to fmt; writes to C FILE stream */
void ajFmtPrintFp (FILE *stream,
    const char *fmt, ...);

/* formats the "..." arguments into a buffer with a maximum size according to fmt */
ajint ajFmtPrintCL (char *buf, ajint size,
    const char *fmt, ...);

/* Block and print a string. String is split at given delimiters */
void ajFmtPrintSplit(AjPFile outf, const AjPStr str,
    const char *prefix, ajint len,
    const char *delim);

/* Formats the "..." arguments into an AjPStr according to fmt */
AjPStr ajFmtPrintS (AjPStr *pthis, const char *fmt, ...);

/* Formats the "..." arguments and appends to an AjPStr according to fmt */
AjPStr ajFmtPrintAppS (AjPStr *pthis, const char *fmt, ...);
```

## 6.6 处理序列模式

### 6.6.1 简介

正则表达式和其他模式用于识别分子序列中的基序。

### 6.6.2 AJAX 库文件

用于处理模式的 AJAX 库文件如下表所示。库文件文档（包括数据类型和函数的完整说明及使用笔记）可在以下网址查阅：http://emboss.open-bio.org/rel/dev/libs/

| 库文件文档 | 描述 |
|---|---|
| ajreg | 正则表达式处理 |
| ajpat | 模式处理 |

ajreg.h/c 定义了正则表达式对象（AjPRegexp）和用于处理正则表达式的函数。

ajpat.h/c 定义了序列模式列表对象（AjPPatlistSeq）和常规模式列表对象（AjPPatlistRegex）以及用于处理正则表达式模式列表的函数。它们包含用于在低级别处理序列模式的静态数据结构和函数。

除非您计划实现代码以扩展库本身的功能，否则不太可能需要这些静态数据结构和函数。

除上述库文件外，EMBOSS 还包含一个函数库，用于支持语法和语义尽可能接近 Perl 5 语言的正则表达式。库文件如下：

```
pcre_config.h
pcre_internal.h
pcre.h
pcre.c
pcreposix.h
pcreposix.c
pcre_printint.c
pcre_chartables.c
pcre_get.c
pcre_study.c
```

此处未对其进行描述，有关更多信息，请参阅在线库文档。

### 6.6.3 ACD 数据类型

有两种用于处理模式输入的数据类型：

- regexp：正则表达式模式
- pattern：序列模式

### 6.6.4 ACD 数据定义

典型的 ACD 定义如下所示。

### 6.6.4.1 regexp

正则表达式输入：

```
regexp: patterns
[
    information: "Regular expression patterns"
    upper: "Y"
    minlength: "3"
    minlength: "10"
]
```

### 6.6.4.2 pattern

模式输入：

```
pattern: seqpatterns
[
    information: "Sequence patterns"
    type: "nucleotide"
    pmismatch: "0"
]
```

### 6.6.4.3 参数名称

所有模式或正则表达式输入的数据定义都应具有标准参数名称 pattern（参见 ）。

### 6.6.4.4 常用属性

通常指定的属性摘要如下。这些属性包括各种特定于数据类型的属性（第 A.5 节，“特定于数据类型的属性”）。

- **最小长度：** 指定正则表达式的最小长度。这用于确保已定义表达式。
- **最大长度：** 指定正则表达式的最大长度。
- **最大大小：** 指定将从文件中读取的模式的最大数量。
- **大小写：** 将正则表达式的大小写设置为大写。`lower` 也可用（只能给出一个）。
- **类型：** 定义正则表达式或模式为 `nucleotide` 或 `protein`，这允许模式匹配使用序列歧义代码。默认情况下，类型为 `string`，它使用精确字符匹配。
- **模式不匹配数：** 设置模式中允许的不匹配数量。正则表达式算法不允许此操作，因此仅适用于序列模式。
- **模式名称：** 设置用于输出的模式名称。多个输入模式会在此名称后附加数字。
- **模式格式：** 定义模式或正则表达式输入格式。默认是将字符串用作模式，或（如序列输入一样）以 `@filename` 形式读取字符串作为模式文件。如果该文件的格式定义为 ‘fasta’，则它具有一个带有可选 `mismatch=nn` 项的 FASTA 风格标识符行，用于设置每个模式的不匹配数量（不匹配不适用于正则表达式）。默认格式是每行一个序列，名称使用 `-pname` 限定符自动定义。

