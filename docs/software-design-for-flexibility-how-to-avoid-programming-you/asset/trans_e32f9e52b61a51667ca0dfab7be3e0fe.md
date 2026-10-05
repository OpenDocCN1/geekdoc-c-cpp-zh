
（对地址空间中特定敏感位置的赋值）。在 Scheme 中，我们允许程序对赋值语句所在词作用环境中的变量进行赋值：

```
(define-generic-procedure-handler g:eval
 (match-args assignment? environment?)
  (lambda (expression environment)
    (set-variable-value! (assignment-variable expression)
      (g:eval (assignment-value expression)
        environment))))
```

赋值的语法为：

```
(define (assignment? exp) (tagged-list? exp 'set!))
(define (assignment-variable assn) (cadr assn))
(define (assignment-value assn) (caddr assn))
```

我们还允许定义，即带有给定值创建一个新变量。定义会在定义语句最局部的词作用环境帧中创建一个新变量。

```
(define-generic-procedure-handler g:eval
 (match-args definition? environment?)
  (lambda (expression environment)
    (define-variable! (definition-variable expression)
      (g:eval (definition-value expression)
        environment))
    (definition-variable expression)))
```

定义的语法比赋值的语法复杂，因为我们允许有多种定义过程：

```
(define (definition? exp) (tagged-list? exp 'define))
```

```
(define (definition-variable defn)
 (if variable? (cadr defn)                ; (DEFINE foo ...)
  (cadr defn))
  (caddr defn))                             ; (DEFINE (foo ...)))
```

```
(define (definition-value defn)
 (if variable? (cadr defn)                ; (DEFINE foo ...)
  (caddr defn))
  (cons 'lambda                             ; (DEFINE (foo p...) b...)))
```

```
(cons (cdadr defn) ; =(DEFINE foo
(cddr defn))); ; (LAMBDA (p...) b...))
```

这完成了定义语言语法的特殊形式的常规列表。当然，通用过程的实现允许轻松地创建新的特殊形式，使得语言能够增长，从而更方便地表达基础语言中未很好支持的计算思想。具有许多不同语法结构的语言可能难以学习、文档化和使用；这是一个经典的工程权衡（记住 Alan Perlis 在第 159 页的格言）。

## 5.1.2 apply

传统的 Scheme apply 接受两个参数：要应用的过程和传递给该过程的求值参数。这对于 Scheme 来说足够了，因为 Scheme 是一种严格的求值顺序语言，只有词法作用域变量。

通过将 apply 泛化为接受三个参数——未求值的操作数和调用环境——我们使得包含对某些参数需要正常求值的过程（例如按需调用）或对参数进行声明（如类型和单位）的过程成为可能。将在 5.2 节进行此类扩展。环境参数也使得适应非词法作用域变量成为，但我们不会这样做；这通常是一个坏主意。我们将从 Scheme 求值顺序开始，并留出扩展的通用钩子。

我们的 apply 是一个带有三个参数的通用过程：

```
(define g:apply)
(simple-generic-procedure 'apply 3 default-apply))

(define (default-apply procedure operands calling-environment)
(error "Unknown procedure type"))
```

我们需要为各种类型的过程提供处理器。某些过程，例如算术加法（通常由运算符 + 命名），是严格的：它们在计算值之前需要求值所有的参数。在 Scheme 中，所有过程都是严格的，包括原生过程（在系统或语言级别之下的硬件中实现）。因此，我们需要为严格原生过程提供一个通用处理器：

```
(define-generic-procedure-handler g:apply
(match-args strict-primitive-procedure?)
  operands?
  environment?)
  (lambda operands calling-environment)
  (apply-primitive-procedure procedure
    (eval-operands operands calling-environment)))
```

原生过程的应用在细节级别上是“魔法”的。操作数求值器（如第 238 页的 if）必须对求值结果调用 g:advance 以确保获得值。

```
(define (eval-operands operands calling-environment)
  (map (lambda g:eval calling-environment)
    (g:advance g:eval calling-environment))
  operands))
```

注意，操作数的求值顺序由 map 的行为决定。

通过求值 lambda 表达式构造的过程不是原生的。在这里我们可以拆解过程。我们可以获取形式参数规范，即形式参数的名称。我们还可以提取过程的主体，将其传递给 eval 并带上包含形式参数绑定的环境。对于词法作用域，该扩展环境是基于构造过程的 lambda 表达式求值时与过程封装的环境构建的。

```
(define-generic-procedure-handler g:apply
(match-args strict-compound-procedure?)
  operands?
  environment?)
  (lambda operands calling-environment)
  (if (not (= (length (procedure-parameters procedure))
      (length operands)))
    "Wrong number of operands supplied")
    (g:eval (procedure-body procedure)
      (extend-environment)
      (procedure-parameters procedure)
      (eval-operands operands calling-environment)
      (procedure-environment procedure))))
```

在这里，strict-compound-procedure? 对于所有对任何参数没有声明的复合过程为真。

## Driver loop

为了与此评估器交互，我们需要一个读取-求值-打印循环：

```
(define repl)
  (check-repl-initialized)
  (let ((input (g:read))
    (write-line g:eval input the-global-environment)
    (repl)))
```

这里 g:read 发出提示符，eval 在终端执行。它接受字符并将其转换为 s 表达式。该 s 表达式随后相对于 the-global-environment 使用 g:eval 求值，结果写回终端。repl 过程递归调用自己。为了让这工作，全局环境必须初始化：

```
(define the-global-environment)
  'not-initialized)
```

```
(define initialize-repl!)
  (set! the-global-environment (make-global-environment))
  'done
```

```
(define check-repl-initialized)
  (if eq? the-global-environment 'not-initialized)
    error
    "Interpreter not initialized. Run (init) first."))
```

这完成了基础评估器。

# Exercise 5.1: Unbound-variable handling

在 Lisp 中 中，尝试评估未定义的符号是一个未定义错误。然而，在某些代数过程中，允许未定义的符号自求值通常是合理的。例如，如果我们通用地扩展算术以构建表达式（如我们在第 3 章中所做的那样），有时允许以下操作：

```
(+ * 2 3) (* 4 5))
(+ * a 3) (* 4 5))
(+ * a 3) 20
```

我们的通用算术支持符号扩展：运算符 * 和 + 在参数不可还原为数字时被扩展。但它不允许将未定义的变量作为字面数字。在这里符号 a 是未定义的。我们可能希望它是自求值的。

- a. 为 eval 进行通用扩展以允许这种行为。为了让这与原生过程 (+ /) 工作，也有必要扩展它们的行为。注意这些运算符应该在底层 Scheme 环境中更改。

- b. 还要增强 apply，允许运算符位置的未定义符号被解释为仅通过名称知的字面函数：(+ f 3) (* 4 5) => (+ f 3) 20

这些 eval 和 apply 的扩展通常是危险的，因为它们隐藏了真实的未定义错误。让它们取决于用户设置变量的值：allow-self-evaluating-symbols。

# Exercise 5.2: n-ary procedures

第 246 页的脚注 10 指出了我们在 g:apply 处理器中放入的一个糟糕假设，该假设暗示了对此评估器未来扩展限制。在 Scheme 中，如果过程-

