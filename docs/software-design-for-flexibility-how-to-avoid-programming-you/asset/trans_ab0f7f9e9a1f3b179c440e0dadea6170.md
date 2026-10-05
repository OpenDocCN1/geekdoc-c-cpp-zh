
扩展的顺序是如何影响结果算术运算属性的？以下过程在单位圆上产生点：

```scheme
(define (unit-circle x)
  (vector (sin x) (cos x))
```

如果我们在安装了 `vec-before-func` 和 `func-before-vec` 后产生的环境中执行以下每个表达式：

```scheme
((magnitude unit-circle) 'a)
((magnitude vector sin cos) 'a)
```

其结果（未简化的）应该是：

```scheme
(sqrt (+ (* (sin a) (sin a)) (* (cos a) (cos a))))
```

然而，这些表达式中的每一个在两种扩展顺序中的其中一种都会执行失败。是否可能创建一种两种情况下都能正确求值的算术运算？请解释原因。

## 3.2 可扩展的通用过程

如 3.1 节所示，通过组合器构建的系统会产生美丽的菱形系统。这有时是一个正确的主意，我们将再次看到它的出现，但要在菱形结构中添加内容非常困难。如果一个系统是像“一团泥”（ball of mud）一样构建的，那么添加更多的泥就容易了。

“一团泥”的一种组织形式是建立在可扩展通用过程基础上的系统。现代动态类型编程语言（如 Lisp、Scheme 和 Python）通常具有内置的算术运算，这些运算对多种数值通用，如整数、浮点数、有理数复数 [115, 64, 105]。但构建在这些语言上的系统通常不是易于扩展的。

3.1.5 节中识别的问题是使用组合器 `add-arithmetics` 的结果。为了解决这些问题，我们将放弃该组合器。然而，算术包抽象仍然是有用的，扩展器（extender）的概念也是如此。我们将构建一个算术包，其中的操作使用通用过程，这些过程可以动态地增加新行为。然后我们就可以扩展通用算术，并将扩展项添加到通用算术中。¹

我们将从实现通用过程开始，通用过程是在通用过程定义后，通过添加处理器（handlers）来动态扩展的过程。通用过程是一个分发器结合一组规则，每条规则都描述了一个适用于给定参数集合的处理器。这种规则将处理器与其可适用性结合在一起。

让我们通过定义一个名为 `plus` 的通用过程来检查它是如何工作的，它的工作类似于对数值和符号数量进行加法：

```scheme
(define simple-generic-procedure 'plus 2 #f)

(define-generic-procedure-handler plus
  (all-args 2 number?)
  (lambda (a b) (+ a b)))

(define-generic-procedure-handler plus
  (any-arg 2 symbolic? number?)
  (lambda (a b) (list '+ a b)))

(plus 1 2)
3

(plus 1 'a)
(+ 'a a)

(plus 'a 2)
(+ 'a 2)

(plus 'a 'b)
(+ 'a b)
```

过程 `simple-generic-procedure` 三个参数：第一个是用于调试时识别过程的任意名称；第二个是过程的元数（arity）；第三个参数用于提供默认处理器；如果没有提供（由 `#f` 表示），且没有特定的处理器适用，则抛出错误。这里 `plus` 被绑定到 `simple-generic-procedure` 返回的新通用过程。它是一个 Scheme 过程，可以使用指定数量的参数进行调用。

过程 `define-generic-procedure-handler` 为现有的通用过程添加一条规则。它的第一个参数是要扩展的通用过程；第二个参数是所添加规则的适用性规范（如第 73 页所示）；第三个参数是用于满足该规范的参数的处理器。

```scheme
(define-generic-procedure-handler generic-procedure applicability handler-procedure)
```

通常有指定一条其中不同参数具有不同类型的规则。例如，为了创建一个向量算术包，我们需要指定运算符。如果两个参数都是向量，相应的处理器计算点积。如果一个参数是标量，另一个是向量，则相应的处理器对向量进行缩放。上述 `simple-generic-procedure` 创建的 `plus` 通用过程是一个分发器，封装了保存、检索和选择处理器的策略。`generic-procedure-constructor` 接收一个分发器并产生一个通用过程，它接受三个参数——调试用的名称、元数以及默认处理器。如果默认处理器参数为 `#f`，则抛出错误：

```scheme
(generic-procedure-constructor dispatch-store)
```

其中 `arithmetic-dispatch-store` 是一个构建了通用过程的运算符。`make-generic-arithmetic` 过程创建一个新的算术。对于每个运算符，它构造一个适用于任何对象的由通用过程实现的运算。`any-object?` 谓词为真。我们以通常的方式安装这种算术。

首先，让我们为通用过程定义一些处理器。现在有了算术对象，这样做非常简单。例如，我们可以从构建的算术中获取操作和常量。

```scheme
(define (add-to-generic-arithmetic! generic-arithmetic arithmetic)
  (add-generic-arith-constants! generic-arithmetic arithmetic)
  (add-generic-arith-operations! generic-arithmetic arithmetic))
```

这接收一个通用算术包和一个具有相同运算符的普通算术包。通过 `constant-union` 将常量合并到通用算术中。对于给定算术的每个运算符，它向对应的通用过程添加一个处理器。为特定运算符添加处理器使用标准的通用过程机制，从算术的操作中提取必要的适用性和过程。

```scheme
(define (add-generic-arith-operations! generic-arithmetic arithmetic)
  (for-each
    (lambda (operator)
      (let ((generic-procedure
             (simple-operation-procedure
               (arithmetic-operator operator
                 generic-arithmetic))
            (operation
              (arithmetic-operator operator arithmetic)))
        (define-generic-procedure-handler
          generic-procedure
          (operation-applicability operation)
          (operation-procedure operation))))
    (arithmetic-operators arithmetic))))
```

`add-generic-arith-operations!` 为通用算术中的每个运算符找到需要增强的通用过程。然后它为该通用过程定义一个处理器，该处理器是给定算术中该运算符的处理器，使用了给定算术中该处理器的适用性。

将算术中的常量添加到通用算术的代码类似。对于通用算术中的每个常量名称，它找到通用算术中名称到常量值的关联条目。然后它替换常量值

## 3.2.1 通用算术

可以使用这种通用过程机制来构建运算符映射到通用过程运算的算术包。这将允许我们创建自引用结构。例如，我们可能想要创建一个两个向量都由相同处理器处理的向量算术。引入的 `add-arithmetics` 无法构建这样的结构。

在 3.2.3 节中，我们将看到实现这种机制的方法。但在之前，让我们看看如何使用它。
