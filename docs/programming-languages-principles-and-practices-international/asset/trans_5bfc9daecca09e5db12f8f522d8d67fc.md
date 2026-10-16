

最后，我们给出使用 `car` 和 `cdr` 访问二叉搜索树的元素的例子，该树被定义为具有结构 `(data leftchild rightchild)` 的列表：

```
```scheme
(define (leftchild B) (car (cdr B)))
(define (rightchild B) (car (cdr (cdr B))))
(define (data B) (car B))
```
```

现在我们可以编写一个树遍历过程 `print-tree`，它按如下方式打印树中的数据：

```
```scheme
(define print-tree (lambda (B)
  (cond ((null? B) '())
        (else (print-tree (leftchild B))
              (display (data B))
              (newline)
              (print-tree (rightchild B))))))
```
```

## 3.2.5 Scheme 中的编程技术

在 Scheme 中，就像在任何函数式语言中一样，递归用于执行循环和其他重复操作。 将重复操作应用于列表的一种标准技术是“cdr 向下，cons 向上”——意思是我们递归地将操作应用于列表的尾部，然后使用 cons 操作符收集结果，通过构造一个包含当前结果的新列表。 一个例子是前一节的 append 过程代码。 另一个例子是用于对数字列表中的所有成员进行平方的过程：

```
```scheme
(define square-list (lambda (L)
  (if (null? L) '()
      (cons (* (car L) (car L)) (square-list (cdr L))))))
```
```

一个不应用于列表的循环的例子是一个过程，它只是从下界到上界打印整数的平方：

```
```scheme
(define print-squares (lambda (low high)
  (cond ((> low high) '())
        (else (display (* low low))
              (newline)
              (print-squares (+ 1 low) high)))))
```
```

对 `(print-squares 1 100)` 的调用将生成所需的结果。

在 print-squares 示例中，我们必须使用额外的参数 `low` 来控制递归，就像循环索引控制重复一样。 之前我们注意到，在这种情况下，尾递归过程是首选的，因为翻译器将其优化为实际循环相对容易。 事实上，`print-squares` 函数是尾递归的。

在上一节中，我们还演示了使用累加参数将非尾递归过程转换为尾递归过程的技术。 作为 Scheme 中的示例，我们将此技术应用于 square-list 函数，通过定义一个带有额外参数来累积中间结果的帮助过程 square-list1：

```
```scheme
(define square-list1 (lambda (L list-so-far)
  (if (null? L) list-so-far
      (square-list1 (cdr L)
                    (append list-so-far (list (* (car L) (car L))))))))
```
```

现在我们将 square-list 定义为对 square-list1 的调用，其第一个累积值为 ()：

```
```scheme
(define square-list (lambda (L) (square-list1 L '())))
```
```

类似地，对于 reverse，我们按如下方式定义 reverse1 和 reverse：

```
```scheme
(define reverse1 (lambda (L list-so-far)
  (if (null? L) list-so-far
      (reverse1 (cdr L) (cons (car L) list-so-far))))

(define reverse (lambda (L) (reverse1 L '())))
```
```

## 3.2.6 高阶函数

由于 Scheme 中的函数是第一类值，我们可以编写将其他函数作为参数的函数，以及将函数作为值返回的函数。 这种函数称为 **高阶函数**。

为了给出一个具有函数参数的函数的简单示例，我们可以编写一个函数 map⁶，它将另一个函数应用于列表中的所有元素，然后将它传递给平方函数以获得 square-list 示例：

```
```scheme
(define map (lambda (f L)
  (if (null? L) '()
      (cons (f (car L)) (map f (cdr L)))))

(define square (lambda (x) (* x x)))

(define square-list (lambda (L) (map square L)))
```
```

下面是一个具有函数参数并且还返回函数值的函数的示例：

```
```scheme
(define make-double (lambda (f)
  (lambda (x) (f x x))))
```
```

此函数假设 f 是一个具有两个参数的函数，并创建重复参数 x 在对 f 的调用中的函数。 由 make-double 返回的函数值 doublefn 由局部 define 创建，然后在末尾写入以使其成为 make-double 的返回值。 请注意，x 不是 make-double 本身的参数，而是由 make-double 创建的函数的参数。

我们可以使用 make-double 来获得平方函数和双倍函数（一个将数值加倍的函数）：

```
```scheme
(define square (make-double *))
(define double (make-double +))
```
```

符号“*”和“+”是乘法和加法函数的名称。 它们的值——即函数值——被传递给 make-double 过程，后者反过来返回被分配给名称 square 和 double 的函数值。 请注意，我们在这里使用的是 define 的简单形式，它只是分配计算值而不是用给定体定义函数。

正如

```
```scheme
(define a 2)
```
```

将值 2 分配给名称 a，表达式

```
```scheme
(define square (make-double *))
```
```

将 make-double 返回的函数值分配给名称 square。

如第 3.2 节末尾所述，函数式语言包括 Scheme 能够从高阶函数返回函数值的能力，这意味着函数式语言的运行时环境比标准块结构化命令式语言的基于栈的环境更复杂。 将函数使用的内存返回以释放存储需要使用自动内存管理技术，例如垃圾回收，这将在第 10.5 节中讨论。

## 3.2.7 静态（词法）作用域

早期的 Lisp 方言是动态作用域的，而更现代的方言，如 Scheme 和 Common Lisp，则是静态作用域的。 术语静态作用域或词法作用域指的是程序文本中变量声明可见的区域。 因此，在静态作用域中，给定变量的含义或值只需通过阅读程序文本即可确定。 相比之下，在动态作用域语言中，变量的含义取决于运行时上下文。

作用域的概念在块结构化语言中很重要，在这些语言中，可以嵌套变量的声明。 例如，考虑以下 Scheme 代码段，它在一个 let 中嵌套了另一个 let：

```
```scheme
> (let ((a 2) (b 3))
    (let ((a (+ a b)))
      (+ a b)))
8
```
```

作用域规则指出，变量的作用域延伸到声明它的块的末尾，包括任何嵌套块，除非该变量在嵌套块中被重新声明。 因此，在此示例中，第一个 (+ a b) 的值为 5，而第二个 (+ a b) 的值为 8。

当我们包含具有自由变量的函数时，这种对作用域规则的直接应用变得更加复杂。 自由变量是在函数内引用的变量，它既不是该函数的形参，也不是在嵌套函数中绑定的变量。 绑定变量是函数内的变量，它也是该函数的形参。 以下是定义和使用包含自由变量和绑定变量的函数的示例：

```
> (let ((pi 3.14))
    (let ((circlearea (lambda (radius)
                     (* pi (* radius radius)))))
        (let ((pi 3.1416))
            (circlearea 10))))
314.0
```

circlearea 函数包含一个绑定变量 radius 和一个自由变量 pi。 绑定变量 radius 也是函数的形参，它在函数调用的上下文中获取其值，当它绑定到值 10 时。 你还可以看到，自由变量 pi 的值必须在函数在此应用中引用它时为 3.14。 因此，自由变量 pi 在函数的定义上下文中获取并保留其值，即外部 let，而不是在函数调用的上下文中，即内部 let。 相比之下，如果 Scheme 是动态作用域的，像旧的 Lisp 一样，在函数应用中使用的 pi 的值将是内部 let 赋予它的值，即函数调用的上下文。 该应用然后将产生值 314.16。 在这种情况下，函数的自由变量将具有与其形参相同的语义。 也就是说，在动态作用域中，自由变量和形参的值随函数调用的上下文而变化。

词法作用域，因为它在代码中的一个位置固定了自由变量的含义，通常比动态作用域更容易阅读和验证程序。

## 3.2.8 符号信息处理和元语言能力

在本节前面，我们表明 Scheme 程序和 Scheme 数据可以具有相同的语法。 例如，从数据角度来看，表达式 (f x y) 只是一个包含三个符号的列表，可以使用列表操作访问和操作。 当被视为程序时，此表达式是将函数名由变量 f 命名应用于其参数值由变量 x 和 y 命名的函数。 构建、操作和转换符号列表然后将其作为程序进行求值的能力赋予 Scheme 程序员创建用于特殊目的的新语言的能力。 Abelson 和 Sussman [1996] 将这种能力称为元语言，并给出了其使用的几个例子。 其中包括为表达关系而非函数而创建约束语言，以及构建支持逻辑推理的语言。

创建这些小语言需要程序员指定其表达式的语法和作为新解释器中实现语义，所有这些都用基础语言 Scheme 编写。 虽然构建新解释器听起来可能比简单地定义新函数或数据类型更令人生畏，但这项工作由于迄今为止本节中讨论的 Scheme 的许多特性而变得出奇地简单。

