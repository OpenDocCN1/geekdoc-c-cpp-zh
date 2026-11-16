

```
CLIPS> (get-deffunction-list)
(hypotenuse-length check-input factorial A B C)
CLIPS> (ppdeffunction factorial)
(deffunction MAIN::factorial
(?n)
(if (> ?n 1)
then
(* ?n (factorial (- ?n 1)))
else
1))
CLIPS>
```

当其他 deffunction 或构造引用要删除的 deffunction 时，你无法删除该 deffunction。在这种情况下，删除 deffunction 的唯一方法是移除其他引用或发出 clear 命令。例如：

```
CLIPS> (undefunction A)
[PRNTUTIL4] Unable to delete deffunction A.
CLIPS> (deffunction C (?n))
CLIPS> (undefunction A)
CLIPS> (undefunction C)
[PRNTUTIL4] Unable to delete deffunction C.
CLIPS> (clear)
CLIPS>
```

## 用户定义的函数

除了 deffunction，CLIPS 还提供了一种调用用 C 语言编写的函数的方法。使用此方法定义的函数称为用户定义函数。这个名称源自 CLIPS 的早期时代，当时 deffunction 构造尚未可用，添加新函数的唯一方法是用 C 语言编写。因此，虽然 deffunction 是由用户定义的，可以用用户定义函数这一术语来描述，但我们仅在指代用 C 语言编写的函数时才使用此术语。

本书随附光盘中包含的《高级编程指南》描述了如何创建并将用户定义函数添加到 CLIPS。通常，编写用户定义函数而非使用 deffunction 只有两个原因。第一是如果你已有用 C 语言编写并希望与 CLIPS 集成的代码。重写大量代码是不希望的，因此在许多情况下，将代码保留在 C 语言中并通过用户定义函数让 CLIPS 调用它更为简单。第二个原因是速度。特别是对于大段代码，编译为本机代码的 C 函数执行速度将远快于在 CLIPS 提供的解释环境中运行的 deffunction。幸运的是，对于大多数任务，能够直接在 CLIPS 环境中定义 deffunction 的便利性足以弥补运行解释代码所导致的速度下降。将用户定义函数添加到 CLIPS 需要创建一个新的 CLIPS 可执行程序，如果你不熟悉编译器的使用或 C 语言编程，这可能是你不想承担的工作量。除了《高级编程指南》中包含的用户定义函数示例外，你还可以通过浏览随光盘附带的 CLIPS 源代码，找到大量用户定义函数的示例。第 7 至 12 节中描述的所有函数和命令均是使用用户定义函数方法添加到 CLIPS 的。

## 10.4 DEFGLOBAL 构造

CLIPS 允许你定义在构造作用域之外仍保留其值的变量。这些变量称为全局变量。迄今为止，在构造中使用的所有变量都是局部变量。这些变量局限于引用它们的构造。例如，考虑以下两条规则中使用的变量 ?x：

```
(defrule example-1
  (data-1 ?x)
  =>
  (printout t "?x = " ?x crlf))
```

```
(defrule example-2
  (data-2 ?x)
  =>
  (printout t "?x = " ?x crlf))
```

规则 example-1 中 ?x 的值绝不会以任何方式限制规则 example-2 中 ?x 的值。如果断言事实 (data-1 3)，则值 3 将被赋给 example-1 规则中的 ?x。这不会将 example-2 规则中的模式限制为仅匹配 ?x 值为 3 的 data-2 事实。此外，再断言事实 (data-1 4) 也不会限制 example-1 规则两次激活中 ?x 的值必须相同。本质上，每条规则的每个部分匹配或激活都有自己的局部变量集。每次 deffunction 调用也是如此。

全局变量使用 defglobal 构造定义。defglobal 的一般格式为：

```
(<defglobal [<defmodule-name>] <global-assignment>*)
```

其中 <global-assignment> 为：

```
<global-variable> = <expression>
```

而 <global-variable> 为：

```
?*<symbol>*
```

<defmodule-name> 是定义全局变量的模块。如果未指定，全局变量将放置在当前模块中。全局变量名称以 * 字符开头和结尾，因此你可以轻松分辨 ?x 是局部变量，而 ?*x* 是全局变量。定义 defglobal 构造时，每个 defglobal 的初始值通过求值 <expression> 并将结果值赋给 defglobal 来确定。例如：

```
CLIPS>
(defglobal ?*x* = 3
?*y* = (+ ?*x* 1))
CLIPS> ?*x*
3
CLIPS> ?*y*
4
CLIPS>
```

请注意，由于全局变量 ?*x* 在 ?*y* 之前定义，我们可以使用其值来确定 ?*y* 的初始值。此外，由于全局变量在构造之外保留其值，我们可以直接在命令提示符下输入全局变量名称来确定其值。除了命令行之外，defglobal 引用可以在任何可以使用 <expression> 的地方使用，这意味着你可以在 deffunction 的主体或规则的 RHS 中使用它们。你不能将它们用作 deffunction 的参数，并且仅当它们包含在函数调用中时，才能在规则的 LHS 中使用它们。例如，以下构造均为非法：

```
(defglobal illegal-1 (?*x* ?y)
(+ ?*x* ?y))
(defrule illegal-2
(data-1 ?*x*)
=>
(defrule illegal-3
(data-1 ?x&~?*x*)
=>
```

### Defglobal 命令

可以使用 bind 命令更改 defglobal 的值。无需指定局部变量，只需指定全局变量即可。提供了多个命令用于操作 defglobals。ppdefglobal（美化打印 defglobal）命令用于显示 defglobal 的文本表示形式。undefglobal 命令用于删除 defglobal。list-defglobals 命令用于显示 CLIPS 中定义的 defglobal 列表。show-defglobals 命令用于显示 CLIPS 中定义的 defglobal 的名称和值。get-defglobal-list 函数返回包含 defglobal 列表的多值字段。这些命令的语法为：

```
(ppdefglobal <defglobal-name>)
(undefglobal <defglobal-name>)
(list-defglobals [<module-name>])
(show-defglobals [<module-name>])
(get-defglobal-list [<module-name>])
```

ppdefglobal 和 undefglobal 命令的 <defglobal-name> 应使用全局变量名称，不包括开头和结尾的 * 字符（例如，使用 x 而不是 *x*）。以下示例使用这些函数：

```
CLIPS> (ppdefglobal y)
(defglobal MAIN ?*y* = (+ ?*x* 1))
CLIPS> (list-defglobals)
x
y
For a total of 2 defglobals.
CLIPS> (get-defglobal-list)
(x y)
CLIPS> (show-defglobals)
?*x* = 3
?*y* = 4
CLIPS> (bind ?*y* 5)
5
CLIPS> (show-defglobals)
?*x* = 3
?*y* = 5
CLIPS> (undefglobal y)
CLIPS> (list-defglobals)
x
For a total of 1 defglobal.
CLIPS>
```

### Defglobal 重置行为

每当发出 reset 命令，或使用 bind 命令更改全局变量的值但未提供新值时，defglobal 的值都会恢复到其原始定义值。例如：

```
CLIPS> (bind ?*x* some-value)
some-value
CLIPS> ?*x*
some-value
CLIPS> (reset)
CLIPS> ?*x*
3
CLIPS> (bind ?*x* another-value)
another-value
CLIPS> ?*x*
another-value
CLIPS> (bind ?*x*)
3
CLIPS> ?*x*
3
CLIPS>
```

可以通过调用 set-reset-globals 函数并提供 FALSE 值来禁用全局变量的重置行为。提供 TRUE 值将恢复该行为。禁用此行为后，reset 命令不会将 defglobal 的值恢复到其原始定义值。例如：

```
CLIPS> (bind ?*x* 5)
5
CLIPS> (set-reset-globals FALSE)
TRUE
CLIPS> (reset)
CLIPS> ?*x*
5
CLIPS> (set-reset-globals TRUE)
FALSE
CLIPS> (reset)
CLIPS> ?*x*
3
CLIPS>
```

### 监视 Defglobals

当使用 watch 命令监视 defglobals 时，每当 defglobal 的值发生变化，就会打印一条信息消息。例如：

```
CLIPS> (watch globals)
CLIPS> (bind ?*x* 6)
```

