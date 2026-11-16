
例如，如果你在顶层提示符中输入的构造有拼写错误，则必须重新输入整个构造。如果你先在编辑器中输入了构造，则可以在编辑器内通过几次按键来更正拼写错误并重新定义构造。最初，所示示例将是直接从顶层输入到 CLIPS 中的规则。

作为示例，让我们考虑可能用于监控和响应一系列可能紧急情况的事实和规则类型。此类紧急情况之一可能是火灾；另一个可能是洪水。工业厂房监控专家系统中可能规则的伪代码如下所示：

```
IF the emergency is a fire
THEN the response is to activate
the sprinkler system
```

在将伪代码转换为规则之前，必须定义规则所引用的事实类型的 deftemplate。紧急情况可以由以下 deftemplate 表示：

```
(deftemplate emergency (slot type))
```

其中 emergency 事实的 type 字段将包含火灾、洪水和停电等符号。同样，响应可以由以下 deftemplate 表示：

```
(deftemplate response (slot action))
```

其中 response 事实的 action 字段指示要采取的响应。以下是用 CLIPS 语法表示的规则。可以在 CLIPS 提示符后输入该规则，但在输入规则之前，必须先输入 emergency 和 response deftemplates。但是，在输入任何这些构造之前，请在顶层提示符处键入命令 (clear) 并按回车。这将删除上一节中创建的 deftemplates 和 deffacts。clear 命令将在第 7.13 节中详细说明。

```
(defrule fire-emergency "An example rule"
(emergency (type fire))
=>
(assert (response
(action activate-sprinkler-system))))
```

如果按所示正确输入规则，CLIPS 提示符将重新出现。否则，将出现一条错误消息，很可能指示关键字拼写错误或括号位置不当。

以下是同一规则，添加了注释以匹配规则的各个部分。注释以分号开头，并持续到回车符。CLIPS 会忽略注释，将在第 7.18 节中讨论。

```
; Rule header
(defrule fire-emergency "An example rule"
  ; Patterns
  (emergency (type fire))
  ; THEN arrow
  =>
  ; Actions
  (assert (response
    (action activate-sprinkler-system))))
```

### 规则的一般格式如下：

```
(defrule <rule name> [<comment>]
  <patterns>* ; Left-Hand Side (LHS) of the rule
  =>
  <actions>*) ; Right-Hand Side (RHS) of the rule
```

整个规则必须用括号括起来，规则中的每个模式和动作也必须用括号括起来。规则可以有多个模式和动作。如果模式和动作嵌套，则围绕它们的括号必须正确匹配。在 fire-emergency 规则中，有一个模式和一个动作。

规则头由三部分组成。规则必须以 defrule 关键字开头，后跟规则名称。名称可以是任何有效的 CLIPS 符号。如果使用与现有规则相同的名称输入规则，则新规则将替换旧规则。在此规则中，规则名称为 fire-emergency。接下来是一个可选的注释字符串。对于此规则，注释为 "An example rule"。注释通常用于描述规则的目的或程序员希望的任何其他信息。与以分号开头的注释不同，规则名称后面的注释不会被忽略，可以与规则的其余部分一起显示（使用将在第 7.13 节中介绍的 ppdefrule 命令）。

规则头之后是零个或多个条件元素（CE）。最简单的 CE 类型是模式 CE 或简称模式。每个模式由一个或多个约束组成，旨在匹配 deftemplate 事实的字段。在 fire-emergency 规则中，模式是 emergency (type fire)。type 字段的约束表示，此规则仅对 type 字段中包含符号 fire 的 emergency 事实满足。CLIPS 尝试将规则的模式与事实列表中的事实进行匹配。如果规则的所有模式都匹配事实，则规则会被激活并放入议程（即已激活规则的集合）。议程中可能有零个或多个规则。

规则中模式后面的符号 => 称为箭头。它是通过输入等号然后再输入大于号形成的。箭头是一个符号，表示 IF-THEN 规则中 THEN 部分的开始。箭头之前的规则部分称为左侧（LHS），箭头之后的部分称为右侧（RHS）。

如果规则没有模式，则特殊模式 (initial-fact) 将作为规则的模式添加。由于 initial-fact deffacts 是自动定义的，因此当执行 reset 命令时，LHS 上没有模式的任何规则都会被激活，因为 (initial-fact) 事实会自动被断言。因此，任何没有 LHS 模式的规则在执行 reset 时都会被放入议程。

规则的最后部分是规则触发时将执行的动作列表。规则可以没有动作。这并不特别有用，但可以这样做。在我们的示例中，一个动作是断言事实 (response (action activate-sprinkler-system))。fires 一词表示 CLIPS 从议程中执行规则的动作。当议程上没有规则时，程序通常会停止执行。当议程上有多个规则时，CLIPS 会自动确定要触发的适当规则。CLIPS 按优先级递增的顺序对议程上的规则进行排序，并触发优先级最高的规则。规则的优先级是一个名为 salience 的整数属性。salience 将在第 9 章中更详细地讨论。

## 7.12 议程与执行

可以使用 run 命令运行 CLIPS 程序。run 命令的语法如下：

```
(run [<limit>])
```

其中可选参数 <limit> 是要触发的规则的最大数量。如果未包含 <limit> 或 <limit> 为 -1，则规则将一直触发直到议程上没有规则为止。否则，在 <limit> 个规则触发后，规则执行将停止。

运行 CLIPS 程序时，会触发议程上 salience 最高的规则。如果议程上只有一条规则，当然该规则会触发。由于 fire-emergency 规则的条件元素由事实 (emergency (type fire)) 满足，因此运行程序时 fire-emergency 规则应会触发。

当规则的所有模式都被事实匹配时，规则即被激活。模式匹配过程始终保持最新，无论事实是在规则定义之前还是之后断言，都会发生此过程。

由于规则需要事实才能执行，reset 命令是在 CLIPS 中启动或重新启动专家系统的关键方法。通常，reset 断言的事实会满足一个或多个规则的模式，并将这些规则的激活放入议程。然后发出 run 命令以开始执行程序。

### 显示议程

可以使用 agenda 命令显示议程上的规则列表。agenda 命令的语法如下：

```
(agenda)
```

如果议程上没有激活，则在发出 agenda 命令后 CLIPS 提示符将重新出现。如果 fire-emergency 规则已由事实索引为 1 的 (emergency (type fire)) 事实激活，则 agenda 命令将产生以下输出：

```
CLIPS> (reset)
CLIPS> (assert (emergency (type fire)))
<Fact-1>
CLIPS> (agenda)
0 fire-emergency: f-1
For a total of 1 activation.
CLIPS>
```

0 表示规则在议程上的 salience。salience 之后是规则名称，然后是匹配规则模式的事实标识符。在此例中，只有一个事实标识符 f-1。

### 规则与反射

当 fire-emergency 规则在议程上时，run 命令将导致规则触发。事实 (response (action activate-sprinkler-system)) 将作为规则的动作添加到事实列表中，如以下输出所示：

```
CLIPS> (run)
CLIPS> (facts)
f-0 (initial-fact)
f-1 (emergency (type fire))
f-2 (response
       (action activate-sprinkler-system))
For a total of 3 facts.
CLIPS>
```

此时会出现一个有趣的问题：如果再次发出 run 命令会怎样？有一条规则和一个满足该规则的事实，因此规则应该再次触发。但是，如果此时尝试 run 命令，将不会产生任何结果。检查议程将验证没有规则被触发，因为议程上没有规则。

规则没有再次触发是因为 CLIPS 的设计方式。CLIPS 中的规则表现出一种称为 refraction 的属性，这意味着它们不会针对特定事实集触发多次。如果没有 refraction，专家系统总会陷入琐碎的循环。也就是说，一旦规则触发，它就会针对同一个事实反复触发。在现实世界中，导致触发的刺激最终会消失。例如，火灾最终会被喷淋系统扑灭或自行燃尽。但是，在计算机世界中，一旦事实被输入事实列表，它就会保留在那里，直到被显式删除。

如有必要，可以通过撤回事实 (emergency (type fire)) 并再次断言它来使规则再次触发。基本上，CLIPS 会记住触发规则触发的事实标识符，并且不会再次激活该规则
