

```
else
    tildeF(i) -=
        item[i]->maskAll(DirichletBoundary, tildeF);
```

通过这种方式，从原始系统 $A(\tilde{x}) = f$ 的两侧减去相同的量，从而得到一个等价的系统。该函数以以下内容结尾：

```
}
}  // 设置 Dirichlet 边界条件
```

## A.34 在电力系统中组装散度方程

为了解决第 29 章末尾的三个最终练习，我们在此处将上述 A.32 节中组装的矩阵进行扩展，将其下方的矩形矩阵 $Z$ 和其右侧的转置 $Z^t$ 放置起来，其中 $Z$ 的每一行是通过将散度方程与某个仅在单个四面体中为 1、在其他地方为 0 的函数进行积分而得到的（或者换句话说，通过对网格中某个四面体 $t$ 中的散度方程进行积分得到）。为此，请回忆单位（或参考）四面体 $T$ 通过仿射映射 $D_t$ 映射到 $t$，其雅可比矩阵为 $S_t$（第 27.1 节）。因此，$t$ 中的节点基函数（在 $t$ 的一个角上值为 1，在其他三个角上值为 0 的线性函数）可以写成复合函数，即先应用 $D_t^{-1}$，然后应用 $T$ 中对应的节点基函数。根据链式法则（第 10.11、12.5、28.5 和 30.10 节），我们知道 $t$ 中原始节点基函数的梯度等于 $S_t^{-1}$ 乘以 $T$ 中对应节点基函数的梯度。幸运的是，后者的梯度具有非常简单的形式：它是 $(-1,-1,-1)^t$、$(1,0,0)^t$、$(0,1,0)^t$ 或 $(0,0,1)^t$，这些值已分别存储在 "point3" 对象的 "gradient[0]"、"gradient[1]"、"gradient[2]" 和 "gradient[3]" 中（第 A.32 节）。

此外，上述复合形式对于积分 $t$ 中的节点基函数也很有用。实际上，人们可以只对参考四面体 $T$ 进行积分，并将结果乘以 $S_t$ 行列式的绝对值。由于单位四面体的体积为 $1/6$，常值函数 1 在 $t$ 上的积分为 $|\det(S_t)|/6$。

系数矩阵的阶数（或离散系统中的未知量数）等于 A.32 节中组装的矩阵的阶数加上矩形矩阵 $Z$ 的行数。幸运的是，$Z$ 的行数也是可用的：它与网格中四面体的数量相同，可以从基类 "linkedList" 继承的函数 "length()" 中获取。

尽管如此，网格中的四面体必须被索引，以便能够在离散系统中引用与每个四面体相关的未知量（或矩阵行）。为此，必须在第 13.3 节中的原始 "finiteElement" 类中添加一个额外的整数字段：

```
int index;
public
    ...
```

在构造函数中的初始化列表中，通过添加 "index(-1)" 将该字段初始化为平凡负值 -1。此外，拷贝构造函数中的初始化列表

还应包含初始化语句 "index(e.index)"。此外，赋值运算符也应在第 13.3 节中 "if" 块的开头包含以下代码行：

```
index = e.index;
```

最后，"finiteElement" 类的代码块还应包含两个额外的成员函数，用于访问有限元在网格中的索引：

```
void setIndex(int i){
index = i;
} // 设置索引

int getIndex() const{
return index;
} // 获取索引
```

最初，网格中的所有四面体都具有平凡索引 -1。随后，在第 13.4 节的 "mesh" 类的成员函数 "indexing()" 中，通过插入代码行

```
int countElements=0;
```

置于函数开头，并在函数中的 "for" 循环内插入代码行

```
runner->item.setIndex(countElements++);
```

来分配非平凡索引。

我们现在可以修改 A.32 节中的构造函数，以组装包含 $Z$ 和 $Z'$ 的扩展矩阵。矩阵的阶数在构造函数开头设置如下：

```
this->item = new row<T>*[
this->number = 3 * nodes + m.length();]
```

（注意，这里我们小心地在继承的成员前添加了 "this →"，因为这是 GNU 编译器新版本的要求。）在构造函数的其他部分，计算并存储 $3 \times 3$ 矩阵 $|\det(S_i)/6|S_i^{-1}$ 以供后续使用：

```
matrix3 SinverseT = transpose(Sinverse);
matrix3 SinverseTdet = fabs(det(S)) * SinverseT;
matrix3 div = (1./6.) * SinverseTdetS;
```

在构造函数的其他部分，在对网格中四面体的 "for" 循环中，在使用索引 "iblock" 的内层 "for" 循环中，定义索引 "I0" 以指代 $Z$ 中对应的行：

```
int I0 = 3 * nodes + (*runner()).getIndex();
```

使用索引 'i' 的更内层 "for" 循环开始方式与 A.32 节中的原始构造函数相同：

```
for(int i=0; i<4; i++){
    int I = (*runner)() [i].getIndex();
```

然而，在这个循环的开头，应插入以下代码行，以构建 $Z$ 中每个块的第 $(I0,I)$ 个元素 [这与 $Z'$ 中对应块的第 $(I,I0)$ 个元素相同]。实际上，该元素是通过对当前外层循环中的四面体 $t$ 中第 'i' 个节点基函数的 x-（如果 "iblock"= 0，表示这是 $Z$ 中的第一个块）、y-（如果 "iblock"= 1，表示这是 $Z$ 中的第二个块）或 z-（如果 "iblock"= 2，表示这是 $Z$ 中的第三个块）偏导数进行积分得到的：

```
T addI0I = (div*gradient[i])[iblock];
if(this->item[I0]){
    row<T> r(addI0I,I+iblock*nodes);
    *this->item[I0] += r;
}
else
    this->item[I0] =
        new row<T>(addI0I,I+iblock*nodes);
if(this->item[I+iblock*nodes]){
    row<T> r(addI0I,I0);
    *this->item[I+iblock*nodes] += r;
}
else
    this->item[I+iblock*nodes] =
        new row<T>(addI0I,I0);
f(I+iblock*nodes) += addI0I * x[I0];
f(I0) += addI0I * x[I+iblock*nodes];
```

其余部分与上述 A.32 节相同。

## A.35 组装 Navier–Stokes 矩阵

在此处，我们组装应在每个牛顿迭代中求解的 Navier–Stokes 刚度系统（第 31.3 和 31.4 节）。幸运的是，这里的刚度矩阵与上述 A.32 和 A.34 节中组装的电力刚度矩阵几乎相同。需要在 A.32 节的代码中做如下三处修改。

首先，使用索引 "jblock" 的内层循环仅当该索引与外层循环中使用的索引 "iblock" 相同时才应执行。（注意，"jblock" 和 "iblock" 分别代表第 31.4 节中的 k − 1 和 m − 1。）通过这种方式，该内层循环的贡献仅作用于刚度矩阵的对角块部分，符合要求。此外，局部 Helmholtz 参数 "helmBlock" 和局部 $3 \times 3$ 矩阵 "derive" 永远不应定义或使用，因为它们在 Navier–Stokes 系统中无关紧要：

```
for(int jblock=0;jblock<3;jblock++){
    if(iblock==jblock){
        matrix3 weight=
            (Epsilon * fabs(det(S)/6.))
        * Sinverse * transpose(Sinverse);
        T addIJ =
            gradient[j]*weight*gradient[i];
        ...
    }
}
```

其中 "Epsilon" 是小的全局参数 ε。通过这种方式，该循环对刚度矩阵的贡献确实是 Laplace 算子弱形式的有限元离散化，并乘以 ε。

其次，在使用索引 'k' 的下一个循环中，应修改局部变量 "radiation" 和 "radiationMatrix" 的定义，以表明混合边界条件不再涉及复数：

```
double radiation =
    l2norm(jMinusi&kMinusi) / 24.;
T radiationMatrix = radiation;
```

通过这种方式，局部 $2 \times 2$ 矩阵 "radiationMatrix" 只是 $2 \times 2$ 单位矩阵的常数倍，因此它仅表示一个没有虚部的实数。（虽然 Navier–Stokes 系统是实数的，这意味着 'T' 实际上可以是 "double" 而不是 "matrix2"，但我们为了简单起见，此处坚持使用 A.32 节中的原始代码，其中刚度矩阵中的元素是 $2 \times 2$ 块矩阵而不是标量。）

第三，让我们组装第 31.4 节中的线性化项。为此，我们需要存储向量函数 $v$（当前牛顿迭代中的近似解）和梯度 $\nabla v_{iblock+1}$。幸运的是，该梯度在当前四面体中是常数，因此与角点 'i' 或 'j' 无关。这就是为什么它可以被定义得更早，即在使用索引 "iblock" 的更外层循环的开头：

```
for(int iblock=0;iblock<3;iblock++){
    point3 gradX3(0.,0.,0.);
    for(int i=0; i<4; i++){
        int I = (*runner)()[i].getIndex();
        gradX3 +=
            x[I+iblock*nodes][0] * gradient[i];
    }
}
```

[这个三维向量稍后将与 $S_j^{-1}$ 相乘，以根据链式法则得到当前四面体 $T$ 中的 $\nabla v_{iblock+1}$。这段代码本应放置在 A.32 节构造函数的更早位置；我们现在回到当前的代码。]

另一方面，函数 $v$ 确实取决于正在考虑的特定节点（在当前四面体中由 'i' 索引，或在整个网格的节点列表中由 'I' 索引）。

