
为什么使用接受过程参数的底层过程（如 `map`）不起作用？请解释。概述修复该问题的策略并实现你的解决方案。注意：做到这一点很微妙，所以不要花费无限的时间试图使其完美。

## 练习 5.6：不同的引用

一些有趣的语言具有非常不同的评估规则和引用规则。例如，在 MDL 中（参见维基百科 [91]），符号被假设是自求值的，而需要查找的变量通过一个前缀字符来区分。此外，在 MDL 中，组合是一种特殊形式，但带有一个隐含的关键字。我们的评估器可以通过更改语法定义来修改以解释类似 MDL 的语法。尝试一下！

## 练习 5.7：中缀符号

与 Lisp 不同，大多数计算机语言使用中缀表示法。如果我们想在 Scheme 中包含中缀表达式，我们可以写：

```
(infix
"fact := lambda n:
  if n == 0
    then 1
    else n*fact(n-1))
```

```
(fact 6)    ; Lisp 过程现在已定义
720
```

```
(infix "fact(5)")    ; 可以在中缀表示法中使用。
120
```

这完全是一个语法小问题（哈！）。然而，让它运行是一个有趣的项目。你不需要更改解释器。工作在于解析字符字符串将其编译为 Lisp 表达式，就像 `>if` 的工作一样。Lisp 程序员已经这样做很多次了，但编写 Lisp 的人们似乎喜欢原生的 Lisp 波兰前缀符号！12 噢，好吧……

## 5.2：非严格参数过程

在本节中，我们将研究在过程的形式参数中添加声明，以允许对应操作数进行延迟评估。

在 Scheme 中，过程是*严格的*（strict）。严格过程要求在评估过程体之前，评估调用表达式的所有操作数，并将结果参数绑定到形式参数上。但对于 *if* 表达式，谓词部分必须被评估，以确定是评估结果部分还是备选部分；它们不会被评估。这就是为什么 *if* 必须是一个特殊形式，而不是过程。*非严格*（non-strict）过程是指延迟某些操作数评估的过程。我们如何让程序员能够根据需要定义非严格过程，而不是仅仅使用语言定义中指定的少数特殊形式（如 *if*）呢？

例如，假设我们想让名为 *unless* 的过程，它的工作方式类似于特殊形式 *if*，即不评估不需要的备选部分¹³ 使用 *unless*，我们可以写：

```
(define (unless condition consequent alternative)
  (if condition
      alternative
      consequent))
```

如果我们想让一个过程是非严格的，我们必须在需要时才评估其参数。我们可以通过将参数封装在一个特殊结构中（通常称为承诺 promise），然后提供一种评估该承诺的机制来实现。

```
(define (promise expression)
  (list 'promise expression))
(define (force p)
  (if (equal? (car p) 'promise)
      (let ((val (eval (cdr p))))
        (set! (car p) val)
        val)
      p))
```

现在我们可以重新定义 *unless* 为非严格的：

```scheme
(define (unless-ns condition consequent alternative)
  (let ((cond (force condition)))
    (if cond
        (force alternative)
        (force consequent))))
```

这样，`consequent` 和 `alternative` 只在实际需要时被评估。这就是非严格参数的力量，它们可以实现许多强大的控制结构。

（注意：上述代码为了解释概念进行了简化。在 Scheme 解释器中非严格参数的实际实现会更复杂。）

```scheme
(lambda (parameter operand environment)
(postpone-memo operand environment))
```

当然，我们必须扩展 `g:advance`（到目前为止它只有一个默认处理器，参见第 236 页），以执行延迟求。注意 `g:advance` 本身的结果可能是延迟，因此我们可能需要对结果进行推进。

```scheme
(define-generic-procedure-handler g:advance
(match-args postponed?)
(lambda (object)
  (g:advance (g:eval
    (postponed-expression object)
    (postponed-environment object)))))
```

如果延迟表达式的目的是对结果进行记忆化，那么结果将由 `advance-memo!` 保存：

```scheme
(define-generic-procedure-handler g:advance
(match-args postponed?)
(lambda (object)
  (let ((value
    (g:advance
      (g:eval
        (postponed-expression object)
        (postponed-environment object))))
    (advance-memo! object value)
    value)))
```

记忆化的值永远不需要再次求值。`advance-memo!` 过程更改延迟对象的类型以满足谓词 `advanced-memo?` 并保存该值，使其可以通过 `advanced-value`；16 访问：

```scheme
(define-generic-procedure-handler g:advance
(match-args advanced-memo?)
advanced-value)
```

## 示例：惰性参数赋予了我们新的能力。

带有惰性参数的过程可以定义构造函数 `kons` 以及选择器 `kar` 和 `kdr`，这样我们就可以在不计算其内容的情况下创建对。17 在这里，我们将 `kons` 实现为一个按需调用（call-by-need）参数（即记忆化的惰性）的过程。它产生一个消息接收器 `the-pair` 供 `kar` 和 `kdr` 使用。它还会在 `the-pair` 上贴上一张“便利签”，以识别它为 `kons` 的结果。

```scheme
(define (kons x lazy memo) (y lazy memo))
(define (the-pair m)
  (cond ((eq? m 'kar) x)
      (eq? m 'kdr) y)
      (else (error "Unknown message - kons" m x y))))
(hash-table-set! kons-registrations the-pair #t)
(the-pair)
```

```scheme
(define (kar x)
  (x 'kar))
```

```scheme
(define (kdr x)
  (x 'kdr))
```

我们之所以需要便利签，是为了能够识别一个 `kons` 节点：

```scheme
(define (kons? object)
(hash-table-exists? kons-registrations object))
```

使用这种惰性对机制，我们可以轻松地实现流类型（stream-type）处理。流类似于列表，但它们是由消费它们的进程按需构建的。18 因此，一个无限长的流可以被增量地处理，在任何时候只有有限的片段是实际存在的。

有些流是有限的，因此为空流选择一种表示方法是有用的。让我们让它和空列表相同：

```scheme
(define the-empty-stream '())
```

```scheme
(define (empty-stream? thing)
  (null? thing))
```

我们添加流的操作：

```scheme
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```

我们可以找到流的第 $n$ 个元素：

```scheme
(define (ref-stream stream n)
  (if (= n 0)
      (kar stream)
      (ref-stream (kdr stream) (- 1))))
```

给定这些，我们可以创建一个（可能是无限的）斐波那契流，包含两个初始项，其余部分通过将流与其 `kdr` 相加形成：

```scheme
(define fibs
  (kons 0 (kons 1 (add-streams (kdr fibs) fibs))))
```

我们可以查看几个斐波那契数：

```scheme
(ref-stream fibs 10)
55
```

```scheme
(ref-stream fibs 100)
35422484179261950
```

普通的斐波那契程序是指数级的，因此在这一步无法期望得到黄金比例。注意斐波那契数列已经收敛于 1.61803398874989。

（注：此处整合修复了原文中混乱的 OCR 错误）

## 练习 5.8：积分

不幸的是，`cons` 的使用本身并没有解决所有问题。假设我们在给定某些条件下积分一个微分方程。我们进行如下：

```scheme
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```

**b.** 允许过程具有可选参数（可能带有指定的默认值）可能也会有用。例如，一个数值过程可以允许用户指定近似的容差，或者在用户未提供容差时指定一个默认值：

```
(lambda (x (epsilon flo:ulp-of-one))
...)
```

在这里，`flo:ulp-of-one` 是一个全局定义的符号，它指定了与 1.0 相加时产生的值不等于 1.0 的最小 2 的幂。在 C 库中，它被称为 `DBL_EPSILON`。（对于那些感兴趣的人来说，在 IEEE 双精度浮点数中，`flo:ulp-of-one` 的值为 2.22046092503136e-16。）

让 `optional` 声明也运行起来！确保你的扩展可以与所有其他声明混合使用——只要这符合逻辑即可。

## 5.3 编译为执行过程

我们一直在使用的评估器非常灵活且可扩展，但它是“愚笨”的：我们的程序运行得相当慢。原因之一是评估器在反复查看程序的语法（无论它多简单）。在第 4 章中，我们通过在第 4.3 节将每个匹配模式转换为匹配过程的组合（这些过程都具有相同的形状——一种组合器语言）规避了这个问题。在解释语言时，我们可以以类似的方法将其编译为执行过程的组合，从而避免重新检查语法结构。因此，在深入研究评估之前，让我们完成这一过渡。

核心思想是将相对于环境的表达式评估问题拆分为两个阶段。在第一阶段，对表达式进行分析并将其转换为执行过程。在第二阶段，将该执行过程应用于环境，从而产生预期的评估结果。我们直接实现这一主意，将其视为这两个阶段的组合。

```
(define (x:eval expression environment)
((analyze expression) environment))
```

表达式的分析和转换被称为“编译”，它所做的工作是在“编译时”完成的。编译器提取了表达式中不依赖于自由变量取值的行为部分。这大部分是语法分析，但也是一个可以通过语法规则实现某些优化的场所。生成的执行过程依赖于环境中符号到值的映射；它所做的工作是在“运行时”完成的。

## 表达式分析

由于我们希望能够根据需要扩展语言，因此我们将分析实现为一个通用过程，默认是操作符对操作数的应用。对于 Lisp/Scheme 来说，这必须是默认值，因为没有语法关键字来区分应用。

```
(define x:analyze default-analyze)
```

`analyze` 的约定是它接收一个表达式作为参数并返回一个执行过程，该过程接收一个环境。`analyze` 过程捕获了一种常见的用法模式：

```
(define (analyze expression)
(make-executor (analyze expression)))
```

用执行器（executor）封装执行过程目的是为了调试。生成的执行器也是一个与其封装的执行过程具有相同参数的程序。该封装器的一个有用方面是它维护了一个“执行轨迹”，这在确定程序是如何到达某个故障点时非常有帮助。正如我们所说，默认分析是应用。

```
(define (default-analyze expression)
(cond ((application? expression)
  (analyze expression))
  (else (error "Unknown expression type" expression))))
```

```
(define (analyze-application expression)
(let ((operator-exec (analyze operator))
  (operand-execs (map analyze operands))
  (lambda (environment)
    (x:apply operator-exec environment))))
```

这里的分工是：操作符和操作数从表达式中提取并进行分析，以生成执行过程 `operator-exec` 和 `operand-exec`。这可能需要大量的分析。应用的执行过程是由 lambda 表达式创建的过程，它接收一个环境并执行应用。`x:apply` 过程类似于解释器中的 `g:apply`；但 `x:apply` 接收的是操作数的执行过程，而不是 `g:apply` 使用的操作数表达式。引入 `x:advance`（类似于 `g:advance`）的原因相同。评估器的每个部分都可以以此方式进行转换。

自求值表达式（如数字、布尔值或字符串）的转换是显而易见的。这部分困难的部分在于表达式的实际语法，由 Scheme 解析器处理。程序文本在到达评估器之前就会解析为标记（tokens）和 s 表达式，因此我们不需要担心那些复杂性。

```
(define (analyze-self-evaluating expression)
(lambda (environment) expression))
```

```
(define (analyze-generic-procedure-handler x:analyze)
(match-args self-evaluating?)
  analyze-self-evaluating))
```

引用（Quotation）很容易，再次是因为困难的部分在解析器中。

```
(define (analyze-quoted expression)
(let ((qval (text-of-expression)))
  (lambda (environment) qval))
```

```
(define (analyze-generic-procedure-handler x:analyze)
(match-args quoted?)
analyze-quoted)
```

变量也很容易。一旦我们确定了变量，所有的工作都在执行过程中完成。

```
(define (analyze-variable expression)
(lambda (environment)
(lookup-variable-value expression))
```

```
(define (analyze-generic-procedure-handler x:analyze)
(variable-
```

定义

在 Lisp/Scheme 中通过 lambda 表达式表示的过程定义是分工的一个强大示例。在构建执行过程之前，分析器（编译器）解析 lambda 表达式，提取形式规范并编译体。因此，执行过程不需要做这些工作。

```
(define (analyze-lambda expression)
(let ((vars (lambda-parameters expression))
  (body-exec (analyze-body expression)))
  (lambda (environment)
  (make-compound-procedure body-exec environment)))
```

```
(define (analyze-generic-procedure-handler x:analyze)
(lambda?)
analyze-lambda)
```

特殊形式 `if` 是另一个分离分析与执行优势的清晰示例。`if` 表达式的三个部分在编译时分析，允许执行过程只需从谓词中提取布尔值，以决定执行哪一个分支。子表达式的分析没有必要在运行时进行（在使用执行过程时）。

```
(define (analyze-if expression)
(let ((predicate-exec
