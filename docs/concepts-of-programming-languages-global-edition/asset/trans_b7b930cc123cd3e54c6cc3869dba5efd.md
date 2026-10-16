
1
(* n (factorial (- n 1)))
))

回想一下，Scheme 的多重选择构造 COND 已在第 8 章讨论过。以下是使用 COND 的一个简单函数的示例：

```
(DEFINE (leap? year)
  (COND
    ((ZERO? (MODULO year 400)) #T)
    ((ZERO? (MODULO year 100)) #F)
    (ELSE (ZERO? (MODULO year 4))))
)
```

以下小节包含 COND 用法的其他示例。Scheme 的第三种控制机制是递归，它与数学中一样用于指定重复。第 15.5.10 节中的大多数示例函数都使用递归。

## 15.5.8 列表函数

Lisp 语言最常见的用途之一是列表处理。本小节介绍 Scheme 处理列表的函数。回想一下，Scheme 的列表操作已在第 6 章简要介绍过。以下是关于 Scheme 中列表处理的更详细讨论。

Scheme 程序由函数应用函数 EVAL 解释。当应用于原始函数时，EVAL 首先计算给定函数的参数。当函数调用中的实际参数本身就是函数调用时，这种操作是必要的，这经常会发生。然而，在某些调用中，参数是数据元素而不是函数引用。当参数不是函数引用时，它显然不应该被求值。我们之前没有关心这个问题，因为数值字面量总是求值到自身，不能被误认为是函数名。

假设我们有一个函数有两个参数，一个原子和一个列表，该函数的目的是确定给定的原子是否在给定的列表中。原子和列表都不应被求值；它们是要处理的字面数据。为了避免求值一个参数，它首先作为参数传递给原始函数 QUOTE，该函数只是原样返回它。以下示例说明了 QUOTE：

```
(QUOTE A) returns A
(QUOTE (A B C)) returns (A B C)
```

对 QUOTE 的调用通常通过在要引用的表达式前加上撇号（'）并省略表达式周围的括号来缩写。因此，而不是 (QUOTE (A B))，使用 '(A B)。

QUOTE 的必要性源于 Scheme（以及其他 Lisp 语言）的根本特性：数据和代码具有相同的形式。虽然这对命令式语言程序员来说可能显得奇怪，但它导致了一些有趣而强大的过程，其中之一在第 15.5.14 节中讨论。

CAR、CDR 和 CONS 函数已在第 6 章介绍。以下是 CAR 和 CDR 操作的更多示例：

```
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

CAR 和 CDR 函数的名字充其量是古怪的。这些名字的起源在于 Lisp 的第一个实现，该实现运行在 IBM 704 计算机上。704 的内存字有两个字段，名为 decrement 和 address，它们用于各种操作数寻址策略。这两个字段中的每一个都可以存储一个机器内存地址。704 还包括两个机器指令，也名为 CAR（寄存器地址部分的內容）和 CDR（寄存器减量部分的內容），用于提取相关字段。将两个字段用于存储列表节点的两个指针是自然的，这样一个内存字就可以整齐地存储一个节点。使用这些约定，704 的 CAR 和 CDR 指令提供了高效的列表选择器。这些名字被保留到所有 Lisp 方言的原语中。

作为另一个简单函数的示例，考虑

```
(DEFINE (second a_list) (CAR (CDR a_list)))
```

一旦该函数被求值，它就可以被使用，如

```
(second '(A B C))
```

它返回 B。

Scheme 中最常用的一些函数式组合被内置为单个函数。例如，(CAAR x) 等价于 (CAR (CAR x))，(CADR x) 等价于 (CAR (CDR x))，而 (CADDAR x) 等价于 (CAR (CDR (CDR (CAR x))))。在函数名中 'C' 和 'R' 之间最多四个 A 和 D 的任意组合都是合法的。作为示例，考虑以下对 CADDAR 的求值：

```
(CADDAR '((A B (C) D) E)) =
(CAR (CDR (CDR (CAR '((A B (C) D) E))))) =
(CAR (CDR (CDR '(A B (C) D)))) =
(CAR (CDR '(B (C) D))) =
(CAR '((C) D)) =
(C)
```

### 以下是 CONS 的示例调用：

```
(CONS 'A '()) returns (A)
(CONS 'A '(B C)) returns (A B C)
(CONS '() '(A B)) returns (() A B)
(CONS '(A B) '(C D)) returns ((A B) C D)
```

这些 CONS 操作的结果显示在图 15.2 中。注意 CONS 在某种意义上是 CAR 和 CDR 的逆运算。CAR 和 CDR 将列表拆开，而 CONS 从两个给定的列表部分构造一个新列表。CONS 的两个参数成为新列表的 CAR 和 CDR。因此，如果 a_list 是一个列表，则

```
(CONS (CAR a_list) (CDR a_list))
```

返回一个具有与 a_list 相同结构和相同元素的列表。

### 图 15.2

若干 CONS 操作的结果

```
(CONS 'A '())
```

![](img/e382387aad0004c80a0dd0a70be9a623_673_0.png)

```
(A)
```

```
(CONS 'A '(B C))
```

![](img/e382387aad0004c80a0dd0a70be9a623_673_1.png)

```
(A B C)
```

```
(CONS '() '(A B))
```

![](img/e382387aad0004c80a0dd0a70be9a623_673_2.png)

```
(() A B)
```

```
(CONS '(A B) '(C D))
```

![](img/e382387aad0004c80a0dd0a70be9a623_673_3.png)

```
((A B) C D)
```

仅处理本章讨论的相对简单的问题和程序，很可能不会故意将 CONS 应用于两个原子，尽管这是合法的。这种应用的结果是一个点对，因 Scheme 显示方式而得名。例如，考虑以下调用：

```
(CONS 'A 'B)
```

如果显示此结果，它将显示为

```
(A . B)
```

这个点对表示该单元不是原子和指针或指针和指针，而是两个原子。

LIST 是一个从可变数量参数构造列表的函数。它是嵌套 CONS 函数的简写形式，如下所示：

```
(LIST 'apple 'orange 'grape)
```

返回

```
(apple orange grape)
```

使用 CONS，上面的 LIST 调用写成如下：

```
(CONS 'apple (CONS 'orange (CONS 'grape '()))
```

## 15.5.9 用于符号原子和列表的谓词函数

Scheme 有三个基本的谓词函数 EQ?、NULL? 和 LIST?，用于符号原子和列表。

EQ? 函数以两个表达式作为参数，尽管它通常用于两个符号原子参数。它返回 #T，如果两个参数具有相同的指针值——即它们指向同一个原子或列表；否则返回 #F。如果两个参数是符号原子，EQ? 返回 #T，如果它们是相同的符号（因为 Scheme 不会重复创建符号）；否则返回 #F。考虑以下示例：

```
(EQ? 'A 'A) returns #T
(EQ? 'A 'B) returns #F
(EQ? 'A '(A B)) returns #F
(EQ? '(A B) '(A B)) returns #F or #T
(EQ? 3.4 (+ 3 0.4)) returns #F or #T
```

正如第四个示例所示，使用 EQ? 比较列表的结果是不一致的。其原因是完全相同的两个列表通常不会在内存中重复。Scheme 系统在创建列表时，会检查是否已存在这样的列表。如果存在，新的列表只不过是指向现有列表的指针。在这些情况下，EQ? 会判断这两个列表相等。然而，在某些情况下，可能很难检测到相同列表的存在，在这种情况下会创建一个新列表。在这种情况下，EQ? 返回 #F。

最后一个例子表明，加法可能产生一个新值，在这种情况下它与 3.4 不相等（使用 EQ?），或者它可能认识到它已经有 3.4 的值并使用它，在这种情况下 EQ? 将使用旧 3.4 的指针并返回 #T。

正如我们所见，EQ? 对符号原子有效，但不一定对数值原子有效。= 谓词对数值原子有效，但不适用于符号原子。如前所述，EQ? 对列表参数也不可靠。

有时方便能够测试两个原子的相等性，而不知道它们是符号还是数值。为此目的，Scheme 有一个不同的谓词 EQV?，它同时适用于数值和符号原子。考虑以下示例：

```
(EQV? 'A 'A) returns #T
(EQV? 'A 'B) returns #F
(EQV? 3 3) returns #T
(EQV? 'A 3) returns #F
(EQV? 3.4 (+ 3 0.4)) returns #T
(EQV? 3.0 3) returns #F
```

注意，最后一个示例表明浮点值与整数值不同。EQV? 不是指针比较，而是值比较。

使用 EQ? 或 = 而不是 EQV? 的主要原因是，当可能时，EQ? 和 = 比 EQV? 更快。

LIST? 谓词函数如果其唯一参数是列表则返回 #T，否则返回 #F，如以下示例所示：

```
(LIST? '(X Y)) returns #T
(LIST? 'X) returns #F
(LIST? '()) returns #T
```

NULL? 函数测试其参数以确定它是否是空列表，如果是则返回 #T。考虑以下示例：

