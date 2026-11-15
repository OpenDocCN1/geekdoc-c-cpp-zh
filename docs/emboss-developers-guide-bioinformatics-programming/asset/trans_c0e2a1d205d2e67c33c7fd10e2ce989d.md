

AjBool ajStrMatchWildC (const AjPStr thys, const char* text);
AjBool ajStrMatchWildS (const AjPStr thys, const AjPStr wild);
AjBool ajStrMatchWildCaseC (const AjPStr thys, const char* text);
AjBool ajStrMatchWildCaseS (const AjPStr thys, const AjPStr wild);
AjBool ajStrMatchWildWordC (const AjPStr str, const char* text);
AjBool ajStrMatchWildWordS (const AjPStr str, const AjPStr text);
AjBool ajStrMatchWildWordCaseC (const AjPStr str, const char* text);
AjBool ajStrMatchWildWordCaseS (const AjPStr str, const AjPStr text);
AjBool ajStrMatchWordAllS(const AjPStr str, const AjPStr str2);
AjBool ajStrMatchWordOneS(const AjPStr str, const AjPStr str2);
AjBool ajStrPrefixC(const AjPStr str, const char* txt2);
AjBool ajStrPrefixS(const AjPStr str, const AjPStr str2);
AjBool ajStrPrefixCaseC (const AjPStr str, const char* pref);
AjBool ajStrPrefixCaseS (const AjPStr str, const AjPStr pref);
AjBool ajStrSuffixC (const AjPStr thys, const char* suff);
AjBool ajStrSuffixS (const AjPStr thys, const AjPStr suff);
AjBool ajStrSuffixCaseC (const AjPStr str, const char* pref);
AjBool ajStrSuffixCaseS (const AjPStr str, const AjPStr pref);

让我们来看看函数 ajStrMatchWildWordCaseS 的命名规则是如何工作的。这是你可能遇到的最难的示例：

- 1. @nam1rule aj 函数属于 AJAX 库。

  此规则在文件部分中定义第一个函数名组件为 aj。AJAX 库中的所有函数都带有此前缀。

- 2. @nam2rule Str 函数用于操作字符串。

  此规则在 AJAX (AjPStr) 字符串的数据部分中定义第二个函数名组件为 Str。AJAX 字符串库 (ajstr.h/c) 中所有操作 AJAX (AjPStr) 字符串的函数都带有前缀 ajStr。

- 3. @nam3rule Match 比较两个完整字符串。

  此规则在标准部分中用于‘比较’函数，定义第三个函数名组件为 Match。自由文本表明，所有带有前缀 ajStrMatch* 的函数都是用于比较两个完整字符串。

- 4. @nam4rule MatchWild 使用通配符字符进行比较。

  此规则定义第四个函数名组件为 Wild，并表明带有前缀 ajStrMatchWild* 的函数使用通配符字符比较两个（完整）字符串。

- 5. @nam5rule MatchWildWord 对两个字符串内首个单词进行区分大小写的通配符比较。

  此规则定义第五个函数名组件为 Word，并表明带有前缀 ajStrMatchWildWord 的函数使用通配符字符比较两个完整字符串，仅使用两个字符串内的首个单词。

- 6. @nam6rule MatchWildWordCase 对两个字符串内首个单词进行不区分大小写的通配符比较。

  此规则定义第六个函数名组件为 Case，并表明带有前缀 ajStrMatchWildWordCase 的函数使用通配符字符比较两个完整字符串，仅使用两个字符串内的首个单词，且不区分大小写。

- 7. @suffix C [char*] C 字符字符串。

  此规则在文件部分中定义，表明带有后缀 C 的函数接受 C 类型 (char *) 字符串参数。

> **重要**
>
> 命名规则应仅在严格需要区分现有函数时才定义。不应在可以在语义上*可能*拆分功能，但因没有其他类似函数而无理由这样做的情况下使用。在这种情况下，函数在基本前缀之后应只有一个组件（例如 ajStr）。此组件通常是一个大写单词，但如果使用多个单词能真正提高清晰度，则应使用 `SentenceCase`。

## D.5 数据类型文档

出现在 C 数据结构之前的结构化注释具有以下一般格式：

```
/* @data PointerName ***********************************************************
**
** DatatypeDescription
** DatatypeDescription cont.
**
** @alias StructName
** @alias ObjectName
**
** @new Description
** @delete Description
** @assign Description
**
** @attr Element1 [Datatype1] Description
** @attr Element2 [Datatype2] Description
**
** @@
** Comments
** Comments cont.
**
**********************************************************************************/

typedef struct StructName
{
    Datatype1 Element1;
    Datatype2 Element2;
} ObjectName

#define PointerName ObjectName*
```

### 其中：

- `PointerName` 是指针数据类型，例如 AjPStr。
- `StructName` 是结构名称，例如 AjSStr。
- ObjectName 是对象数据类型，例如 AjOStr。
- DatatypeDescription 是出现在在线文档中的数据类型描述。它可能跨多行。
- Element* 是结构中元素的变量名。
- Datatype* 是结构中元素的数据类型。
- Description 是对结构中元素或对其进行操作的函数的描述（有关标签的使用，请参见下文）。
- Comments 是可选注释，不会出现在在线文档中。

在下面的示例中，有一个额外的指针数据类型 (AjPStr)。这对于大多数数据类型不是必需的：

```
/* @data AjPStr ****************************************************************
**
** Ajax string object.
**
** Holds a null terminated character string with additional data.
** The length is known and held internally.
** The reserved memory size is known and held internally.
** The reference count is known and held internally.
** New pointers can refer to the same string without needing
** to duplicate the character data.
**
** If a string has multiple references it cannot be changed. Any
** instance to be changed is first copied to a new string. This
** means that any function which can change the character data must
** pass a pointer to the string so that the string can be moved.
**
** A default null string is provided. New strings are by default
** implemented as pointers to this with increased reference counters.
**
** AjPStr is implemented as a pointer to a C data structure.
**
** @alias AjPPStr
** @alias AjSStr
** @alias AjOStr
** @iterator AjIStr
**
** @attr Res [ajuint] Reserved bytes (usable for expanding in place)
** @attr Len [ajuint] Length of current string, excluding NULL at end
** @attr Ptr [char*] The string, as a NULL-terminated C string.
** @attr Use [ajuint] Use count: 1 for single reference, more if several
**                     pointers share the same string.
**                     Must drop to 0 before deleting. Modifying means making
**                     a new string if not 1.
** @attr Padding [ajuint] Padding to alignment boundary
** @@
*******************************************************************************/

typedef struct AjSStr
{
    ajuint Res;
    ajuint Len;
    char *Ptr;
    ajuint Use;
    ajint Padding;
};

} AjOStr;
#define AjPStr AjOStr*
typedef AjPStr* AjPPStr;
```

### D.5.1 数据类型文档标签

可用标签以 @ 开头。一些标签引用作用于数据结构的函数。

| Tag | Description |
| :--- | :--- |
| @data | 结构化注释的开始。给出指向数据结构的指针的数据类型（例如 AjPStr），后面可跟任意数行带标记的自由文本。如果数据结构不对外可见，请使用 @datastatic。 |
| @datastatic | 与 @data 相同，但用于静态（内部）数据类型。 |
| @alias | 相关数据类型和名称的别名。标准做法是使用指针名称（AjPStr 等）作为主名称，并使用对象名称（AjOStr 等）和结构名称（AjSStr 等）作为别名。这些用于在源代码中通过别名标记引用。 |
| @iterator | 与此数据类型关联的迭代器数据类型的名称（例如 AjIStr），如果有的话。 |
| @other | 与此数据类型关联的任何其他数据类型的名称。 |
| @new | 构造函数。给出函数名称，后跟函数描述的副本。 |
| @delete | 析构函数。给出函数名称，后跟函数描述的副本。 |
| @assign | 赋值（覆盖值）。给出函数名称，后跟函数描述的副本。 |
| @modify | 修改器（更新值）。给出函数名称，后跟函数描述的副本。 |
| @cast | 将值转换为其他内容作为返回类型或另一个参数。给出函数名称，后跟函数描述的副本。 |
| @use | 使用值但不修改它或返回任何部分。给出函数名称，后跟函数描述的副本。 |
| @input | 输入函数（读取输入源并填充数据类型）。给出函数名称，后跟函数描述的副本。 |
| @output | 输出函数（将值写入输出文件）。给出函数名称，后跟函数描述的副本。 |
| @iterate | 迭代函数（对值或值数组进行迭代）。给出函数名称，后跟函数描述的副本。 |
| @attr | 属性名称、类型和描述。属性按其在结构中出现的相同顺序定义。名称和类型必须与真实定义匹配。 |
| @cc | 在属性组之间插入的注释。结构本身不允许有注释（以提供干净的解析），因此注释插入在标题中。 |

