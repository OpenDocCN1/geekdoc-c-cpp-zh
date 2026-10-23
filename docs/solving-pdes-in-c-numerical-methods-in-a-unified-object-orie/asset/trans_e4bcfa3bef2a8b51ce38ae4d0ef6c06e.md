

## 23.12 多重网格融合算法

为了定义多重网格融合算法，让我们回到缺陷校正公式的基础公式：

$$A_1(\tilde{x}+\tilde{e}) - A_1(\tilde{x}) = f - A(\tilde{x}).$$

然而在这里，$f$ 是不精确的，因此我们更感兴趣的是近似式

$$A_1(\tilde{x}+\tilde{e}) - A_1(\tilde{x}) \doteq f - A(\tilde{x}),$$

其中 '$\doteq$' 表示近似。

幸运的是，这里假设 $A$ 易于求逆。因此，选择

$$\tilde{x} \equiv A^{-1}(f).$$

是有意义的。

此外，粗网格算子 $A_1$ 定义为

$$A_1 \equiv A P Q^{-1} R A.$$

并且，粗网格校正项 $\tilde{e}$ 以隐式方式定义，使得

$$A_1(\tilde{x}+\tilde{e}) = A(P U),$$

其中 $U$ 是通过将多重网格融合算法递归应用于粗网格而非细网格获得的。在这种递归应用中使用粗网格右端项向量 $F$ 被假设比朴素选择 $R f$ 更精确。例如，可以通过对 $R f^{(1)}, R f^{(2)}, \dots, R f^{(m)}$ 应用上述 max() 函数来生成 $F$：

$$F \equiv \max(R f^{(1)}, R f^{(2)}, \dots, R f^{(m)}).$$

这样，$F$ 确实包含了与粗网格相关的源汇项。然而，$F$ 可能未能包含与多重网格层次中更粗网格相关的源汇项。这就是为什么粗网格问题仍然只是一个使用 '$\doteq$' 而非 '=' 的近似方程。

因此，归纳地假设 $U$ 不仅是粗网格（如朴素解 $Q^{-1}(F)$）在源汇项方面最优融合的图像，而且在更粗的网格上也是最优融合的。只有在没有更粗网格的情况下（两级情况，其中粗网格也是最粗网格），$U$ 才简单地定义为

$$U \equiv Q^{-1} F.$$

另一方面，在三级（或多级）情况下，$U$ 只是隐式地定义为将多重网格融合算法递归应用于粗网格（而非细网格）的结果。

结果是，我们有公式

$$A(P U) - A(P Q^{-1}(R f)) + A(A^{-1}(f)) \doteq f.$$

如果 $A$ 确实如离散拉普拉斯算子那样是线性的，那么这简化为

$$A\left(P U - P Q^{-1} R f + A^{-1} f\right) \doteq f.$$

因此，多重网格融合算法建议我们接受细网格图像

$$P U - P Q^{-1} R f + A^{-1} f,$$

其中 $U$ 通过将相同的多重网格融合算法递归应用于粗网格获得 [82]。

上述公式中的项

$$A^{-1}f - P Q^{-1} R f = (A^{-1} - P Q^{-1} R)f$$

可以被视为一种缺陷校正，它被加到由最佳可用粗网格近似 $U$ 的朴素延拓得到的朴素细网格近似 $PU$ 上。

## 23.13 实现

当前的面向对象框架对于上述多重网格融合算法的实现特别有用。从下面的代码中可以清楚地看出这一点。（为了能够在新版本的 GNU 环境中编译，当前代码在继承成员之前使用了额外的关键字 "this->"。）

首先，我们在第 16 章第 16.4 节的 "sparseMatrix" 类块中定义一个新的构造函数。该构造函数接受稀疏矩阵 `m` 作为参数，并生成包含 `m` 行和的对角矩阵：

```cpp
sparseMatrix(const sparseMatrix&m, char*){
    this->number = m.rowNumber();
    this->item =
        m.rowNumber() ? new row<T>*[m.rowNumber()] : 0;
    for(int i=0; i<m.rowNumber(); i++)
        this->item[i] = new row<T>(m[i].rowSum(),i);
} // 构造对角行和矩阵
```

请注意，为了将上述构造函数与复制构造函数区分开来，它还接受一个虚拟字符串参数。上述行和构造函数稍后将在另一个构造函数中使用，该构造函数仅在 "sparseMatrix" 类块中声明：

```cpp
sparseMatrix(const dynamicMatrix<T>&);
```

现在可以将这个构造函数的详细定义放在该块外部。具体来说，该构造函数接受包含数字图像的动态矩阵 `u`，并使用它来构造第 10 章第 10.4 节中的稀疏系数矩阵。在多重网格融合算法中，特别是，我们将稍后使用平凡均匀图像 `u ≡ 1` 来获得所需的离散拉普拉斯算子。

```cpp
template<class T>
sparseMatrix<T>::sparseMatrix(const dynamicMatrix<T>&u){
    const int N = u.width();
    const int M = u.height();
    const double hx = 1./(N - 1);
```

如果该列已经存在，则调用 "append()" 函数。否则，如果该列尚不存在，则首先使用 "new" 命令为其分配内存。

```cpp
for(int i = 0; i < M; i++)
    for(int j = 0; j < N; j++) {
        if(j<N-1)
            if(this->item[i*N+j])
                this->item[i*N+j]->append(
                    -gradushiftx(i,j,"read"), i*N+j+1);
            else
                this->item[i*N+j] = new row<double>(
                    -gradushiftx(i,j,"read"), i*N+j+1);
        if(i<M-1)
            if(this->item[i*N+j])
                this->item[i*N+j]->append(
                    -gradushifty(i,j,"read"), i*N+j+N);
            else
                this->item[i*N+j] = new row<double>(
                    -gradushifty(i,j,"read"), i*N+j+N);
    }
```

我们现在准备好添加严格下三角部分：

```cpp
*this += transpose(*this);
```

我们现在准备好添加主对角线。为此，我们使用生成对角行和矩阵的构造函数：

```cpp
*this -= sparseMatrix<T>(*this,"rowsum");
```

最后，我们还在主对角线上加一个小正数以避免奇异性：

```cpp
*this += sparseMatrix<T>(rowNumber(), .1);
} // 构造融合矩阵
```

这完成了第 10 章第 10.4 节中稀疏矩阵的构造。特别是，当参数 'u' 是平凡均匀图像 'u ≡ 1' 时，该构造函数生成多重网格融合算法所需的离散拉普拉斯算子。

为了实现该算法，我们还需要在第 17 章第 17.10 节的 "multigrid" 类块中添加更多成员函数。这些函数用于访问多重网格层次中最细层级的私有矩阵，以及访问下一较粗层级的地址：

```cpp
const sparseMatrix<T>& getP() const{
    return P;
} // 读取 P
```

```cpp
const sparseMatrix<T>& getA() const{
    return A;
} // 读取 A
```

```cpp
const sparseMatrix<T>& getR() const{
    return R;
} // 读取 R

const multigrid<T>* getNext() const{
    return next;
} // 获取指向下一层级的指针
```

有了这些函数，我们现在可以定义（在 "multigrid" 类块外部）一个新的二元运算符，它接受向量 f 并返回 A⁻¹ f，使用第 17 章第 17.10 节中的多重网格迭代，并如第 17 章第 17.11 节和附录 A.19 节所示，通过 PCG 加速：

```cpp
template<class T>
const dynamicVector<T>
operator/(const dynamicVector<T>&f,const multigrid<T>&mg){
    dynamicVector<T> x(f.dim(), 0.);
    PCG(mg,mg.getA(),f,x);
    return x;
} // 通过多重网格和 PCG 计算 A^{-1}f
```

使用此运算符，可以简单地写 "f/MG" 来获取 A⁻¹f，其中 'f' 是给定向量，A 是给定 "multigrid" 对象 "MG" 中的系数矩阵。

以下二元运算符将列表中的所有项乘以任意类型的常数值对象：

```cpp
template<class S, class T>
const list<T>
operator*(const S&R, const list<T>&l){
    list<T> R1(l.size(), R * l[0]);
    for(int i=1; i<l.size(); i++)
        R1(i) = R * l[i];
    return R1;
} // 矩阵乘以列表
```

在上面的循环中，局部列表 "R1" 中的项通过第 3 章第 3.4 节中的非常量 "operator()" 访问，并定义为 'R' 乘以原始列表 'l' 中对应的项。上述运算符确实可以在多重网格融合算法中使用，通过将右端项向量列表（从左侧）乘以限制矩阵 R 来将其限制到粗网格。

以下函数实现了上文第 23.9 节中带有两个向量参数的 "max(u,v)" 函数：

```cpp
template<class T>
const dynamicVector<T>
max(const dynamicVector<T>&u, const dynamicVector<T>&v){
    dynamicVector<T> maxuv(u);
    for(int i=0; i<u.dim(); i++)
```

