
```
此外，如果 A 或 B 不像 A 一样严格，则程序是非法的，因为覆盖基类虚函数的异常规格至少要与基类一样。 — 示例结束
```

没有显式异常规格符的去分配函数 (`3.7.4.2`) 其异常规格为空集。

在以下情况下认为需要异常规格符：
- (`19.1`) 在表达式中，该函数是重载函数集的唯一查找结果或选定的成员 (`3.4`, `13.3`, `13.4`；
- (`19.2`) 该函数被 `odr`-使用 (`3.2`)，或者如果它出现在未求值的操作数中，如果表达式被潜在求则会被 `odr`-使用；
- (`19.3`) 将异常规格与另一个派生版本（例如显式特化或覆盖的虚函数）进行比较；
- (`19.4`) 在函数定义处；
- (`19.5`) 调用该函数的默认成员函数需要异常规格。[注意：默认声明不需要在派生函数的隐式异常规格被需要时才求值基成员函数的异常规格，但显式异常规格需要隐式异常规格来对比比较。 — 注意结束]

默认特殊成员函数的异常规格在需要时按上述方法进行求值；同样地，模板或成员函数特化版本的异常规格在需要时进行实例化。
`20` 在动态特化中，类型标识符后跟省略号（ellipsis）是包展开 (`14.5.3`)；
`21` [注意：动态特化的使用已弃用（参见附录 D）] — 结束

# 15.5 特殊函数

[except.terminate]

`std::terminate()` (`15.5.1`) 和 `std::unexpected()` (`15.5.2`) 用于异常机制处理与异常机制相关的错误。`std::current_exception()` (`18.8.5`) 和类 `std::nested_exception` (`18.8.6`) 可用于程序捕获完全处理的异常。

# 15.5.1 std::terminate() 函数

[except.terminate]

在某些情况下必须放弃异常处理而采用较不微妙的处理技术。[注意：情况包括：
- (`1.1`) 当异常机制在激活异常处理器之前完成异常对象初始化 (`15.1`)，一个函数通过异常退出，或
- (`1.2`) 当异常机制找不到抛出异常的处理器时 (`15.3`)，或者对处理程序的搜索（`15.3`）遇到了一个不允许异常的 `noexcept` 规格外部块 (`15.4`)，
- (`1.4`) 当栈回溯（`15.2`）期间对象的析构通过抛出异常终止，或
- (`1.5`) 当静态或线程存储期的非局部变量初始化 (`3.6.2`) 通过异常退出时，或
- (`1.6`) 当静态或线程存储期的对象的析构 (`3.6.3`) 通过异常退出时，或
- (`1.7`) 当注册到 `std::atexit` 和 `std::quick_exit` 的函数执行 (`18.5`) 通过异常退出时，或
- (`1.8`) 当无操作数的抛表达式 (`5.17`) 在没有异常被处理的情况下尝试重抛异常时 (`15.1`)，
]

# ISO/IEC N4296

- (`1.9`) 当 `std::unexpected` 期望一个先先违反的异常规范所允许的类型异常，且该异常规范未包含 `std::bad_exception` (`15.5.2`) 时，

- (`1.10`) 当调用实现的默认意外异常处理程序时 [D.8.1]，或

- (`1.11`) 当对未捕获任何异常的对象调用 `std::nested_exception::rethrow_nested` 函数时 (`18.8.6`)，或

- (`1.12`) 当初始线程的执行发现意外异常时 (`30.3.1.2`)，或

- (`1.13`) 当对引用可连接线程（joinable thread）的 `std::thread` 类型对象调用拷贝赋值运算符的析构函数时 (`30.3.1.3`, `30.3.1.4`)。

> — 注意
> `2` 在调用 `std::terminate()` 的情况下 [18.8.3]。在未找到匹配的处理程序的情况下，在调用 `std::terminate()` 之前是否进行栈回溯取决于实现定义。在搜索处理程序 (`15.3`) 遇到不允许该异常的函数异常规范的最外层块 (`15.4`) 时，在调用之前是否部分或完全进行栈回溯取决于实现定义。在所有其他情况下，在调用 `std::terminate()` 之前不应进行栈回溯。实现不允许根据回溯过程最终会导致对 `std::terminate()` 的调用而提前结束回溯。

## 15.5.2 std::unexpected() 函数 [except::unexpected]

- `1` 如果一个具有动态异常规范的函数抛出了一个其异常规范不允许的类型异常，则在完成该函数的栈回溯后立即调用 `std::unexpected()` [D.8]。

- `3` `std::unexpected()` 函数不应抛出异常，但它可以抛出（或重新抛出）异常。如果它抛出一个被之前违反的异常规范允许的新异常，则对另一个处理程序的搜索将在动态异常规范不允许的类型调用处继续，发生以下情况：如果它以动态异常规范不允许的类型异常退出，则调用类 `std::bad_exception` (`18.8.2`)，然后调用函数 `std::terminate()`；否则该异常将被一个实现定义的 `std::bad_exception` 类型对象替换，并且对另一个处理程序的搜索将在违反动态异常规范的函数调用处继续。

- `4` [注意：因此，动态异常规范保证了函数仅通过列出的类型的异常退出。如果动态异常规范包含了 `std::bad_exception` 类型，那么该类型以外的任何异常类型可以在 `std::unexpected()` 函数内部被替换为 `std::bad_exception` — 注释结束]

## 15.5.3 std::uncaught_exceptions() 函数 [except.uncaught]

- `1` 异常在完成异常对象的初始化 (`15.1`) 后到完成异常处理程序的激活 (`15.3`) 之前被视为未捕获。这包括栈回溯。如果异常被重新抛出 (`15.1`)，则从重新抛出点到重新抛出的异常再次被捕获之前被视为未捕获。函数 `std::uncaught_exceptions()` (`18.8.4`) 返回未捕获异常的数量。

# 预处理指令

预处理指令由一组满足以下约束的预处理标记组成：序列中的第一个标记为 `#` 预处理标记（在翻译阶段 4 刚时），它要么是源文件中的第一个字符（可选地位于包含无换行字符的空白之后），要么跟在包含至少一个换行符的空白之后。序列中的最后一个标记如果出现在本应是函数类宏调用的范围内，则为第一个换行符。换行符结束预处理：

```cpp
preprocessing-file:
  group:
    group-part
    group group-part
  group-part:
    if-section
    control-line
    text-line
    # non-directive
  if-section:
    if-group elif-groups_opt else-group_opt endif-line
  if-group:
    # if
      constant-expression new-line group_opt
    # elif
      identifier new-line group_opt
    # endif
      identifier new-line group_opt
  elif-groups:
    elif-group
    elif-groups elif-group
  elif-group:
    # elif
      constant-expression new-line group_opt
  else-group:
    # else
      new-line group_opt
  endif-line:
    # endif
      new-line
  control-line:
    # include
      pp-tokens new-line
    # define
      identifier [paren identifier-list-opt] replacement-list new-line
    # define
      identifier [paren ... ] replacement-list new-line
    # define
      identifier [paren identifier-list, ... ] replacement-list new-line
    # undef
      identifier new-line
    # line
      pp-tokens new-line
    # error
      pp-tokens_opt new-line
    # pragma
      new-line
```

`145` 因此，预处理指令通常被称为“行”。这些“行”没有句法意义，但在某些情况下除外。

```
preprocessing-file:
  group:
    group-part
    group group-part
  group-part:
    if-section
    control-line
    text-line
    # non-directive
  if-section:
    if-group elif-groups_opt else-group_opt endif-line
  if-group:
    # if
      constant-expression new-line group_opt
    # elif
      identifier new-line group_opt
    # endif
      identifier new-line group_opt
  elif-groups:
    elif-group
    elif-groups elif-group
  elif-group:
    # elif
      constant-expression new-line group_opt
  else-group:
    # else
      new-line group_opt
  endif-line:
    # endif
      new-line
  control-line:
    # include
      pp-tokens new-line
    # define
      identifier [paren identifier-list-opt] replacement-list new-line
    # define
      identifier [paren ... ] replacement-list new-line
    # define
      identifier [paren identifier-list, ... ] replacement-list new-line
    # undef
      identifier new-line
    # line
      pp-tokens new-line
    # error
      pp-tokens_opt new-line
    # pragma
      new-line
```

ISO/IEC N4296
© ISO/IEC

# 源文件包含

+ `1` `#include` 应当标识一个可以被实现处理的头文件或源文件。

+ `2` 如下形式的预处理指令：

```cpp
# include <h-char-sequence> new-line
```

将搜索由 `<` 和 `>` 分隔符之间的指定序列唯一标识的一系列实现定义的位置，并将该指令替换为头文件的全部内容。这些位置的指定方式或头文件的查找方式由实现定义。

+ `3` 如下形式的预处理指令：

```cpp
# include "q-char-sequence" new-line
```

将该指令替换为由 `"` 分隔符之间的序列所标识的源文件的全部内容。命名的源文件将以实现定义的方式进行搜索。如果不支持此项，或者搜索失败，则该指令被重新处理，正如同读取了
`# include <h-char-sequence> new-line`

+ `4` 如下形式的预处理指令：

```cpp
# include pp-tokens new-line
```

（不匹配上述两种形式的任何一种）是被允许的。`include` 之后的预处理令牌将被处理，并像普通令牌一样（即每个当前定义为宏名的标识符都被替换为它的替换预处理令牌列表）。如果在所有替换之后，指令不匹配上述两种形式之一，则行为是未定义的。`151` 将 `<` 和 `>` 预处理对或一对 `"` 字符之间的预处理令牌序列组合成单个头文件名称预处理令牌的方法由实现定义。

+ `5` 实现为由一个或多个非数字或数字（`2.10`）后跟一个点（`.`）和一个单个非数字组成的序列提供唯一的映射。第一个字符不能是数字。实现可以对字母字符进行区分。

+ `6` `#include` 预处理指令可能出现在由于另一个文件中的 `#include` 指令而被读取的源文件中，其嵌套深度受限于实现定义的限制。

> [7: 注意：尽管实现可能提供一种机制，使得可以通过 `< >` 搜索提供任意源文件，但通常情况下，程序员应使用 `< >` 用于由实现提供的头文件，并使用 `" "` 用于实现控制之外的源文件。例如：

```cpp
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include "myprog.h"
```
-- end --

+ `8` 示例：这些宏替换的 `#include` 指令：

```cpp
#if VERSION == 1
#define INFILE "vers1.h"
#elif VERSION == 2
#define INFILE "vers2.h" // 等此类推
#else
#define INFILE "versN.h"
```
`151` 注意，相邻的字符串字面量不会合并成单个字符串字面量（见 `2.2` 中的翻译阶段）；因此，导致两个字符串字面量的扩展是无效指令。

```cpp
#endif
#include INCFILE
```

- 示例结束 ]

# 16.3 宏替换 [cpp.replace]

+ `1` 如果两个替换列表中的所有预处理令牌在数量、顺序、拼写和空格分隔上相同（且所有空格分隔被视为相同），则这两个替换列表是相同的。

+ `2` 被定义为对象类宏的标识符可以通过另一个 `#def` 预处理指令重新定义，前提是第二个定义也是对象类宏定义且替换列表相同，否则程序将是格式错误的。被定义为函数类宏的标识符可以通过另一个 `#def` 预处理指令重新定义，前提是第二个定义是函数类宏，且具有相同数量和拼写的参数，并具有相同的替换列表，否则程序将是格式错误的。

+ `3` 在对象类宏的定义中，在标识符和替换列表之间应当存在空格。

+ `4` 如果宏定义中的标识符列表不以省略号（`...`）结尾，则在函数类宏的调用中的参数数量（包括那些不包含预处理令牌的参数）应等于宏定义中的参数数量。否则，如果参数多于 `...`，则应存在一个 `)` 预处理令牌来结束调用。

+ `5` 标识符 `_VA_ARGS_` 应仅出现在参数中带有省略号的函数类宏的替换列表中。

+ `6` 紧随 `def` 之后的参数标识符在其作用域内应当唯一声明。

+ `7` 紧随 `def` 之后的标识符称为宏名称。

+ `8` （此处为原文重复内容，已去重处理）

+ `9` （此处为原文重复内容，已去重处理）

+ `10` （此处为原文重复内容，已去重处理）

+ `11` （此处为原文重复内容，已去重处理）

+ `12` （此处为原文重复内容，已去重处理）

+ `13` （此处为原文重复内容，已去重处理）

+ `14` （此处为原文重复内容，已去重处理）

+ `15` （此处为原文重复内容，已去重处理）

+ `16` （此处为原文重复内容，已去重处理）

+ `17` （此处为原文重复内容，已去重处理）

+ `18` （此处为原文重复内容，已去重处理）

+ `19` （此处为原文重复内容，已去重处理）

+ `20` （此处为原文重复内容，已去重处理）

+ `21` （此处为原文重复内容，已去重处理）

序列；然而，如果参数不包含任何预处理标记，则该参数将被一个标记位（placemark）预处理标记代替¹155

`3` 对于类对象类和函数类的宏调用，在重新检查替换列表以查找更多待替换的宏名称之前，替换列表中每个 `##` 预处理标记的实例（来自参数）都会被删除，并将被删除的预处理标记与随后的预处理标记拼接。标记位预处理标记经过特殊处理：两个标记位的拼接将产生一个单一标记位预处理标记，而与非标记位预处理标记的拼接将产生该非标记位预处理标记。如果结果不是有效的预处理标记，则行为是未定义的。`##` 运算符的评估顺序是未定义的。

示例：在以下阶段中：

```
#define hash_hash ## ##
#define mkstr(a) # a
#define in_between(a) mkstr(a)
#define in_between(c, d) hash_hash d
char p[] = join(x, y);
// 等同于
// char p[] = "* ## y";
```

在各个阶段的展开：

```
join(x, y)
in_between(x hash_hash y)
in_between(## y)
mkstr(## y)
```
