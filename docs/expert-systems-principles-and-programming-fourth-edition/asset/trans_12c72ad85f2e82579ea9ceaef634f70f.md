

```
for each condition in the antecedent
of the rule do
if Solve_Goal with condition attribute
if the value returned by solve_goal is not
equal to the value required by the condition
then
Return unsuccessful.
end if
end for

Return successful

end procedure
```

过程 Attempt_Rule 将从规则的第一个条件开始，在尝试规则的后续条件之前先尝试证明它。为了确定条件是否满足，过程 Attempt_Rule 必须知道条件中正在测试的属性的值。为了确定该值，过程 Solve_Goal 会被递归调用。如果过程 Solve_Goal 返回的值与条件所需的值不相等，过程 Attempt_Rule 将以返回值 unsuccessful 退出（请记住，条件中只测试相等性）。否则，将测试规则的下一个条件。如果规则的所有条件都满足，过程 Attempt_Rule 将以返回值 successful 退出。

## 在 CLIPS 中表示后向链式规则

再次强调，解决此问题的第一步是确定知识应如何表示。由于 CLIPS 不会自动执行后向链式推理，因此将后向链式规则表示为事实将很有用，以便可以由充当后向链式推理引擎的规则来检查前件和后件。表示后向链式规则的 deftemplate 如下所示。它将存储在 defmodule BC 中（将在本小节末尾定义，一旦确定了后向链式引擎所需的所有 deftemplate）：

```
(deftemplate BC::rule
(multislot if
(multislot then))
```

if 和 then 槽将分别存储每个规则的前件和后件。每个前件将包含以下格式的单个属性-值对：

```
<attribute> is <value>
```

或由符号 and 连接的一系列此类属性-值对。每个规则的后件只允许包含单个属性-值对。

作为使用此格式表示规则的示例，请考虑图 12.2 中的决策树。如前所述，该树可以轻松转换为使用 AV 对的规则。转换后规则的伪代码如下：

```
IF main-course is red-meat
THEN best-color is red

IF main-course is poultry and
meal-is-turkey is yes
THEN best-color is red

IF main-course is poultry and
meal-is-turkey is no
THEN best-color is white

IF main-course is fish
THEN best-color is white
```

规则中使用的属性为 main-course、meal-is-turkey 和 best-color。main-course 属性对应于决策树问题“主菜是什么？”确定的答案。meal-is-turkey 属性对应于问题“主菜是火鸡吗？”确定的答案。请注意，确定最佳颜色未知的决策树分支未表示为规则，因为我们的后向链式推理器的局限性之一是未表示未知值。如果主菜不是产生答案的那些之一，在这种情况下，将询问用户 best-color 属性的值。

以下 deffacts 展示了如何使用后向链式规则格式表示葡萄酒规则。由于这些规则事实不是后向链式机制的固有部分，它们将被放置在 MAIN 模块中（请回顾，MAIN 模块从所有其他模块导入，因此规则 deftemplate 对其可见）：

```
(deffacts MAIN::wine-rules
  (rule (if main-course is red-meat)
        (then best-color is red))

  (rule (if main-course is fish)
        (then best-color is white))

  (rule (if main-course is poultry and
        meal-is-turkey is yes)
        (then best-color is red))

  (rule (if main-course is poultry and
        meal-is-turkey is no)
        (then best-color is white))))
```

这种表示在操作后向链式规则时提供了很大的灵活性。例如，如果确定属性 main-course 的值为 poultry，则可以从事实列表中删除以下事实：

```
(rule (if main-course is red-meat)
(then best-color is red))
```

和：

```
(rule (if main-course is fish)
(then best-color is white))
```

以指示这些规则不适用，并且以下事实：

```
(rule (if main-course is poultry and
meal-is-turkey is yes)
(then best-color is red))
```

和：

```
(rule (if main-course is poultry and
meal-is-turkey is no)
(then best-color is white))
```

分别可修改为以下事实：

```
(rule (if meal-is-turkey is yes)
(then best-color is red))
```

和：

```
(rule (if meal-is-turkey is no)
(then best-color is white))
```

以指示这两个规则的第一个条件已满足。

随着后向链式推理的进行，将生成子目标以确定属性的值。需要一个事实来表示关于目标属性的信息。将使用有序事实来表示目标属性，其格式如下：

```
(deftemplate BC::goal
(slot attribute))
```

最初，目标属性是 best-color。可以使用如下所示的 deffacts 来表示：

```
(deffacts MAIN::initial-goal
(goal (attribute best-color)))
```

当确定属性值时，需要将其存储，可以使用以下 deftemplate 完成：

```
(deftemplate BC::attribute
  (slot name)
  (slot value))
```

现在所有 deftemplate 都已确定，我们可以提供 BC 模块的定义。请记住，在加载构造文件时，包含其他构造的 defmodule 必须在其包含的构造定义之前定义：

```
(defmodule BC
  (export deftemplate rule goal attribute))
```

## CLIPS 后向链式推理引擎

后向链式推理引擎可以用两组规则实现。第一组将为属性生成目标，并在无法通过规则确定这些值时要求用户提供属性值。第二组规则将执行更新操作。更新操作包括在条件满足时修改规则以及在目标满足时删除目标。第一组规则如下：

```
(defrule BC::attempt-rule
  (goal attribute ?g-name)
  (rule (if ?a-name $?)
  (then ?g-name $?))
  (not (attribute (name ?a-name)))
  (not (goal (attribute ?a-name)))
  =>
  (assert (goal (attribute ?a-name))))
```

```
(defrule BC::ask-attribute-value
  ?goal <- (goal (attribute ?g-name))
  (not (attribute (name ?g-name)))
  (not (rule (then ?g-name $?)))
  =>
  (retract ?goal)
  (printout t "What is the value of "
  ?g-name "? ")
  (assert (attribute (name ?g-name)
  (value (read)))))
```

attempt-rule 规则搜索其前件将为目标属性提供属性值的规则。第一个模式与目标事实匹配。第二个模式搜索所有向目标属性分配值的前件的规则。第三个模式检查目标属性的值是否尚未确定。第四个模式确认不存在确定属性值的现有目标。对于找到的每个规则，attempt-rule 规则的 RHS 将断言一个目标，以确定规则第一个条件所测试属性的值。

ask-attribute-value 规则与 attempt-rule 规则非常相似。其前两个模式相同。其第三个模式检查是否没有剩余规则可用于确定目标属性的值。在这种情况下，将要求用户提供属性的值。将断言表示属性值的事实，并撤销该属性的目标事实。

接下来的四条规则用于更新表示为事实的后向链式规则和目标。这些规则被赋予 salience 100，以便在尝试生成新目标或询问用户属性值之前发生更新：

```
(defrule BC::goal-satisfied
(declare (salience 100))
?goal <- (goal attribute ?g-name)
(attribute (name ?g-name))
=>
(retract ?goal))
```

```
(defrule BC::rule-satisfied
(declare (salience 100))
(goal (attribute ?g-name))
(attribute (name ?a-name)
(value ?a-value))
?rule <- (rule (if ?a-name is ?a-value)
(then ?g-name is ?g-value))
=>
(retract ?rule)
(assert (attribute (name ?g-name)
(value ?g-value))))
```

```
(defrule BC::remove-rule-no-match
(declare (salience 100))
(goal (attribute ?g-name))
(attribute (name ?a-name) (value ?a-value))
?rule <- (rule (if ?a-name is -?a-value)
(then ?g-name is ?g-value))
=>
(retract ?rule))
```

```
(defrule BC::modify-rule-match
(declare (salience 100))
(goal (attribute ?g-name))
(attribute (name ?a-name) (value ?a-value))
?rule <- (rule (if ?a-name is ?a-value and
?rest-if)
(then ?g-name is ?g-value))
```

