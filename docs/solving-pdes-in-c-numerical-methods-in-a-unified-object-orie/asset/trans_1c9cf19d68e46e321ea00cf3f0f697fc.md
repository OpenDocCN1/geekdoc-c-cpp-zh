

## 17.19 近似逆的朴素实现

我们从近似逆的朴素实现开始，该实现使用了过多的行操作。稍后，此实现将通过用更高效的向量操作替换这些昂贵的行操作而得到改进。为此，我们必须首先实现一些初步的运算符和函数。

```cpp
row<T>& operator()(int i) {
return list<row<T> >::operator()(i);
} // read/write ith row
```

此版本仅调用基类 "list" 的 "operator()" 来访问矩阵中的第 "i" 行。通过此版本，不仅可以用 A[i][j] 读取稀疏矩阵 'A' 中的第 "i" 行，还可以用 "A(i)" 读取或更改此行。

```cpp
const T operator*(const row<T>& r) const {
return getColumn() > r.getColumn() ?
r * *this :
r * *this;
}
```

现在，如果当前的 "row" 对象仅包含一个行元素，则所需的实数内积只是该元素与 'r' 中对应元素的乘积：

```cpp
!next ?
getColumn() == r.getColumn() ?
getValue() * r.getValue()
0
```

如果另一方面，当前的 "row" 对象中有多个行元素，则必须使用递归调用来计算并加上当前 "row" 对象的 "尾部" 的贡献：

```cpp
getColumn() == r.getColumn() ?
getValue() * r.getValue()
+ r * *(row<T>*)readNext()
:
r * *(row<T>*)readNext();
} // row times row (real inner product)
```

我们现在使用上述函数来实现形式为 $A(r^t)$ 的乘积，其中 $A$ 是稀疏矩阵，$r$ 是行：

```cpp
template<class T>
const dynamicVector<T>
operator*(const sparseMatrix<T>&M,const row<T>&r){
  dynamicVector<T> result(M.rowNumber(),0.);
  for(int i=0; i<M.rowNumber(); i++)
    result(i) = M[i] * r;
  return result;
}  // matrix times row
```

最后，我们向 "sparseMatrix" 类的块中添加一个成员运算符，该运算符将当前 "sparseMatrix" 对象中的每一行除以动态向量中的对应分量：

```cpp
const sparseMatrix&
operator/=(const dynamicVector<T>&D){
  for(int i=0; i<rowNumber(); i++)
    *item[i] /= D[i];
  return *this;
}  // divide each rows by the components of a vector
```

我们现在准备实现近似逆。这是在 ILU 的上下文中使用的原始版本的 "factorize" 函数的以下版本中完成的。

```cpp
template<class T>
const sparseMatrix<T>
sparseMatrix<T>::factorize(double threshold){
```

首先，我们计算并存储 $A^t$，即当前 "sparseMatrix" 对象的转置：

```cpp
sparseMatrix<T> At = transpose(*this);
```

我们还存储 $W^t$ 和 $Z^t$，并将它们初始化为单位矩阵：

```cpp
sparseMatrix<T> Wt(rowNumber(),1.);
sparseMatrix<T> Zt(rowNumber(),1.);
```

我们还将 $D$ 的主对角线存储在动态向量中：

```cpp
dynamicVector<T> D(rowNumber(),0.);
```

我们现在准备开始算法中的嵌套双循环：

```cpp
for(int i=0; i<rowNumber(); i++){
  row<T> r = *item[i];
```

## 17.20 近似逆的更高效实现

以下实现通过避免昂贵的行操作并用更高效的向量操作替换它们来改进原始实现。为此，我们必须首先定义一些初步的运算符和函数。

以下（普通）运算符使用对行中元素的循环将一行添加到动态向量中：

```cpp
template<class T>
void operator+=(dynamicVector<T>&v, const row<T>&r) {
    for(const row<T>* runner = &r; runner;
        runner = (const row<T>*)runner->readNext())
        v(runner->getColumn()) += runner->getValue();
} // adding a row to a dynamic vector
```

以下构造函数应添加到 "row" 类的块中。它从给定的动态向量构造一行：

```cpp
row(const dynamicVector<T>&v, double threshold=0.) {
    row<T>* runner = this;
    int first = 1;
```

在构造函数开始时，基类 "linkedList" 的默认构造函数被隐式调用，以构造一个仅包含一个（平凡）"rowElement" 对象的平凡链表。局部指针 "runner" 指向底层链表中的最后一个项目，或指向行中的最后一个行元素。局部整数 "first" 指示是否即将定义第一个行元素。以下循环扫描给定动态向量的分量并检测幅度不太小的分量：

```cpp
for(int i=0; i<v.dim(); i++)
    if(fabs(v[i])>threshold) {
```

为了向行添加新的行元素，我们首先需要检查 "first" 是否等于 1，或者这是否是构造的 "row" 对象中的第一个行元素。如果是，则 "runner" 已经指向它，可以用来定义它。如果另一方面，第一个行元素已经定义并且这是一个即将定义的另一个行元素，则必须首先为其分配新的内存，并且 "runner" 必须向前推进以指向此新项目：

```cpp
if(!first) {
    runner->next = new row<T>;
    runner = (row<T>*)runner->next;
}
```

最后，我们定义一个普通运算符来计算两个动态向量的实数内积：

```cpp
template<class T>
const T operator&&(const dynamicVector<T>&u,
    const dynamicVector<T>&v){
    T sum = 0;
    for(int i = 0; i < u.dim(); i++)
        sum += u[i] * v[i];
    return sum;
} // real inner product
```

我们现在准备引入近似逆的改进实现。

```cpp
template<class T>
const sparseMatrix<T>
sparseMatrix<T>::factorize(double threshold){
    sparseMatrix<T> At = transpose(*this);
    sparseMatrix<T> Wt(rowNumber());
    sparseMatrix<T> Zt(rowNumber());
```

与原始实现不同，这里稀疏矩阵 "Wt" 和 "Zt"（将存储 $W^t$ 和 $Z^t$）是由仅带一个参数的构造函数构造的：一个整数，表示矩阵中的行数。然而，行本身仍然未构造且未分配内存。这将在行以其最终形式可用时稍后完成。

```cpp
dynamicVector<T> D(rowNumber(),0.);
for(int i=0; i<rowNumber(); i++){
    row<T> r = *item[i];
```

与原始实现不同，这里 W 中的第 i 列存储在动态向量 "wi" 中，Z 中的第 i 列存储在动态向量 "zi" 中：

```cpp
dynamicVector<T> wi(rowNumber(),0.);
wi(i) = 1.;
dynamicVector<T> zi(rowNumber(),0.);
zi(i) = 1.;
for(int j=0; j<i; j++){
    row<T> wj = -1. * (Zt[j] * r) / D[j] * Wt[j];
    wi += wj;
}
row<T> c = At[i];
for(int j=0; j<i; j++){
    row<T> zj = -1. * (Wt[j] * c) / D[j] * Zt[j];
    zi += zj;
}
```

这样，使用廉价的矩阵-向量乘积来计算 $D_{i,i}$，而不是昂贵的矩阵-行乘积：

```cpp
D(i) = wi && (*this * zi);
```

最后，所需的 W（或 Z）中的第 i 列是从 "wi"（或 "zi"）的那些幅度不太小的分量构造的：

```cpp
Wt.item[i] = new row<T>(wi,threshold);
Zt.item[i] = new row<T>(zi,threshold);
}
*this = transpose(Zt);
return Wt /= D;
} // efficient approximate inverse
```

对于本书中的应用，近似逆（即使使用此高效实现）作为预条件子本身以及作为多网格 V 循环中的松弛方法，都远不如 Gauss–Seidel。 这就是为什么我们在下面的应用中不使用它。 尽管如此，近似逆对于其他类型的应用可能仍有其自身的优势，特别是当考虑并行实现时。 比较近似逆与 [66] 中的并行 ILU 版本的性能将是有趣的。

## 17.21 练习

- 1. "GaussSeidel" 函数必须是 "sparseMatrix" 类的朋友吗？为什么？

- 2. 实现 Kaczmarz 迭代以求解实数或复数稀疏线性系统。 Kaczmarz 迭代等价于应用于正规方程的 Gauss–Seidel 迭代
  A* A x = A* f.
  其中 A* ≡ Āᵀ 是 A 的厄米伴随。 使用第 16 章第 4 节的 "sparseMatrix<complex>" 类。 解可在附录 A.16 节中找到。

- 3. 以这样的方式重写第 17.7 节中 "factorize()" 函数，使得永远不使用填充；也就是说，L 或 U 中的一个元素只有在原始矩阵 A 的对应元素非零时才可以非零。 解可在附录 A.17 节中找到。

- 4. 实现第 16 章第 4 节中声明的 "forwardElimination" 和 "backSubstitution" 函数。 解可在附录 A.17 节中找到。

