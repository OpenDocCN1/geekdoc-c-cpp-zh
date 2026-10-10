
那么（在 MIT/GNU Scheme 中）执行过程将拥有一个名称，告诉我们它是哪种类型的执行过程。在所有执行过程中实现这个想法。

思考并可能实现其他方法，让我们在不损害执行速度的情况下提高运行时代码的可调试性。你可能做的一件事是将表达式 `exp` 作为“便签页”添加到执行过程上。

## 练习 5.14：常量折叠

假设我们有一个声明来告诉分析器某些符号具有给定的含义（例如，声明常规算术运算符 `{+, -, *, sqrt}` 指向已知的常量过程）。那么任何与这些运算符的常量组合，例如 `(/ (+ 1 (sqrt 5)) 2)`，都可以由分析器在编译时求值，并使用结果而不是在运行时执行计算。这种编译时优化被称为常量折叠。

在分析器中实现常量折叠。为了进行常量折叠，分析器需要知道程序文本中的哪些符号可以被绑定到已知值。例如，它需要知道 `car` 是否实际上绑定到对的选择器。假设分析器可以调用一个查找已知符号绑定的过程。该过程应该接受一个符号

并返回分析器可能依赖的值，如果该符号不在分析器的控制范围内，则返回 `#f`。

## 练习 5.15: 其他优化

有很多可以改进程序执行的简单变换。例如，我们可以使用模式匹配技术来构建一个项重写系统，实现孔洞优化（peephole optimization）和循环不变代码移动（loop-invariant code motion）。或许添加公共子表达式消除会很好；但要小心赋值带来的副作用。在分析中添加一个优化阶段，实现一些经典的编译器优化，并展示它们的效果。

## 练习 5.16: 编译形式参数声明

虽然向执行过程组合的转换是非常有效的，并且产生的代码比直接解释要快得多，但我们提出的版本并不聪明：用于 `x:apply` 的复合过程执行过程通过解析形式参数列表来确定如何处理操作数。这实际上应该在编译时而不是运行时完成：创建复合过程的 lambda 表达式的分析应该产生一个知道如何处理操作数和调用环境的执行过程。

想出来并实现它。确保你不要携带调用环境超出绝对必要的范围。

注意：这是一个大大的项目。

## 5.4 探索性行为

我们已经遇到过模式匹配中匹配段变量的显式回溯搜索。但即使在没有段变量的情况下，项重写系统的实现也需要一些回溯搜索。当规则的后件表达式确定匹配没有足够的选择性以至于后件无法替换数据中被匹配的部分时，即使规则的前件模式匹配了部分数据，后件表达式也会返回 `#f`，回溯到匹配过程并尝试不同的规则。

此外，用于优化通用过程访问的 `tri` 机制也处理了回溯。`tri` 追踪一组参数序列必须满足的谓词序列。但谓词的初始段与参数的初始段之间可能有多种匹配方式，因此 `tri` 机制中内部构建了一个隐式搜索。

我们通常将回溯及其在搜索中的极端使用视为一种 AI 技术。然而，回溯可以被视为一种构建模块化且可独立演化系统的方法，就像生物系统的探索性行为一样。考虑一个简单实用的例子：解二次方程。二次方程有两个根。我们可以两个都返回，并假设解决方案知道如何处理，或者返回一个并听天运气。（标准的平方根程序 `sqrt` 返回正平方根，尽管有两个平方根！）返回两个解决方案的缺点是，结果的接收者必须知道对两者都尝试计算并拒绝其中一个，或者返回计算的两个结果，而计算本身可能包含某些选择。只返回一个解决方案的缺点是它可能不是接收者目的所需的。这在物理系统的仿真中可能是一个真实的问题。

### 语言学隐式搜索

我们显式构建的搜索是可以接受的，但也许通过在语言基础设施中构建回溯机制可以做得更好。平方根程序应该返回根之一，并提供在接收者判定第一个选择不合适时改变主意并返回另一个根的选项。

确定用于其计算的成分是否合适且可接受，是接收者的责任，也应该是接收者的责任。这本身可能需要复杂的计算，涉及如果不进行进一步计算其后果可能是不而易见的；因此该过程是递归的。当然，这会导致我们对程序中已做的所有选择的所有可能赋值进行潜在致命的指数级搜索。

考虑搜索策略在多大程度上可以与程序的与其他分离是重要的，这样人们就可以在不大幅修改程序的情况下交换搜索策略。在这里我们进一步追求将搜索和搜索控制推到语言支持的基础设施中，而不是完全在程序中显式构建搜索。将搜索隐式化可能会鼓励过度使用搜索。像通常一样，模块灵活性可能是危险的。

这个想法有悠久的历史。1961年，John McCarthy [90] 提出了非确定性操作符 `amb` 的想法，它对于表示非确定自动机有用。1967年，Bob Floyd [35] 有将回溯搜索作为语言基础设施的一部分构建到计算机语言的想法。1969年，Carl Hewitt [56] 提出了一种语言 PLANNER，体现了这些思想。20世纪70年代，Colmerauer、Kowalski、Rousseau 和 Warren 开发了 Prolog [78]，一种基于一阶谓词逻辑的语言。

### 5.4.1 amb

McCarthy 的 `amb`，确定用于其计算的成分是否合适且可接受，是接收者的责任，也应该是接收者的责任。这本身可能需要复杂的计算，涉及如果不进行进一步计算其后果可能是不而易见的；因此该过程是递归的。当然，这会导致我们对程序中已做的所有选择的所有可能赋值进行潜在致命的指数级搜索。

```
;; ...)
;; fail = (lambda () ...)
...
;; 尝试得到结果。如果不能，则 (fail)。
...)
```

向延续传递风格（continuation-passing style）的转换有点不太愉快，因为它会大幅扩展代码，但它基本上是机械的。例如，第 260 页上的 `analyze-application` 过程如下：

```scheme
(define analyze-application expression)
(let ((operator-exec (analyze operator expression)))
  (operand-execs (map analyze operands expression))
  (lambda (environment)
  (x:apply (x:advance operator-exec environment))
    operand-execs
    environment))))
```

如果我们将代码转换为延续传递风格，就会得到：23

```scheme
(define analyze-application exp)
(let ((operator-exec (analyze operator exp)))
  (operand-execs (map analyze operands exp)))
  (lambda (env succeed fail)
    (operator-exec env
      (lambda operator-value fail-1)
        (a:advance operator-value)
        (lambda (procedure fail-2))
          (a:apply procedure
            operand-execs
            env
            succeed
            fail-2))
    fail-1))))
```

这个执行过程比它推导出来的那个更复杂。在原始执行过程体内，表达式 `(operator-exec environment)` 返回一个值给表达式 `(x:advance ...)`，而后者又返回一个值给表达式 `(x:apply)`。在新的执行过程中，这些嵌套表达式消失了。每个过程通过调用一个接受其计算结果的过程来“返回”。

由于我们经常必须强制求值（force a value），因此创建一个捕捉强制求值的抽象是合适的。`execute-strict` 过程隐藏了与强制求值延迟表达式评估相关的无关紧要细节，以确保获得一个未延迟的值。在上面的 `analyze-application` 中，它被用于强制操作符的值，以便获取一个可用的过程。

```scheme
(define (execute-strict env succeed fail)
  (executor env
    (lambda (value fail-1)
      (a:advance value succeed fail-1))
    fail)))
```

`execute-strict` 过程调用给定的执行过程（`executor`）。其结果随后传递给 `a:advance` 进行强制求值。强制后的值随后传递给 `execute-strict` 的成功延续（`succeed`），有效地将强制求值的结果返回给 `execute-strict` 的调用者。

使用 `execute-strict` 我们可以重写 `analyze-application`：

```scheme
(define (analyze-application exp)
  (let ((operator-exec analyze (operator exp))
        (operand-execs map analyze (operands exp))
        (lambda (env succeed fail)
          (execute-strict operator-exec
            env
          (lambda (procedure fail-2)
            (a:apply procedure
              operand-execs
                env
                succeed
                fail-2)))))
```

每个执行过程都必须以此方式进行转换。我们在 `analyze-if` 中使用 `execute-strict` 来强制条件判断谓词的值，如果没有它，我们就无法继续。

```scheme
(define (analyze-if exp)
  (let ((predicate-exec analyze (if-predicate exp))
        (consequent-exec analyze (if-consequent exp))))
```

```scheme
(alternative-exec (analyze (if-alternative exp)))
(lambda env succeed fail)
  execute-strict predicate-exec
    env
    (lambda (pred-value pred-fail))
      ((if pred-value
        consequent-exec
        alternative-exec)
        env succeed pred-fail))
    fail)))
```

大部分转换都是直接的，我们将在文中向你介绍细节。但有一个趣有趣的案例：赋值。在回溯系统中，我们通常需要两种不同的赋值。通常的永久赋值 `set!` 用于在搜索过程中累积信息，例如某个分支被调查了多少次。还有一种可撤销的赋值 `maybe-set!`，如果它所在的分支被撤回，则必须撤销。通常的永久赋值实现如下：

```scheme
(define analyze-assignment exp)
(let ((var (assignment-variable exp))
       (value-exec (analyze (assignment-value exp)))
    (lambda env succeed fail)
    value-exec env
      (lambda (new-val val-fail)
        (set-variable-value! var new-val env)
        (succeed 'ok val-fail)))
    fail)))
```

可撤销的赋值更为复杂。随成功赋值传递的失败延续会将被赋值变量的值恢复到其之前的值。

```scheme
(define analyze-undoable-assignment exp)
(let ((var (assignment-variable exp))
       (value-exec (analyze (assignment-value exp)))
    (lambda env succeed fail)
    value-exec env
      (lambda (new-val val-fail)
        (let ((old
              (lookup-variable-value var env)))
          (set-variable-value! var new-val env)
        (succeed 'ok)))
```

```scheme
(lambda ()
  (set-variable-value! var
    old-val
    env)
  (val-fail)))
```

另一个有趣的案例是 `amb` 本身的实现。当最后一个提出的备选项被拒绝时，我们必须选择下一个备选项。这是通过当前备选项的失败延续实现的：

```scheme
(define (analyze-amb exp)
(let ((alternative-execs
    (map analyze amb-alternatives exp))
  (lambda (env fail)
    (let loop ((alts alternative-execs))
      (if (pair? alts)
          ((car alts) env
            succeed
              (lambda ()
                (loop (cdr alts)))) fail))))
```

如果没有剩余的备选项，`amb` 的执行过程将调用调用它时的失败延续。这使得程序对备选项树执行深度优先搜索。通过递归缩小备选项列表来检查备选项；因此搜索从左到右进行。

除了对 `read-eval-print` 循环（第 246 页）进行调整以适应延续传递结构外，就是这些了！

# 练习题 5.17：一个谜题

使用 `amb` 形式化并解决以下谜题：

两名女性（Alyssa 和 Eva）和四个男性（Ben, Louis, Cy 和 Lem）坐在一张圆桌旁玩牌。每个人都有一手牌牌；没有两手牌牌是相同的。

- Alyssa 和 Eva；没有两手牌牌是相同的。
- Ben, Louis, Cy 和 Lem。
- Ben 坐在 Eva 的对面。
- Alyssa 坐在 Louis 的对面。
- Ben 坐在 Cy 的对面。
- Cy 坐在 Ben 的对面。
- Louis 坐在 Alyssa 的对面。
- Eva 坐在 Lem 的对面。
- Eva 坐在 Cy 的对面。

## 练习 5.20: 选择排序

`amb` 机制按照目前的写法，总是按照 `amb` 表达式给出的顺序尝试选择。但有时我们可以利用上下文信息来做出更好的排序。例如，在棋类游戏中，从所有可能的合法移动中选择某一步应该取决于棋盘的状态。让我们发明一个 `amb` 的版本，能够给我们提供这种灵活性。假设每个选择表达式都配对了一个数值权重表达式：

```
choose <weight-1> <choice-1> ... <weight-n> <choice-n>
```

我们可以评估所有的权重表达式，并使用它们来选择下一个要评估并返回的选择表达式。当然，在做出一个选择后，该选择就会被耗尽；如果失败返回到这个 `choose` 形式，那么在进行下一次选择之前，必须重新评估剩余的权重表达式。

- a. 实现 `choose`，使得权重最大的选项被选中。
- b. 在现实情况下，权重通常不足以做出唯一的选择。有时一种良好的策略是按照与计算出的权重成比例的概率进行随机选择。实现另一种选择器 `pchoose`，其语法与 `choose` 相同，工作方式如下。

## 5.5 暴露底层的延续

现在我们就可以处理真正的魔法了！

大多数语言（包括 Scheme）都是围绕着“表达式”的概念组织的。一个表达式有一个会“返回”的值。一个表达式由子表达式组成，每个子表达式都有一个返回给其所属大表达式的值。表达式的核心思想是什么？

考虑以下复合表达式

```
(+ 1 (* 2 3) (/ 8 2))
```

当然，它的值是 11。它是通过评估运算符和操作数，然后将运算符的值（过程）应用于操作数的值（参数）来计算的。
