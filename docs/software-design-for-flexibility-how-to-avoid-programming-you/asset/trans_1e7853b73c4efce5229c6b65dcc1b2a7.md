
例如，如果我们想计算二阶导数，必须对一个导数函数再次求导。这种函数的求值将涉及两个无穷小量。为了实现对多阶导数以及多变量函数导数的计算，我们在“无穷小空间”中定义了一阶微分对象的代数。这些对象是多变量幂级数，其中没有任何无穷小增量的指数大于 1。

微分对象由幂级数数项的标记列表（tagged list）表示。每个项都有一个系数和一个无穷小增量因子列表。这些项按降序保持排序。（阶数是增量的数量。因此 $\delta \text{}dx$ 的阶数高于 $\delta \text{}x$ 或 $\delta \text{}y。）这里是一个快速而直接的实现：

```scheme
(define differential-tag 'differential')

(define (differential? x)
  (and (pair? x) (eq? (car x) differential-tag)))

(define (diff-h)
  (if (differential? h)
    (cdr h)
    (list (make-diff-term h ')))))
```

该列表仅仅是微分对象的 `cdr`。然而，如果我们给出的对象不是显式的微分对象（例如一个数字），我们将其强制转换为一个只有一个项且没有增量因子的微分对象。当我们从一个（预先排序的）数项列表创建微分对象时，我们总是尝试返回一个简化后的版本，该版本可能只是数字，而它并不是显式的微分对象：

```scheme
(define (make-differential terms) ; 非零项
  (let ((terms
    (filter
      (lambda (term)
        (let ((coeff (diff-coefficient term))
          (not (number? coeff) (= coeff 0))))
    terms)) 0))
    (cond ((null? terms)
      (and (null? (cdr terms)))
            ;; 仅有限部分：
            (null? (diff-factors (car terms))))
    (diff-coefficient (car terms))))

```

```scheme
  ((every diff-term? terms)
  (cons differential-tag terms)
  (else (error "Bad terms")))
```

在此实现中，数项也被表示为标记列表，每个列表包含一个系数和一个有序的因子列表。

```scheme
(define diff-term-tag 'diff-term)

(define (make-diff-term coefficient factors)
  (list diff-term-tag coefficient factors))

(define (diff-term? x)
  (pair? x) (eq? (car x) diff-term-tag))
```

```scheme
(define diff-coefficient x)
  (cadr x))
```

```scheme
(define diff-factors x)
  (caddr x))
```

为了计算导数，我们需要能够加和乘法微分对象：

```scheme
(define d:+ x y)
  (make-differential
  (+diff-termlists diff-terms x) (diff-terms y)))
```

```scheme
(define d:* x y)
  (make-differential
  (*diff-termlists diff-terms x) (diff-terms y)))
```

我们还需要这个：

```scheme
(define (make-infinitesimal dx)
  (make-differential (list (make-diff-term 1 (list dx))))
```

数项列表的加法是le强制并使用数项排序的地方，高阶项位于列表的前部。只有当两个项具有相同因子时，我们才将它们相加。如果系数之和为零，我们就不包含生成的项。

```scheme
(define (+diff-termlists l11 l12)
  (cond ((null? l11) l12)
        ((null? l12) l11)
        (else
```scheme
  (let ((t1 (car l11)) (t2 (car l12)))
    (cond ((equal? (diff-factors t1) (diff-factors t2))
              (let ((newcoeff (+ (diff-coefficient t1)
                              (diff-coefficient t2)))
                (if (and (number? newcoeff)
                    (= newcoeff 0))
                    (+diff-termlists (cdr l11) (cdr l12))
                  (cons
                    (make-diff-term newcoeff
                      (diff-factors t1))
                    (+diff-termlists (cdr l11)
                      (cdr l12))))))
          ((diff-term? t1 t2)
            (cons t1 (+diff-termlists (cdr l11) (cdr l12))))
          (else
            (cons t2
              (+diff-termlists l11 (cdr l12))))))))
```

数项列表的乘法是直接的，只要我们可以乘以单个项。两个数项列表 `l11` 和 `l12` 的乘积是：将 `l1` 中的每一项与 `l12` 中的每一项相乘所得的数项列表相加得到的数项列表。

```scheme
(define *diff-termlists l11 l12)
  (reduce (lambda (x y)
    (+diff-termlists x y)
    '()
    (map (lambda (t1) (map (lambda (t2)
      (*diff-terms t1 t2))
    l12))))
```

一个项包含系数和一个因子列表（无穷小量）。微分对象可能有一个指数大于1的无穷小量，因为 $\delta x = 0$。因此，当我们乘以两个项时，必须检查因子列表是否合并了没有因子。