
```
(2) 2 Exit: speed(chevy, 105)
(3) 2 Call: time(chevy, _6)?
(3) 2 Exit: time(chevy, 21)
(4) 2 Call: _0 is 105*21?
(4) 2 Exit: 2205 is 105*21
(1) 1 Exit: distance(chevy, 2205)

Chevy_Distance = 2205
```

跟踪中以**下划线**字符（`_`）开头的符号是用于存储实例化值的内部变量。跟踪的第一列表示当前正在尝试匹配的子目标。例如，在上述跟踪中，标记为（3）的第一行是尝试用 chevy 的时间值来实例化临时变量 `_6`，其中 `time` 是描述距离计算语句右侧的第二个项。第二列表示匹配过程的调用深度。第三列表示当前操作。

为了说明回溯过程，请考虑以下示例数据库和带跟踪的复合目标：

```
likes(jake, chocolate).
likes(jake, apricots).
likes(darcie, licorice).
likes(darcie, apricots).

trace.
likes(jake, X), likes(darcie, X).
```

```
(1) 1 Call: likes(jake, _0)?
(1) 1 Exit: likes(jake, chocolate)
(2) 1 Call: likes(darcie, chocolate)?
(2) 1 Fail: likes(darcie, chocolate)
(1) 1 Redo: likes(jake, _0)?
(1) 1 Exit: likes(jake, apricots)
(3) 1 Call: likes(darcie, apricots)?
(3) 1 Exit: likes(darcie, apricots)

X = apricots
```

我们可以用图形方式来理解 Prolog 的计算过程：将每个目标视为一个带有四个端口——call（调用）、fail（失败）、exit（退出）和 redo（重做）——的盒子。控制流通过 call 端口沿正向进入目标。控制流也可以通过 redo 端口沿反向进入目标。控制流离开目标的方式有两种：如果目标成功，则控制流通过 exit 端口离开；如果目标失败，则控制流通过 fail 端口离开。图 16.1 显示了该示例的模型。在此示例中，控制流两次经过每个子目标。

## 图 16.1

目标 `likes(jake, X), likes(darcie, X)` 的控制流模型

![](img/e382387aad0004c80a0dd0a70be9a623_731_0.png)

第二个子目标第一次失败，这迫使控制流通过 redo 返回到第一个子目标。

## 16.6.7 列表结构

到目前为止，我们讨论的唯一 Prolog 数据结构是原子命题（atomic proposition），它看起来更像函数调用而非数据结构。原子命题也称为结构（structure），实际上是一种记录形式。支持的另一种基本数据结构是列表。列表是任意数量元素的序列，元素可以是原子、原子命题或任何其他项，包括其他列表。

Prolog 使用 ML 和 Haskell 的语法来指定列表。列表元素用逗号分隔，整个列表用方括号界定，例如：

```
[apple, prune, grape, kumquat]
```

记号 `[]` 用于表示空列表。Prolog 没有显式的列表构造和拆分函数，而是使用一种特殊记号。`[X | Y]` 表示以 X 为表头、Y 为表尾的列表，其中表头和表尾分别对应于 LISP 中的 CAR 和 CDR。这与 ML 和 Haskell 中使用的记号类似。

可以通过简单结构来创建列表，例如：

```
new_list([apple, prune, grape, kumquat]).
```

该语句声明常量列表 `[apple, prune, grape, kumquat]` 是名为 `new_list`（我们刚虚构的一个名字）的关系的新元素。这条语句并不将列表绑定到名为 `new_list` 的变量；它所做的类似于命题

```
male(jake)
```

所做之事。也就是说，它声明 `[apple, prune, grape, kumquat]` 是 `new_list` 的一个新元素。因此，我们可以有另一个带列表参数的命题，例如：

```
new_list([apricot, peach, pear])
```

在查询模式下，可以通过以下方式将 `new_list` 的一个元素拆分为表头和表尾：

```
new_list([New_List_Head | New_List_Tail]).
```

如果 `new_list` 已设置为包含上述两个元素，则该语句会用第一个列表元素的表头（此处为 `apple`）实例化 `New_List_Head`，并用列表的表尾（即 `[prune, grape, kumquat]`）实例化 `New_List_Tail`。如果这是复合目标的一部分，并且回溯迫使它重新求值，那么 `New_List_Head` 和 `New_List_Tail` 将分别被重新实例化为 `apricot` 和 `[peach, pear]`，因为 `[apricot, peach, pear]` 是 `new_list` 的下一个元素。

用于拆解列表的 `|` 运算符也可以用于从已实例化的表头和表尾分量构建列表，例如：

```
[Element_1 | List_2]
```

如果 `Element_1` 已被实例化为 `pickle`，而 `List_2` 已被实例化为 `[peanut, prune, popcorn]`，则此示例记号将为这一次引用创建列表 `[pickle, peanut, prune, popcorn]`。

如前所述，包含 `|` 符号的列表记号是通用的：它既可以指定列表构建，也可以指定列表拆解。进一步注意以下写法是等价的：

```
[apricot, peach, pear | []]
[apricot, peach | [pear]]
[apricot | [peach, pear]]
```

使用列表时，通常需要某些基本操作，例如 LISP、ML 和 Haskell 中的那些操作。作为 Prolog 中此类操作的一个例子，我们考察 `append` 的定义，它与 LISP 中的此类函数相关。在这个例子中，可以看出函数式语言与声明式语言之间的异同。我们无需指定 Prolog 如何根据给定列表构建新列表；只需根据给定列表来指定新列表的特征。

在外观上，Prolog 的 `append` 定义与第 15 章中出现的 ML 版本非常相似，并且类似地在消解中使用了一种递归来生成新列表。在 Prolog 中，递归是由消解过程引发和控制的。与 ML 和 Haskell 一样，模式匹配过程用于根据实际参数在 `append` 过程的两个不同定义之间进行选择。

以下代码中 `append` 操作的前两个参数是要拼接的两个列表，第三个参数是结果列表：

```
append([], List, List).
append([Head | List_1], List_2, [Head | List_3]) :-
    append(List_1, List_2, List_3).
```

第一条命题指定当空列表与任何其他列表拼接时，该其他列表即为结果。该语句对应于 ML 中 `append` 函数的递归终止步骤。注意，终止命题被放在递归命题之前。这样做是因为我们知道 Prolog 会按顺序匹配这两个命题，从第一个开始（因为它采用深度优先顺序）。

第二条命题指定了新列表的几个特征。它对应于 ML 函数中的递归步骤。左侧谓词说明新列表的第一个元素与第一个给定列表的第一个元素相同，因为它们都命名为 `Head`。每当 `Head` 被实例化为某个值时，目标中所有出现的 `Head` 实际上都会同时被实例化为该值。第二条语句的右侧指定：第一个给定列表的表尾（`List_1`）拼接上第二个给定列表（`List_2`），形成结果列表的表尾（`List_3`）。

阅读 `append` 第二条语句的一种方式如下：将列表 `[Head | List_1]` 拼接到任何列表 `List_2` 上会产生列表 `[Head | List_3]`，但前提是列表 `List_3` 由 `List_1` 拼接 `List_2` 而成。在 LISP 中，这将是：

```
(CONS (CAR FIRST) (APPEND (CDR FIRST) SECOND))
```

在 Prolog 和 LISP 版本中，结果列表都是直到递归产生终止条件时才构建；在这里，第一个列表必须变为空。然后，使用 `append` 函数本身构建结果列表；从第一个列表中取出的元素按相反顺序添加到第二个列表中。反转是通过递归的展开来完成的。

Prolog 的 `append` 与 LISP 和 ML 的 `append` 有一个根本区别：Prolog 的 `append` 是一个谓词——它不返回列表，而是返回 yes 或 no。新列表是其第三个参数的值。

为了说明 `append` 过程的进展，请考虑以下带跟踪的示例：

```
trace.
append([bob, jo], [jake, darcie], Family).
```

```
(1) 1 Call: append([bob, jo], [jake, darcie], _10)?
```

