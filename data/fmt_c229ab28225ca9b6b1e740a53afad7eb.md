
## 28.17 计算偏导数

```cpp
polynomial<double> p(1, yy);
P(3) = polynomial<polynomial<polynomial<double>>>(Zero, One);
```

这完成了节点基函数 $p_0, p_1, p_2$ 和 $p_3$ 的定义。现在，这些定义被用于计算在四面体上三个基函数三乘积的积分：

```cpp
print(integral(P[0]*P[1]*P[2]));
printf("\n");
print(integral(P[1]*P[2]*P[3]));
printf("\n");
print(integral(P[2]*P[3]*P[0]));
printf("\n");
print(integral(P[3]*P[0]*P[1]));
printf("\n");
return 0;
```

## 28.17 计算偏导数

在这里我们定义一个计算并返回多项式参数第 $k$ 阶导数的函数。为此，我们使用了第 28.4 节中定义的 `C()` 函数。

```cpp
template<class T>
const polynomial<T> d(const polynomial<T>& p, int k) {
  if (k > p.degree())
    return polynomial<T>(1, 0);
}
```

显然，如果 $k$ 大于多项式的次数，则返回零多项式。另一方面，如果 $k$ 小于或等于多项式的次数，则将第 $k$ 阶导数存储在多项式对象 `dp` 中：

```cpp
polynomial<T> dp(p.degree() + 1 - k, 0);
for (int n = 0; n < dp.degree(); n++)
  dp(n) = C(n + k) * p[n + k];
return dp;
} // kth 阶导数
```

上述函数现在被用于计算二元多项式的 $(j, k)$ 阶偏导数：

## 第 28 章附录：练习题

```cpp
template<class T>
const polynomial<polynomial<T>>& d(const polynomial<polynomial<T>>& p, int j, int k) {
  polynomial<polynomial<T>> zero(1, 0);
  if (k < p.degree())
    return polynomial<polynomial<T>>(1, zero);
}
```

注意 `p.degree()` 并不是通常意义上的 $p$ 的次数，而是 $p = \sum_n a_n(x)^y$ 中的 $y$ 幂次。显然，如果 $k$ 大于这个数字，则返回零多项式且函数终止。否则，函数继续计算 $(j,k)$ 阶偏导数，使用之前的函数来计算 $a_n(x)$ 的第 $i$ 阶导数。

```cpp
polynomial<polynomial<T>> dp(p.degree() + 1, zero);
for (int n = 0; n < p.degree(); n++)
  dp(n) = C(n + k, k) * d(p[n + k], j);
return dp; // (j,k) 阶偏导数
```

最后，以下函数使用之前的函数来计算三元多项式的 $(i,j,k)$ 阶偏导数：

```cpp
template<class T>
const polynomial<polynomial<polynomial<T>>>& d(const polynomial<polynomial<polynomial<T>>>& p, int i, int j, int k) {
  polynomial<polynomial<T>> zero(1, 0);
  polynomial<polynomial<T>> Zero(1, zero);
  if (k < p.degree())
    return polynomial<polynomial<polynomial<T>>>(1, Zero);
}
```

再次，“p.degree()" 是 $p = \sum_n a_n(x,y)z^n$ 中最大的 $z$ 幂次。显然，如果 $k$ 大于这个数字，则返回零多项式且函数终止。否则，函数继续计算 $(i,j,k)$ 阶偏导数，使用 $a_n(x)$ 的 $(i,j)$ 阶偏导数。

```cpp
polynomial<polynomial<polynomial<T>>> dp(p.degree() + 1, zero);
for (int n = 0; n <= p.degree(); n++)
  dp(n) = C(n + k, k) * d(p[n + k], i, j);
return dp; // (i,j,k) 阶偏导数
```

## 28.18 稀疏多项式的复合

在这里我们使用第 25 章 25.7 节中的 `operator()` 函数产生两个给定稀疏多项式 $p(x)$ 和 $q(x)$ 的复合 $p \circ q$。操作如下：首先，将 $p = \sum a_ix^i$ 转换为“两个”变量的虚拟多项式：

```math
$p_2(x, y) = \sum_i a_i(x)y^i$
```

其系数 $a_i(x) \equiv a_i$ 实际上完全不依赖于 $x$。然后，将原始的 `operator` 函数应用于此虚拟多项式，以计算在固定参数 $y=q$ 处的多项式值：

```math
$p_2(x, q) = \sum a_iq^i = p \circ q$
```

```cpp
template<class T>
const sparsePolynomial<T>& operator(const sparsePolynomial<T>& p, const sparsePolynomial<T>& q) {
  sparsePolynomial<T> result;
  // ... (实现细节)
  return result;
}
```

*(注：此处原文示例中代码实现不完整，翻译保持结构对齐)*

## 28.19 稀疏多项式的运算

在这里我们使用第 25 章 25.7 节中的 `operator()` 函数产生两个给定稀疏多项式 $p(x)$ 和 $q(x)$ 的复合 $p \circ q$。操作如下：首先，将 $p = \sum a_ix^i$ 转换为“两个”变量的虚拟多项式：

```math
$p_2(x, y) = \sum_i a_i(x)y^i$
```

其系数 $a_i(x) \equiv a_i$ 实际上完全不依赖于 $x$。然后，将原始的 `operator` 函数应用于此虚拟多项式，以计算在固定参数 $y=q$ 处的多项式值：

```math
$p_2(x, q) = \sum a_iq^i = p \circ q$
```

```cpp
template<class T>
const sparsePolynomial<T>& operator(const sparsePolynomial<T>& p, const sparsePolynomial<T>& q) {
  sparsePolynomial<T> result;
  // ...
  return result;
}
```

*(注：提供的原文文本中 28.18 和 28.19 内容似乎高度重复，此处根据翻译要求逐行翻译)*

## 28.20 刚度矩阵

我们刚刚进入了对 $M$ 中形式为 $t$ 的四面体的循环。指针 `runner` 指向网格中的其余四面体，它已从一个简单的四面体链表指针显式转换为指向四面体具体网格的指针。通过这种方式，可以通过编写 `*runner()` 调用底层链表对象的 `operator()` 来仅引用链表“尾部”中的第一个四面体，也可以引用 3x3 矩阵 $S$ 的成员函数，定义如下：

```cpp
matrix3 S((*runner())[1]() - (*runner())[0](),
          (*runner())[2]() - (*runner())[0](),
          (*runner())[3]() - (*runner())[0]());
```

```cpp
matrix3 weight = Sinverse * transpose(Sinverse);
for (int i = 0; i < 4; i++) {
  int I = (*runner())[i].getIndex();
}
```

我们进入了内层循环，该循环在 `runner` 指向的四面体顶点上运行。在这个内层循环中遇到的每个顶点 $i$，整数 $T$ 表示其在节点列表 $N$ 中的索引 $i$。然后，检查 $i$ 是否为 $b$ 中的边界点。如果是，则将动态向量 `boundary` 中对应的分量赋值：

```cpp
if (((*runner())[i][0] >= 1. - 1.e-6
  || ((*runner())[i][1] <= 1.e-6)
  || ((*runner())[i][1] >= 1. - 1.e-6)
  || ((*runner())[i][2] <= 1.e-6)
  || ((*runner())[i][2] >= 1. - 1.e-6))
  boundary(I) = 1);
```

```cpp
for (int i = 0; i < 4; i++) {
  int I = (*runner())[i].getIndex();
  for (int j = 0; j < 4; j++) {
    int J = (*runner())[j].getIndex();
  }
}
```

我们刚刚进入了对 `runner` 指向的四面体 $t$ 顶点的双重嵌套循环。索引 $T'$ 和 $J$ 代表第 26 节 26.1 节中用于索引顶点 $i$ 和 $j$ 的索引。因此，我们实际上计算了四面体 $t$ 对 $A$ 中第 $(T',J')$ 个元素的贡献。为此，我们区分了两种情况：如果构建的矩阵中第 $T'$ 行已存在，则将此贡献直接加到上面：

```cpp
if (item[i]) {
  row<T> r(gradient[j] * weight * gradient[i], J);
  *item[I] += r;
} else
  item[I] = new row<T>(gradient[j] * weight * gradient[i], J);
```

接下来，我们还来自四面体 $t$ 对边界矩阵 $A$ 的潜在贡献，这是刚度矩阵 $As$ 中的第二项。这是通过对形式为 $k \in t$ 的顶点的内层循环实现的，这些顶点与外层循环遍历的顶点 $i$ 和 $j$ 共同构成一个形式为 $\Delta(i,j,k)$ 的三角形，位于：

```cpp
for (int k = 0; k < 4; k++) {
  int K = (*runner())[k].getIndex();
  if ((i != j) && (j != k) && (k != i)
      && boundary[I]
      && boundary[J]
      && boundary[K]) {
  }
}
```

这个 `if` 问题确保了 $\Delta(i,j,k)$ 确实是 $b$ 中的边界三角形。它对 $A_b$ 中第 $(T',J')$ 元素的贡献现在被计算，方法与第 28.10 节中的叉积运算符类似：

```cpp
point3 jMinusi = (*runner())[j]() - (*runner())[i]();
point3 kMinusi = (*runner())[k]() - (*runner())[i]();
double boundaryTerm = 12 * norm(jMinusi & kMinusi) / 24;
row<T> boundaryTerm(boundaryTerm, J);
*item[I] += boundaryTerm;
```

对 $A_b$ 中 $(T',J')$ 元素的相同贡献也必须进入对应的对角线元素，即 $A_b$ 中的 $(T',J')$ 元素：

```cpp
row<T> boundaryTermI(boundaryTerm, I);
*item[I] += boundaryTermI;
}
}
}
// 构建刚度矩阵
```

## 28.21 牛顿质量矩阵

这完成了 $\alpha = 1$ 时刚度矩阵 $A^{(s)}$ 的构建。

## 28.21 牛顿质量矩阵

在这里，我们实现了接受四个参数（通过引用）的构造函数：网格 `m`

```cpp
template<class T>
sparseMatrix<T>::sparseMatrix(mesh<tetrahedron>& m,
  const list<polynomial<polynomial<T>>>& P,
  const dynamicVector<T>& v, dynamicVector<T>& f) {
  item = dynamicVector<T>*[number = m.index()];
  f = dynamicVector<T>(number, 0.0);
  for (int i = 0; i < number; i++)
    item[i] = 0;
  polynomial<T> zero(1, 0);
  polynomial<polynomial<T>> Zero(1, zero);
}
```

以下循环遍历网格中所有形式为 $t = (k, l, n)$ 的四面体：

```cpp
for (const mesh<tetrahedron>* runner = &m;
     runner = (const mesh<tetrahedron>*)runner->readNext()) {
  matrix3 S((*runner())[1] - (*runner())[0](),
            (*runner())[2] - (*runner())[0](),
            (*runner())[3] - (*runner())[0]());
}
```

这定义了 $3 \times 3$ 矩阵 $S$。下面的三维多项式 `V` 首先设置为零，然后在 `runner` 指向的四面体的内层循环中恢复为 $v_k P_{k,t}+v_l P_{l,t}+v_m P_{m,t}+v_n P_{n,t}$。在第 28.16 节中存储的、用于计算并传递给构造函数的多项式列表 `P`：

```cpp
polynomial<polynomial<T>> V(1, Zero);
for (int i = 0; i < 4; i++) {
  int I = (*runner())[i].getIndex();
  V += v[I] * P[i];
}
polynomial<polynomial<T>> V2 = V * V;
polynomial<polynomial<T>> V3 = V2 * V;
double dtS = det(S);
for (int i = 0; i < 4; i++) {
  int I = (*runner())[i].getIndex();
  f(I) += dtS * integral(V3 * P[i]);
  for (int j = 0; j < 4; j++) {
    int J = (*runner())[j].getIndex();
    double Jacobian = dtS * integral(V2 * P[j]);
    if (item[I]) {
      row<T> Jacobian(Jacobian, J);
      item[I] += Jacobian;
    } else {
      item[I] = new row<T>(Jacobian, J);
    }
  }
}
// 构建牛顿质量矩阵
```

在给定网格函数 $v$ 处完成了牛顿质量矩阵 $A^{(n)}$ 的构建。作为副作用，还计算了 $f(v)$ 并存储在通过引用传递给构造函数的动态向量 $f$ 中。

## 28.22 亥姆霍兹质量矩阵

这是产生亥姆霍兹矩阵 $A^{(h)}(v)$ 的构造函数，其中 $v$ 是 $(\mathbb{R}^2)^N$ 中的给定网格函数。作为副作用，构造函数还产生了网格函数 $f(v) \in (\mathbb{R}^2)^N$，即 $v$ 在 $f$ 下的像。由于这是一个带有存储 $f_i \in \mathbb{R}^2$ 的非常量动态向量，输出 $f(v)$ 确实保存在其中供后续使用。

## 28.22 亥姆霍兹矩阵

假设用户调用此构造函数时 `T` 为 `matrix2`，以存储所需的 $2 \times 2$ 块 $A_{i,j}^{(h)}$。

```cpp
template<class T>
sparseMatrix<T>::sparseMatrix(mesh<tetrahedron>& m,
```
