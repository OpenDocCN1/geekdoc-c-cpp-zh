

`:= ?*x* ==> 6 <=> 3
6
CLIPS> (bind ?*x* 7)
==> ?*x* ==> 7 <=> 6
7
CLIPS> (reset)
==> ?*x* ==> 3 <=> 7
CLIPS> (unwatch globals)
CLIPS> (bind ?*x* 8)
8
CLIPS>

信息消息开头的 := 表示正在对全局变量进行赋值。下一个符号是被更改的 defglobal 的名称。随后是 ==> 和全局变量的新值。接下来是 <=> 和全局变量的旧值。

## Defglobals 与模式匹配

Defglobals 可用于规则左侧（LHS）的表达式中，但对 defglobals 的更改不会触发模式匹配。例如，请考虑以下 defglobal 和 defrule：

```
(defglobal ?*z* = 4)
(defrule global-example
(data ?z&:(> ?z ?*z*))
=>)
```

现在考虑当与 global-example 规则中的单个模式匹配的数据事实被断言时会发生什么：

```
CLIPS> (reset)
CLIPS> ?*z*
4
CLIPS> (assert (data 5) (data 6))
<Fact-2>
CLIPS> (facts)
f-0 (initial-fact)
f-1 (data 5)
f-2 (data 6)
For a total of 3 facts.
CLIPS> (agenda)
0 global-example: f-1
0 global-example: f-2
For a total of 2 activations.
CLIPS>
```

当断言事实 (data 5) 时，值 5 绑定到局部变量 ?z，然后将此值与全局变量 ?*z* 的值（即 4）进行比较。由于 5 大于 4，global-example 规则被事实 f-1 激活。同样，由于 6 大于 4，该规则也被事实 f-2 激活。此时，模式匹配已完成，更改 ?*z* 的值不会导致为该规则生成的激活重新评估模式：

```
CLIPS> (bind ?*z* 5)
5
CLIPS> (agenda)
0 global-example: f-1
0 global-example: f-2
For a total of 2 activations.
CLIPS>
```

将 ?*z* 的值更改为 5 并不会移除由事实 f-1 引起的激活，即使与 global-example 规则匹配的数据事实中找到的值 5 不再大于存储在全局变量 ?*z* 中的值。但是，撤销该事实并重新断言它，将重新触发模式匹配过程，并使用全局变量的新值，就像任何新断言的事实一样：

```
CLIPS> (retract 1)
CLIPS> (assert (data 5))
<Fact-3>
CLIPS> (agenda)
0 global-example: f-2
For a total of 1 activation.
CLIPS> (assert (data 7))
<Fact-4>
CLIPS> (agenda)
0 global-example: f-2
0 global-example: f-4
For a total of 2 activations.
CLIPS>
```

当 (data 5) 事实 f-1 被撤销后重新断言时，global-example 规则不再由该事实满足，因此不会生成激活。但是，断言事实 (data 7) 将导致激活，因为 ?z 的值为 7，这大于全局变量 ?*z* 的新值 5。

## Defglobals 的用途

Defglobals 最适合在规则中用作常量，或用于传递仅在规则右侧（RHS）使用且不应触发模式匹配的信息。作为常量使用时，defglobals 可以使您的程序更易于理解。请考虑以下规则：

```
(defrule plant-advisory
   (temperature ?value Fahrenheit)
   (test (<= ?value 32))
   =>
   (printout t "It's freezing." crlf)
   (printout t "Bring your plants inside." crlf))
```

当然，大多数人都知道水的冰点是 32° 华氏度（或 0° 摄氏度），因此 plant-advisory 规则中常量 32 的含义应该很容易推断出来。但并非所有常量都是常识。通过将值 32 赋给全局变量，我们可以在 plant-advisory 规则中使用有意义的符号名称，使其更易于理解：

```
(defglobal ?*water-freezing-point-Fahrenheit* = 32)

(defrule plant-advisory
   (temperature ?value Fahrenheit)
   (test (<= ?value ?*water-freezing-point-Fahrenheit*))
   =>
   (printout t "It's freezing." crlf)
   (printout t "Bring your plants inside." crlf))
```

使用 defglobals 避免触发模式匹配的一种用途是调试。假设您想打印 watch 命令提供的信息之外的一些附加信息。一种方法是在规则中添加类似于以下内容的 printout 或 format 命令：

```
(defrule debug-example
   (data ?x)
   =>
   (printout t "Debug-example ?x = " ?x crlf))
```

然而，问题在于您可能不希望一直看到这些调试消息，因此在不需要它们生效时，您必须要么删除它们，要么将其转换为注释。绕过此问题的一种便捷方法是将调试输出发送到的逻辑名称存储在 defglobal 中。如果 nil 被用作 printout 或 format 命令的逻辑名称参数，则不会产生任何输出（尽管 format 命令仍会将格式化字符串作为其返回值返回）。您可以利用这一事实在不想看到调试信息时丢弃它。以下是修改 debug-example 规则以使用 defglobal 的方法：

```
(defglobal ?*debug-print* = nil)
```

```
(defrule debug-example
(data ?x)
=>
(printout
"Debug-example ?x = " ?x crlf)
)
```

默认情况下，调试信息将发送到逻辑名称 nil，因此您不会在屏幕上看到它被打印。要将输出发送到屏幕，您只需将 ?*debug-print* 全局变量的值设置为符号 t，如以下对话所示：

```
CLIPS> (reset)
CLIPS> (assert (data a) (data b) (data c))
<Fact-3>
CLIPS> (agenda)
0 debug-example: f-1
0 debug-example: f-2
0 debug-example: f-3
For a total of 3 activations.
CLIPS> (run 1)
CLIPS> (bind ?*debug-print* t)
t
CLIPS> (run 2)
Debug-example ?x = b
Debug-example ?x = c
CLIPS>
```

请注意，我们是在允许一个 debug-example 激活触发后才启用调试信息的。如果我们将调试信息存储在事实中，就无法做到这一点。在这种情况下，debug-example 规则将如下所示：

```
(defrule debug-example
(debug ?debug-print)
(data ?x)
=>
(printout ?debug-print "Debug-example ?x = " ?x
crlf))
```

撤销 debug-print 事实并用新值重新断言它，将重新触发任何已经触发的 debug-example 激活，这将非常不希望。

## 10.5 DEFGENERIC 和 DEFMETHOD 构造

除了使用 defgeneric 构造定义的函数之外，CLIPS 还提供泛型函数。**泛型函数**本质上是一组共享通用名称的相关函数（称为**方法**）。事实上，拥有多个方法的泛型函数被称为**重载**（因为同一名称可能用于引用多个方法）。组中的每个方法都有自己的签名：它期望的参数数量和类型。当对泛型函数进行调用时，会检查参数，并执行与参数签名匹配的方法。此过程称为**泛型分派**。**defgeneric** 构造用于定义一组方法使用的通用泛型函数名称。defgeneric 的一般格式为：

```
(defgeneric <defgeneric-name> [<optional-comment>])
```

您唯一需要显式定义 defgeneric 的原因是，在引用泛型函数但尚未为该泛型函数定义任何方法时，它作为前向声明。如果在指定 defgeneric 构造之前定义了泛型函数的方法，则会为您自动生成一个 defgeneric。

泛型函数的特定方法使用 **defmethod** 构造定义。defmethod 的一般格式为：

```
(defmethod <defgeneric-name> [<index>]
[<optional-comment>]
[<regular-parameter-restriction>]*
[<wildcard-parameter-restriction>]
<expression>*)
```

特定的 defmethod 没有名称。构成泛型函数的所有方法都使用相同的 <defgeneric-name>。但是，每个特定方法都会被分配一个唯一的整数索引，可用于引用该方法。您可以在定义方法时通过指定 <index> 为方法分配特定索引。如果未指定 <index>，CLIPS 会自动为您创建一个。对于给定的泛型函数，特定参数签名（即 <regular-parameter-restriction> 和 <wildcard-parameter-restriction> 提供的值）只能有一个方法。如果您定义的泛型函数方法与该泛型函数现有方法具有相同的参数签名，且未指定 <index>，则现有方法将被新方法替换，并使用相同的索引。如果在定义方法时指定了 <index>，且存在具有相同参数签名的泛型函数方法，则 <index> 必须与具有相同签名的现有方法的索引相同，如果是，则现有方法将被新方法替换。

每个 <regular-parameter-restriction> 可以是两种形式之一。它可以是单字段变量（如 deffunction 中），也可以是以下形式：

