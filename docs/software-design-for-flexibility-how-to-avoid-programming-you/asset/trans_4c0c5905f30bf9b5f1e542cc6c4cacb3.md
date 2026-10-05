

```scheme
(success ((a z z z)) ??) 3)
#f
```

现在，回到已经有值的分段变量的情况，我们需要确保该值与数据的初始分段匹配。这会将值中的元素与数据进行比较。如果成功，它将通过调用 `ok`（作为第三个参数传递的过程）来返回，参数是从数据中消耗的元素个数（这必须等于值的长度）；否则，它返回 `#f`。

```scheme
(define (match:segment-equal? data value ok)
  (let lp ((data data) (value value) (n 0))
    (cond ((pair? data)
           (if (and (pair? data) (car data) (car value))
               (lp (cdr data) (cdr value) (+ n 1))
               #f))
          (null? value) (ok n)
          (else #))))
```

## 匹配列表

最后是 `match:list` 组合器，它接收一个匹配过程列表，并产生一个匹配过程。当且仅当给定的匹配消耗了数据列表中的所有元素时，该过程才会匹配数据列表。它按顺序应用匹配。每个匹配都会告诉列表组合器，在将剩余数据传递给下一个匹配器之前，需要跳过多少项。

```scheme
(define (match:list matches)
  (define (list-match data dictionary succeed)
    (and (pair? data)
        (let lp ((data-list (car data))
                (matchers matches))
              (dictionary dictionary))
          (cond ((pair? matches)
                ((car matches))
                data-list
                dictionary
                (lambda (new-dictionary n))
                  ;; 列表匹配的本质
                  (lp (list-tail data-list n))
                  (cdr matches)))))
      new-dictionary))))
      ((pair data-list) #f ;未匹配的数据
      ((null? data-list) succeed dictionary 1))
      (else #f)))
    list-match)
```

注意 `match:list` 组合器返回的匹配器 `list-match` 与匹配匹配具有完全相同的接口，允许它被整合到组合中。所有基础匹配过程具有完全相同的接口，这一事实使其成为了一个组合器系统。

现在，我们可以通过组合创建一个匹配器，它可以匹配任意数量元素的列表，以符号 `a` 开头，以符号 `b` 结尾，并在之间有一个分段变量 `(?? x)`：

```scheme
(match:list list (match:eqv 'a
    (match:segment '$(?? x))
    (match:eqv 'b)))
```

```scheme
'((a 1 2 b))
(matchnew-dict)
result-receiver)
(success ((x 1 2) ??)) 1)
```

这是一个成功的匹配。返回的字典恰好有一个条目：`x=(1 2)`，且匹配从提供的列表中精确地匹配了一个元素（列表 `a 1 2 b`）。

```scheme
(match:list list (match:eqv 'a
    (match:segment '$(?? x))
    (match:eqv 'b)))
```

```scheme
'((a 1 2 b 3))
(matchnew-dict)
result-receiver)
#f
```

这是一个失败的匹配，因为在输入数据中 `b` 之后没有可以匹配 `3` 的内容。

## 字典

我们将使用的字典只是绑定的头部列表（headed list）。每个绑定都是包含变量名、其值和类型的列表。

```scheme
(define (match:new-dict))
  (list 'dict))
```

```scheme
(define (match:bindings dict))
  (cdr dict))
```

```scheme
(define (match:new-bindings dict bindings))
  (cons 'dict bindings))
```

```scheme
(define (match:extend-dict var value dict)
  (match:new-bindings dict
    (cons (match:make-binding var value)
      (match:bindings dict))))
```

```scheme
(define (match:lookup var dict))
  (let ((name var)
        (if (symbol? var)
          (match:var-name var)))
    (find (lambda (binding)
      (eq? name (match:binding-name binding))
      (match:bindings dict))))))
```

```scheme
(define (match:make-binding var value))
  (list (match:var-name var)
    value
    (match:var-type var)))
```

```scheme
(define (match:binding-name car))
(define (match:binding-type caddr))
```

```scheme
(define (match:binding-value))
  (simple-generic-procedure 'match:binding-value 1 caddr))
```

访问器 `match:binding-value` 仅仅是 `caddr`，但它是通用的，允许未来的扩展。这在支持 4.5 的代码中是需要的。

## 4.3.1 编译模式

我们可以使用一个基础编译器从模式自动构建模式匹配器。编译器产生的值是一个适用于其给定模式的匹配过程，该过程与上面提供的基础匹配器具有完全相同的接口。

匹配过程接口对于组合匹配器非常方便，但对人类并不友好。为了测试匹配器，使用以下方式更方便：

```scheme
(define (run-matcher match-procedure datum succeed)
  (match-procedure (list datum)
    (match:new-dict)
    (lambda (dict)
      (and (= n 1))
      (succeed dict))))
```

通过这种接口，我们隐藏了关于匹配过程的几个细节：我们将输入的数据封装在列表中；我们检查是否恰好有一个元素被匹配；我们提供了初始字典。一些简单的例子如下：

```scheme
(run-matcher
  (match:compile-pattern '(a ((? b) 2 3) (? b) c))
  '(a (1 2 3) 1 c)
  match-bindings)

```
(run-matcher
  (match:compile-pattern '(a ((? b) 2 3) (? b) c))
  '(a 1 2 3))

正如之前看到的，涉及分段变量的模式可能有多种匹配方式，我们可以通过让匹配失败来触发下一个匹配，直到它们耗尽：

```scheme
(run-matcher
  (match:compile-pattern '(a ((? x) (??) (? x) c))
  '(a b b c)
  print-all-matches)
  ((y b b) ??) (x ??))
  ((y b b) ??) (x b) ??)
  ((y b) ??) (x b) ??)
  ((y) ??) (x b) ??))
```

可能的匹配要求 `(??)` 的两个实例匹配相同的数据。`print-all-matches` 过程强制执行失败。

```scheme
(define (print-all-matches dict)
  (pp dict)
  #f)
```

为了制作这个编译器，我们需要定义模式变量的语法。目前我们有一个简单的语法：模式变量是一个包含类型 `??` 和名的列表。

```scheme
(define (match:var-type var)
  (car var))
```

```scheme
(define (match:var-type object)
  (memq object match-types))
```

```scheme
(define (match-types '((??)))
```

```scheme
(define (match:named-var object)
  (and (pair? object)
    (match:var-type (car object))
    (>= (length object) 2)
    (symbol? (cadr object))))
```

```scheme
(define (match:element-var object)
  (and (match:var object)
    (eq? '? (match:var-type object))))
```

```scheme
(define (match:segment-var object)
  (and (match:var object)
    (eq? '?? (match:var-type object))))
```这段代码比预期的要复杂，因为我们将在 4.5 节和一些练习中扩展变量语法。

```scheme
(define (match:var-name)
  (simple-generic-procedure 'match:var-name
    (constant-generic-procedure-handler #f)))
```

```scheme
(define (generic-procedure-handler match:var-name)
  (match-args match:named-var?)
  cadr)
```

默认处理器是一个始终返回假的过程，目前只有一个实质性的处理器，用于检索命名变量的名字。我们还将判断参数是否为匹配变量的谓词变为通用的，尽管目前满足 `match:var?` 的对象只有命名变量。

```scheme
(define match:var?
  (simple-generic-procedure 'match:var? 1)
  (constant-generic-procedure-handler #f)))
```

```scheme
(define (generic-procedure-handler match:var?)
  (match-args match:named-var?)
  (constant-generic-procedure-handler #t))
```

# 编译器将模式映射到对应的匹配器：

```scheme
(define (match:compile-pattern pattern)
  (cond ((match:var? pattern)
         (case (match:var-type pattern)
          ((?)) (match:element pattern))
          ((???) (match:segment pattern))
          (else (error "Unknown var type:" pattern))))
         (list? pattern)
         (match:list (map match:compile-pattern pattern)))
         (else ; 常量
         (match:eqv pattern))))
```

通过改变这个编译器，我们可以任意地改变模式的语法。

```scheme
(run-matcher
  (match:compile-pattern '(a ((? b) 2 3) (? b) c))
  '(a (1 2 3) 1 c)
  match-bindings
  ((b 1 ?)))
```

## 练习 4.5：回溯

在 177 页的示例中，我们得到了多个匹配，从成功过程 `print-all-matches` 返回了 `#f`。这可能相当神秘。它是如何工作的？请用简短但清晰的段落解释匹配序列是如何生成的。

## 4.3.2 匹配变量限制

我们通常想要限制模式变量可以匹配的对象类型。例如，我们可能想创建一个模式，其中变量只能匹配正整数。实现此点的一种方法（我们在 4.2.1 节的术语重写系统中使用过）是允许变量携带一个谓词来测试数据的可接受性。例如，我们可能对正弦函数的正幂感兴趣。我们可以这样写我们需要的模式：

```scheme
(expt (sin (? x)) (? n ,exact-positive-integer))
```

我们不能对这种模式使用引号，因为谓词表达式（此处为 `exact-positive-integer?`）必须在包含在模式之前进行求值。在重写（4.2节）中，我们使用反引号机制。

为了创建一个检查数据是否满足此类谓词的匹配器，我们在 `match:element` 中添加了一行：

```scheme
(define match:element variable)
(define element-match data dictionary)
  (and (pair? data)
    (match:satisfies-restriction variable (car data))
    (let ((binding match:binding variable dictionary))
      (if binding
          (and (equal? (match:binding-value binding)
            (car data))
            (succeed dictionary 1))
          (succeed (match:extend-dict variable
            (car data)
            dictionary)))))
```

```scheme
element-match
```

```scheme
(define match:satisfies-restriction? var value)
  (or (not (match:var-has-restriction? var))
    ((match:var-restriction var) value)))
```

