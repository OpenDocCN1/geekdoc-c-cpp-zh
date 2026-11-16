

```
<== Focus MAIN
==> Focus MAIN
CLIPS> (run)
Fire 1 start: f-0
==> Focus DETECTION from MAIN
Fire 2 example-1: f-0
<== Focus DETECTION to MAIN
==> Focus MAIN
CLIPS>
```

关于此示例有两点值得注意。首先，为了使 DETECTION 模块中的规则能够通过使用默认 *initial-fact* 模式而被激活，*initial-fact* deftemplate 必须由 MAIN 模块导出并由 DETECTION 模块导入。其次，请注意 return 命令 *immediately* 停止规则 RHS 的执行。return 命令之后的 *printout* 命令不会在 *example-1* 规则中执行（在 *example-2* 规则中也不会，因为它没有机会触发）。请注意，*return* 命令的功能与 *pop-focus* 命令相似，但不完全相同，*pop-focus* 命令会从焦点栈中移除当前焦点，但会允许规则 RHS 中的操作继续执行。如果在这个示例中使用 *pop-focus* 命令代替 return 命令，那么在执行 *example-1* 规则的操作时，字符串 "No printout." 就会被打印出来。

## 自动聚焦特性

除了可以使用 *focus* 命令显式聚焦于模块外，还可以在该模块中的特定规则被激活时自动聚焦于该模块。默认情况下，规则被激活时其模块不会自动聚焦。可以通过使用 **auto-focus** 属性来更改这一点。auto-focus 属性在 declare 语句中与 salience 属性一起指定。指定关键字 *auto-focus*，后跟 TRUE（启用该功能）或 FALSE（禁用该功能）。模块中不需要所有规则都启用 auto-focus 功能，才能让模块中的某些规则使用它。同样，如果为规则使用 declare 语句，也不需要同时声明 salience 属性和 auto-focus 属性。以下示例说明了 auto-focus 功能的使用：

```
CLIPS> (clear)
CLIPS>
(defmodule MAIN
   (export deftemplate initial-fact))
CLIPS>
(defmodule DETECTION
   (import MAIN deftemplate initial-fact))
CLIPS>
(defrule DETECTION::example
   (declare (auto-focus TRUE))
   =>)
CLIPS> (watch focus)
CLIPS> (reset)
<== Focus MAIN
==> Focus MAIN
==> Focus DETECTION from MAIN
CLIPS>
```

当发出 reset 命令时，由于焦点栈为空，MAIN 模块会自动聚焦。example 规则通过断言 initial-fact 事实被激活。由于该规则启用了 auto-focus 属性，其模块（即 DETECTION 模块）会自动压入焦点栈。auto-focus 功能特别适用于检测约束违规的规则。因为约束规则的模块会立即成为当前焦点，所以可以在违规发生时采取行动，而不是设置一个显式阶段来检测违规。

## 替换阶段和控制事实

通过使用 defmodules、focus 和 return 命令以及 auto-focus 功能，现在可以使用一种更显式的机制来替代阶段和控制事实，用于控制规则执行流程。第 9.4 节中描述的用于控制执行的结构可以用以下结构替代：

```
(defmodule DETECTION)
(defmodule ISOLATION)
(defmodule RECOVERY)
```

```
(deffacts MAIN::control-information
(phase-sequence DETECTION ISOLATION RECOVERY)))
```

```
(defrule MAIN::change-phase
   ?list <- (phase-sequence ?next-phase
                            $?other-phases)
   =>
   (focus ?next-phase)
   (retract ?list)
   (assert (phase-sequence
            ?next-phase)))
```

执行控制将在 DETECTION 模块、ISOLATION 模块和 RECOVERY 模块之间循环，然后再返回。每个模块中的所有规则都会触发，然后才允许下一个模块中的规则触发（除非发出了 return 命令，或因 auto-focus 功能而聚焦于新模块）：

```
CLIPS> (unwatch all)
CLIPS> (reset)
CLIPS> (watch rules)
CLIPS> (watch focus)
CLIPS> (run 5)
FIRE 1 change-phase: f-1
==> Focus DETECTION from MAIN
==> Focus DETECTION to MAIN
FIRE 2 change-phase: f-2
==> Focus ISOLATION from MAIN
==> Focus ISOLATION to MAIN
FIRE 3 change-phase: f-3
==> Focus RECOVERY from MAIN
==> Focus RECOVERY to MAIN
FIRE 4 change-phase: f-4
==> Focus DETECTION from MAIN
==> Focus DETECTION to MAIN
FIRE 5 change-phase: f-5
==> Focus ISOLATION from MAIN
==> Focus ISOLATION to MAIN
CLIPS>
```

## 9.9 RETE 模式匹配算法

像 CLIPS、Jess、Eclipse 和 OPS5 这样的基于规则的语言使用一种非常高效的算法，用于将事实与规则中的模式进行匹配，以确定哪些规则的条件已得到满足。该算法称为 **Rete 模式匹配算法**（Forgy 79）（Forgy 85）（Brownston 85）。编写高效的 CLIPS 规则不需要理解 Rete 算法。然而，理解 CLIPS 和其他基于规则的语言中使用的底层算法，有助于更容易地理解为什么以一种方式编写规则比以另一种方式更高效。

要理解 Rete 算法为何高效，有助于首先总体审视将事实与规则匹配的问题，然后再考察其他效率不高的算法。图 9.6 显示了 Rete 算法所解决的问题。

### 图 9.6 模式匹配：规则和事实

![](img/2c460d4de56b7ffaad3834eee20beaa0_548_0.png)

如果匹配过程只需发生一次，那么问题的解决方法就很简单。推理引擎可以检查每条规则，然后搜索事实集合以确定规则的模式是否已得到满足。如果规则的模式已得到满足，则可以将规则放入议程。图 9.7 显示了这种方法。

### 图 9.7 规则搜索事实

![](img/2c460d4de56b7ffaad3834eee20beaa0_548_1.png)

然而，在基于规则的语言中，匹配过程会反复进行。通常，在每个执行周期中，事实列表都会被修改。新事实可能会添加到事实列表中，或旧事实可能会从中删除。这些变化可能导致先前未满足的模式得到满足，或者反之。匹配问题现在成为一个持续的过程。在每个周期中，随着事实的添加和删除，必须维护和更新满足条件的规则集。

让推理引擎在每个执行周期后检查每条规则以指导事实搜索，为解决这个问题提供了一种简单直接的技术。这种方法的主要缺点是可能非常缓慢。大多数基于规则的专家系统表现出一种称为 *temporal redundancy* 的属性。通常，规则的操作只会更改事实列表中的少数几个事实。也就是说，专家系统中的事实随时间缓慢变化。每个执行周期可能只会添加或删除少量百分比的事实，因此通常只有少量百分比的规则受到事实列表变化的影响。因此，让规则驱动所需事实的搜索需要大量不必要的计算，因为大多数规则在当前周期中找到的事实很可能与上一个周期中找到的事实相同。

### 图 9.8 规则搜索事实时的不必要计算

![](img/2c460d4de56b7ffaad3834eee20beaa0_549_0.png)

周期。这种方法的低效性在图 9.8 中显示。阴影区域表示已对事实列表所做的更改。通过记住周期之间已匹配的内容，然后仅计算新添加或新删除事实所需的更改，可以避免不必要的重新计算，如图 9.9 所示。规则保持静态，而事实发生变化，因此应该是事实去查找规则，而不是反过来。

Rete 模式匹配算法旨在利用基于规则的专家系统所表现出的时间冗余。它通过保存周期之间的匹配过程状态，并仅针对事实列表中发生的更改重新计算此状态的变化来实现这一点。也就是说，如果一组模式在一个周期中找到了三个所需事实中的两个，则不需要

### 图 9.9 事实搜索规则

![](img/2c460d4de56b7ffaad3834eee20beaa0_549_1.png)

