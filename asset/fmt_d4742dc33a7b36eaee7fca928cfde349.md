
`(analyze (if-predicate expression)))`

`consequent-exec`

`(analyze (if-consequent expression)))`

`alternative-exec`

`(analyze (if-alternative expression))))`

`(lambda (environment)`

`(if (x:apply predicate-exec environment)`

`(consequent-exec environment)`

`(alternative-exec environment)))))`

```
```

`(define (analyze-generic-procedure-handler x:analyze)`

`(if?)`

`analyze-if)`

```

要评估的表达式序列是分析与执行分离的一个特别好的示例。没有理由在每次进入过程体时都重新编译表达式序列；这项工作可以在编译时一次完成。

`analyze-begin` 过程首先分析 `begin` 表达式的每个子表达式，生成执行过程列表（保留 `begin` 表达式中表达式的顺序）。然后使用 `reduce-right` 和一个成对组合器这些执行过程连接在一起，该组合器接收两个执行过程并产生一个顺序执行这两个给定执行过程的执行过程。

```
(define (analyze-begin expression)
(reduce-right (lambda (excl exec2)
    (lambda (environment)
      (excl environment)
      (exec2 environment)))
#
(map analyze
  (let ((exps
    (begin-actions expression)))
    (if (null? exps)
      (error "Empty sequence")
    exps))))
```

```
(define (analyze-generic-procedure-handler x:analyze)
```

```
(match-args begin?)
analyze-begin)
```

## 在没有编译器优化的情况下，赋值的处理并不是问题。

```
(define (analyze-assignment expression))
(let ((var
  (assignment-variable expression))
  (value-exec
    (analyze (assignment-value expression))))
  (lambda (environment))
  (set-variable-value! var
    (value-exec environment)
    environment)))
'ok))
```

```
(define-generic-procedure-handler x:analyze
(match-args assignment?)
analyze-assignment)
```

如果需要进行编译器优化，赋值就会带来严重的问题。事实上，赋值为程序引入了“时间”的概念：某些事情发生在赋值之前，另一些发生在赋值之后，而赋值可能会改变引用被修改变量的事件。因此，例如，如果公共子表达式引用了一个可以被赋值的变量，它们可能并不真的具有相同的值！

定义并不是问题，除非我们将它们（并错误地使用）视为赋值，从而可能干扰编译器优化。

```
(define (analyze-definition expression))
(let ((var
  (definition-variable expression))
  (value-exec
    (analyze (definition-value expression))))
  (lambda (environment))
  (define-variable! var
    (value-exec environment)
    environment)))
var)))
```

```
(define-generic-procedure-handler x:analyze
(match-args definition?)
analyze-definition)
```

```
(define-generic-procedure-handler x:analyze
(match-args cond?)
(compose analyze->if)
```

## 过程的应用

应用的执行过程会调用操作数的执行过程，以获取要调用的复合过程。（参见第 260 页的 `analyze-application`）。操作数也被转换成了执行过程。

过程 `x:apply` 与初级评估器中的 `g:apply`（见第 245 页）是类似的：

```
(define x:apply
(simple-generic-procedure 'x:apply 3 default-apply))
```

```
(define default-apply procedure operand-execs environment
(error "Unknown procedure type") procedure)
```

注意，这里的 `default-apply` 与 `g:apply` 使用的两个未使用参数的名称是相同的。

与之前一样，我们需要为各种类型过程的应用提供处理器，特别是特定类型的参数。严格原生过程的应用处理器必须强制强制执行参数，然后执行该原生过程。

```
(define-generic-procedure-handler x:apply
(match-args strict-primitive-procedure?
executors?
environment?)
(lambda (procedure operand-execs environment))
```

```
(apply-primitive-procedure procedure)
(map (lambda operand-exec)
  (x:advance (operand-exec environment))
  operand-execs)))
```

## 通用过程的应用处理器与之前展示的初级评估器中的处理器略有不同。区别在于，我们处理的是执行过程，而不是操作数表达式。

```
(define-generic-procedure-handler x:apply)
(match-args compound-procedure? executors? environment?)
(lambda (procedure operand-execs calling-environment)
  (if (not (n:= (length (procedure-parameters procedure))
                (length operand-execs))
      (error "Wrong number of operands supplied"))
      (let ((params (procedure-parameters procedure))
            (body-exec (procedure-body procedure))
            (let ((names map procedure-parameter-name params))
              (arguments
                (map (lambda param operand-exec
                  (x:handle-operand param
                    operand-exec
                    calling-environment))
                operand-execs))
              (body-exec (extend-environment names arguments)
                (procedure-environment procedure))))))))
```

这个复合过程的应用处理器需要能够处理复合过程中可能存在的各种类型的形式参数。这是通过我们通常的方法，将 `x:handle-operand` 为一个通用过程来实现的。在进入复合过程的主体之前评估操作数的默认方法是立即执行操作数执行过程以获取一个值。然而，惰性参数和记忆化的惰性参数需要适当地推迟执行。

```
(define x:handle-operand)
(simple-generic-procedure 'x:handle-operand 3
(lambda (parameter operand-exec environment)
  (operand-exec environment)))
```

```
(define-generic-procedure-handler x:handle-operand
(match-args lazy?) executor? environment?)
(lambda (parameter operand-exec environment)
(postpone operand-exec environment))
```

```
(define-generic-procedure-handler x:handle-operand
(match-args lazy-memo?) executor? environment?)
(lambda (parameter operand-exec environment)
(postpone-memo operand-exec environment))
```

推迟操作数的执行过程与推迟操作数表达式是相同的。但处理推迟执行过程的通用过程 `x:advance` 处理器与 `g:advance` 不同：推迟的执行过程必须在推迟的环境上调用，而不是相对于该环境进行评估（对比第 253 页的 `g:advance`）。

```
(define-generic-procedure-handler x:advance
(match-args postponed?)
(lambda (object)
(x:advance ((postponed-expression object))
(postponed-environment object))))
```

```
(define-generic-procedure-handler x:advance
(match-args postponed-memo?)
(lambda (object)
(let ((value
(x:advance ((postponed-expression object))
(postponed-environment object))))
(advance-memo! object value)
value)))
```

此 `x:apply` 中操作数的处理并不非常巧妙。事实上，它对执行过程中的形式参数列表进行了大量的“解析”，因此我们没有完全编译复合过程。改进这种编译的一个步骤是像我们之前那样，将严格复合过程的处理器分离出来。修复这个棘手问题是你在练习 5.16 中的任务。

## 练习 5.12：实现 n 元过程

在第 5.2 和 5.11 练习中，我们注意到，拥有一个可以接受不定数量参数的过程通常是有价值的。Scheme 中的加法和乘法过程就是此类过程的示例。

在 Scheme 中定义这样的过程，我们将形式参数指定为单个符号而不是列表。该符号将绑定到提供的列表。例如，为了编写一个接受多个参数并返回平方列表的过程，我们可以写道：

```
(lambda x (map x))
```

或者

```
(define (ss . x) (map x))
```

然后我们可以说：

```
(ss 1 2 3 4) => (4 9 16)
```

修改分析器以允许这一点。提示：你不需要更改涉及 `lambda` 的代码！这完全是分析器的更改。证明你的修改允许这一点，并且不会引起其他问题。

## 练习 5.13：简化调试

这个编译器的一个问题是执行过程都是匿名表达式。因此，几乎没有信息可以供回溯报告。然而，改进这些情况很容易。如果我们重写为应用创建执行过程的过程：

```
(define analyze-application exp)
(let ((operator-exec (analyze (operator exp)))
(operand-execs (map analyze (operands exp))))
(lambda (env)
(x:apply (x:advance operator-exec env)
env)))
```
