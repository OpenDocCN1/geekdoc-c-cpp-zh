

(if <predicate-expression> then <expression>+
[else <expression>+])

如果 `<predicate-expression>` 求值为符号 FALSE，则求解函数中 `else` 部分包含的表达式，否则求解 `then` 部分包含的表达式。

```
(loop-for-count <range-spec> [do <expression>*])
<range-spec> ::= <end-index> |
(<loop-variable> <end-index>) |
(<loop-variable> <start-index> <end-index>) |
(<loop-variable> <start-index> <end-index> <index>)
```

按 <range-spec> 指定的次数求解 <expression>*。如果未给出 <start-index>，则假定为 1。如果 <start-index> 大于 <end-index>，则循环体永远不会执行。如果指定了 <loop-variable>，可以使用该变量检查当前迭代的整数值。

```
(progn <expression>*)
```

求解所有参数，并返回最后一个求解参数的值。

```
(progn$ <list-spec> <expression>*)
<list-spec> ::= <multifield-expression> |
(<list-variable>
<multifield-expression>)
```

为 <list-spec> 包含的每个字段求解 <expression>*。如果指定了 <list-variable>，可以使用该变量检查当前迭代中字段的值。此外，可以使用变量 <list-variable>-index 检查当前迭代的整数索引值。

```
(return [<expression>])
```

终止当前正在执行的 deffunction、泛型函数方法、消息处理程序或 defrule RHS 的执行。如果没有任何参数，则没有返回值。但是，如果包含参数，则其求解结果作为 deffunction、方法或消息处理程序的返回值。

```
(switch <test-expression> <case-statement>* [<default-statement>])
<case-statement> ::=
(case <comparison-expression> then <expression>*)
<default-statement> ::= (default <expression>*)
```

按顺序求解 <test-expression>，并将其与每个 case 中的 <comparison-expression> 结果进行比较。如果找到匹配的 case，则为该 case 求解 <expression>* 并返回。如果未找到匹配项且存在 <default-statement>，则执行默认语句中的 <expression>*。

```
(while <predicate-expression> [do <expression>]*)
```

只要 <predicate-expression> 不求值为符号 FALSE，就持续求解 <expression>*。

## 性能分析

`(get-profile-percent-threshold)`

返回当前的性能分析百分比阈值。

`(profile constructs | user-functions | off)`

启用/禁用对构造和用户函数的性能分析。

`(profile-info)`

显示当前为构造或用户函数收集的性能分析信息。

`(profile-reset)`

重置当前为构造或用户函数收集的所有性能分析信息。

`(set-profile-percent-threshold <number-in-range-of-0-to-100>)`

设置执行构造或用户函数所花费时间的最小百分比，以便 profile-info 命令将其显示出来。

## 序列展开

`(expand$ <multifield-expression>*)`

在函数调用内部使用时，将其参数作为单独的参数展开到函数中。$ 运算符只是 expand$ 函数调用的简写表示法。

`(get-sequence-operator-recognition)`

返回当前的序列运算符识别行为值。

`(set-sequence-operator-recognition <boolean-expression>)`

设置序列运算符识别行为。

## 字符串

`(build <string-or-symbol-expression>)`

将字符串作为在命令提示符下输入的内容进行求解。仅允许求解构造。

`(check-syntax <string-expression>)`

允许检查构造或函数调用的文本表示是否存在语法和语义错误。如果未检测到错误或警告，则返回 `FALSE`。

`(eval <string-or-symbol-expression>)`

将字符串作为在命令提示符下输入的内容进行求解。仅允许求解函数。

`(lowercase <string-or-symbol-expression>)`

返回其参数，并将所有大写字母替换为小写字母。

`(str-cat <expression>*)`

将所有参数作为字符串连接后返回。

`(str-compare <string-or-symbol-expression> <string-or-symbol-expression>)`

如果两个参数相等，则返回零；如果第一个参数在词典顺序上大于第二个参数，则返回正整数；如果第一个参数在词典顺序上小于第二个参数，则返回负整数。

`(str-index <lexeme-expression> <lexeme-expression>)`

如果第一个参数是第二个参数的子串，则返回第一个参数在第二个参数中的整数位置，否则返回 `FALSE`。

`(str-length <string-or-symbol-expression>)`

返回字符串的字符长度。

`(string-to-field <string-or-symbol-expression>)`

将字符串转换为字段。

`(sub-string <begin-integer-expression> <end-integer-expression> <string-expression>)`

返回 <string-expression> 中指定范围（<begin-integer-expression> 到 <end-integer-expression>）的子串。

`(sym-cat <expression>*)`

将所有参数作为符号连接后返回。

`(upcase <string-or-symbol-expression>)`

返回其参数，并将所有小写字母替换为大写字母。

## 文本处理

`(fetch <file-name>)`

将指定文件加载到内部查找表中。

`(print-region <logical-name> <lookup-file> <topic-field>*)`

在先前加载到查找表中的特定文件中查找指定条目，并将该条目的内容打印到指定的逻辑名称。

`(toss <file-name>)`

从内部查找表中卸载指定文件。

## 三角函数

`(acos <numeric-expression>)`

返回其参数的反余弦值（弧度）。

`(acosh <numeric-expression>)`

返回其参数的双曲反余弦值（弧度）。

`(acot <numeric-expression>)`

返回其参数的反余切值（弧度）。

`(acoth <numeric-expression>)`

返回其参数的双曲反余切值（弧度）。

`(acsc <numeric-expression>)`

返回其参数的反余割值（弧度）。

`(acsch <numeric-expression>)`

返回其参数的双曲反余割值（弧度）。

`(asec <numeric-expression>)`

返回其参数的反正割值（弧度）。

`(asech <numeric-expression>)`

返回其参数的双曲反正割值（弧度）。

`(asin <numeric-expression>)`

返回其参数的反正弦值（弧度）。

`(asinh <numeric-expression>)`

返回其参数的双曲反正弦值（弧度）。

`(atan <numeric-expression>)`

返回其参数的反正切值（弧度）。

`(atanh <numeric-expression>)`

返回其参数的双曲反正切值（弧度）。

`(cos <numeric-expression>)`

返回其参数的余弦值（弧度）。

`(cosh <numeric-expression>)`

返回其参数的双曲余弦值（弧度）。

`(cot <numeric-expression>)`

返回其参数的余切值（弧度）。

`(coth <numeric-expression>)`

返回其参数的双曲余切值（弧度）。

`(csc <numeric-expression>)`

返回其参数的余割值（弧度）。

`(csch <numeric-expression>)`

返回其参数的双曲余割值（弧度）。

`(sec <numeric-expression>)`

返回其参数的正割值（弧度）。

`(sech <numeric-expression>)`

返回其参数的双曲正割值（弧度）。

`(sin <numeric-expression>)`

返回其参数的正弦值（弧度）。

`(sinh <numeric-expression>)`

返回其参数的双曲正弦值（弧度）。

`(tan <numeric-expression>)`

返回其参数的正切值（弧度）。

`(tanh <numeric-expression>)`

返回其参数的双曲正切值（弧度）。

