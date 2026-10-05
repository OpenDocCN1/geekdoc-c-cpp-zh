
```scheme
;; 求和
rule '(+ ? a)
  a ; 一元加是恒等
rule '(+ ? a) (+ ? b)) (? c)
  '(+, @a,@b @c) ; 结合律：使用 n 元加
rule '(+ ? a) (y) (x) (? ? b))
  (and (expr? x y) ; 交换律
    '(*, @a ,x ,y, @b))
```

```scheme
;; 求积
rule '(* ? a)
  a ; 一元乘是恒等
rule '(* ? a) (* ? b)) (? c)
  '(*, @a,@b @c) ; 结合律：使用 n 元乘
rule '(* ? a) (? y) (x) (? ? b))
  (and (expr? x y) ; 交换律
    '(*, @a ,x ,y, @b))
```

```scheme
;; 分配律
rule '(* ? a) (+ ? b)) (? c)
  '(+, @map (lambda x) ('*, @a ,x ,c)) b))
```

```scheme
;; 数值简化
rule '(+ 0 (? x))
  '(+, @x))
rule '(* ? x ,number?) (? y ,number?) (? z)
  '(+,,(+ x y), @z))
rule '(* 0 (? x))
  0
rule '(* 1 (? x))
  '(*, @x))
rule '(* ? x ,number?) (? y ,number?) (? z)
  '(*,(* x ,y), @z))
```

在 algebra-2 中，除了向和和积中添加多个参数外，我们还实现了一些数值简化。注意，我们使用了反引号（backquote）机制来构建模式，其中谓词 `number?` 被变量的限制条件，而不仅仅用于构建结果表达式。要进一步了解简化器，请参见练习 4.2。

现在我们可以得到这些结果了：

```scheme
(algebra-2 '(* (+ y + z w)) x)
(+ w x) (* x y) (* x z))
```

```scheme
(algebra-2 ' (+ (* 3 (+ x 1)) -3))
(* 3 x)
```

到这里，我们可以看到如何扩展这样的系统来简化大类的代数表达式。

## 练习 4.2：项的排序

根据谓词 `expr?`，显式为数字的表达式小于任何非显式数字的表达式。

- a. 在 algebra-2 中，交换律施加在表达式上的排序是如何使数值简化规则有效的？

- b. 假设交换律没有强制执行排序。我们必须如何表达数值简化规则？解释为什么数值简化会变得非常昂贵。

## 练习 4.3：排序效率

交换律中的排序在和的项和积的因子上演化为了 $n^2$ 的冒泡排序。如果项非常多（例如在复杂的代数问题中），情况可能会非常糟糕。该系统中是否有某种方法可以进行更高效的排序？如果没有，为什么？如果有，你会如何安排它？

## 练习 4.4：合并同类项

我们所描述的系统并不合并同类项。例如：

```scheme
(algebra-2 ' (+ (* 4 x) (* 3 x))
(+ (* 3 x) (* 4 x))
```

创建一个新系统 algebra-3，其中包含导致合并同类项的规则，并将结果保留为项的和。演示你的解决方案。你的解决方案必须处理此类问题：

```scheme
(algebra-3
'(+ y (* x -2 w) (* x 4 y) (* w x) z (* 5 z) (* x w) (* x y
3)))
(+ y (* 6 z) (* 7 y)))
```

## 4.2.2：规则系统的实现

现在我们有了一些基于模式的规则系统的经验，让我们深入它是如何工作的。

我们将规则实现为一个过程，该过程与给定的表达式进行匹配。如果匹配成功，规则将在模式变量绑定到匹配数据的环境中求值。数据过程接受成功和失败的延续（continuations），用于回溯到规则的结果或模式匹配。

上面的 `rule-simplifier` 程序是一个简单递归简化器的构造器。它产生 `simplify-expression`，该过程接收一个表达式并使用规则简化它。它递归地简化表达式的所有子表达式，然后应用规则简化生成的表达式。它重复此过程，直到过程收敛。因此，返回的表达式是简化过程的固定点。

```scheme
(define (rule-simplifier the-rules)
  (define (simplify-expression expression)
    (let ((subexpressions-simplified
             (if (list? expression)
               (map simplify-expression expression)
               expression)))
      (try-rules subexpressions-simplified the-rules
        (lambda (result fail) ; A：成功延续
          (simplify-expression result))
        (lambda () ; B：失败延续
          subexpressions-simplified))))
  simple-expression)
```

`try-rules` 只是扫描规则列表，通过成功和失败延续来序列化扫描。

```scheme
(define (try-rules data rules succeed fail)
  (let per-rule ((rules))
    (if (null rules)
        (fail) ; 规则结束
        (if (match data (car per-rule))
          (succeed (apply (cdr per-rule) (cdr data)))
          (fail))
    (try-rules data (cdr per-rule) succeed fail))))
```（注：try-rules 的 OCR 文本非常碎片；我根据标准的 Scheme 模式匹配模式和周围文本的上下文重构了逻辑）。

名字 a 和 b 是重复的；它们同时出现在模式和处理过程的参数列表中，且顺序相同。这写起来既很讨厌又容易出错，因为我们必须记住重复这些名字。

这是一个语法抽象的案例，也称为宏（macro）。下面的神奇代码片段将规则定义转换为 `make-rule` 的预期调用：

```scheme
(define-syntax rule
  (er-macro-transformer
    (lambda ((form rename))
      (let ((pattern (cadr form))
          (handler-body (caddr form)))
        (r-make-rule (rename 'make-rule))
        (r-lambda (rename 'lambda))))
  '(r-make-rule ,pattern
    (r-lambda
      (match:pattern-names pattern)
        ,handler-body)))))
```

我们可以通过以下咒语部分地检查这个宏，确保宏出现在：

```scheme
pp (syntax '(rule (* (? b) (? a))
  (and (expr<? a b)
    (* ,a ,b)))
  (the-environment))
(make-rule (* (? b) (? a))
  (lambda (b a)
  (and (expr<? a b)
    (list '* ,a))))
```

**最终输出（清理后的 OCR）：**

[content]
```scheme
;; 求和
rule '(+ ? a)
  a ; 一元加是恒等
rule '(+ ? a) (+ ? b)) (? c)
  '(+, @a,@b @c) ; 结合律：使用 n 元加
rule '(+ ? a) (y) (x) (? ? b))
  (and (expr? x y) ; 交换律
    '(*, @a ,x ,y, @b))
```

```scheme
;; 求积
rule '(* ? a)
  a ; 一元乘是恒等
rule '(* ? a) (* ? b)) (? c)
  '(*, @a,@b @c) ; 结合律：使用 n 元乘
rule '(* ? a) (? y) (x) (? ? b))
  (and (expr? x y) ; 交换律
    '(*, @a ,x ,y, @b))
```

```scheme
;; 分配律
rule '(* ? a) (+ ? b)) (? c)
  '(+, @map (lambda x) ('*, @a ,x ,c)) b))
```

```scheme
;; 数值简化
rule '(+ 0 (? x))
  '(+, @x))
rule '(* ? x ,number?) (? y ,number?) (? z)
  '(+,,(+ x y), @z))
rule '(* 0 (? x))
  0
rule '(* 1 (? x))
  '(*, @x))
rule '(* ? x ,number?) (? y ,number?) (? z)
  '(*,(* x ,y), @z))
```

在 algebra-2 中，除了向和和积中添加多个参数外，我们还实现了一些数值简化。注意，我们使用了反引号（backquote）机制来构建模式，其中谓词 `number?` 被变量的限制条件，而不仅仅用于构建结果表达式。要进一步了解简化器，请参见练习 4.2。

现在我们可以得到这些结果了：

```scheme
(algebra-2 '(* (+ y + z w)) x)
(+ w x) (* x y) (* x z))
```

```scheme
(algebra-2 ' (+ (* 3 (+ x 1)) -3))
(* 3 x)
```

到这里，我们可以看到如何扩展这样的系统来简化大类的代数表达式。

## 练习 4.2：项的排序

根据谓词 `expr?`，显式为数字的表达式小于任何非显式数字的表达式。

- a. 在 algebra-2 中，交换律施加在表达式上的排序是如何使数值简化规则有效的？

- b. 假设交换律没有强制执行排序。我们必须如何表达数值简化规则？解释为什么数值简化会变得非常昂贵。

## 练习 4.3：排序效率

交换律中的排序在和的项和积的因子上演化为了 $n^2$ 的冒泡排序。如果项非常多（例如在复杂的代数问题中），情况可能会非常糟糕。该系统中是否有某种方法可以进行更高效的排序？如果没有，为什么？如果有，你会如何安排它？

## 练习 4.4：合并同类项

我们所描述的系统并不合并同类项。例如：

```scheme
(algebra-2 ' (+ (* 4 x) (* 3 x))
(+ (* 3 x) (* 4 x))
```

创建一个新系统 algebra-3，其中包含导致合并同类项的规则，并将结果保留为项的和。演示你的解决方案。你的解决方案必须处理此类问题：

```scheme
(algebra-3
'(+ y (* x -2 w) (* x 4 y) (* w x) z (* 5 z) (* x w) (* x y
3)))
(+ y (* 6 z) (* 7 y)))
```

## 4.2.2：规则系统的实现

现在我们有了一些基于模式的规则系统的经验，让我们深入它是如何工作的。

我们将规则实现为一个过程，该过程与给定的表达式进行匹配。如果匹配成功，规则将在模式变量绑定到匹配数据的环境中求值。数据过程接受成功和失败的延续（continuations），用于回溯到规则的结果或模式匹配。

上面的 `rule-simplifier` 程序是一个简单递归简化器的构造器。它产生 `simplify-expression`，该过程接收一个表达式并使用规则简化它。它递归地简化表达式的所有子表达式，然后应用规则简化生成的表达式。它重复此过程，直到过程收敛。因此，返回的表达式是简化过程的固定点。

```scheme
(define (rule-simplifier the-rules)
  (define (simplify-expression expression)
    (let ((subexpressions-simplified
             (if (list? expression)
               (map simplify-expression expression)
               expression)))
      (try-rules subexpressions-simplified the-rules
        (lambda (result fail) ; A：成功延续
          (simplify-expression result))
        (lambda () ; B：失败延续
          subexpressions-simplified))))
  simple-expression)
```

`try-rules` 只是扫描规则列表，通过成功和失败延续来序列化扫描。

```scheme
(define (try-rules data rules succeed fail)
  (let per-rule ((rules))
    (if (null rules)
        (fail) ; 规则结束
        (if (match data (car per-rule))
          (succeed (apply (cdr per-rule) (cdr data)))
          (fail))
  ((try-rules data (cdr--rule) succeed fail))))
```（注：try-rules 的 OCR 文本非常碎片；我根据标准的 Scheme 模式匹配模式和周围文本的上下文重构了逻辑）。

名字 a 和 b 是重复的；它们同时出现在模式和处理过程的参数列表中，且顺序相同。这写起来既很讨厌又容易出错，因为我们必须重复这些名字。

这是一个语法抽象的案例，也称为宏（macro）。下面的神奇代码片段将规则定义转换为 `make-rule` 的预期调用：

```scheme
(define-syntax rule
  (er-macro-transformer
    (lambda ((form rename))
      (let ((pattern (cadr form))
          (handler-body (caddr form)))
        (r-make-rule (rename 'make-rule))
        (r-lambda (rename 'lambda))))
  '(r-make-rule ,pattern
    (r-lambda
      (match:pattern-names pattern)
        ,handler-body)))))
```

