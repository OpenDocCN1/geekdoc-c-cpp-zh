

![](img/e22931b583977bc24a4263ee43d0f0bb_735_0.png)

两次。第二个子目标第一次失败，这会强制通过重做返回到第一个子目标。

### 16.6.7 列表结构

到目前为止，我们讨论过的唯一 Prolog 数据结构是原子命题，它看起来更像函数调用而不是数据结构。原子命题也称为结构，实际上是一种记录。支持的另一种基本数据结构是列表。列表是任意数量元素的序列，其中元素可以是原子、原子命题或任何其他项，包括其他列表。

Prolog 使用 ML 和 Haskell 的语法来指定列表。列表元素用逗号分隔，整个列表用方括号括起来，如下所示：

```
[apple, prune, grape, kumquat]
```

记号 `[]` 用于表示空列表。Prolog 不使用显式函数来构造和拆解列表，而只是使用一种特殊记号。[X | Y] 表示一个头为 X、尾为 Y 的列表，其中头和尾分别对应 LISP 中的 CAR 和 CDR。这类似于 ML 和 Haskell 中使用的记号。

可以用一个简单结构创建列表，如下所示：

```
new_list([apple, prune, grape, kumquat]).
```

该语句声明常量列表 [apple, prune, grape, kumquat] 是名为 new_list 的关系的一个新元素（这个名字是我们刚刚编造的）。这条语句并没有把列表绑定到名为 new_list 的变量；相反，它做的是命题 `male(jake)` 所做的那类事情。也就是说，它声明 [apple, prune, grape, kumquat] 是 new_list 的一个新元素。因此，我们可以有第二个带列表参数的命题，例如

```
new_list([apricot, peach, pear])
```

在查询模式下，可以用以下语句将 new_list 的某个元素拆解为头和尾：

```
new_list([New_List_Head | New_List_Tail]).
```

如果 new_list 已被设置为具有所示的两个元素，那么这条语句会用第一个列表元素的头（在本例中是 apple）实例化 New_List_Head，并用该列表的尾（即 [prune, grape, kumquat]）实例化 New_List_Tail。如果这是某个复合目标的一部分，并且回溯迫使对它进行新的求值，那么 New_List_Head 和 New_List_Tail 将分别被重新实例化为 apricot 和 [peach, pear]，因为 [apricot, peach, pear] 是 new_list 的下一个元素。

用于拆解列表的 | 运算符也可以根据给定的已实例化头和尾组件来创建列表，如下所示：

```
[Element_1 | List_2]
```

如果 Element_1 已用 pickle 实例化，List_2 已用 [peanut, prune, popcorn] 实例化，那么对于这一次引用，示例记号将创建列表 [pickle, peanut, prune, popcorn]。

如前所述，包含 | 符号的列表记号是通用的：它既可以指定列表构造，也可以指定列表拆解。进一步注意，以下写法是等价的：

```
[apricot, peach, pear | []]
[apricot, peach | [pear]]
[apricot | [peach, pear]]
```

对于列表，经常需要某些基本操作，例如 LISP、ML 和 Haskell 中的那些操作。作为 Prolog 中此类操作的一个例子，我们考察 append 的定义，它与 LISP 中的此类函数相关。在这个例子中，可以看到函数式语言和声明式语言之间的差异与相似之处。我们不需要指定 Prolog 如何从给定列表构造新列表；相反，我们只需要根据给定列表指定新列表的特征。

从表面上看，append 的 Prolog 定义与第 15 章中出现的 ML 版本非常相似，并且以类似方式使用归结中的一种递归来生成新列表。在 Prolog 的情况下，递归由归结过程引起并受其控制。与 ML 和 Haskell 一样，使用模式匹配过程，根据实际参数在 append 过程的两个不同定义之间进行选择。

以下代码中 append 操作的前两个参数是要追加的两个列表，第三个参数是结果列表。

```prolog
append([], List, List).
append([Head | List_1], List_2, [Head | List_3]) :-
    append(List_1, List_2, List_3).
```

第一个命题规定，当空列表追加到任何其他列表时，该其他列表就是结果。这条语句对应于 ML 的 append 函数中的递归终止步骤。注意，终止命题放在递归命题之前。这样做是因为我们知道 Prolog 将按顺序匹配这两个命题，从第一个开始（因为它使用深度优先顺序）。

第二个命题规定了新列表的几个特征。它对应于 ML 函数中的递归步骤。左侧谓词指出，新列表的第一个元素与第一个给定列表的第一个元素相同，因为它们都命名为 Head。每当 Head 被实例化为某个值时，目标中所有出现的 Head 实际上都会同时被实例化为该值。第二条语句的右侧规定，第一个给定列表（List_1）的尾部追加了第二个给定列表（List_2），以形成结果列表的尾部（List_3）。

理解 append 第二条语句的一种方式如下：将列表 [Head | List_1] 追加到任意列表 List_2 会产生列表 [Head | List_3]，但仅当列表 List_3 是通过将 List_1 追加到 List_2 而形成时。在 LISP 中，这将是

```lisp
(CONS (CAR FIRST) (APPEND (CDR FIRST) SECOND))
```

在 Prolog 和 LISP 两个版本中，直到递归产生终止条件时才构造结果列表；在这种情况下，第一个列表必须变为空。然后，使用 append 函数本身构建结果列表；从第一个列表取出的元素按相反顺序添加到第二个列表。这种反转是通过递归的展开完成的。

Prolog 的 append 与 LISP 和 ML 的 append 之间的一个根本区别是，Prolog 的 append 是一个谓词——它不返回列表，而是返回 yes 或 no。新列表是其第三个参数的值。

为了说明 append 过程如何推进，考虑以下跟踪示例：

```prolog
trace.
append([bob, jo], [jake, darcie], Family).

(1) 1 Call: append([bob, jo], [jake, darcie], _10)?
(2) 2 Call: append([jo], [jake, darcie], _18) ?
(3) 3 Call: append([], [jake, darcie], _25) ?
(3) 3 Exit: append([], [jake, darcie], [jake, darcie])
(2) 2 Exit: append([jo], [jake, darcie], [jo, jake,
    darcie])
(1) 1 Exit: append([bob, jo], [jake, darcie],
    [bob, jo, jake, darcie])
Family = [bob, jo, jake, darcie]
yes
```

前两个调用表示子目标，它们的 List_1 非空，因此它们从第二条语句的右侧创建递归调用。第二条语句的左侧实际上指定了递归调用（或目标）的参数，从而每一步拆解第一个列表的一个元素。当第一个列表在某个调用或子目标中变为空时，第二条语句右侧的当前实例通过匹配第一条语句而成功。其效果是，将空列表追加到第二个原始参数列表后得到的值作为第三个参数返回。在相继的退出（表示成功匹配）中，从第一个列表移除的元素被追加到结果列表 Family 中。当第一个目标的退出完成时，过程就完成了，并显示结果列表。

Prolog 的 append 与 LISP 和 ML 的 append 之间的另一个区别是，Prolog 的 append 比那些语言中的 append 更灵活。例如，在 Prolog 中，我们可以用以下语句使用 append 来确定哪两个列表可以追加得到 [a, b, c]：

```
append(X, Y, [a, b, c]).
```

这会产生以下结果：

```
X = []
Y = [a, b, c]
```

如果在这个输出处输入分号，我们会得到另一个结果：

```
X = [a]
Y = [b, c]
```

继续，我们得到以下结果：

```
X = [a, b]
Y = [c];
X = [a, b, c]
Y = []
```

