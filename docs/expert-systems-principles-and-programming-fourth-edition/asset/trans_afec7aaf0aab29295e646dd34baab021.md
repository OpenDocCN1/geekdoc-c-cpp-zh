

CLIPS> (ppdefrule RECOVERY::example1)
(defrule RECOVERY::example1
==>
CLIPS> (ppdefrule DETECTION::example1)
(defrule DETECTION::example1
==>
CLIPS>

以下命令允许将模块指定为构造名称的一部分：ppdefrule、undefrule、ppdeftemplate、undeftemplate、ppdeffacts、undeffacts、matches、refresh、remove-break 和 set-break。

## 9.7 导入和导出事实

您已学习如何通过将构造放在单独的模块中来对其进行分区。事实本身也可以分区。断言的事实会自动与定义其对应 deftemplate 的模块关联。例如：

```
CLIPS>
(deftemplate DETECTION::fault
(slot component))
CLIPS> (assert (fault (component A)))
<Fact-0>
CLIPS> (facts)
f-0 (fault (component A))
For a total of 1 fact.
CLIPS>
(deftemplate ISOLATION::possible-failure
(slot component))
CLIPS> (assert (possible-failure (component B)))
<Fact-1>
CLIPS> (facts)
f-1 (possible-failure (component B))
For a total of 1 fact.
CLIPS> (set-current-module DETECTION)
ISOLATION
CLIPS> (facts)
f-0 (fault (component A))
For a total of 1 fact.
CLIPS>
```

请注意，在 ISOLATION 模块中列出的唯一事实是 possible-failure 事实，其对应的 deftemplate 包含在 ISOLATION 模块中。DETECTION 模块中的 fault 事实也是如此。

facts 命令（与 list-defrules 及类似命令一样）可以接受模块名称作为可选参数。facts 命令的语法为：

```
{facts [<module-name>]
[<start> [<end> [<maximum>]]]]}
```

与 list-defrules 命令一样，指定模块名称仅列出指定模块中包含的事实。如果对模块名称使用 *，则列出所有事实：

```
CLIPS> (facts DETECTION)
f-0     (fault (component A))
For a total of 1 fact.
CLIPS> (facts ISOLATION)
f-1     (possible-failure (component B))
For a total of 1 fact.
CLIPS> (facts RECOVERY)
CLIPS> (facts *)
f-0     (fault (component A))
f-1     (possible-failure (component B))
For a total of 2 facts.
CLIPS>
```

与 defrule 和 deffacts 构造不同，deftemplate 构造（以及使用该 deftemplate 的所有事实）可以与其他模块共享。事实由包含其 deftemplate 的模块“拥有”，但拥有模块可以导出与事实关联的 deftemplate，从而使该事实以及使用该 deftemplate 的所有其他事实对其他模块可见。仅导出 deftemplate 不足以使事实对另一个模块可见。要使用在另一个模块中定义的 deftemplate，模块还必须导入 deftemplate 定义。

导出 deftemplate 的模块必须在其 deftemplate 定义中使用 export 属性。export 属性必须使用以下格式之一：

```
(export ?ALL)
(export ?NONE)
(export deftemplate ?ALL)
(export deftemplate ?NONE)
(export deftemplate <deftemplate-name>+)
```

第一种格式将导出模块中的所有可导出构造。在本书迄今讨论的构造中，只有 deftemplate 是可导出的。CLIPS 中的其他一些过程式和面向对象编程构造也可以导出，导出这些构造的语法将在第 10 章和第 11 章中讨论。第二种格式表示不导出任何构造，并且是 deftemplate 的默认设置。第三种格式表示模块中的所有 deftemplate 都被导出。就本书讨论的构造而言，这与第一种格式相同。同样，第四种格式表示不导出任何 deftemplate 构造。第二种和第四种格式主要用于明确说明模块导出的构造。最后，第五种格式给出模块导出的 deftemplate 的特定列表。export 属性可以在 defmodule 定义中使用多次，以指定不同类型的导出构造，但由于 deftemplate 是我们讨论过的唯一可导出构造，因此无需使用多个 export 属性语句。

import 属性也有五种可能的格式：

```
(import <module-name> ?ALL)
(import <module-name> ?NONE)
(import <module-name> deftemplate ?ALL)
(import <module-name> deftemplate ?NONE)
(import <module-name> deftemplate <deftemplate-name>+)
```

每种格式的含义均与其 export 对应格式相同，只是导入指定的构造。此外，必须指定正在从中导入构造的模块。与 export 属性类似，defmodule 定义可以有多个 import 属性。

构造必须在被指定到导入列表之前定义，但不必在被指定到导出列表之前定义（为了将构造放入模块，必须先定义模块，因此实际上不可能在导出它的模块定义之前定义构造）。由于此限制，两个模块不可能相互导入（即，如果模块 A 从模块 B 导入，则模块 B 不可能从模块 A 导入）。

为了说明导入和导出事实，假设 RECOVERY 模块想要从 DETECTION 模块导入 fault deftemplate，并从 ISOLATION 模块导入 possible-failure deftemplate。与其他构造不同，一旦定义，defmodule 就不能重新定义。因此，为了更改 defmodule 的导入和导出属性，必须先发出 clear 命令。此限制有一个例外：预定义的 MAIN 模块可以重新定义一次，以包含不同的导入和导出属性（默认情况下，MAIN 模块既不导出也不导入任何内容）。请注意，MAIN 模块的默认定义不导出 initial-fact deftemplate。回顾第 8 章，(initial-fact) 模式在某些情况下会添加到规则的 LHS（例如，当第一个 CE 是 not CE 时）。如果将此类规则放在不从 MAIN 模块导入 initial-fact deftemplate 的模块中，则该规则无法被激活。另请注意，定义规则时不会收到错误，因为 (initial-fact) 模式会导致在当前模块中创建一个隐式 initial-fact deftemplate。

DETECTION、ISOLATION 和 RECOVERY 模块及其 deftemplate 的新定义（均应在 clear 命令之后输入）如下：

```
(defmodule DETECTION
(export deftemplate fault))
(deftemplate DETECTION::fault
(slot component))
```

```
(defmodule ISOLATION
(export deftemplate possible-failure))
(deftemplate ISOLATION::possible-failure
(slot component))
(defmodule RECOVERY
(import DETECTION deftemplate fault)
(import ISOLATION deftemplate possible-failure))
```

定义 defmodule 和 deftemplate 后，现在可以在 DETECTION 和 RECOVERY 模块中断言 fault 事实，并在 ISOLATION 和 RECOVERY 模块中断言 possible-failure 事实：

```
CLIPS>
(deffacts DETECTION::start
(fault (component A)))
CLIPS>
(deffacts ISOLATION::start
(possible-failure (component B)))
CLIPS>
(deffacts RECOVERY::start
(fault (component C))
(possible-failure (component D)))
CLIPS> (reset)
CLIPS> (facts DETECTION)
f-0   (fault (component A))
f-2   (fault (component C))
For a total of 2 facts.
CLIPS> (facts ISOLATION)
f-1   (possible-failure (component B))
f-3   (possible-failure (component D))
For a total of 2 facts.
CLIPS> (facts RECOVERY)
f-0   (fault (component A))
f-1   (possible-failure (component B))
f-2   (fault (component C))
f-3   (possible-failure (component D))
For a total of 4 facts.
CLIPS>
```

请注意，DETECTION 和 RECOVERY 模块都能看到任一模块断言的 fault 事实。ISOLATION 和 RECOVERY 模块断言的 possible-failure 事实也是如此。

## 9.8 模块和执行控制

除了控制模块可以导入和导出哪些 deftemplate 之外，defmodule 构造还可用于控制规则的执行。CLIPS 中定义的每个模块都有自己的议程，而不是仅作为一个总议程的一部分。然后可以通过决定选择哪个模块的议程来执行规则来控制执行。例如，以下 defrule 应该都会被前一个示例中断言的 fault 和 possible-failure 事实激活：

```
(defrule DETECTION::rule-1
   (fault (component A | C))
   =>)
(defrule ISOLATION::rule-2
   (possible-failure (component B | D))
   =>)
(defrule RECOVERY::rule-3
   (fault (component A | C))
   (possible-failure (component B | D))
   =>)
```

加载这些规则后，如果发出 agenda 命令，将显示 RECOVERY 模块的议程，因为最后定义的规则被放置在该模块中：

```
CLIPS> (get-current-module)
RECOVERY
CLIPS> (agenda)
0     rule-3: f-0,f-3
0     rule-3: f-0,f-1
0     rule-3: f-2,f-3
0     rule-3: f-2,f-1
For a total of 4 activations.
CLIPS>
```

与 list-defrules 和 facts 命令一样，agenda 命令接受一个可选参数，如果指定了该参数，则表示将列出其议程的模块：

```
CLIPS> (agenda DETECTION)
0     rule-1: f-2
0     rule-1: f-0
For a total of 2 activations.
CLIPS> (agenda ISOLATION)
0     rule-2: f-3

