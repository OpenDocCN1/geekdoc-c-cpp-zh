
调用 `f(2)` 可能会展开为 `2*f(9)` 或 `2*g*` 严格符合标准的程序不被允许依赖于此类未定义确定的行为。

## 6.10.3.5 宏定义的作用域

- 宏定义的持续时间（独立于块结构）直到遇到相应的 `#undef` 指令，或者（如果没有遇到）直到预处理翻译单元的结束。在翻译阶段 4 之后，宏定义没有意义。

- 形式如下的预处理指令

```
# undef identifier 新行
```

会导致指定的标识符不再定义为宏名称。如果指定的标识符当前未被定义为宏名称，则忽略它。
示例 此功能最简单的用法是定义一个“显式常量”，如
`#define TABSIZE 100`

`int table[TABSIZE];`

- 4 示例 2 下面定义了一个函数类宏，其值为参数的最大值。它的优点是适用于任何兼容的类型参数，并且生成内联代码而没有函数调用的开销。它的缺点是会再次评估参数中的其中一个（包括副作用），并在多次调用时生成比函数更多的代码。它还无法访问其地址，因为它没有地址。

```
#define max(a, b) ((a) > (b) ? (a) : (b))
```

括号确保了参数和生成的表达式被正确绑定。

- 5 示例 3 为了说明重定义和重新检查的规则，序列

```
#define x 3

#define f(a) f (*a)

#undef x 2

#define x 2

#define g f

#define z z[0]

#define h g(-w

#define m(a) a(w)

#define w 0,1

#define t(a) a

#define p() int

#define q(x) x

#define r(x,y) x ## y

#define str(x)-w # x #
```

```
f(1) + f(z) * t (g (0) + t) (1);

g(+(3,4)-w) | h 5 & m

f("*m(m);

p[q(i)] = { q(1), r(2,3), r(4), r(5), r(i) };

char c[6] = { str(i) };
```

结果为
`f(2) * f (2 * (z[0])) * f (2+(3,4)-0,1) | f (2 * 0))^m(0;1); i = { 1, 23, 4, 5 }; char c[6] = { "", "" };`

- 6 示例 4 为了说明创建字符字符串和拼接标记的规则，序列

```
#define str(s) # s

#define xstr(s) str(s)

#define debug(s, t) printf("x" # s = %d", x # t = "%s")

#define INFILE(n) vers ## n

#define glue(a, b) a ## b

#define xglue(a, b) glue(a, b)

#define HIG "hello"

#define LOW "world",
```

```
debug(1, 2);

puts(str(strncmp("abc", "abc", '\'))); // 这行消失

== 0); str(s);

#include xstr(INCFILE(2).h)

glue("HIGH, LOW);
```

结果为
`printf("x" "1" =d, "2" =s", x1, x2);`
`puts(str(strncmp("abc", "abc", '\')) == 0);`
`#include "vers2.h" (在宏替换后，文件访问之前) "hello", "world"`

宏中 `#` 和 `##` 标记周围的空格是可选的。

- 5 示例 5 为了说明占位符预处理标记的规则，序列

```
#define t(x,y,z) x # y
int j[] = { t(1,2,3), t(4,5), t(6,7), t(8,9), t(10), t(11), t(12) };
```

结果为
`int j[] = { 123, 45, 67, 89, 10, 11 };`

- 6 示例 6 为了说明替换规则，以下序列是有效的：

```
#define OBJ_LIKE (1)

#define OBJ_LIKE /* white space */ (1)

#define FUNC_LIKE(a) ( a )
```

但以下是无效的：

```
#define OBJ_LIKE (0) //不同的标记序列

#define OBJ_LIKE (1 - 1) //不同的空格

#define FUNC_LIKE(b) ( a ) // 参数用法

#define FUNC_LIKE(b) ( b ) // 不同的拼写
```

- 7 示例 7 最后，显示变量列表宏：

```c
#define debug(...)           fprintf(stderr, __VA_ARGS__)

#define showlist(...)        puts(%s,
```

```
debug("Flag");

debug("X = %d\n", x);

showlist("The first, second, and third items.");

report(x, y, "X is %d but y is %d", x, y);
```

结果为
```c
fprintf(stderr, "Flag");

fprintf(stderr, "X = %d\n", x);

puts("The first, second, and third items.");

((x->y)?puts("x->y");

printf("x is %d but y is %d", x, y));
```

## 6.10.4 行控制

约束

- 1 `#line` 指令的字符串字面量（如果存在）应当是字符串字面量。

- 2 当前源行的号比翻译阶段 1（5.1.1.2）处理源文件时读取或解释的换行字符数多一。

- 3 形式如下的预处理指令

```
# line digit-sequence 新行
```

导致实现的行为如同后续源序列从数字序列指定的（解释为十进制整数）行开始。数字序列不指定零，或大于 2147483647 的数。

- 4 形式如下的预处理指令

```
# line digit-sequence s-char-sequence<sub>opt</sub> 新行
```

设置假设行号，并将源文件的假设行更改为字符串字面量的内容。

- 5 形式如下的预处理指令

```
# line pp-tokens 新行
```

（不匹配上述两种形式之一的）是允许的。`line` 之后的预处理标记将像普通文本一样被处理（每个当前定义为宏名称的都被替换为其预处理标记列表）。替换后生成的指令匹配前两种形式之一，并进行适当处理。

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

其中指令中的预处理令牌 `STDC` 并不紧跟在 `pragma` 之后（在任何宏替换之前）$^{174}$，会导致实现以实现定义的方式行为。该行为可能会导致翻译失败，或导致翻译器或生成的程序以不符合规范的方式行为。任何未被实现识别的此类 pragma 均被忽略。

2 如果预处理 `STDC` 在指令中紧跟在 `pragma` 之后（在任何宏替换之前），则对该指令不执行宏替换，且该指令应具有以下形式之一$^{175}$，其含义在其他处描述：

```
#pragma STDC FP_CONTRACT on-off-switch
#pragma STDC FENV_ACCESS on-off-switch
#pragma STDC CX_LIMITED_RANGE on-off-switch
on-off-switch: 
    ON OFF DEFAULT
```

前向引用：`FP_CONTRACT` pragma (7.12.2)，`FENV_ACCESS` pragma (7.6.1)，`CX_LIMITED_RANGE` pragma (7.3.4)。

174 实现不要求在 pragmas 中执行宏替换，但除了标准 pragmas（其中 `STDC` 紧跟在 `pragma` 之后）外，允许执行替换。如果非标准 pragma 中的宏替换形式与标准 pragma 相同，其行为仍然是实现定义的；实现允许得像标准 pragma 一样行为，但并非强制。

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

+   1 下列子句$^{176}$ 中列出的预定义宏的值（除 `__FILE__` 和 `__LINE__` 外）在整个翻译单元中保持不变。
2 这些宏名称以及定义的标识符均不应 `#define` 的对象。任何其他预定义宏名称应以下划线开头，后跟一个大写字母或第二个下划线。
3 实现不应重新定义 `__cplusplus`。

前向引用：标准头文件 (7.1.2)。

### 6.10.8.1 强制宏

+   1 实现应定义以下宏名称：
`__DATE__` 预处理单元的日期：一个形式为 `"Mmm dd yyyy"` 的字符字面量，其中月份名称与 `asctime` 函数相同，如果 `dd` 小于 10，第一个字符为空格。如果日期不可用，则提供实现定义的日期。
`__FILE__` 当前源文件的推断文件名（一个字符字符串）。
`__LINE__` 当前源文件的推断行号（当前源文件内的）（一个整数）$^{77}$
`__STDC__` 整数常量 1，用于表示符合实现。
`__STDC_HOSTED__` 如果实现是托管的，则为整数常量 1；否则为常量 0。

176 参见“未来语言方向”（6.11.9）。
177 推断文件名和行号可以通过 `#line` 指令更改。

6.10.8.1 语言

`__STDC_VERSION__` 整数常量 2011ym$^{78)}$
`__TIME__` 预处理单元的时间：一个形式为 `"hh:mm:ss"` 的字符字面量，如 `asctime` 函数生成的时间。如果时间不可用，则提供实现定义的时间。

**前向引用：`ctime` 函数 (7.27.3.1)。

### 6.10.8.2 环境宏

+   1 实现条件定义以下宏：
   `__STDC_ISO_1046__` 形式为 `yyyymym` 的整数常量（例如，1997ym）。如果此符号被定义，则 Unicode 要求集中的每个存储在 `wchar_t` 类型对象中的字符的值与该字符的短标识符相同。Unicode 要求集由 ISO/IEC 10646 根据指定的年份和月份定义的所有修订和技术修正。如果使用了其他编码，则该宏不定义，实际使用的编码是实现定义的。
   `__STDC_MB_MAX_NEQ__` 整数常量 1，用于表示基本字符集的成员不等于其整数常量的值。
   `__STDC_UTF_16__` 整数常量 1，表示 `char16_t` 类型的值采用 UTF-16 编码。如果使用了其他编码，则宏不定义，实际使用的编码是实现定义的。
   `__STDC_UTF_32__` 整数常量 1，表示 `char32_t` 类型的值采用 UTF-32 编码。如果使用了其他编码，则宏不定义，实际使用的编码是实现定义的。

**前向引用：共同定义 (7.19)，unicode 工具 (7.28)。

178) 此宏在 ISO/IEC 9899:1990 中未指定，在 ISO/IEC 9899:1990/Amd.1:1995 中指定为 199409L，在 ISO/IEC 9899:1999 中指定为 199501L。其意图是保持为随着本国际标准每次修订而创建的 long 类型整数常量。

## 6.10.8.3 条件宏

实现条件定义以下宏：

+   - `__STC_ANALYZABLE__` 整数常量 1，表示符合附录 L（可分析性）规范。
+   - `__STC_IEC_559__` 整数常量 1，表示符合附录 F（IEC 60559 浮点运算）规范。
+   - `__STC_IEC_559_COMPLEX__` 整数常量 1，表示符合附录 G（IEC 60559 兼容复数运算）规范。
+   - `__STC_LIB_EXT__` 整数常量 2011L，表示支持附录 K（边界检查接口）的扩展$^{79)}$
+   - `__STC_NO_ATOMICS__` 整数常量 1，表示实现不支持原子类型（包括 `stdatomic.h` 头文件）。
+   - `__STC_NO_COMPLEX__` 整数常量 1，表示实现不支持复数类型或 `<complex.h>` 头文件。
+   - `__STC_NO_THREADS__` 整数常量 1，表示实现不支持 `<threads.h>` 头文件。
+   - `__STC_NO_VLA__` 整数常量 1，表示实现不支持变长数组或变修类型。

定义 `__STC_NO_COMPLEX__` 的实现不应定义 `__STC_IEC_559__`。

179) 其意图是保持为随着本国际标准每次修订而增加的 long int整数。

## 6.10.9 Pragma 运算符 (Pragma operator)

语义

如下形式的一元运算符表达式：

```
_Pragma ( string-literal )
```

处理方式如下：对字符串字面量去字符串化，删除任何编码前缀，删除首尾引号，将每个转义序列 `\` 替换为双引号，并将转义序列 `\` 替换为单个反斜杠。生成的字符序列通过翻译阶段 3 处理产生预处理令牌，其执行方式就像它们是 pragma 指令中的 `pp-tokens` 一样。该元运算符表达式中的原始四个预处理令牌被移除。

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
