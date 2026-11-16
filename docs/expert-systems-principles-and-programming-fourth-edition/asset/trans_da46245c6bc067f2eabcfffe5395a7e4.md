

与完全相同的事实标识符组合。相同的事实标识符集必须在顺序和事实索引上一一匹配。本章后面的示例将展示单个事实可以以多种方式匹配模式。在这种情况下，对于单个规则，具有相同事实标识符集的多个激活可以放在议程上，每个不同的匹配对应一个。

或者，可以使用 refresh 命令使规则再次触发。refresh 命令将规则已触发的所有激活重新放回议程（限制是触发激活的事实仍存在于事实列表中）。refresh 命令的语法是：

```
(refresh <rule-name>)
```

以下命令展示了如何使用 refresh 命令重新激活 fire-emergency 规则：

```
CLIPS> (agenda)
CLIPS> (refresh fire-emergency)
CLIPS> (agenda)
0 fire-emergency: f-1
For a total of 1 activation.
CLIPS>
```

### 监视激活、规则和统计信息

如果正在监视激活，CLIPS 会在每次激活被添加到或从议程中移除时自动打印一条消息。与事实一样，字符序列 ==> 表示正在从议程中移除激活，字符序列 ===> 表示正在将激活添加到议程中。在初始命令序列之后，激活将以 agenda 命令使用的相同格式打印。以下命令序列说明了正在监视的激活：

```
CLIPS> (reset)
CLIPS> (watch activations)
CLIPS> (assert (emergency (type fire)))
==> Activation 0 fire-emergency: f-1
<Fact-1>
CLIPS> (agenda)
0 fire-emergency: f-1
For a total of 1 activation.
CLIPS> (retract 1)
==> Activation 0 fire-emergency: f-1
CLIPS> (agenda)
CLIPS>
```

如果正在监视规则，CLIPS 会在每次规则触发时打印一条消息。以下命令序列说明了正在监视的激活和规则：

```
CLIPS> (reset)
CLIPS> (watch rules)
CLIPS> (assert (emergency (type fire)))
==> Activation 0 fire-emergency: f-1
<Fact-1>
CLIPS> (run)
FIRE 1 fire-emergency: f-1
CLIPS> (agenda)
CLIPS>
```

符号 FIRE 后面的数字表示自给出 run 命令以来已触发的规则数量。例如，如果在 fire-emergency 规则之后又有一条规则触发，它将前面带有“FIRE 2”。打印触发顺序后，会打印规则名称，后跟匹配规则模式的事实索引。请注意，监视激活不会导致在规则触发时（因此从议程中移除）显示消息。

可以通过在 watch 命令末尾指定一个或多个规则名称来监视特定规则和激活。例如，(watch activations fire-emergency) 将仅显示 fire-emergency 规则的激活消息。

如果正在监视统计信息，CLIPS 将在运行完成时打印诸如以下的信息消息：

```
CLIPS> (unwatch all)
CLIPS> (reset)
CLIPS> (watch statistics)
CLIPS> (assert (emergency (type fire)))
<Fact-1>
CLIPS> (run)
1 rules fired         Run time is 0.02 seconds
50.0 rules per second
3 mean number of facts (3 maximum)
1 mean number of instances (1 maximum)
1 mean number of activations (1 maximum)
CLIPS> (unwatch statistics)
CLIPS>
```

监视统计信息时，run 命令后会打印出六项统计信息。首先显示的是已触发规则的总数、触发规则所花费的秒数以及每秒触发的规则平均数（第一项统计除以第二项统计）。此外，对于每个执行周期，CLIPS 会保留事实、激活和实例数量的统计信息。事实的平均数是每次规则触发后事实列表中事实总数之和除以已触发规则的数量。括号中紧跟单词 maximum 的数字表示任何一次规则触发中事实列表包含的最大事实数。同样，激活的平均数和最大数统计信息分别表示每次规则触发的平均激活数和任何一次规则触发中议程上的最大激活数。实例的平均数和最大数显示与 COOL 相关的信息。

## 7.13 操作构造的命令

### 显示指定构造的成员列表

list-defrules 命令用于显示 CLIPS 维护的当前规则列表。同样，list-deftemplates 和 list-deffacts 命令分别可用于显示当前的 deftemplates 列表或当前的 deffacts 列表。这些命令的语法是：

```
(list-defrules)
(list-deftemplates)
(list-deffacts)
```

例如，

```
CLIPS> (list-defrules)
fire-emergency
For a total of 1 rule.
CLIPS> (list-deftemplates)
initial-fact
emergency
response
For a total of 3 deftemplates.
CLIPS> (list-deffacts)
initial-fact
For a total of 1 deffacts.
CLIPS>
```

### 显示指定构造成员的文本表示

ppdefrule（美观打印 defrule）、ppdeftemplate（美观打印 deftemplate）和 ppdeffacts（美观打印 deffacts）命令分别用于显示 defrule、deftemplate 和 deffacts 的文本表示。这些命令的语法是：

```
(ppdefrule <defrule-name>)
(ppdeftemplate <deftemplate-name>)
(ppdeffacts <deffacts-name>)
```

每个命令的单个参数指定要显示的 defrule、deftemplate 或 deffacts 的名称。显示时，CLIPS 将构造的不同部分放在不同的行上，以提高可读性。例如，

```
CLIPS> (ppdefrule fire-emergency)
(defrule MAIN::fire-emergency "An example rule"
   (emergency (type fire))
   =>
   (assert (response
      (action activate-sprinkler-system)))))
CLIPS> (ppdeftemplate response)
(deftemplate MAIN::response
   (slot action))
CLIPS> (ppdeffacts initial-fact)
CLIPS> (deffacts start-fact (start-fact))
CLIPS> (ppdeffacts start-fact)
(deffacts MAIN::start-fact
   (start-fact))
CLIPS>
```

构造名称前的符号 MAIN:: 表示构造所在的模块。模块提供了一种分区知识库的机制，将在第 9 章中详细讨论。请注意，initial-fact deffacts 没有文本表示（因为它由 CLIPS 自动创建）。但是，输入的 start-fact deffacts 确实有文本表示。

### 删除指定的构造成员

undefrule、undeftemplate 和 undeffacts 命令分别用于删除 defrule、deftemplate 和 deffacts。这些命令的语法是：

- (undefrule <defrule-name>)
- (undeftemplate <deftemplate-name>)
- (undeffacts <deffacts-name>)

每个命令的单个参数指定要删除的 defrule、deftemplate 或 deffacts 的名称。例如，

```
CLIPS> (undeffacts start-fact)
CLIPS> (list-deffacts)
initial-fact
For a total of 1 deffacts.
CLIPS> (undefrule fire-emergency)
CLIPS> (list-defrules)
CLIPS>
```

请注意，initial-fact deffacts 和 initial-fact deftemplate 可以像任何其他用户定义的构造一样删除。如果现在执行 reset 命令，(initial-fact) 事实将不会被添加到事实列表中。

如果将符号 * 作为任何构造删除命令的参数，则会删除适当类型的所有构造。例如，(undefrule *) 将删除所有 defrules。符号 * 也可以与 retract 命令一起用于删除所有事实。

被其他构造引用的构造在引用它们的构造被删除之前不能删除。如以下对话所示，initial-fact deftemplate 在 initial-fact deffacts 被删除、事实 (initial-fact) 被删除以及 example defrule 被删除（它使用默认的 initial-fact 模式）之前不能删除：

```
CLIPS> (defrule example =>)
CLIPS> (undeftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (undeffacts initial-fact)
CLIPS> (undeftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (undefrule example)
CLIPS> (undeftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (retract *)
CLIPS> (undeftemplate initial-fact)
CLIPS>
```

### 清除 CLIPS 环境中的所有构造

clear 命令可用于删除 CLIPS 环境中包含的所有信息。它删除 CLIPS 中当前包含的所有构造和事实列表中的所有事实。clear 命令的语法是：

```
(clear)
```

清除 CLIPS 环境后，clear 命令将 initial-fact deffacts 添加到 CLIPS 环境中：

```
CLIPS> (list-deffacts)
CLIPS> (list-deftemplates)
environment
response
start-fact
For a total of 3 deftemplates.
CLIPS> (clear)
CLIPS> (list-deffacts)
initial-fact
For a total of 1 deffacts.
```

