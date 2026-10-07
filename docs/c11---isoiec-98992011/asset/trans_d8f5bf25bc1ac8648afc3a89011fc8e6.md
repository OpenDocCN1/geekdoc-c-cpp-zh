

# ISO/IEC 9899:2011 (E)

ISO/IEC 2011 – 版权所有

## 6.10.5 错误指令 (Error directive)

语义

1 如下形式的预处理指令：

```
# error pp-tokensopt new-line
```

会导致实现产生一条诊断消息，其中包含指定的预处理令牌序列。

## 6.10.6 Pragma 指令 (Pragma directive)

语义

1 如下形式的预处理指令：

```
# pragma pp-tokensopt new-line
```

其中指令中的预处理令牌 STDC 并不紧跟在 pragma 之后（在任何宏替换之前）$^{174}$，会导致实现以实现定义的方式行为。该行为可能会导致翻译失败，或导致翻译器或生成的程序以不符合规范的方式行为。任何未被实现识别的此类 pragma 均被忽略。

2 如果预处理 STDC 在指令中紧跟在 pragma 之后（在任何宏替换之前），则对该指令不执行宏替换，且该指令应具有以下形式之一$^{175}$，其含义在其他处描述：

```
#pragma STDC FP_CONTRACT on-off-switch
#pragma STDC FENV_ACCESS on-off-switch
#pragma STDC CX_LIMITED_RANGE on-off-switch
on-off-switch: 
    ON OFF DEFAULT
```

前向引用：FP_CONTRACT pragma (7.12.2)，FENV_ACCESS pragma (7.6.1)，CX_LIMITED_RANGE pragma (7.3.4)。

174 实现不要求在 pragmas 中执行宏替换，但除了标准 pragmas（其中 STDC 紧跟在 pragma 之后）外，允许执行替换。如果非标准 pragma 中的宏替换形式与标准 pragma 相同，其行为仍然是实现定义的；实现允许得像标准 pragma 一样行为，但并非强制。

175 参见“未来语言方向”（6.11.48）。

174 语言

6.10.6

## 6.10.7 空指令 (Null directive)

语义

+   如下形式的预处理指令
```
# new-line
```
没有效果。

## 6.10.8 预定义宏名称 (Predefined macro names)

+   1 下列子句$^{176}$ 中列出的预定义宏的值（除 __FILE__ 和 __LINE__ 外）在整个翻译单元中保持不变。
2 这些宏名称以及定义的标识符均不应 #define 的对象。任何其他预定义宏名称应以下划线开头，后跟一个大写字母或第二个下划线。
3 实现不应重新定义 __cplusplus。

前向引用：标准头文件 (7.1.2)。

### 6.10.8.1 强制宏

+   1 实现应定义以下宏名称：
__DATE__ 预处理单元的日期：一个形式为 "Mmm dd yyyy" 的字符字面量，其中月份名称与 asctime 函数相同，如果 dd 小于 10，第一个字符为空格。如果日期不可用，则提供实现定义的日期。
__FILE__ 当前源文件的推断文件名（一个字符字符串）。
__LINE__ 当前源文件的推断行号（当前源文件内的）（一个整数）$^{77}$
__STDC__ 整数常量 1，用于表示符合实现。
__STDC_HOSTED__ 如果实现是托管的，则为整数常量 1；否则为常量 0。

176 参见“未来语言方向”（6.11.9）。
177 推断文件名和行号可以通过 #line 指令更改。

6.10.8.1 语言

__STDC_VERSION__ 整数常量 2011ym$^{78)}$
__TIME__ 预处理单元的时间：一个形式为 "hh:mm:ss" 的字符字面量，如 asctime 函数生成的时间。如果时间不可用，则提供实现定义的时间。

**前向引用：ctime 函数 (7.27.3.1)。

### 6.10.8.2 环境宏

+   1 实现条件定义以下宏：
   __STDC_ISO_1046__ 形式为 yyyymym 的整数常量（例如，1997ym）。如果此符号被定义，则 Unicode 要求集中的每个存储在 wchar_t 类型对象中的字符的值与该字符的短标识符相同。Unicode 要求集由 ISO/IEC 10646 根据指定的年份和月份定义的所有修订和技术修正。如果使用了其他编码，则该宏不定义，实际使用的编码是实现定义的。
   __STDC_MB_MAX_NEQ__ 整数常量 1，用于表示基本字符集的成员不等于其整数常量的值。
   __STDC_UTF_16__ 整数常量 1，表示 char16_t 类型的值采用 UTF-16 编码。如果使用了其他编码，则宏不定义，实际使用的编码是实现定义的。
   __STDC_UTF_32__ 整数常量 1，表示 char32_t 类型的值采用 UTF-32 编码。如果使用了其他编码，则宏不定义，实际使用的编码是实现定义的。

**前向引用：共同定义 (7.19)，unicode 工具 (7.28)。

178) 此宏在 ISO/IEC 9899:1990 中未指定，在 ISO/IEC 9899:1990/Amd.1:1995 中指定为 199409L，在 ISO/IEC 9899:1999 中指定为 199501L。其意图是保持为随着本国际标准每次修订而创建的 long 类型整数常量。

## 6.10.8.3 条件宏

实现条件定义以下宏：

+   - __STC_ANALYZABLE__ 整数常量 1，表示符合附录 L（可分析性）规范。
+   - __STC_IEC_559__ 整数常量 1，表示符合附录 F（IEC 60559 浮点运算）规范。
+   - __STC_IEC_559_COMPLEX__ 整数常量 1，表示符合附录 G（IEC 60559 兼容复数运算）规范。
+   - __STC_LIB_EXT__ 整数常量 2011L，表示支持附录 K（边界检查接口）的扩展$^{79)}$
+   - __STC_NO_ATOMICS__ 整数常量 1，表示实现不支持原子类型（包括 stdatomic.h 头文件）。
+   - __STC_NO_COMPLEX__ 整数常量 1，表示实现不支持复数类型或 <complex.h> 头文件。
+   - __STC_NO_THREADS__ 整数常量 1，表示实现不支持 <threads.h> 头文件。
+   - __STC_NO_VLA__ 整数常量 1，表示实现不支持变长数组或变修类型。

定义 __STC_NO_COMPLEX__ 的实现不应定义 __STC_IEC_559__。

179) 其意图是保持为随着本国际标准每次修订而增加的 long int整数。

## 6.10.9 Pragma 运算符 (Pragma operator)

语义

如下形式的一元运算符表达式：

```
_Pragma ( string-literal )
```

处理方式如下：对字符串字面量去字符串化，删除任何编码前缀，删除首尾引号，将每个转义序列 \ 替换为双引号，并将转义序列 \ 替换为单个反斜杠。生成的字符序列通过翻译阶段 3 处理产生预处理令牌，其执行方式就像它们是 pragma 指令中的 pp-tokens 一样。该元运算符表达式中的原始四个预处理令牌被移除。

示例如下形式的指令：

```
#pragma listing on "..\listing.dir"
```

也可以表示为：

```
_Pragma ( "listing on \"..listing.dir\" )
```

后者无论是字面出现还是作为宏替换的结果，其处理方式都是相同的：

```
#define LISTING(x) PRAGMA (listing on #x)
#define PRAGMA(x) _Pragma (#x)
```

```
LISTING ( ..listing.dir )
```

