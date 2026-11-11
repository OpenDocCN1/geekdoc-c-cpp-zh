
```scheme
1
(* n (factorial (- n 1)))
))
```

回顾一下，Scheme 的多重选择结构 COND 已在第 8 章讨论过。下面是一个使用 COND 的简单函数示例：

```scheme
(DEFINE (leap? year)
  (COND
    ((ZERO? (MODULO year 400)) #T)
    ((ZERO? (MODULO year 100)) #F)
    (ELSE (ZERO? (MODULO year 4)))
  ))
```

以下小节包含更多使用 COND 的示例。Scheme 的第三种控制机制是递归，它和数学中一样，用于指定重复。15.5.10 节中的大多数示例函数都使用递归。

### 15.5.8 列表函数

基于 Lisp 的编程语言更常见的用途之一是列表处理。本小节介绍 Scheme 中用于处理列表的函数。回顾一下，Scheme 的列表操作已在第 6 章简要介绍过。下面将更详细地讨论 Scheme 中的列表处理。

Scheme 程序由函数应用函数 EVAL 解释。当 EVAL 应用于一个基本函数时，它首先求值给定函数的参数。当函数调用中的实际参数本身也是函数调用时（这种情况很常见），这一动作是必要的。然而，在某些调用中，参数是数据元素而不是函数引用。当一个参数不是函数引用时，显然不应对它求值。我们之前没有关心这一点，因为数字字面量总是求值为其自身，不会被误认为函数名。

假设我们有一个函数，它有两个参数：一个原子和一个列表，该函数的目的是判断给定原子是否在给定列表中。原子和列表都不应被求值；它们是要处理的字面数据。为了避免对参数求值，可将其作为基本函数 QUOTE 的参数传入，QUOTE 只是原样返回它而不做任何改变。下面的示例说明了 QUOTE 的用法：

```scheme
(QUOTE A) returns A
(QUOTE (A B C)) returns (A B C)
```

对 QUOTE 的调用通常缩写为在被引用的表达式前加一个撇号（'），并省略表达式外面的括号。因此，使用 '(A B) 而不是 (QUOTE (A B))。

QUOTE 的必要性源于 Scheme（以及其他基于 Lisp 的语言）的基本性质：数据和代码具有相同的形式。尽管这对命令式语言的程序员来说可能显得奇怪，但它带来了一些有趣而强大的处理过程，其中一种将在 15.5.14 节讨论。

CAR、CDR 和 CONS 函数已在第 6 章介绍过。下面是 CAR 和 CDR 操作的更多示例：

```scheme
(CAR '(A B C)) returns A
(CAR '((A B) C D)) returns (A B)
(CAR 'A) is an error because A is not a list
(CAR '(A)) returns A
(CAR '()) is an error
(CDR '(A B C)) returns (B C)
(CDR '((A B) C D)) returns (C D)
(CDR 'A) is an error
(CDR '(A)) returns ()
(CDR '()) is an error
```

CAR 和 CDR 函数的名称至少可以说很奇特。这些名称的起源在于 Lisp 的最初实现，那是在 IBM 704 计算机上完成的。704 的内存字有两个字段，分别名为 *decrement* 和 *address*，用于各种操作数寻址策略。这两个字段都可以存储一个机器内存地址。704 还包括两条机器指令，也分别名为 CAR（寄存器 address 部分的内容）和 CDR（寄存器 decrement 部分的内容），用于提取相关字段。自然地，可以用这两个字段存储列表节点的两个指针，从而使一个内存字几乎可以存储一个节点。按照这些约定，704 的 CAR 和 CDR 指令提供了高效的列表选择器。这些名称延续到了所有 Lisp 方言的基本函数中。

作为另一个简单函数的示例，考虑

```scheme
(DEFINE (second a_list) (CAR (CDR a_list)))
```

这个函数一旦求值，就可以像下面这样使用：

```scheme
(second '(A B C))
```

它返回 B。

Scheme 中一些最常用的函数组合被内置为单个函数。例如，(CAAR x) 等价于 (CAR (CAR x))，(CADR x) 等价于 (CAR (CDR x))，而 (CADDAR x) 等价于 (CAR (CDR (CDR (CAR x))))。在函数名中的 'C' 和 'r' 之间，最多四个 A 和 D 的任意组合都是合法的。作为示例，考虑下面 CADDAR 的求值过程：

```scheme
(CADDAR '((A B C) D E)) =
(CAR (CDR (CDR (CAR '((A B C) D E))))) =
(CAR (CDR (CDR '(A B C)))) =
(CAR (CDR '(B C))) =
(CAR '(C)) =
(C)
```

下面是调用 CONS 的示例：

```scheme
(CONS 'A '()) returns (A)
(CONS 'A '(B C)) returns (A B C)
(CONS '() '(A B)) returns (() A B)
(CONS '(A B) '(C D)) returns ((A B) C D)
```

这些 CONS 操作的结果如图 15.2 所示。注意，从某种意义上说，CONS 是 CAR 和 CDR 的逆操作。CAR 和 CDR 将一个列表拆开，而 CONS 从两个给定的列表部分构造一个新列表。CONS 的两个参数成为新列表的 CAR 和 CDR。因此，如果 `a_list` 是一个列表，那么

```scheme
(CONS (CAR a_list) (CDR a_list))
```

将返回一个与 `a_list` 具有相同结构和相同元素的列表。

### 图 15.2

若干 CONS 操作的结果

![](img/e22931b583977bc24a4263ee43d0f0bb_677_0.png)

它会检查是否已经存在这样的列表。如果存在，新列表不过是指向现有列表的指针。在这些情况下，EQ? 会判定这两个列表相等。然而，在某些情况下，可能难以检测是否存在完全相同的列表，此时会创建一个新列表。在这种情况下，EQ? 会返回 #F。

最后一种情况表明，加法可能产生一个新值，在这种情况下，它（用 EQ? 判断）不会等于 3.4；或者它可能识别出自己已经拥有值 3.4 并使用该值，在这种情况下，EQ? 会使用指向旧 3.4 的指针并返回 #T。

正如我们所见，EQ? 适用于符号原子，但不一定适用于数字原子。= 谓词适用于数字原子，但不适用于符号原子。如前所述，EQ? 对列表参数也不能可靠工作。

有时，在不知道两个原子是符号原子还是数字原子时，能够测试它们是否相等会很方便。为此，Scheme 提供了另一个谓词 EQV?，它同时适用于数字原子和符号原子。考虑下面的示例：

```scheme
(EQV? 'A 'A) returns #T
(EQV? 'A 'B) returns #F
(EQV? 3 3) returns #T
(EQV? 'A 3) returns #F
(EQV? 3.4 (+ 3 0.4)) returns #T
(EQV? 3.0 3) returns #F
```

注意，最后一个示例表明浮点值与整数值不同。EQV? 不是指针比较，而是值比较。

在可能的情况下，使用 EQ? 或 = 而不是 EQV? 的主要原因是 EQ? 和 = 比 EQV? 更快。

谓词函数 LIST? 如果其单个参数是列表，则返回 #T，否则返回 #F，如下面的示例所示：

```scheme
(LIST? '(X Y)) returns #T
(LIST? 'X) returns #F
(LIST? '()) returns #T
```

NULL? 函数测试其参数以确定它是否为空列表，如果是，则返回 #T。考虑下面的示例：

```scheme
(NULL? '(A B)) returns #F
(NULL? '()) returns #T
(NULL? 'A) returns #F
(NULL? '(())) returns #F
```

最后一次调用返回 #F，因为该参数不是空列表。相反，它是一个包含单个元素（即空列表）的列表。

### 15.5.10 Scheme 函数示例

本节包含几个 Scheme 函数定义示例。这些程序解决简单的列表处理问题。

考虑判断给定原子是否属于给定列表的问题，该列表不包含子列表。这样的列表称为简单列表。如果函数名为 member，则可以如下使用：

```scheme
(member 'B '(A B C)) returns #T
(member 'B '(A C D E)) returns #F
```

从迭代的角度来看，成员资格问题就是按某种顺序逐个比较给定原子和给定列表中的各个元素，直到找到匹配项，或者列表中没有更多元素可供比较。类似的过程也可以用递归完成。该函数可以将给定原子与列表的 CAR 进行比较。如果它们匹配，则返回值 #T。如果不匹配，则应忽略列表的 CAR，并继续在列表的 CDR 上搜索。为此，可以让函数以列表的 CDR 作为列表参数调用自身，并返回该递归调用的结果。如果给定原子在列表中被找到，这一过程就会结束。如果原子不在列表中，函数最终会（由自身）以空列表作为实际参数被调用。该事件必须迫使函数返回 #F。在这个过程中，有两种退出递归的方式：要么在某次调用时列表为空，此时返回 #F；要么找到匹配项并返回 #T。

总而言之，该函数必须处理三种情况：输入列表为空；原子与列表的 CAR 匹配；原子与列表的 CAR 不匹配，从而触发递归调用。这三种情况就是 COND 的三个参数，其中最后一个是默认情况，由 ELSE 谓词触发。完整函数如下：5

```scheme
(DEFINE (member atm a_list)
    (COND
        ((NULL? a_list) #F)
        ((EQ? atm (CAR a_list)) #T)
        (ELSE (member atm (CDR a_list)))
    )
)
```

这种形式是简单的 Scheme 列表处理函数的典型形式。在这类函数中，列表中的数据一次处理一个元素。各个元素用 CAR 指定，并通过在列表的 CDR 上递归继续处理。

注意，空列表测试必须放在相等测试之前，因为对空列表应用 CAR 会出错。
