

## 6 使用 AJAX 进行编程

### 6.5.12 字符串替换函数

字符串替换函数将使用其他字符或子串来替换字符串中的字符或子串。

前缀为 ajStrExchange 的函数将把字符串中一个子串（或字符）的所有出现替换为另一个字符串（或字符）。该函数的变体支持用于目标和替换子串的字符串对象（AjPStr）和 C 类型（char *）字符串：

```c
/* C-type string target and replacement. */
AjBool ajStrExchangeCC (AjPStr* Pstr, const char* txt, const char* txtnew);

/* C-type string target, string replacement */
AjBool ajStrExchangeCS (AjPStr* Pstr, const char* txt, const AjPStr strnew);

/* Character target and replacement */
AjBool ajStrExchangeKK (AjPStr* Pstr, char chr, char chrnew);

/* String target, C-type string replacement */
AjBool ajStrExchangeSC (AjPStr* Pstr, const AjPStr str, const char* txtnew);

/* String target and replacement */
AjBool ajStrExchangeSS (AjPStr* Pstr, const AjPStr str, const AjPStr strnew);
```

前缀为 ajStrExchangeSet 的函数类似，只不过它们将把字符串中一组字符的所有出现替换为另一个字符或一组字符。该函数的变体使用字符串对象（AjPStr）和 C 类型（char *）字符串来定义这些集合：

```c
/* C-type string target and replacement sets */
AjBool ajStrExchangeSetCC (AjPStr* Pstr, const char* txt, const char* newc);

/* String target and replacement sets */
AjBool ajStrExchangeSetSS (AjPStr* Pstr, const AjPStr str, const AjPStr strnew);

/* Replace C-type target with single character */
AjBool ajStrExchangeSetRestCK (AjPStr* Pstr, const char* txt, char chr);

/* Replace string target with single character */
AjBool ajStrExchangeSetRestSK (AjPStr* Pstr, const AjPStr str, char chr);
```

### 6.5.13 字符串查询函数

字符串查询函数用于测试字符串的属性。所有前缀为 ajStrIs 的函数，如果字符串满足某些基本测试，则返回 ajTrue。以下函数说明了可以执行的查询测试范围，但完整列表请参阅在线文档：

```c
/* Alphanumeric characters only. */
AjBool ajStrIsAlnum (const AjPStr str);

/* Alphabetic characters only. */
AjBool ajStrIsAlpha (const AjPStr str);

/* Represents Boolean value. */
AjBool ajStrIsBool (const AjPStr str);

/* Represents integer value. */
AjBool ajStrIsInt (const AjPStr str);

/* Represents float value. */
AjBool ajStrIsFloat (const AjPStr str);

/* No uppercase alphabetic characters. */
AjBool ajStrIsLower (const AjPStr str);

/* Decimal digits only. */
AjBool ajStrIsNum (const AjPStr str);

/* Uppercase alphabetic characters only. */
AjBool ajStrIsUpper (const AjPStr str);
```

### 6.5.14 字符串属性和字符检索函数

为方便起见，提供了宏来检索字符串的属性，包括其长度、C 类型（char *）字符串、使用计数和当前保留大小。这些函数都返回字符串 C 数据结构的一个元素：

```c
#define MAJSTRGETLEN(str) str->Len /* String length */
#define MAJSTRGETPTR(str) str->Ptr /* String char * pointer */
#define MAJSTRGETRES(str) str->Res /* Reserved length */
#define MAJSTRGETUSE(str) str->Use /* Usage count */
```

可以使用函数从字符串中返回单个字符。

```c
/* Get first character */
char ajStrGetCharFirst (const AjPStr str);

/* Get last character */
char ajStrGetCharLast (const AjPStr str);

/* Get character from specified position */
char ajStrGetCharPos (const AjPStr str, ajint pos);
```

### 6.5.15 字符串转换函数

字符串可以使用以下某个函数转换为其他数据类型：

```c
AjBool ajStrToBool (const AjPStr str, AjBool* Pval); /* To boolean */
AjBool ajStrToDouble (const AjPStr str, double* Pval); /* To double */
AjBool ajStrToFloat (const AjPStr str, float* Pval); /* To float */
AjBool ajStrToHex (const AjPStr str, ajint* Pval); /* To hexadecimal */
AjBool ajStrToInt (const AjPStr str, ajint* Pval); /* To integer */
AjBool ajStrToLong (const AjPStr str, ajlong* result); /* To long */
AjBool ajStrToUint (const AjPStr str, ajuint* Pval); /* To unsigned integer */
```

在所有情况下，如果转换成功执行，函数均返回 ajTrue。它们采用适当类型变量的地址。例如，要将字符串转换为整数值：

```c
ajint val = 0;
AjPStr str = NULL;

str = ajStrNewC("10");

if (!ajStrToInt(str, &val))
    ajFatal("This error message will not be printed.");

ajStrDel(&str);
```

相反，可以使用以下函数将 C 数据类型转换为 EMBOSS 字符串：

```c
AjBool ajStrFromBool (AjPStr* Pstr, AjBool val); /* From bool */
AjBool ajStrFromDouble (AjPStr* Pstr, double val, ajint precision); /* From double */
AjBool ajStrFromDoubleExp (AjPStr* Pstr, double val, ajint precision); /* From double in exponential form. */
AjBool ajStrFromFloat (AjPStr* Pstr, float val, ajint precision); /* From float */
AjBool ajStrFromInt (AjPStr* Pstr, ajint val); /* From integer */
AjBool ajStrFromLong (AjPStr* Pstr, ajlong val); /* From long */
AjBool ajStrFromUint (AjPStr* Pstr, ajuint val); /* From unsigned integer */
```

同样，这些函数在转换成功执行时返回 ajTrue，并采用字符串的地址。例如，要将整数转换为字符串：

```c
ajint val = 0;
AjPStr str = NULL;

str = ajStrNew();
val = 100;

if (!ajStrFromInt(&str, val))
    ajFatal("This error message will not be printed.");

ajStrDel(&str);
```

### 6.5.16 字符串格式化函数

用于重新格式化字符串的函数具有前缀 ajStrFmt。例如，可以使用以下函数将字符串或字符串区域转换为大写或小写：

```c
/* Convert to lower-case */
AjBool ajStrFmtLower (AjPStr* Pstr);

/* Convert region to lower-case */
AjBool ajStrFmtLowerSub (AjPStr* Pstr, ajint pos1, ajint pos2);

/* Convert to upper-case */
AjBool ajStrFmtUpper (AjPStr* Pstr);

/* Convert region to upper-case */
AjBool ajStrFmtUpperSub (AjPStr* Pstr, ajint pos1, ajint pos2);
```

要重新格式化的字符串的地址会被传递，如果重新格式化成功，则返回 ajTrue。有关其他格式化函数，请参阅在线文档。

### 6.5.17 字符串比较函数

EMBOSS 提供全面的字符串比较函数。

前缀为 ajStrMatch 的函数将一个字符串与另一个字符串进行比较。这些函数执行区分大小写和不区分大小写的比较，可带通配符字符，也可不带。有关以 C 类型（char *）字符串作为第二个参数的变体函数可用，但此处未显示：

```c
/* Simple string to C-type string comparison */
AjBool ajStrMatchC (const AjPStr thys, const char* txt);

/* Simple string to string comparison */
AjBool ajStrMatchS (const AjPStr thys, const AjPStr str);

/* Case-insensitive string to string comparison */
AjBool ajStrMatchCaseS (const AjPStr thys, const AjPStr str);

/* String to string comparison with wildcards */
AjBool ajStrMatchWildS (const AjPStr thys, const AjPStr wild);

/* Case-insensitive string to string comparison with wildcards */
AjBool ajStrMatchWildCaseS (const AjPStr thys, const AjPStr wild);
```

以下函数将比较字符串中的前两个单词：

```c
/* String to C-type string comparison with wildcards. */
AjBool ajStrMatchWildWordC (const AjPStr str, const char* text);

/* String to string comparison with wildcards. */
AjBool ajStrMatchWildWordS (const AjPStr str, const AjPStr text);

/* Case-insensitive string to C-type string comparison with wildcards. */
AjBool ajStrMatchWildWordCaseC (const AjPStr str, const char* text);

/* Case-insensitive string to string comparison with wildcards. */
AjBool ajStrMatchWildWordCaseS (const AjPStr str, const AjPStr text);
```

### 6.5.18 字符串搜索函数

字符串搜索函数具有前缀 ajStrFind，用于在字符串中查找子串或字符：

```c
/* Find a string */
ajint ajStrFindS (const AjPStr str, const AjPStr str2);
/* Find a character */
ajint ajStrFindAnyK(const AjPStr str, char chr);
/* Find any character in a set */
ajint ajStrFindAnyS (const AjPStr str, const AjPStr str2);
/* Find a string (case-insensitive) */
ajint ajStrFindCaseS (const AjPStr str, const AjPStr str2);
/* Find any character not in a set */
ajint ajStrFindRestS (const AjPStr str, const AjPStr str2);
/* Find any character not in a set (case-insensitive) */
ajint ajStrFindRestCaseS (const AjPStr str, const AjPStr str2);
/* Find last occurence of a string */
ajint ajStrFindLastS (const AjPStr str, const AjPStr str2);
```

这些函数返回搜索文本在序列中的起始位置，如果未找到文本，则返回 -1。

ajStrFindAnyS、ajStrFindRestS 和 ajStrFindRestCaseS 使用作为字符串（str2）提供的一组字符。

