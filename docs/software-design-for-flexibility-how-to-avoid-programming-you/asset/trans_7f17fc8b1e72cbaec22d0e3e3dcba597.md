
(lambda (expression environment) expression))

在 Lisp 语言中，自求值表达式包括数字、布尔值和字符串。在 Scheme 中，`number?` 是一个复杂的谓词。满足 `number?` 的对象包括任意大小的整数、分数和复数.^4

```
(define (self-evaluating? exp)
  (or number? exp)
  (boolean exp)
  (string exp?))
```

可能还有其他的自求值表达式，为了使其具有真正的灵活性，我们可以将 `self-evaluating?` 定义为一个通用过程。但在这里没有必要，因为我们只需要为 `g:eval` 编写另一个处理器来定义我们可能想要添加的任何自求值表达式类型。

在允许操作语言符号表达式的语言中，引用是必须的.^5 引用是从求值过程中产生子表达式的表达式。

```
(define-generic-procedure-handler g:eval
  (match-args quoted environment?)
  (lambda (expression environment))
    (text-of-quotation expression)))
```

在基于 Lisp 的语言中，引用表达式的列表结构表示是一个带有关键字 `quote` 的列表。Lisp 的读取器（解析器）会将任何以撇号字符开头的表达式（例如 `'(a b c)`）展开为引用表达式（即 `(quote (a b c))`）。

```
(define (quoted? exp) (tagged-list? exp 'quote))
(define (text-of-quotation quote) (cadr quote))
```

## 标记列表只是以给定的唯一符号开头的列表：

```
(define (tagged-list? e t) (and (pair? e) (eq? (car e) t)))
```

Scheme 变量直接在环境中查找。在其他语言中，变量有更复杂的规则。例如，在 C 语言中存在左值（lvalues）和右值（rvalues），它们的处理方式不同。

```
(define-generic-procedure-handler g:eval
  (match-args? environment?)
  lookup-variable-value)
```

在基于 Lisp 的语言中，变量由符号表示。⁶

```
(define variable? exp (symbol? exp))
```

过程 `lookup-variable-value` 在给定的环境中查找其参数。如果没有找到该变量的值，它会在底层的 Scheme 中查找值.^⁷ 如果没有找到值，则会抛出 Unbound（未绑定）错误。

二元条件表达式（if-then-else）有一个简单的处理器。如果表达式的谓词部分求值为真，则求值表达式的后续部分，否则求值表达式的备选部分。

```
(define-generic-procedure-handler g:eval
  (match-args? environment?)
  (lambda (expression environment))
    (if g:advance
      (g:eval (if-predicate expression environment))
      (g:eval (if-consequent expression environment))
      (g:eval (if-alternative expression environment))))
```

我们必须对求值的谓词调用 `g:advance`，因为我们需要知道值来做决策。注意，`if` 的求值器使用了嵌入语言的构造来完成工作！

`if` 表达式的语法非常简单。如果没有指定备选部分，谓词为假的 `if` 表达式的值为全局变量 `the-unspecified-value` 的值。

```
(define (if? exp (tagged-list? exp '))
(define (if-predicate exp) (cadr exp))
(define (if-consequent exp) (caddr exp))
```

```
(define (if-alternative exp)
  (if (not (null? (cdddr exp)))
    (cadddr exp)))
```

```
(define (make-if pred conseq alternative)
  (list 'if pred conseq alternative))
```

第一个真正有趣的特殊形式是匿名过程的规范，由 lambda 表达式表示。lambda 表达式是一个特殊形式，是过程的构造器。
