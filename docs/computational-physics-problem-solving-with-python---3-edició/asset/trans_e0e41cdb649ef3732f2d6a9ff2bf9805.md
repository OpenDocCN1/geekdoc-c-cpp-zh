

in NumPy 和各种相关规则；我们建议认真使用的用户探索 NumPy 的广泛文档以获取更多信息。

### 6.5.1 NumPy 的 linalg 包

NumPy 和 Visual 的数组对象与数学矩阵并不相同，尽管数组可用于表示矩阵。幸运的是，有 LinearAlgebra 包，它将 2D 数组（1D 数组的 1D 数组）视为数学矩阵，并且还提供了对强大的 LAPACK 线性代数库（Anderson et al., 2013）的简单接口。正如我们一直所说，与编写自己的矩阵例程相比，使用这些库在速度和可靠性方面可以获得很多好处。

我们从线性代数中的第一个例子是标准矩阵方程

**A** **x** = **b** , (6.31)

其中我们使用大写粗体字符表示矩阵，使用小写粗体斜体字符表示 1D 矩阵（向量）。方程 6.31 描述了一组线性方程，其中 x 是未知向量，A 是已知矩阵。现在我们取 A 为 3 × 3，b 为 3 × 1，并让程序推断出 x 必须为 3 × 1 向量。⁶ 我们首先导入所有包，通过输入矩阵和向量，然后打印出 A 和 x：

```
>>> from numpy import *
>>> from numpy.linalg import *
>>> A = array([ [1,2,3], [22,32,42], [55,66,100] ]) # Array of arrays
>>> print ('A =', A)
A = [[ 1  2  3]
     [ 22 32 42]
     [ 55 66 100]]
>>> b = array([1,2,3])
>>> print ('b =', b)
b = [1 2 3]
```

由于我们有矩阵 A 和 b，我们可以继续使用 NumPy 的 solve 命令求解 A x = b，然后测试 A x − b 与零向量有多接近：

```
>>> from numpy.linalg import solve
>>> x = solve(A, b)                # Finds solution
>>> print ('x =', x)
x = [ -1.4057971 -0.1884058 0.92753623]   # The solution
>>> print ('Residual =', dot(A, x) - b)   # LHS-RHS
Residual = [4.44089210e-16 0.00000000e+00 -3.55271368e-15]
```

这真的令人印象深刻。我们已用单个命令 solve 求解了整个线性方程组（通过消元），用单个命令 dot 执行了矩阵乘法，用通常的运算符执行了矩阵减法，得到的残差本质上等于机器精度。

⁶ 不要为虽然我们认为这些向量是 3 × 1，但它们有时会被打印为 1 × 3 而困扰；想想能节省多少树木！

尽管有更高效的数值方法，直接求解

**A** **x** = **b** (6.32)

的方法是计算逆 **A**⁻¹，然后将等式两边乘以逆，得到

**x** = **A**⁻¹ **b** (6.33)

```
>>> from numpy.linalg import inv      # Test inverse
>>> dot(inv(A), A)
array([[ 1.00000000e+00, -1.33226763e-15, -1.77635684e-15],
       [ 8.88178420e-16,  1.00000000e+00,  0.00000000e+00],
       [ -4.44089210e-16,  4.44089210e-16,  1.00000000e+00]])
>>> print ('x =', dot(inv(A), b))
x = [-1.4057971 -0.1884058 0.92753623]      # Solution
>>> print ('Residual =', dot(A, x) - b)
Residual = [ 4.44089210e-16  0.00000000e+00 -3.55271368e-15]
```

这里我们首先通过查看 A 乘以 inv(A) 是否等于单位矩阵来测试 inv(A) 是否确实是 A 的逆。然后我们使用逆直接求解矩阵方程，得到了与之前相同的结果（在机器精度水平上的一些误差是可以的）。

我们的第二个例子出现在立方体主轴系统的求解中，要求我们找到使惯性张量对角化的坐标系。这需要求解特征值问题

**I** **ω** = λ **ω** , (6.34)

其中 **I** 是惯性矩阵（张量），**ω** 是未知特征向量，λ 是未知特征值。程序 Eigen.py 求解特征值和向量，并展示了处理矩阵是多么容易。这里以简化的解释模式给出：

```
>>> from numpy import *
>>> from numpy.linalg import eig
>>> I = array([[2./3, -1./4], [-1./4,2./3]])
>>> print('I =\n', I)
I =
[[ 0.66666667 -0.25 ]
 [-0.25  0.66666667 ]]
>>> Es, evectors = eig(I)                 # Solves eigenvalue problem
>>> print('Eigenvalues =', Es, '\n Eigenvector Matrix =\n', evectors)
Eigenvalues = [ 0.91666667  0.41666667 ]
Eigenvector Matrix =
[[ 0.70710678  0.70710678 ]
 [-0.70710678  0.70710678 ]]
>>> Vec = array([ evectors[0, 0], evectors[1, 0] ])
>>> LHS = dot(I, Vec)                     # Matrix x vector
>>> RHS = Es[0]*Vec                       # Scalar mult
>>> print('LHS - RHS =', LHS-RHS)         # Test for zero
LHS - RHS = [ 1.11022302e-16 -1.11022302e-16]
```

我们在这里看到，在第 3 行设置数组 I 之后，我们然后用第 8 行的单个语句 Es, evectors = eig(I) 求解其特征值和特征向量。然后我们在第 14 行提取第一个特征向量，并连同第一个特征值一起检查 (6.34) 是否确实在机器精度内得到满足。

好吧，我们认为到现在你已经对 NumPy 的使用有了一些概念。在表 6.1 中我们指出了更多可用的内容。

**表 6.1 NumPy 的运算符及其效果。**

| Operator | Effect | Operator | Effect |
|---|---|---|---|
| dot(a, b[,out]) | Dot product arrays | vdot(a, b) | Dot product |
| inner(a, b) | Inner product arrays | outer(a, b) | Outer product |
| tensordot(a, b) | Tensor dot product | einsum() | Einstein sum |
| linalg.matrix_power(M, n) | Matrix to power n | kron(a, b) | Kronecker product |
| linalg.cholesky(a) | Cholesky decomp | linalg.qr(a) | QR factorization |
| linalg.svd(a) | Singular val decomp | linalg.eig(a) | Eigenproblem |
| linalg.eigh(a) | Hermitian eigen | linalg.eigvals(a) | General eigenvalues |
| linalg.eigvalsh(a) | Hermitian eigenvals | linalg.norm(x) | Matrix norm |
| linalg.cond(x) | Condition number | linalg.det(a) | Determinant |
| linalg.slogdet(a) | Sign and log(det) | trace(a) | Diagonal sum |
| linalg.solve(a, b) | Solve equation | linalg.tensorsolve(a, b) | Solve ax = b |
| linalg.lstsq(a, b) | Least-squares solve | linalg.inv(a) | Inverse |
| linalg.pinv(a) | Penrose inverse | linalg.tensorinv(a) | Inverse N–D array |

## 6.6 练习：测试矩阵程序

在你指示计算机对某个矩阵的数百万个元素进行繁重的计算之前，最好先在小型矩阵上测试你的程序，尤其是你知道正确答案的矩阵。这样，你只需很短的时间就能意识到让调用程序完美有多困难。以下是一些练习。

- 1. 求

  A = ⎛ +4  −2  +1 ⎞
      ⎜ +3  +6  −4 ⎟
      ⎝ +2  +1  +8 ⎠.

  的数值逆。

  - a) 作为一般性检查，即使你不知道解析答案，也检查你的逆在两个方向上；即检查 A A⁻¹ = A⁻¹ A = I，并注意这是成立的小数位数。这也让你对计算的精度有所了解。
  - b) 确定你的数值逆与解析结果之间的一致小数位数：

    A⁻¹ = 1/263 ⎛ +52  +17  +2 ⎞
                ⎜ -32  +30  +19 ⎟
                ⎝  -9   -8  +30 ⎠

    这与 A A⁻¹ 中的误差相似吗？

- 2. 考虑与之前相同的矩阵 A，现在用于描述三个同时线性方程，A x = b，或显式地，

  ⎛ a00 a01 a02 ⎞ ⎛ x0 ⎞   ⎛ b0 ⎞
  ⎜ a10 a11 a12 ⎟ ⎜ x1 ⎟ = ⎜ b1 ⎟ .   (6.35)
  ⎝ a20 a21 a22 ⎠ ⎝ x2 ⎠   ⎝ b2 ⎠

  现在 RHS 上的向量 b 假定已知，问题是求解向量 x。使用适当的子程序求解这些方程，对这三个不同的 b 值求解三个不同的 x 向量：

  b₁ = ⎛ +12 ⎞ ,  b₂ = ⎛ +4 ⎞ ,  b₃ = ⎛ +20 ⎞
       ⎜ -25 ⎟       ⎜ -10 ⎟       ⎜ -30 ⎟
       ⎝ +32 ⎠       ⎝ +22 ⎠       ⎝ +40 ⎠

  解应为

  x₁ = ⎛ +1 ⎞ ,  x₂ = ⎛ +0.312 ⎞ ,  x₃ = ⎛ +2.319 ⎞
       ⎜ -2 ⎟       ⎜ -0.038 ⎟       ⎜ -2.965 ⎟ .   (6.36)
       ⎝ +4 ⎠       ⎝ +2.677 ⎠       ⎝ +4.790 ⎠

- 3. 考虑矩阵

  A = ⎛  α   β ⎞
      ⎝ -β   α ⎠

  其中你可以自由使用你想要的 α 和 β 值。使用数值特征值问题求解器证明特征值和特征向量是共轭复数：

  x₁,₂ = ⎛ +1 ⎞ ,  λ₁,₂ = α ∓ iβ .   (6.37)
          ⎝ ∓ i ⎠

- 4. 使用你的特征值问题求解器求矩阵的特征值

  A = ⎛ -2  +2  -3 ⎞
      ⎜ +2  +1  -6 ⎟ .   (6.38)
      ⎝ -1  -2  +0 ⎠

  - a) 验证你得到特征值 λ₁ = 5, λ₂ = λ₃ = -3。注意重根可能导致问题。特别是，它们的特征向量存在唯一性问题，因为这些特征向量的任意组合也是特征向量。

