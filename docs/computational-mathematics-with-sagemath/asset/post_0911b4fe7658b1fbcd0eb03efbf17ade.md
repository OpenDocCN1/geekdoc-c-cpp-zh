
with zero, one or several arguments, which returns (resp. does not return) a result. Let us define the function \((x, y) \mapsto x^2 + y^2\):

```sage
sage: def fct2 (x, y):
....:   return x^2 + y^2
sage: a = var('a')
sage: fct2 (a, 2*a)
5*a^2
```

The function evaluation ends with the `return` command, whose argument, here \(x^2 + y^2\), is the result of the function.

A procedure is like a function, but does not return any value, and without any `return` instruction the instruction body of the procedure is evaluated until its end. In fact a procedure returns the `None` value, which means “nothing”.

By default, all variables appearing in a function are considered local variables. Local variables are created at each function call, destroyed at the end of the function, and do not interact with other variables of the same name. In particular, global variables are not modified by the evaluation of a function having local variables of the same name:

```sage
sage: def foo (u):
....:   t = u^2
....:   return t*(t+1)
sage: t = 1 ; u = 2
sage: foo(3), t, u
(90, 1, 2)
```

It is possible to modify a global variable from within a function, with the `global` keyword:

```sage
sage: a = b = 1
sage: def f(): global a; a = b = 2
sage: f(); a, b
(2, 1)
```

Consider again the computation of the arithmetic-harmonic mean of two positive numbers:

```sage
sage: def AHmean (u, v):
....:   u, v = min(u, v), max(u, v)
....:   while v-u > 2.0e-8:
....:     u, v = 2*u*v/(u+v), (u+v)/2
....:   return (u+v) / 2
```

```sage
sage: AHmean (1., 2.)
1.41421356237309
sage: AHmean                 # corresponds to a function
  <function AHmean at ...>
```

The `AHmean` function has two parameters u and v which are local variables, whose initial values are those of the function arguments; for example with `AHmean (1., 2.)` the function body begins with `u = 1.0` and `v = 2.0`.

The structured programming paradigm recommends to have the `return` statement at the very end of the function body. However, it is possible to put it in the middle of the instruction block, then the following instructions will not be executed. And the function body might contain several `return` occurrences.

Translating the mathematician’s viewpoint into the computer suggests the use of functions that return results from their arguments, instead of procedures that output those results with a `print` command. The Sage computer algebra system is itself built on numerous functions like `exp` or `solve`, which return a result, for example a number, an expression, a list of solutions, etc.

## Iterative and Recursive Methods.

As we have seen above, a user-defined function is a sequence of instructions. A function is called recursive when during its evaluation, it calls itself with different parameters. The factorial sequence is a toy example of recursive sequence:

0! = 1,  (n + 1)! = (n + 1)n! for all n ∈ ℕ.

The two following functions yield the same result for a nonnegative integer argument n; the first function uses the iterative method with a `for` loop, while the second one is a word-by-word translation of the above recursive definition:

```sage
sage: def fact1 (n):
....:     res = 1
....:     for k in [1..n]: res = res*k
....:     return res
```

```sage
sage: def fact2 (n):
....:     if n == 0: return 1
....:     else: return n*fact2(n-1)
```

The Fibonacci sequence is a recurrent relation of order 2 since uₙ₊₂ depends on uₙ and uₙ₊₁:

u₀ = 0,  u₁ = 1,  uₙ₊₂ = uₙ₊₁ + uₙ for all n ∈ ℕ.

The function `fib1` below applies an iterative scheme to compute terms of the Fibonacci sequence: the variables U and V store the two previous values before computing the next one:

```sage
sage: def fib1 (n):
....:     if n == 0 or n == 1: return n
....:     else:
....:         U = 0 ; V = 1 # the initial terms u0 and u1
....:         for k in [2..n]: W = U+V ; U = V ; V = W
....:         return V
sage: fib1(8)
21
```

The for loop applies the relation \(u_n = u_{n-1} + u_{n-2}\) from \(n = 2\). Note: a parallel assignment `U,V = V,U+V` in place of `W=U+V; U=V; V=W` would avoid the need of an auxiliary variable W, and would translate the order-1 vectorial recurrence \(X_{n+1}=f(X_n)\) with \(f(a,b)=(b,a+b)\), for \(X_n=(u_n,u_{n+1})\). Those iterative methods are efficient, however programming them requires to manually deal with variables corresponding to different terms of the sequence.

On the contrary, the recursive function `fib2` follows more closely the mathematical definition of the Fibonacci sequence, which makes its programming and understanding easier:

```sage
sage: def fib2 (n):
....:     if 0 <= n <= 1: return n       # for n = 0 or n = 1
....:     else: return fib2(n-1) + fib2(n-2)
```

The result of this function is the value returned by the conditional statement: either 0 or 1 respectively for \(n = 0\) and \(n = 1\), otherwise the sum `fib2(n-1)+fib2(n-2)`; each branch of the test consists of a return instruction.

This method is however less efficient since several computations are duplicated. For example `fib2(5)` evaluates `fib2(3)` and `fib2(4)`, which are in turn evaluated in the same manner. Therefore, Sage computes twice `fib2(3)` and three times `fib2(2)`. This recursive process ends by the evaluation of either `fib2(0)` or `fib2(1)`, of value 0 or 1, and the evaluation of `fib2(n)` eventually consists in computing \(u_n\) by adding \(u_n\) ones, and \(u_{n-1}\) zeroes. The total number of additions performed to compute \(u_n\) is thus \(u_{n+1}-1\). This number grows very quickly, and no computer is able to compute \(u_{100}\) this way.

Other methods are also possible, for example remembering the intermediate terms using the decorator `@cached_function`, or using properties of matrix powers: the following paragraph shows how to compute the millionth term of this sequence. For example, compare the efficiency of the function `fib2` defined above with the following one, for example on \(n = 30\):

```sage
sage: @cached_function
sage: def fib2a (n):
....:     if 0 <= n <= 1: return n
....:     else: return fib2a(n-1) + fib2a(n-2)
```

### 3.2.4 Example: Fast Exponentiation

The naive method for computing \(a^n\) for \(n \in \mathbb{N}\) performs \(n\) multiplications by \(a\) using a for loop:

```sage
sage: a = 2; n = 6; res = 1       # 1 is the product neutral element
sage: for k in [1..n]: res = res*a
sage: res                          # the value of res is 2^6
64
```

Integer powers often arise in mathematics and computer science; this paragraph discusses a general method to compute $a^n$ in a much faster way than the naive method. The sequence $(u_n)_{n\in\mathbb{N}}$ below satisfies $u_n=a^n$; this follows by induction from the equalities $a^{2k}=(a^k)^2$ and $a^{k+1}=a a^k$:

\[
u_n = \begin{cases}
1 & \text{if } n=0,\\
u_{n/2}^2 & \text{if } n \text{ is even positive},\\
a u_{n-1} & \text{if } n \text{ is odd}.
\end{cases}
\qquad (3.2)
\]

For example, for $n = 11$:

\[
u_{11}=a u_{10},\quad u_{10}=u_5^2,\quad u_5=a u_4,\quad u_4=u_2^2,\\
u_2=u_1^2,\quad u_1=a u_0=a;
\]

therefore:

\[
u_2=a^2,\quad u_4=u_2^2=a^4,\quad u_5=a a^4=a^5,\\
u_{10}=u_5^2=a^{10},\quad u_{11}=a u_{10}=a^{11}.
\]

The computation of $u_n$ only involves terms $u_k$ with $k\in\{0,\ldots,n-1\}$, and is thus well performed in a finite number of operations.

This example also shows that $u_{11}$ is obtained after the evaluation of 6 terms $u_{10}$, $u_5$, $u_4$, $u_2$, $u_1$ and $u_0$, which performs 6 multiplications only. In general, the computation of $u_n$ requires between $\log n/\log 2$ and $2\log n/\log 2$ multiplications. Indeed, $u_n$ is obtained from $u_k$, $k\le n/2$, with one or two additional steps, according to the parity of $n$. This method is thus much faster than the naive one when $n$ is large: about twenty products for $n=10^4$ instead of $10^4$ products:

| indices k: | 10000 | 5000 | 2500 | 1250 | 625 | 624 | 312 | 156 | 78 |
|---|---|---|---|---|---|---|---|---|---|
|  | 39 | 38 | 19 | 18 | 9 | 8 | 4 | 2 | 1 |

However, this method is not always the best one; the following operations using $b$, $c$, $d$ and $f$ perform 5 products to compute $a^{15}$, whereas the above method — using $u$, $v$, $w$, $x$ and $y$ — requires 6 products, without counting the initial product $a\cdot 1$:

$b=a^2 \quad c=ab=a^3 \quad d=c^2=a^6 \quad f=cd=a^9 \quad df=a^{15}$ : 5 products;

$u=a^2 \quad v=au=a^3 \quad w=v^2=a^6$

$x=aw=a^7 \quad y=x^2=a^{14} \quad ay=a^{15}$ : 6 products.

The recursive function pow1 uses the recurrent sequence (3.2) to compute $a^n$:

```sage
sage: def pow1 (a, n):
....:     if n == 0: return 1
....:     elif n % 2 == 0: b = pow1 (a, n/2); return b*b
....:     else: return a * pow1(a, n-1)
```

```sage
sage: pow1 (2, 11)               # result is 2^11
```
