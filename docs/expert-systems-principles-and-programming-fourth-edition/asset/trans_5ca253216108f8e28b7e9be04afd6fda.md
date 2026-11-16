
=>
(retract ?rule)
(modify ?rule (if $?reset-if))

目标满足规则会移除任何属性值已被确定的规则。

规则满足规则会搜索任何只剩一个条件的规则。如果存在满足该剩余条件的属性，并且存在确定该属性值的目标，则该规则后件的属性值会被添加到事实列表中。

移除不匹配规则会搜索那些前件可以为目标属性提供属性值，并且包含一个或多个条件（其中第一个条件与分配给某个属性的值冲突）的规则。如果是这种情况，则该规则会从事实列表中移除，因为它不再适用。

修改规则匹配规则会搜索那些前件可以为目标属性提供属性值，并且包含两个或多个条件（其中第一个条件已被分配给某个属性的值满足）的规则。如果找到这样的规则，则从规则中移除第一个条件，只留下剩余条件，这些剩余条件必须进行测试。

既然所有后向链式规则都已提供，启动后向链式进程所需的就是聚焦于 BC 模块。这可以通过将以下规则添加到 MAIN 模块来实现：

```
(defrule MAIN ::start-BC
=>
(focus BC))
```

## 后向链式器逐步跟踪

可以通过观察其执行过程来了解使用规则实现的 CLIPS 后向链式推理引擎的行为。假设 wine-rules 和 initial-goal 默认值已与后向链式推理引擎规则一起加载，则 reset 命令后系统的初始状态如下（同样，部分输出已缩进以提高可读性）：

```
CLIPS> (unload all)
CLIPS> (reset)
CLIPS> (facts:)
f-0	(initial-fact)
f-1	(goal (attribute best-color))
f-2	(rule (if main-course is red-meat)
        (then best-color is red))
f-3	(rule (if main-course is fish)
        (then best-color is white))
f-4	(rule (if main-course is poultry and
        meal-is-turkey is yes)
        (then best-color is red))
f-5   (rule (if main-course is poultry and
        meal-is-turkey is no)
        (then best-color is white))
For a total of 6 facts.
CLIPS> (agenda)
0   start-BC: f-0
For a total of 1 activation.
CLIPS>
```

start-BC 规则仅聚焦于 BC 模块。一旦该规则触发，BC 模块即成为当前焦点：

```
CLIPS> (run 1)
CLIPS> (agenda)
0   attempt-rule: f-1,f-5,,
0   attempt-rule: f-1,f-4,,
0   attempt-rule: f-1,f-3,,
0   attempt-rule: f-1,f-2,,
For a total of 4 activations.
CLIPS>
```

请注意，议程中包含 attempt-rule 规则的四个激活。初始目标是确定事实 f-1 所指定的 best-color 属性的值。由于规则事实 f-2、f-3、f-4 和 f-5 的后件都会为 best-color 属性赋值，因此应尝试每个规则以满足 best-color 属性目标。

执行的下一步是触发 attempt-rule 规则的第一个激活。在规则触发之前，规则和事实监视项已被激活：

```
CLIPS> (watch rules)
CLIPS> (watch facts)
CLIPS> (run 1)
FIRE 1 attempt-rule: f-1,f-5,,
==> f-6 (goal (attribute main-course))
CLIPS> (agenda)
0   ask-attribute-value: f-6,,
For a total of 1 activation.
CLIPS>
```

attempt-rule 规则部分基于事实 f-5 触发，该事实表示此处所示的后向链式规则：

```
IF main-course is poultry and
meal-is-turkey is no
THEN best-color is white
```

在此规则可应用于为 best-color 属性赋值之前，其前件中的 CEs 必须得到满足。第一个条件需要 main-course 属性的值。由于该属性未知，因此为其创建了一个目标，并由事实 f-6 表示。由于没有规则为 main-course 属性赋值，因此 ask-attribute-value 规则被激活。

继续执行，ask-attribute-value 规则触发以确定 main-course 属性的值：

```
CLIPS> (run 1)
FIRE    1 ask-attribute-value: f-6,,
    <<= f-6    (goal (attribute main-course))
    What is the value of main-course? poultry.
    ==> f-7    (attribute (name main-course)
                (value poultry))
CLIPS> (agenda)
100    remove-rule-no-match: f-1, f-7, f-3
100    remove-rule-no-match: f-1, f-7, f-2
100    modify-rule-match: f-1, f-7, f-5
100    modify-rule-match: f-1, f-7, f-4
For a total of 4 activations.
CLIPS>
```

由于正在要求用户提供 main-course 属性的值，因此该属性的目标 f-6 被移除。用户提供的值被断言为属性事实 f-7。此事实的断言导致四个新激活被放置到议程中。由事实 f-4 和 f-5 表示的规则都要求第一个条件是 main-course 属性为 poultry。由于 main-course 属性的值为 poultry，因此这两个规则事实都必须修改以表示第一个条件已满足。因此，这两个事实都会导致 modify-rule-match 规则的激活。由事实 f-2 和 f-3 表示的规则都要求第一个条件是 main-course 属性不是 poultry。因此，这两个事实都不再适用。remove-rule-no-match 规则被激活以将它们移除。

允许两个 remove-rule-no-match 激活触发会产生以下输出：

```
CLIPS> (run 2)
FIRE    1 remove-rule-no-match: f-1, f-7, f-3
    == f-3    (rule (if main-course is fish)
                (then best-color is white))
FIRE    2 remove-rule-no-match: f-1, f-7, f-2
    == f-2    (rule (if main-course is red-meat)
                (then best-color is red))
CLIPS> (agenda)
100    modify-rule-match: f-1, f-7, f-5
100    modify-rule-match: f-1, f-7, f-4
For a total of 2 activations.
CLIPS>
```

事实 f-2 和 f-3 从事实列表中移除，表示这些事实所代表的规则不再适用。当事实被移除时，这些事实的 attempt-rule 激活也会从议程中移除。

现在转到执行两个 modify-rule-match 激活，会产生以下输出：

```
CLIPS> (run 2)
FIRE    1 modify-rule-match: f-1,f-7,f-5
<=  f-5     (rule (if main-course is poultry and
                meal-is-turkey is no)
            (then best-color is white))
==> f-8     (rule (if meal-is-turkey is no)
            (then best-color is white))
FIRE    2 modify-rule-match: f-7,f-4
<=  f-4     (rule (if main-course is poultry and
                meal-is-turkey is yes)
            (then best-color is red))
==> f-9     (rule (if meal-is-turkey is yes)
            (then best-color is red))
CLIPS> (agenda)
0      attempt-rule: f-1,f-9,,
0      attempt-rule: f-1,f-8,,
For a total of 2 activations.
CLIPS>
```

modify-rule-match 规则的第一次触发部分基于事实 f-5，该事实表示以下后向链式规则：

```
IF main-course is poultry and
meal-is-turkey is no
THEN best-color is white
```

modify-rule-match 规则的操作将此后向链式规则修改为：

```
IF meal-is-turkey is no
THEN best-color is white
```

表示修改后规则的新事实是 f-8。这个新事实表示初始规则在第一个条件满足后剩余的条件，并为此后向链式规则引发另一个 attempt-rule 规则的激活。这个新激活将断言一个新目标以确定 meal-is-turkey 的值，以便规则的后件可以应用来为 best-color 属性赋值。

modify-rule-match 规则的第二次触发与第一次类似。表示该规则的事实：

```
IF main-course is poultry and
meal-is-turkey is yes
THEN best-color is red
```

被修改为以下规则：

```
IF meal-is-turkey is yes
THEN best-color is red
```

该事实由 f-9 表示。同样，这个新事实会引发 attempt-rule 规则的激活，以替换当表示规则的事实被撤回时丢失的激活。

允许第一个 attempt-rule 激活触发会产生以下输出：

```
CLIPS> (run 1)
FIRE 1 attempt-rule: f-1,f-9,
==> f-10 (goal (attribute meal-is-turkey))
CLIPS> (agenda)
0 ask-attribute-value: f-10,
For a total of 1 activation.
CLIPS>
```

事实 f-10 被断言，表示确定 meal-is-turkey 属性值的目标。由于没有规则为该属性赋值，因此 ask-attribute-value 规则被激活以确定该值。

允许 ask-attribute-value 规则触发会产生以下输出：

```
CLIPS> (run 1)
FIRE 1 ask-attribute-value: f-10,
<<= f-10 (goal (attribute meal-is-turkey))
What is the value of meal-is-turkey? yes
==> f-11 (attribute (name meal-is-turkey)
                (value yes))
CLIPS> (agenda)
100 rule-satisfied: f-1,f-11,f-9
100 remove-rule-no-match: f-1,f-11,f-8
For a total of 2 activations.
CLIPS>
```

作为该规则触发的结果，表示 meal-is-turkey 属性值的属性事实被断言。此外，确定该属性值的目标事实被移除。这个新属性事实导致两个激活。第一个激活是针对 remove-rule-no-match 规则。由于事实 f-8 的第一个条件与新属性的值不一致，并且该事实所代表的规则不再适用，因此需要移除该事实。第二个激活是针对 rule-satisfied 规则。由于事实 f-9 的剩余条件由新属性事实满足，因此可以应用该事实的后件。
