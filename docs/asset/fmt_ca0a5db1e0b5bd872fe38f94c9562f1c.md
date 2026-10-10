
### 练习 3.3

将此安排为 `3.1` 节引入的基于组合子的算术有多困难？为什么？

第 `86` 页的练习 `3.3` 询问了向量扩展的影响。通用系统能够支持那里讨论的表达式（复制如下）：`((magnitude unit-circle)`

有没有好的方法让以下内容有效？

```
(vector cos 3)
```

```
(-98999249660044 .14112008059867)
```

显示使其有效的代码或解释困难之处。

### 练习 3.5：一个 Bug

考虑 `arith.scm` 中的 `+-like` 程序（所示），它是安装算术的一部分实现的二元过程。它返回一个名称和一个处理器的对；安装程序会将名称绑定到处理器。

它似乎被写为每次在没有参数的情况下调用时都执行 `get-identity` 程序。

```scheme
(define (+like operator identity-name)
  (lambda (arithmetic))
    (let ((binary-operation
            (find-arithmetic-operation operator arithmetic))
      (and binary-operation
        (let ((binary
                (operation-procedure binary-operation)
                (get-identity
                  (identity-name->getter identity-name
                    arithmetic))))
          (cons operator
            (lambda args)
              (case (length args)
                ((0) (get-identity))
                ((1) (car args))
                (else (pairwise binary args))))))))
```

也许运算符的单位元只需要计算一次，而不是每次调用处理器时。因此，建议将代码如下：

```scheme
(define (+like operator identity-name)
  (lambda (arithmetic))
    (let ((binary-operation
            (find-arithmetic-operation operator arithmetic))
      (and binary-operation
        (let ((binary
                (operation-procedure binary-operation)
                (identity
                  (identity-name->getter identity-name
                    arithmetic))))
          (cons operator
            (lambda args))))
```

```scheme
(case (length args)
((0) identity)
((1) (car args))
(else (pairwise binary args))))))))))
```

然而，这里有一个微妙的 bug！你能找出这个 bug 吗？能解释它吗？

### 练习 3.6：矩阵

矩阵在科学和技术计算中无处不在。

- a. 为数字矩阵创建一个并安装算术包，包含 `+`、`negate` 和 `*` 操作。这种算术需要能够知道矩阵的行数列数，因为只有当第一个矩阵的列数等于第二个矩阵的行数时，矩阵乘法才有定义。

确保你的乘法器可以将矩阵与标量或向量相乘。为了让矩阵与向量良好协作，你可能需要区分行向量和列向量。这如何影响向量包的设计？（见第 `85` 页的练习 `3.2`。）

你可以假设向量和矩阵的维度都是较小的，因此你不需要处理稀疏表示。矩阵的一种合理表示是一个 Scheme 向量，其中每个元素都是代表一行的 Scheme 向量。

- b. 向量和矩阵可能包含符号数值。让这部分工作起来。

- c. 矩阵求逆适用于你的算术。如果一个符号矩阵是密密的，逆矩阵占用的空间可能是维度的阶乘增长。为什么？

注意：我们并没有要求你实现矩阵求逆。

### 练习 3.7：字面量向量和矩阵

通过向量和矩阵的符号表达式代数，对字面量矩阵和字面量向量进行运算也是。你能让这些复合结构的符号代数与带有符号数值表达式元素的向量和矩阵良好协作吗？注意：这非常困难。也许作为长期项目的一部分是合适的。

## 3.3 示例：自动求分

可扩展通用过程的一个显著应用是自动求分。¹¹⁴ 这是一种获取计算给定程序所计算函数导数的优美方法。¹¹⁵ 自动求分现在机器学习应用中的重要组成部分。

我们将看到，实现自动求分的一种简单方法是将通用算术原语扩展为处理微分对象（differential objects），一种新的复合数据类型。这将实现符号函数和数值函数的自动求分。它还将让自动求分适用于高阶程序——即返回其他程序作为值的程序。

这里有一个自动求分的简单示例，用来说明我们所讨论的内容：

```scheme
((derivative (lambda x) (expt x 3))) 2)
12
```

注意，计算参数立方函数的导数是一个新函数，当给定 `2` 作为参数时，它返回 `12` 作为值。

如果我们将算术扩展以处理符号表达式，并对结果进行一些代数简化，我们得到：

```scheme
((derivative lambda (x) (expt x 3))) 'a
(* 3 (expt a 2))
```

编程语言的完整功能都是可用，包括高阶程序。这种系统在处理有趣的物理问题中出现的极大表达式非常有用。¹¹⁰

让我们来看一个简单的应用：通过牛顿法计算方程的根。该思想是找到使 `$f(x) = 0$` 的 `$x$` 值。如果 `$f$` 足够光滑，且我们有一个足够接近的猜测值 `$x_0$`，我们可以通过公式计算新的猜测值 `$x_1$` 来改进猜测：

```
$x_{n+1} = x_n - \frac{f(x_n)}{Df(x_n)}$
```

可以根据需要重复此过程，以获得足够准确的结果。一个实现此目的的基础程序：

```scheme
(define (root-newton f initial-guess tolerance)
  (let ((Df (derivative f)))
    (define (improve-guess xn)
      (- xn (/ (f xn) (Df xn))))
    (let loop ((xn initial-guess))
      (let (xn+1 (improve-guess xn))
        (if (close-enuff xn xn+1 tolerance)
            xn+1
            (loop xn+1)))))
```

注意 `root-newton` 中名为 `Df` 的局部过程是一个通过作为 `f` 传递的程序计算函数导数的程序。

例如，假设我们知道第一象限内满足 `$\cos(\theta) = \sin(\theta)$` 的角度 `$\theta$`。（答案是 `$\pi/4 \approx .7853981633974484$`）我们可以写：

```scheme
(define (cs theta)
  (- (cos theta) (sin theta)))
```

```scheme
(root-newton cs 0.5 1e-8)
.7853981633974484
```

这个结果在机器精度上是准确的。

### 3.3.1 自动求分是如何工作的

自动求分程序直接源自导数的定义。假设给定一个函数 `$f$` 和其定义域中的一个点 `$x$`，我们想知道函数在附近点 `$f(x+\Delta x)$` 处的值，其中 `$\Delta x$` 是一个微小的增量。函数 `$f$` 的导数被定义为导数 `$Df$`，其对于特定参数 `$x$` 的值是能够与参数的增量 `$\Delta x$` “相乘”，以得到 `$f$` 的值增量的最可能的线性近似：

$$
f(x+\Delta x) \approx f(x) + Df(x)\Delta x
$$

我们使用一种称为微分对象（*differential object*）的数据类型来实现定义。微分对象 `[x, \delta x]` 可以被看作带有微小增量 `$x + \delta x$` 的数字。但我们将其视为一个新的数值：它有两个部分，有限部分（*finite part*）和无穷小部分（*infinitesimal part*）。¹⁷ 我们扩展每个原语算术以处理微分对象：每个原语算术函数 `$f$` 必须知道其导数函数 `$Df$`，以便：

$$
[x, \delta x] \xrightarrow{f} [f(x), Df(x)]
$$

注意，`$f$` 在点 `$x$` 处的导数 `$Df(x)$` 是结果微分对象中 `$\delta x$` 的系数。

```scheme
(define diff:exp (diff:unary-proc exp exp))
```

```scheme
(define diff:log (diff:unary-proc log (lambda x) (/ 1 x))))
```

```scheme
(define diff:sin (diff:unary-proc sin cos))
```

```scheme
(define diff:cos
  (diff:unary-proc cos (lambda x) (* -1 (sin x))))
```

## 二元算术运算稍微复杂一些。

$g(x + \Delta x, y + \Delta y) \approx g(x, y) + \partial_x g(x, y) \Delta x + \partial_y g(x, y) \Delta y \quad (3.6)$

其中 `$\partial_o f$` 和 `$\partial_j f$` 是 `$f$` 对两个参数的偏导数函数。设 `$f$` 为一个二参数函数；那么 `$\partial_o f$` 是一个新的二参数函数，用于计算 `$f$` 对其第一个参数的偏导数：

> `$\partial_o f(x, y) = \frac{\partial}{\partial u} f(u, v)|_{u=x, v=y}$`

因此，二元运算的规则如下：

```
$([x, \delta x], [y, \delta y]) \xrightarrow{f} f(x, y), \partial_o f(x, y) \delta x + \partial_j f(x, y) \delta y$
```

实现二元运算，我们可能会认为只需遵循一元运算的计划，其中 `d0f` 和 `d1f` 是两个偏导数函数：

```scheme
(define diff:binary-proc f d0f d1f)
(define (bop x y)
  (let ((dx (infinitesimal-part x))
        (dy (infinitesimal-part y))
        (xf (finite-part x))
        (yf (finite-part y))))
```

```scheme
(d+: (f x yf))
 (d+: (+ (d* dx (d0f xf yf))
         (d* (d1f xf yf) dy))))
```

这是一个很好的计划，但它并不完全正确：它没有确保两个两个参数选择的有限部分和无穷小部分是一致的。我们需要对如何选择这些部分更加小心。我们将在 `3.3.3` 节解释这一技术细节并修复它，但目前我们先使用这段大致正确的代码。

加法和乘法很直观，因为偏导数很简单，但除法和幂运算更有趣。我们只展示 `diff:` 的处理程序分配，因为其他所有的都是相似的。

```scheme
(define diff:+
  (diff:binary-proc +
    (lambda (x y) 1)
    (lambda (x y) 1)))
```

```scheme
(assign-handler! + diff+: differential? any-object?)
(assign-handler! + diff+: any-object? differential?)
```

```scheme
(define diff:*
  (diff:binary-proc *
    (lambda (x y) y)
    (lambda (x y) x)))
```

```scheme
(define diff:/
  (diff:binary-proc /
    (lambda (x y)
      (/ 1 y))
    (lambda (x y)
      (* -1 (/ x (square y))))))
```

幂运算 `$f(x, y) = x$` 的处理程序有点复杂。对第一个参数的偏导是简单的：`$\partial_o f(x, y) = y^{-1}$`。但对第二个参数的偏导通常为 `$\partial_f f(x, y) = x \log x$`，除非是某些特殊情况：

```scheme
(define diff:expt
  (diff:binary-proc expt
    (lambda (x y)
      (* y (expt x (- y 1)))))
```

```scheme
  (lambda (x y)
    (if (and (number? x) (zero? x))
        (if (number? y)
          (if (positive? y)
            0
            (error "Derivative undefined: EXPT
                   x y))
        0)
      (* log x) (expt y)))))
```

### 提取导数的值

为了计算函数导数的值，我们将函数应用于微分对象并获得结果。我们必须从该结果中提取导数的值。有几种必须处理的情况。如果结果是微分对象，我们需要把导数的值提取出来。如果结果不是微分对象，则导数的值为零。还有其他我们未提到的情况。这需要一个产生零的通用过程。

```scheme
(define extract-dx-default value 0)
```

```scheme
(define extract-dx-part generic-procedure)
``````

在返回微分对象的情况下，`$dx$` 的系数就是所需的导数。这证明将变得有点复杂，但基本思想可以表述如下：

```scheme
(define extract-dx-differential value
  (extract-dx-coefficient (infinitesimal-part value)))
```

```scheme
(define generic-procedure-handler extract-dx-handler match-args differential?)
```

之所以这不完全正确，由于技术原因，微分对象的结构比我们已经展示的要复杂。将在 `3.3.3` 节中进行详细解释。注意：我们将提取器设为通用的，以便未来扩展到返回函数或复合对象的函数，例如向量、矩阵和张量（参见第 `124` 页的练习题 `3.12`）。除了可能包含更多原语算子和数据结构之外，这就是实现自动微分所需的所有内容！所有的过程都是算术运算的通常通用过程；它们可能包括符号和函数算术。

### 3.3.2 多元函数的导数

对于多参数的函数，我们需要能够计算对每个参数的偏导数。其中一种方法是：

```scheme
(define ((partial i) f)
  (define (the-derivative args)
    (if (not (< i (length args)))
        (error "Not enough arguments for PARTIAL" i args))
    (let ((dx (make-new-dx)))
      (value
        (apply f (map (lambda arg j
          (if (= i j)
            (d:+ arg (make-infinitesimal dx))
            arg))
          (iota (length args))))))
      (extract-dx-part)))))
```

在返回微分对象的情况下，`$dx$` 的系数就是所需的导数。这证明将变得有点复杂，但基本思想可以表述如下：

例如，如果我们想计算二阶导数，必须对一个导数函数再次求导。这种函数的求值将涉及两个无穷小量。为了实现对多阶导数以及多变量函数导数的计算，我们在“无穷小空间”中定义了一阶微分对象的代数。这些对象是多变量幂级数，其中没有任何无穷小增量的指数大于 `1`。

微分对象由幂级数数项的标记列表（tagged list）表示。每个项都有一个系数和一个无穷小增量因子列表。这些项按降序保持排序。（阶数是增量的数量。因此 `$\delta \text{}dx$` 的阶数高于 `$\delta \text{}x$` 或 `$\delta \text{}y$`。）这里是一个快速而直接的实现：

```scheme
(define differential-tag 'differential')
```

```scheme
(define (differential? x)
  (and (pair? x) (eq? (car x) differential-tag)))
```

```scheme
(define (diff-h)
  (if (differential? h)
    (cdr h)
    (list (make-diff-term h ')))))
```
