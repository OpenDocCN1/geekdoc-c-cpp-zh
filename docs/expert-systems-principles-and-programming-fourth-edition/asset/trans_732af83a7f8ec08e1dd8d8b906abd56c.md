

- 12.9 添加规则，在警告阶段打印一条消息，以指示传感器已保持正常状态至少 n 个周期，其中数字 n 在一个事实中指定。仅每 n 个周期打印一次该消息。

- 12.10 第 12.4 节中的后向链规则如何修改以允许前向链？

- 12.11 修改第 702 页问题 11.1 中开发的程序，使表示灌木的事实通过 load-facts 函数从文件加载。提供解释后，应询问用户是否需要另一次灌木选择，如果是，则应再次运行程序。

- 12.12 使用问题 11.3 中开发的程序，修改第 620 页问题 10.10 中开发的程序，使得“添加小装置”子菜单中仅列出未选中的小装置，“移除小装置”子菜单中仅列出已选中的小装置。在主菜单中，“添加小装置”菜单选项仅在存在未选中的小装置时出现，“移除小装置”菜单选项仅在存在已选中的小装置时出现。

- 12.13 使用第 702 页问题 11.3 中开发的程序，修改第 618 页问题 10.4 中开发的程序，以使用菜单驱动界面。应为用户提供单独的菜单选项，用于指定正在识别的宝石的颜色、硬度和密度。颜色的指定应使用包含有效颜色的子菜单来完成。应提供一个菜单选项，列出满足当前指定标准的宝石。例如，如果用户仅指定宝石为黑色，则选择此菜单选项将仅列出可能为黑色的宝石。还应提供另外两个菜单选项，一个列出为标准指定的当前值，另一个将所有标准重置为未指定状态。

## BIBLIOGRAPHY
## 参考文献

(Firebaugh 88). Morris W. Firebaugh, 《人工智能：一种基于知识的方法》, Boyd & Fraser 出版社, 第 309 页, 1988.

## APPENDIX A
## 附录 A
Some Useful Equivalences
一些有用的等价式

p ≡ p
p → q ≡ ¬p ∨ q ≡ ¬q → ¬p
¬(p ∧ q) ≡ ¬p ∨ ¬q
¬(p ∨ q) ≡ ¬p ∧ ¬q
p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)
p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)
(p ∧ q) ∧ r ≡ p ∧ (q ∧ r)
(p ∨ q) ∨ r ≡ p ∨ (q ∨ r)
p ∧ q ≡ q ∧ p
p ∨ q ≡ q ∨ p

¬(∀x) P(x) ≡ (∃x) ¬P(x)
¬(∃x) P(x) ≡ (∀x) ¬P(x)
(∀x) P(x) ∧ (∀x) Q(x) ≡ (∀x) (P(x) ∧ Q(x))
(∃x) P(x) ∨ (∃x) Q(x) ≡ (∃x) (P(x) ∨ Q(x))

Note: The ∀ does not distribute over an ∨, and ∃ does not distribute over ∧, so a new dummy variable, z, is needed in the following two equivalences.
注意：∀ 不分配于 ∨，且 ∃ 不分配于 ∧，因此在以下两个等价式中需要一个新的哑变量 z。

(∀x) P(x) ∨ (∀x) Q(x) ≡ (∀x) P(x) ∨ (∀z) Q(z)
≡ (∀x) (∀z) (P(x) ∨ Q(z))
(∃x) P(x) ∧ (∃x) Q(x) ≡ (∃x) P(x) ∧ (∃z) Q(z)
≡ (∃x) (∃z) (P(x) ∧ Q(z))

## APPENDIX B
## 附录 B
Some Elementary Quantifiers and Their Meanings
一些基本量词及其含义

| Formula | Meaning |
| :--- | :--- |
| (∀ x) (P(x) → Q(x)) | 对所有 x，所有 P 都是 Q |
| (∀ x) (P(x) → ¬Q(x)) | 对所有 x，没有 P 是 Q |
| (∃ x) (P(x) ∧ Q(x)) | 对某些 x，x 是 P 和 Q |
| (∃ x) (P(x) ∧ ¬Q(x)) | 对某些 x，x 是 P 且不是 Q |
| (∀ x) P(x) | 对所有 x，x 是 P |
| (∃ x) P(x) | 某些 x 是 P（或存在 P） |
| ¬(∀ x) P(x) | 不是所有 x 都是 P（或某些 x 是 P） |
| (∀ x) ¬P(x) | 所有 x 都不是 P |
| (∀ x) (∃ y) P(x,y) | 对所有 x，存在一个 y 使得 P |
| (∃ x) ¬P(x) | 某些 x 不是 P |

## APPENDIX C
## 附录 C
Some Set Properties
一些集合属性

| Property | Formula |
| :--- | :--- |
| 交换律 | \( A \cup B = B \cup A \)<br>\( A \cap B = B \cap A \) |
| 结合律 | \( A \cup (B \cup C) = (A \cup B) \cup C \)<br>\( A \cap (B \cap C) = (A \cap B) \cap C \) |
| 幂等律 | \( A \cup A = A \)<br>\( A \cap A = A \) |
| 分配律 | \( A \cup (B \cap C) = (A \cup B) \cap (A \cup C) \)<br>\( A \cap (B \cup C) = (A \cap B) \cup (A \cap C) \) |
| 排中律 | \( A \cup A' = U \) |
| 矛盾律 | \( A \cap A' = \emptyset \) |
| 恒等律 | \( A \cup \emptyset = A \)<br>\( A \cap U = A \) |
| 吸收律 | \( A \cup (A \cap B) = A \)<br>\( A \cap (A \cup B) = A \) |
| 摩根定律 | \( (A \cap B)' = A' \cup B' \)<br>\( (A \cup B)' = A' \cap B' \) |
| 对合律 | \( (A')' = A \) |
| 等价式 | \( (A' \cup B) \cap (A \cup B') = (A' \cap B') \cup (A \cap B) \) |
| 对称差 | \( (A' \cap B) \cup (A \cap B') = (A' \cup B') \cap (A \cup B) \) |

## APPENDIX D CLIPS Support Information
## 附录 D CLIPS 支持信息

The CD-ROM included with this book contains CLIPS 6.22 executables for MS-DOS, Windows 2000/XP, and MacOS X. Also included on the CD-ROM are all of the CLIPS source code, the three-volume CLIPS Reference Manual, and the CLIPS User's Guide. Volume I of the CLIPS Reference Manual, The Basic Programming Guide, provides the definitive description of CLIPS syntax and examples of usage. Volume II, The Advanced Programming Guide, provides details on customizing CLIPS, adding new functions to CLIPS, embedding CLIPS, and other advanced features. Volume III, The Interfaces Guide, provides information on the environment-specific interfaces for CLIPS. An X Windows version of CLIPS can be created by compiling the X Windows interface and CLIPS source code found on the CD-ROM.

本书随附的 CD-ROM 包含适用于 MS-DOS、Windows 2000/XP 和 MacOS X 的 CLIPS 6.22 可执行文件。CD-ROM 中还包含所有 CLIPS 源代码、三卷本 CLIPS 参考手册以及 CLIPS 用户指南。CLIPS 参考手册第 I 卷《基本编程指南》提供了 CLIPS 语法的权威描述和使用示例。第 II 卷《高级编程指南》提供了有关自定义 CLIPS、向 CLIPS 添加新函数、嵌入 CLIPS 以及其他高级功能的详细信息。第 III 卷《接口指南》提供了 CLIPS 的环境特定接口信息。可以通过编译 CD-ROM 上的 X Windows 接口和 CLIPS 源代码来创建 CLIPS 的 X Windows 版本。

Bug fixes, updates, and other information related to CLIPS can be found at the CLIPS home page at http://www.ghg.net/clips/CLIPS.html. Questions regarding CLIPS can be sent via electronic mail to clipsYYYY@ghg.net where YYYY is the current year (for example, 2004). Usenet users can find information and post questions about CLIPS at the comp.ai.shells news group.

与 CLIPS 相关的错误修正、更新和其他信息可在 CLIPS 主页 http://www.ghg.net/clips/CLIPS.html 上找到。有关 CLIPS 的问题可以通过电子邮件发送到 clipsYYYY@ghg.net，其中 YYYY 是当前年份（例如，2004）。Usenet 用户可以在 comp.ai.shells 新闻组中查找信息并发布关于 CLIPS 的问题。

The CLIPS Developers' Forum, located at http://www.cpbinc.com/clips, is a thread-based message board that provides a site for discussion of research, development, and implementation of the CLIPS Expert System and related technologies.

CLIPS 开发者论坛位于 http://www.cpbinc.com/clips，是一个基于主题的留言板，为讨论 CLIPS 专家系统及相关技术的研究、开发和实现提供了一个平台。

An electronic conferencing facility is also available to CLIPS users. Subscribers to this facility may send questions, observations, answers, editorials, and so forth in the form of electronic mail to the conference. All subscribers will have a copy of these messages reflected back to them at their respective email addresses. To subscribe, send a single line message to clips-request@discmsys.com containing the word "subscribe". The subject field is ignored but the address found in the "Reply:", "Reply to:", or "From:" field will be entered in the distribution list. Upon subscription you will receive a mail message instructing you how to participate in the conference from that point forward.

CLIPS 用户还可以使用电子会议设施。该设施的订阅者可以以电子邮件形式向会议发送问题、观察、答案、社论等等。所有订阅者都会收到这些消息的副本，反馈到其各自的电子邮件地址。要订阅，请向 clips-request@discmsys.com 发送一条包含单词 "subscribe" 的单行消息。主题字段将被忽略，但 "Reply:"、"Reply to:" 或 "From:" 字段中找到的地址将被加入分发列表。订阅后，您将收到一封邮件，指导您如何从此点开始参与会议。

## APPENDIX E CLIPS Commands and Functions Summary
## 附录 E CLIPS 命令和函数摘要

### Agenda
### 议程

- `(agenda [<module-name>])`
  Lists the activations on the agenda of the specified module (or in the current module if `<module-name>` is unspecified).

- `(agenda [<module-name>])`
  列出指定模块（或如果未指定 `<module-name>`，则为当前模块）议程上的激活项。

- `(clear-focus-stack)`
  Returns all the module names from the focus stack.

- `(clear-focus-stack)`
  返回焦点栈中的所有模块名称。

- `(focus <module-name>+)`
  Pushes one or more modules onto the focus stack. The specified modules are pushed onto the focus stack in the reverse order from the argument list.

- `(focus <module-name>+)`
  将一个或多个模块压入焦点栈。指定的模块按参数列表的逆序压入焦点栈。

- `(get-focus)`
  Returns the module name of the current focus.

- `(get-focus)`
  返回当前焦点的模块名称。

- `(get-focus-stack)`
  Returns all the module names in the focus stack as a multifield value.

- `(get-focus-stack)`
  以多字段值的形式返回焦点栈中的所有模块名称。

- `(get-salience-evaluation)`
  Returns the current salience evaluation behavior.

- `(get-salience-evaluation)`
  返回当前的显著性评估行为。

- `(get-strategy)`
  Returns the current conflict resolution strategy.

- `(get-strategy)`
  返回当前的冲突解决策略。

- `(halt)`
  Stops the execution of rules.

- `(halt)`
  停止规则的执行。

- `(list-focus-stack)`
  Lists all the module names on the focus stack.

- `(list-focus-stack)`
  列出焦点栈上的所有模块名称。

- `(pop-focus)`
  Returns the module name of the current focus and removes the current focus from the focus stack.

- `(pop-focus)`
  返回当前焦点的模块名称，并从焦点栈中移除当前焦点。

- `(refresh-agenda [<module-name>])`
  Forces reevaluation of the salience of rules on the agenda of the specified module (or in the current module if `<module-name>` is unspecified).

- `(refresh-agenda [<module-name>])`
  强制重新评估指定模块（或如果未指定 `<module-name>`，则为当前模块）议程上规则的显著性。

```
(run [<integer-expression>])
```

Starts the execution of rules in the current focus. If <integer-expression> is specified then only that number of rules is executed, otherwise execution halts when the agenda is empty.

```
(run [<integer-expression>])
```

启动当前焦点中规则的执行。如果指定了 <integer-expression>，则仅执行该数量的规则，否则执行将在议程为空时停止。

```
(set-salience-evaluation <behavior>)
<behavior> ::= when-defined | when-activated |
every-cycle
```

Sets the salience evaluation behavior.

```
(set-salience-evaluation <behavior>)
<behavior> ::= when-defined | when-activated |
every-cycle
```

设置显著性评估行为。

```
(set-strategy <strategy>)
<strategy> ::= depth | breadth | simplicity |
complexity | lex | mea | random
```

Sets the current conflict resolution strategy.

```
(set-strategy <strategy>)
<strategy> ::= depth | breadth | simplicity |
complexity | lex | mea | random
```

设置当前的冲突解决策略。

### Basic Math
### 基本数学

```
(abs <numeric-expression>)
```

Returns the absolute value of its only argument.

```
(abs <numeric-expression>)
```

返回其唯一参数的绝对值。

```
(div <numeric-expression> <numeric-expression>+)
```

Returns the value of the first argument divided by each of the subsequent arguments. Division is performed using integer arithmetic.

```
(div <numeric-expression> <numeric-expression>+)
```

返回第一个参数除以后续每个参数的值。除法使用整数运算执行。

```
(float <numeric-expression>)
```

Returns its only argument converted to type float.

```
(float <numeric-expression>)
```

将其唯一参数转换为 float 类型后返回。

```
(integer <numeric-expression>)
```

Returns its only argument converted to type integer.

```
(integer <numeric-expression>)
```

将其唯一参数转换为 integer 类型后返回。

```
(max <numeric-expression> <numeric-expression>+)
```

Returns the value of its largest argument.

```
(max <numeric-expression> <numeric-expression>+)
```

返回其最大参数的值。

```
(min <numeric-expression> <numeric-expression>+)
```

Returns the value of its smallest argument.

```
(min <numeric-expression> <numeric-expression>+)
```

返回其最小参数的值。

```
(+ <numeric-expression> <numeric-expression>+)
```

Returns the sum of its arguments.

```
(+ <numeric-expression> <numeric-expression>+)
```

返回其参数之和。

```
(- <numeric-expression> <numeric-expression>+)
```

Returns the value of the first argument minus the sum of all subsequent arguments.

```
(- <numeric-expression> <numeric-expression>+)
```

返回第一个参数减去所有后续参数之和的值。

```
(* <numeric-expression> <numeric-expression>+)
```

Returns the product of its arguments.

```
(* <numeric-expression> <numeric-expression>+)
```

返回其参数的乘积。

```
(/ <numeric-expression> <numeric-expression>+)
```

Returns the value of the first argument divided by each of the subsequent arguments.

```
(/ <numeric-expression> <numeric-expression>+)
```

返回第一个参数除以后续每个参数的值。

### Conversion
### 转换

```
(deg-grad <numeric-expression>)
```

Returns the value of its argument converted from units of degrees to units of gradients.

```
(deg-grad <numeric-expression>)
```

将其参数从度单位转换为梯度单位后返回其值。

```
(deg-rad <numeric-expression>)
```

Returns the value of its argument converted from units of degrees to units of radians.

```
(deg-rad <numeric-expression>)
```

将其参数从度单位转换为弧度单位后返回其值。

```
(exp <numeric-expression>)
```

Returns the value of e raised to the power of its only argument.

```
(exp <numeric-expression>)
```

返回 e 的其唯一参数次幂的值。

```
(grad-deg <numeric-expression>)
```

Returns the value of its argument converted from units of gradients to units of degrees.

```
(grad-deg <numeric-expression>)
```

将其参数从梯度单位转换为度单位后返回其值。

