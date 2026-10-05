
操作符规则模式。匹配规则的后续部分（consequent）计算要返回的值。
例如，我们可以编写传统的阶乘过程，将条件分布如下：

```
(define factorial
(make-pattern-operator
  (rule `'0) 1)
  (rule `((? n ,positive?))
    (* n (factorial (- n 1)))))
```

```
(factorial 10)
3628800
```

我们还可以使用这种机制来构建其行为取决于所提供参数数量的过程。例如，Lisp 中的 `-` 运算符在应用于一个参数时是取反，在应用于多个参数时是减法：

```scheme
(define -
(make-pattern-operator
  (rule `((? x)) (n:- x))
  (rule `((? x) (? y)) (n:- (apply n:+ y)))))
```

我们允许动态地通过额外的规则扩展模式操作符。此类操作符类似于通用过程（generic procedures），允许程序员在非本地范围内分布规则定义。例如，在孔洞优化器（peehole optimizer）中，我们可能希望将各种优化操作与编译器代码生成器的不同部分分组。

```
(define peehole (make-pattern-operator))
```

```
(attach-rule! peehole
  (rule `'((push ? regl))
    (pop (? reg2))
    (if eqv? reg reg2
      ()
      '(move ,reg1 ,reg2))))
```

```
(attach-rule! peehole
  (rule `'((or ? reg) (? const1 ,unsigned-integer?))
    ((or ? reg) (? const2 ,unsigned-integer?))
    '(or ,reg
      (bitwise-or const1 const2)))))
```

第一条规则可以位于优化器的控制结构部分，而第二条规则可以位于优化器的逻辑算术部分。

这是实现模式操作符的一种方法。传递给 `make-pattern-operator` 的最后一个规则是默认规则。无论后来添加了什么其他规则，它总是会被尝试。

```
(define (make-pattern-operator rules)
(let ((rules
  (cons 'rules
    (if (pair? rules)
      (except-last-pair rules)
      '())))
(default-rule
  (and (pair? rules)
    (last rules))))
(define (the-operator data)
  (define (succeed value fail) value)
  (define fail
    (error "No applicable operations:" data))
(try-rules data
  (cdr rules)
    succeed
    (if default-rule
      (lambda ()
        (try-rule data
          default-rule
            succeed
            fail))))
(set-pattern-metadata! the-operator rules)
```

我们使用 `set-pattern-metadata!` 将规则列表作为“便签”附加到操作符上，并在下面的代码中使用 `pattern-metadata` 来检索它。我们有过程向操作符规则列表的头部（`override-rule!`）或末尾（`attach-rule!`）添加规则：

```
(define (attach-rule! operator rules)
(let ((metadata (pattern-metadata operator)))
  (set-cdr metadata
    (append (cdr metadata)
      (list rule))))
```

```
(define override-rule operator rule)
(let ((metadata (pattern-metadata operator)))
  (set-cdr metadata)
  (cons rule (cdr metadata))))
```

## 4.3 匹配器的设计

现在我们已经看到了模式匹配的一些强大之处，我们将开始探索它是如何工作的。我们的匹配器由一组匹配过程（或称为匹配器）以及一些将它们组合以产生复合匹配器的组合器（combinators）构造而成。³ 模式中的每个原始元素都由一个原始匹配器表示，而唯一的组合——列表，则由一个组合列表元素匹配器的组合器来表示，以形成一个复合匹配器。所有匹配过程都接受三个参数：一个包含要匹配数据的列表、一个模式变量的绑定字典，以及一个在匹配成功时被调用的延续过程（`succeed`）。`succeed` 的参数必须是匹配结果产生的新字典，以及从输入列表中消耗的项数。该数字将用于确定在分段匹配返回后继续继续到何处。如果匹配失败，匹配过程将返回 `#f`。

有三个原始匹配过程和一个组合器。让我们过一遍它们。我们还需要一个很小的过程，可以将其作为参数传递给匹配过程以报告结果：

```
(define (result-receiver dict n-eaten)
 '(succeed ,(match:bindings dict) ,n-eaten))
```

## 模式常量

`match:eqv` 过程接受模式常量（例如 `x`），并产生一个匹配过程 `eqv-match`，当且仅当第一个数据项与模式常量相等（使用 `eqv?`）时，该过程将成功。它不会向字典添加内容。`succeed` 的第二个参数是匹配的项数，对于此匹配过程该数值为 1。

```
(define match:eqv pattern-constant)
(define eqv-match data dictionary succeed)
(and (pair? data)
(eqv? (car data) pattern-constant)
(succeed dictionary 1)))
eq-match)
```

## 示例：

```
(define x-matcher (match:eqv 'x))
```

```
(x-matcher ' (x))
```

```
(x-matcher ' (y))
(match-dict)
(result-receiver)
```

## 元素变量

`match:element` 过程用于创建一个匹配过程，针对模式变量（例如 `x`），该过程当且仅当匹配单个项时成功。它不会向字典中添加新项。`succeed` 的第二个参数是匹配的项数，对于此匹配过程为 1。如果变量有值，则将其绑定到字典；如果没有，则不添加。

```
(define match:element variable)
(define (element-match data succeed)
(and (pair? data)
  (let ((binding (lookup variable dictionary)))
    (if binding
      ((- (--(
-data)
        )
        (match-value binding)
        (lambda (n) (succeed (length dictionary))
      (let ((n (length data))
        (let ((i 0))
          (and ( succeed (match-dict-dict

variable(list(head-)

            )

            i

(          (lp 1))))1
```

## 段变量

针对变量（例如 `??`）的段匹配器用于匹配项序列。段匹配器比元素匹配器更复杂，因为它可以消耗未知数量的项。因此，段匹配器不仅要通知调用者新的字典，还要通知从数据中消耗了多少项。当匹配段变量时，有两种可能：变量已经有值，或者还没有。如果变量有值，则通过 `match-segment-equal?` 对数据进行检查（从 `i=0` 开始，假设段不消耗项）。然而，如果该成功导致后续匹配失败，段匹配器会尝试比已经消耗的多消耗一个项（通过执行 `(+ i 1)`）。如果段匹配器用完了数据项，则匹配失败。

```
(define (match:segment variable)
(define (match-segment data succeed)
(and (list? data)
  (let ((binding (lookup variable dictionary)))
    (if binding
      (match-segment-equal?
        data
        (match-value binding)
        (lambda (n) (succeed (length dictionary))))
      (let ((n (length data))
        (let ((i 0))
          (and ( succeed (match-extend-dict
            variable
            (list-head data i)
            dictionary)
            i))
          (lp (+ i 1))))))))```

这里有一些示例：

```
((match:segment '?? a))
'(z z) (match:new-dict) result-receiver)
(success ((a () ??)) 0)
```

当然，零长度段是可以接受的。如果我们想看到所有可能的匹配，可以让结果接收器在打印成功结果后返回 `#f`。这将导致匹配过程产生另一种替代值。

```
(define (print-all-results dict n-eaten)
(pp '(success ,(match-bindings dict) ,n-eaten))
;; 返回 #f 我们强制回溯。
#f)
```

```
((match:segment '?? a))
'(z z) (match:new-dict) print-all-results)
(success ((a () ??)) 0)
(success ((a (z) ??)) 1)
(success ((a (z z) ??)) 2)
```
