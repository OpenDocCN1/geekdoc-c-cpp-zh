

```
** @@
**
** This library is free software; you can redistribute it and/or
** modify it under the terms of the GNU Library General Public
** License as published by the Free Software Foundation; either
** version 2 of the License, or (at your option) any later version.
**
** This library is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
** Library General Public License for more details.
**
** You should have received a copy of the GNU Library General Public
** License along with this library; if not, write to the
** Free Software Foundation, Inc., 59 Temple Place - Suite 330,
** Boston, MA 02111-1307, USA.
**********************************************************************/
```

标签与应用程序头中的标签相同，但 LibraryArea 描述库的一般区域，例如 "string"。
示例：

```
/**********************************************************************
** @source AJAX string functions
**
** AjPStr objects are reference counted strings
** Any change will need a new string object if the use count
** is greater than 1, so the original AjPStr is provided as a pointer
** so that it can be reallocated in any routine where string modification
** may be needed.
**
** In many cases the text is always a copy, even of a constant original, so
** that it can be simply freed.
**
** @author Copyright (C) 1998 Peter Rice
** @version 1.0
** @modified Jun 25 pmr First version
** @@
**
** This library is free software; you can redistribute it and/or
** modify it under the terms of the GNU Library General Public
** License as published by the Free Software Foundation; either
** version 2 of the License, or (at your option) any later version.
**
** This library is distributed in the hope that it will be useful,
** but WITHOUT ANY WARRANTY; without even the implied warranty of
** MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
** Library General Public License for more details.
**
** You should have received a copy of the GNU Library General Public
** License along with this library; if not, write to the
** Free Software Foundation, Inc., 59 Temple Place - Suite 330,
** Boston, MA 02111-1307, USA.
**********************************************************************/
```

## D.4.2 库数据类型和函数

所有库函数和数据类型都需要结构化注释（见下文）。

## D.4.3 功能章节

库源文件 (*.c) 中的函数被组织为章节，这些章节定义了具有相关功能的函数组。这些章节使用结构化注释进行文档化，该注释定义了函数命名规则、函数参数命名和数据类型规则以及返回数据类型定义规则。这确保了库文件内部，以及在一定程度上跨库文件的函数，呈现出直观且一致的 API。

向现有库文件添加新函数时，应将其放置在文件的相应章节下。创建新库文件时，建议但不强制要求向文件添加章节。

章节分为三种类型。结构化注释的开始由给定的标签指示：

- 文件章节 (@filesection)
- 数据章节 (@datasection)
- 标准章节 (@section)。

函数本身之前应给出一个文件章节。这包含整个库的基本文档和规则。文件章节包含若干数据章节，每个主要数据类型对应一个，由函数处理。

通常会为头文件中定义的所有公共数据类型（由 @data 标识）提供数据章节。例如，ajstr.h 定义了三种新数据类型，AjPStr、AjIStr 和 AjPStrTok，但也存在主要参数为 C 风格 (char*) 字符串的函数。因此，在文件章节下总共列出了四个数据章节。

标准章节位于数据章节之下。这些章节定义了具有相关功能、相似名称和相似参数的函数组。标准章节所属的数据章节取决于返回值或主要参数的数据类型。例如，默认字符串构造函数没有参数但返回一个 AjPStr 字符串，因此列在 AjPStr 数据章节下。什么定义了“主要”参数在一定程度上是主观的。对于所有具有多个参数的函数，如果主要参数不是由返回类型确定的，则应为列表中的第一个参数。

每个 @filesection、@datasection 和 @section 包含下文描述的标准文本标签。

### D.4.3.1 函数章节文档标签

可用标签以 @ 开头。

| 标签 | 说明 |
|---|---|
| @filesection | 文件章节结构化注释的开始，后跟库名称，以及任意数量的带标记的自由文本行。 |
| @datasection | 数据章节结构化注释的开始，后跟数据类型、数据类型描述，以及任意数量的带标记的自由文本行。 |
| @section | 一般章节结构化注释的开始，后跟章节名称，以及任意数量的带标记的自由文本行。 |
| @fnote | 用于关于章节的一般注释，例如，其与其他章节的关系。 |
| @namXrule | 定义函数命名规则。后跟一个文本标记，指示函数名称的一个组件（子字符串），以及一行或多行描述具有该命名组件的函数功能的自由文本。X 是一个整数，定义该组件在函数名称中的顺序（见下文）。 |
| @suffix | 定义命名规则，用于区分功能本质相同但仅在单个参数数据类型上不同的函数。例如，两个字符串插入函数都向 EMBOS (AjPStr) 字符串插入内容，但一个插入 AjPStr，另一个插入 C 类型 (char *) 字符串。首先给出可能出现在函数名称中的后缀（在 @namXrule 标签定义的组件之后，见下文）。随后是括号中的数据类型以及描述该数据类型的自由文本。 |
| @fdata（仅限标准章节） | 仅出现在标准章节中，且必须存在。它定义章节中函数操作或返回的主要数据类型（括号中）。该数据类型必须与当前数据章节中给出的相同。会检查函数，以确保数据类型针对函数类别被适当使用和传递（参见 @fcategory）。 |
| @argrule | 定义函数参数命名和数据类型规则，以及（可选）函数名称后缀定义规则。后跟一个文本标记，指示函数名称的后缀，如果未指定则为 ‘*’。第二个文本标记给出参数名称。然后给出参数数据类型（括号中），后跟一行或多行描述参数的自由文本。 |
| @valrule | 定义函数返回类型。后跟一个文本标记，指示适用此返回类型的函数名称后缀。返回数据类型随之而来（括号中），随后是描述在各种条件下返回值的一行或多行自由文本。 |
| @fcategory（仅限标准章节） | 定义用于功能类别的标准名称。这用于验证数据类型（参见 @fdata）传递给函数的方式。值可以是："new","delete", "assign", "modify", "cast", "derive", "use", "iterate", "input", "output", "misc" 或 "internals"。 |

### D.4.3.2 示例

以下显示了 ajstr.c 的摘录，指示文件中的第一个文件章节、数据章节和标准章节：

```
/* filesection ajstr ************************************************************************
**
** @nam1rule aj Function belongs to the AJAX library.
**
** @suffix Len [size_t] length
** @suffix C [char*] C character string
** @suffix S [AjPStr] string object
** @suffix K [char] single character
*/
```

```
/* @datasection [AjPStr] String ************************************************************************
**
** Functions for manipulating AJAX (AjPStr) strings
**
** @nam2rule Str Function is for manipulating strings
**
*/
```

```
/* @section comparison
**
** Functions for comparing strings
**
** @fdata [AjPStr]
**
** @nam3rule Match Compare two complete strings.
** @nam4rule MatchCase Case-insensitive comparison.
** @nam4rule MatchWild Comparison using wildcard characters.
** @nam5rule MatchWild Case Case-insensitive comparison
** using wildcard characters.
** @nam5rule MatchWildWord Case-sensitive wildcard comparison of
** first words within two strings.
** @nam5rule MatchWildWordCase Case-insensitive wildcard comparison of
** first words within two strings.
** @nam4rule MatchWord Comparison using whole words.
** @nam5rule MatchWordOne Comparison using whole words matching any one.
** @nam5rule MatchWordAll Comparison using whole words matching every one.
**
** @nam3rule Prefix Compare start of string to given prefix.
** @nam4rule Prefix Case Case-insensitive comparison.
** @nam3rule Suffix Compare end of string to given suffix.
** @nam4rule Suffix Case Case-insensitive comparison.
**
** @argrule * str [const AjPStr] String
** @argrule C txt2 [const char*] String
** @argrule S str2 [const AjPStr] String
**
** @valrule * [AjBool] True on success
**
** @fcategory use
**
*/
```

‘comparison’ 章节中的函数原型如下：

```
AjBool ajStrMatchC (const AjPStr thys, const char* txt);
AjBool ajStrMatchS (const AjPStr thys, const AjPStr str);
AjBool ajStrMatchCaseC (const AjPStr thys, const char* text);
AjBool ajStrMatchCaseS (const AjPStr thys, const AjPStr str);
```

