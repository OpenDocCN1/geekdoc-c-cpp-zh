

# 求解线性方程组

在扫描过程中从右向左处理：第一个子矩阵为 $\{a_{ij}\}\{i,j=2:n\}$，第二个是 $\{a_{ij}\}\{i,j=3:n\}$ 的变换版本，以此此类推。

下面给出的矩阵新方法使用了了刚刚讨论的思想。

```cpp
Vector Matrix::gauss(const Vector & RHS) const {
  double multiplier = 0;
  Matrix G(nRows, nRows, pA);
  Vector h(nRows, RHS.pA);

  for(int j = 0; j < nCols; j++)column to be swept
    for(int jj = j + 1; jj < nCols; jj++)current operation column
      if(G[j][jj] == 0) {
        cout << "Oops! Division by 0!" << endl;
        exit(1);
      }

      for(int i = j + 1; i < nRows; i++)work down rows
        multiplier = G[i][j]/G[j][j];
        pA[i][jj] = pA[i][jj] - multiplier*G.pA[j][jj];
    }

  for(int i = j + 1; i < nRows; i++)do the same to the RHS
    multiplier = G[i][j]/G[j][j];
    h.pA[i] = h.pA[i] - multiplier*h.pA[j];

  Vector b = G.backward(h);
  return b;
}
```

在我们的 R 计算中，ATemp 和 cTemp 的角色由此列表中的 G 和 h 承担。这些量是通过使用（调用时的）左侧矩阵和作为方法参数提供的右侧向量来初始化的。算法通过遍历 G 的列进行，仅处理对角线下方的元素，同时使用前一节中的向后方法对 h 执行相同的计算。在递归结束时，G 是上三角矩阵，且系统得以求解。现在可以检查，将此 C++ 程序应用于我们在 R 中为示例创建的矩阵和向量，可以证明该命题。

扫描算法的复杂度为 O(n^3) 次浮点运算（练习 7.3）。当 A 的某个对角线元素或其某个高斯变换元素较小时，使用这种方法可能会出现问题。可以通过实现合适的行交换策略来避免这种情况，例如部分主元可以确保任何倍倍的绝对值都不会超过1（练习 7.2）。

## 7.2.3 Cholesky 分解

当我们线性方程组中的矩阵 A 是正定的时，可以使用 Cholesky 分解将其转换为上三角形式。虽然该方法在目标矩阵接近奇异时可能会表现出一些数值不准确性，但它在今天仍然很有用，并在统计学中占据重要地位。

为了在学习 Cholesky 算法之前理解其基本前提，假设对于 $A = \{a_{ij}\}$，可以写成 $A = LL^T$，其中 $L$ 为

```
$L = \begin{pmatrix} l_{11} & 0 & 0 & 0 \\ l_{21} & l_{22} & 0 & 0 \\ l_{31} & l_{32} & l_{33} & 0 \\ \vdots & \vdots & \vdots & \vdots \\ l_{n1} & l_{n2} & l_{n3} & l_{nn} \end{pmatrix}$
```

但，如果是那样的话，系统 $A = LL^T$ 可以直接根据 $A$ 的元素解出 $L$ 的元素 $l_{ij}$。这种方法产生了：

```
$l_{11} = \sqrt{a_{11}}$
$l_{21} = a_{21}/l_{11}$
\vdots
$l_{n1} = a_{n1}/l_{11}$
```

导致：

```
$l_{22} = \sqrt{a_{22}-l_{21}^2}$
$l_{32} = (a_{32}-l_{31}l_{21})/l_{22}$
\vdots
$l_{n2} = (a_{n2}-l_{n1}l_{21})/l_{22}$
```

通用或第 $j$ 步为：

```
$l_{jj} = \sqrt{a_{jj}-\sum_{k=1}^{j-1}l_{jk}^2} \quad (7.2)$
$l_{ij} = (a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk})/l_{jj}, \quad i=j+1,\dots,n. \quad (7.3)$
```

Cholesky 递归可以在算法 7.2 中进行总结。

**算法 7.2** Cholesky 算法
$l_{11} = \sqrt{a_{11}}, a_{i1}/l_{11}, i=2,\dots,n$
for $j=2,\dots,n-1$ **do**
$l_{jj} = \sqrt{a_{jj}-\sum_{k=1}^{j-1}l_{jk}^2}$
$l_{ij} = (a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk})/l_{jj}, i=j+1,\dots,n$
**end for**
$l_{nn} = \sqrt{a_{nn}-\sum_{k=1}^{n-1}l_{nk}^2}$

该算法使用 (7.2)–(7.3) 对 $A$ 进行分解。然后，给定 $L$，如第 7.2 节所示通过正向代换和反向求解 $Ab=c$。与高斯消元一样，Cholesky 算法的复杂度为 $n^3$。然而，可以证明它只需要高斯消元一半的工作量（练习 7.3）。

```cpp
Forward-solve $L=c$ for $h$
Back-solve $L^Tb=h$ for $b$
```

# 求解线性方程组

实现算法 7.2 的细节收集到了另一个新方法中。

```cpp
Matrix::cholesky(const Vector& RHS) const {
    double temp = 0;
    Matrix G(nRows, nCols);
    for(int j = 0; j < nRows; j++){proceed by columns
        if(pA[j][j] == 0) {
            cout << "Singular system!" << endl;
            exit(1);
        }
        temp = pA[j][j];starting value for diagonal
        if (j > 0) {
            for(int k = 0; k < j; k++)
                temp += G[j][k];
        }
        G[j][j] = sqrt(temp);
    }
    for(int i = j + 1; i < nRows; i++){now the rest
        temp = pA[i][j];
        for(int k = 0; k < j; k++)
            temp -= G[i][k];
        G[i][j] = temp/G[j][j];
    }
    cout << "Cholesky factor:" << endl;
    G.printMatrix();
    Vector h = G.forward(RHS);
    Vector b = G.backward(h);
    return b;
}
```

代码实现了算法 7.2 的方案以计算下三角 Cholesky 因子并将其存储在 Matrix 中。通常不需要保留 G，尽管第 7.2.5 节的发展表明并非总是如此。一旦获得了 G，它提供了用于正向求解的矩阵。将我们的 Cholesky 方法应用于上一节构造的矩阵，产生了一个 Cholesky 因子：

| 1.678801 | 0 | 0 | 0 |
| -1.873512 | 1.383693 | 0 | 0 |
| -0.124054 | 1.22679 | 0.767374 | 0 | 0 |
| -2.497718 | 0.600928 | 1.135503 | 0.362715 | 0 |
| -0.064936 | -0.762812 | -0.869516 | -1.025312 | 0.590260 |

```
-303.8929
-99.34466
153.1515
-128.2426
-33.69567
``` 解与之前高斯消元返回的结果一致。为了检查 Cholesky 因子的准确性，我们可以将其与执行 Cholesky 分解的 R 函数产生的答案进行比较，即：

```r
> chol(A)
  [1]         [2]         [3]         [4]         [5]
[1] 1.678801 -1.873512 -0.124054 -2.497715 -0.644936
[2] 0.000000  1.383693  1.227898  0.600928 -0.768212
[3] 0.000000  0.000000  0.767374  1.135502 -0.869516
[4] 0.000000  0.000000  0.000000  0.367215 -1.025312
[5] 0.000000  0.000000  0.000000  0.000000  0.590620
```

两个 Cholesky 因子除了 R 函数返回的是上三角因子外是一致的。因此，在 R 中使用 Cholesky 分解求解系统时，使用上三角因子的转置进行正向求解，并使用 `chol` 返回的因子进行反向求解。在语言上这翻译为

```r
> U <- chol(A)
  h <- forwardsolve(t(U), cVector)
  backsolve(U, h)
[1] -30.89287 -99.34466 153.15147 -128.2426
```

另一种选项是使用 Cholesky 方法计算逆矩阵 $A^{-1}$。这是通过 `chol2inv` 函数完成的，它接受从 `chol` 获取的 Cholesky 因子作为输入。再次例如，这产生了：

```r
> chol2inv(chol(A))%%Vector
  [1]
[1] -30.89287
[2] -99.34466
[3] 153.15147
[4] -128.2426
[5] -33.69567
```

## 7.2.4 带状矩阵

感兴趣的是，如果当 $|i - j| > q$ 时 $a_{ij} = 0$，则矩阵 $A = \{a_{ij}\}$ 被称为带宽为 $q$ 的带限制结构。例如，下面的矩阵是 $6 \times 6$ 且是双带的：

| a11 | a12 | a13 | 0 | 0 | 0 |
| a21 | a22 | a23 | a24 | 0 | 0 |
| a31 | a32 | a33 | a34 | a35 | 0 |
| 0 | a42 | a43 | a44 | a45 | a46 |
| 0 | 0 | a53 | a54 | a55 | a56 |
| 0 | 0 | 0 | a64 | a65 | a66 |

对于正定矩阵 $A$，很容易看出 Cholesky 分解中的矩阵 $L$ 具有 $A$ 相同的下带宽（练习 7.6）。因此，通过关注非零矩阵元素可以大幅减少计算量。

假设我们不在边界处；即对于给定的索引 $i$，$i \pm q$ 都是行列索引。那么，通过追溯我们之前在非带状情况下的推论，非带

