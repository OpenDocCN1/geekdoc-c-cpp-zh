
`let` 表达式的值是体表达式（body）在特定上下文的值，在该上下文中变量 `variable-i` 的值为 `expression-i` 的值。表达式 `expression-i` 的值可以引用 `let` 表达式中赋值的任何变量 `variable-j`。

`let*` 与 `let` 表达式相同，不同之处在于 `expression-i` 可以引用在 `let*` 表达式之前赋值的变量 `variable-j`。

`let` 表达式的一个轻微变体提供了编写循环的方便方法。我们可以编写一个实现阶乘计算替代算法的程序如下：

```scheme
(define (factorial n)
  let factlp ((count 1) (answer 1))
    (if count n)
      answer
      (factlp (+ count 1) (* count answer))))
```

```
(factorial 6)
720
```

在这里，`let` 之后的符号 `factlp` 被局部定义为一个过程，该过程将 `count` 和 `answer` 作为其形式参数。它第一次以 `1` 和 `1` 作为参数调用，初始化循环。以后每当调用名为 `factlp` 的程序时，这些变量就会获得新值，这些值为操作表达式 `(+ count 1)` 和 `(* count answer)` 的值。

表示此过程的等效方法具有显式定义的接口：

```scheme
(define (factorial n)
  (define (factlp count answer)
    (if (> count n)
        answer
        (factlp (+ count 1) (* count answer))))
(factlp 1 1))
```

过程 `factlp` 是局部定义的；它只存在于 `factorial` 的体内。因为 `factlp` 在词法上封装在 `factorial` 的定义中，因此它的体内 `n` 的值是 `factorial` 形式参数的值。

## 复合数据——列表、向量和记录

数据可以胶合形成复合数据结构。列表（list）元素按顺序链接的数据结构。向量（vector）元素封装在线性数组中的数据结构。列表可以添加新元素；访问列表的第 $n$ 个元素所需的时间与 $n$ 成比例。相比之下，向量是固定长度，可以在常数时间内访问其元素。记录（record）与向量类似，但它的字段通过名称而不是索引数字来访问。记录还提供了新的数据类型，可以通过类型谓词进行区分，并保证与其他类型不同。

复合数据对象通过称为构造函数（constructors）的过程由组件构建，并通过选择器（selectors）访问组件。

`list` 过程是列表的构造函数。谓词 `list?` 对任何列表都为真，对所有其他类型的数据都为假。

例如，

```scheme
(define a-list (list 6 946 8 356 12 620))
```

```
a-list
(6 946 8 356 12 620)
```

```
(list? a-list)
#t
```

```
(list? 3)
#f
```

`#t` 和 `#f` 是布尔值 `true` 和 `false` 的打印表示。

列表由对（pairs）构建。一个*对*（pair）使用构造函数 `cons` 构建。对的两个组件的选择器是 `car` 和 `cdr`（读作 "coud-er"）。

```scheme
(define a-pair (cons 1 2))
```

```
a-pair
(1 . 2)
```

```
(car a-pair)
1
```

```
(cdr a-pair)
2
```

```
(car a-list)
6
```

```
(cdr a-list)
(946 8 356 12 620)
```

```
(car (cdr a-list))
946
```

```scheme
(define another-list)
  (cons 32 (cdr a-list)))
```

```
another-list
(32 946 8 356 12 620)
```

```
car (cdr another-list)
946
```

列表 `a-list` 和 `another-list` 共享它们的尾（它们的 `cdr`）。谓词 `pair?` 对对为真，对所有其他类型的数据为假。谓词 `null?` 仅对空列表为真。

向量比列表简单。有一个构造函数 `vector` 用于创建向量，有一个选择器 `vector-ref` 用于访问向量的元素。在 Scheme 中，所有使用数值索引的选择都从零开始：

```scheme
(define a-vector
(vector 37 63 49 21 88 56))
```

```
a-vector
#(37 63 49 21 88 56)
```

## 影响

有时我们在计算过程中需要执行某些操作，例如绘制点或打印值。例如，为了详细查看阶乘程序是如何计算答案的，我们可以在 `factlp` 内部过程体中插入一个 `write-line` 语句，以打印每次迭代的计数和答案列表：

```
(define factorial n)
  (let factlp ((count 1) (answer 1))
    (write-line (list count answer))
    (if (> count n)
        answer
        (factlp (+ count 1) (* count answer)))))
```

当我们调用修改后的阶乘过程时，可以观察计数器的增加以及答案的构建过程：

```
(factorial 6)
(1 1)
(2 1)
(3 2)
(4 6)
(5 24)
(6 120)
(7 720)
720
```

每个过程或 `let` 的体，以及每个 `cond` 子句的后续（consequent），都允许使用具有影响语句。影响语句通常没有有用值。体或子句中的最后一个表达式产生被返回的值。

在这个示例中，`if` 表达式产生了阶乘的值。

## 赋值

像打印值或绘制点这样的影响是非常无害的，但还有更强大（因此也更危险）的影响，被称为“赋值”。赋值会改变变量的值或数据结构中条目的值。我们计算的几乎所有内容都是数学函数：对于特定的输入，它总是产生相同的结果。然而，通过赋值，我们可以创建可被使用的对象。例如，我们可以使用 `set!` 来创建一个每次调用它时都会增加计数的设备！

```
(define (make-counter)
  (let ((count 0))
    (lambda ()
      (set! count (+ count 1))
      count))))
```

让我们创建两个计数器：

```
(define c1 (make-counter))
(define c2 (make-counter))
```

这两个计数器具有独立的局部状态。调用计数器会导致它增加其局部状态变量 `count` 并返回其值。

```
(c1)
1
```

```
(c1)
2
```

```
(c2)
1
```

```
(c1)
3
```

```
(c2)
2
```

为了给数据结构（如对、列表或向量）的元素赋值，Scheme 提供了：

```
(set-car pair new-value)
(set-cdr pair new-value)
```

```
(list-set list index new-value)
(vector-set vector index new-value)
```

可以定义记录以允许对其字段进行赋值：

```
(define p (make-point 1 2))
```

```
(point-x p)
1
(point-y p)
2
```

```
(set-x! p 3)
3
(point-x p)
(point-y p)
2
```

通常情况下，尽可能避免赋值是一个良好习惯，但如果你需要，它们是可用的。

## B.2 更高级的特性

Scheme 提供了许多更强大的功能，但我们在这里不尝试描述它们。例如，你可能想了解哈希表。通常情况下，最好的来源是《算法语言 Scheme 修订报告》(R7RS) 和《MIT/GNU Scheme 参考手册》。但在阅读本书时，这里有你可能需要参考的两个相当复杂的特性：

### 动态绑定

我们有时想要指定某些求值或操作完成的方式——例如，在打印数字时指定进制。为了做到这一点，我们使用一个名为参数（parameter）的对象。

例如，Scheme 过程 `number->string` 产生一个表示给定进制下数字的字符字符串：

```
(number->string 100 2)
"1100100"
(number->string 100 16)
"64"
```

假设我们在一个通过调用 `myprog` 运行的复杂程序中的许多处使用 `number->string`，但我们希望能够控制程序运行时使用的进制。我们可以通过创建一个默认值为 10 的参数 `radix` 来实现这一点：

```
(define radix (make-parameter 10))
```

参数的值通过在不带参数的情况下调用该参数来获得：

```
(radix)
10
```

我们定义了 `number->string` 的特殊版本来代替 `number->string`：

```
(define (number->string-radix number)
(number->string number (radix)))
```

在 `(myprog)` 的执行过程中，每次调用 `number->string-radix` 都会产生一个十进制字符串，因为 `(radix)` 的默认值是。

*注：第 450-452 页的源 OCR 文本包含大量关于“动态绑定”和“参数”的重复和乱码文本。*

在 `(myprog)` 的执行过程中，每次调用 `number->string-radix` 都会产生一个十进制字符串，因为 `(radix)` 的默认值是。

反引号机制还提供了在列表表达式中进行“拼接”的功能：一个求值的子表达式会生成一个列表，然后该列表会被拼接到包裹它的列表中。例如：

```
(a b ,list (+ 20 3) (- 20 3))
(a b 23 17 d)
```

请参阅 Scheme 报告 以获取关于准引用（quasiquotation）的更详细解释。

- 9. 在美国式键盘上，反引号字符 "`" 是该键上的小写字母，而该键的大写字母是波浪号“~”。

- 10. 这是计算机科学术语。“效应”（effect）是指某物的改变。例如，`write-line` 通过在显示器上打印内容来改变显示状态。

- 11. 另一种文化惯俗是，我们用感叹号（!）为具有“副作用”的过程命名结尾。这在警告读者，改变效应的执行顺序可能会改变程序运行的结果。

- 12. 不使用赋值操作的编程学科被称为函数式编程。函数式程序通常比命令式程序更容易理解且 Bug 更少。

- 13. 该术语可以追溯到 ACTOR 框架 和 Smalltalk 编程语言。

## References

- [1] Harold Abelson and Gerald Jay Sussman with Julie Sussman, Structure and Interpretation of Computer Programs (2nd ed.). Cambridge, MA: MIT Press, 1996.

- [2] Harold Abelson, Don Allen, Daniel Coore, Chris Hanson, George Homsy, Thomas F. Knight Jr., Radhika Nagpal, Erik Rauch, Gerald Jay Sussman, and Ron Weiss; “Amorphous Computing,” in Communications of the ACM, 43(5) (May 2000): 74–82.

- [3] Lee Altenberg, “The Evolution of Evolvability in Genetic Programming,” in Advances in Genetic Programming, ed. Kenneth E. Kinnear Jr., 47–74. Cambridge, MA: MIT Press, 1994.

- [4] The ARRL Handbook for Radio Amateurs, American Radio Relay League, Newtown, CT (annual).

- [5] Jean-Paul Arcangeli and Christian Pomian; “Principles of Plasma Pattern and Alternative Structure Compilation,” in Theoretical Computer Science, 71 (1990): 177–191.

- [6] Franz Baader and Wayne Snyder; “Unification theory,” in Handbook of Automated Reasoning, ed. Alan Robinson and Andrei Voronkov. Elsevier Science Publishers B.V., 2001.

- [7] Jonathan B.L. Bard; Morphogenesis, Cambridge: Cambridge University Press, 1990.

- [8] Alan Bawden and Jonathan Rees; “Syntactic closures,” in Proc. Lisp and Functional Programming (1988).

- [9] Jacob Beal; Generating Communications Systems Through Shared Context, S.M. thesis, MIT, also Artificial Intelligence Laboratory Technical Report 2002-002, January 2002.

- [10] Jacob Beal; “Programming an Amorphous Computational Medium,” in Unconventional Programming Paradigms International Workshop (September 2004). Updated version in Lecture Notes in Computer Science, 3566 (August 2005).

- [11] M.R. Bernfield, S.D. Banerjee, J.E. Koda, and A.C. Raprae; “Remodelling of the basement membrane as a mechanism of morphogenic tissue interaction,” in The role of extracellular matrix in development, ed. R.L. Trestad, 542–572. New York: Alan R Liss, 1984.

- [12] Martin Berg; “Automatic differentiation on nonarchimedean analysis,” in Computer Arithmetic and Enclosure Methods, L. Atanassova and J. Herzberger. Elsevier Science Publishers B.V. (North-Holland), 1992.

- [13] Philip L. Bewig; Scheme Requests for Implementation 41: Streams (2008). https://srfi.schemers.org/srfi-41/
