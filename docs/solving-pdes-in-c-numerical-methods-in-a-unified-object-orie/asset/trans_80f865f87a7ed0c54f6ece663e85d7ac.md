

# A.28 三维中的刚度矩阵和质量矩阵

这里我们实现了一个构造函数，它以三维网格作为参数，并生成第 27.2 节至 27.4 节中定义的刚度、边界和质量矩阵之和。假设网格 M 覆盖单位立方体（如上文第 A.27 节所述），并且 b（施加混合边界条件的边界子集）仅包含该立方体的两个侧面：

b = {(x,y,z) | x(1 − x) = 0}.

```
template<class T>
sparseMatrix<T>::sparseMatrix(
    mesh<tetrahedron>&m) {
    item = new row<T>*[number = m.indexing()];
```

由于“sparseMatrix”类派生自行列表，因此它继承了字段“item”，该字段是指向“row”对象的指针数组。在上面的代码行中，该数组被设置为包含与网格中节点数量一样多的指向行的指针，该数量由应用于“mesh”参数 'm' 的“indexing”函数返回。

接下来，我们定义一个整数向量，以指示网格中特定节点是否为 b 中的边界节点：

```
dynamicVector<int> xBoundary(number,0);
```

该向量（或网格函数）初始化为零。稍后，它将在对应于边界节点 i ∈ b 的索引 i 处取值为 1。

```
for(int i=0; i<number; i++)
    item[i] = 0;
point3 gradient[4];
gradient[0] = point3(-1,-1,-1);
gradient[1] = point3(1,0,0);
gradient[2] = point3(0,1,0);
gradient[3] = point3(0,0,1);
for(const mesh<tetrahedron>* runner = &m;
    runner;
    runner =
        (const mesh<tetrahedron>*)runner->readNext()) {
```

我们刚刚进入了对形式为 t ∈ M 的四面体的循环。指针“runner”，它指向四面体底层链表的“尾部”，被显式地从指向四面体链表的指针转换为指向具体四面体网格的指针。这样，不仅可以通过编写“(*runner)()”[调用底层链表对象的“operator()”]来引用链表“尾部”中的第一个四面体，还可以引用派生“mesh”类的成员函数。

接下来，3 × 3 矩阵 S_t 被定义：

```
matrix3
    S(((*runner)()[1]() - (*runner)()[0](),
       (*runner)()[2]() - (*runner)()[0](),
(*runner)()[3]() - (*runner)()[0]());
 matrix3 Sinverse = inverse(S);
 matrix3 weight =
 fabs(det(S)/6.) *
 Sinverse * transpose(Sinverse);
```

我们现在准备进入内部循环，该循环扫描由“runner”指向的四面体 t 的角点。对于在此内部循环中遇到的每个角点，整数 'I' 表示其在整个网格节点列表中的索引。然后检查 i 是否为 b 中的边界节点。如果是，则构造矩阵中第 'I' 个分量在向量“xBoundary”中的值从 0 增加到 1 或 2，以存储 i 确实是 b 中边界节点的有价值信息：

```
for(int i=0; i<4; i++){
 int I = (*runner())[i].getIndex();
 if(((*runner())[i]()[0] <= 1.e-6)
 xBoundary(I) = 1;
 if(((*runner())[i]()[0] >= 1. - 1.e-6)
 xBoundary(I) = 2;
 }
```

我们现在准备计算 t 对构造矩阵中矩阵元素 a_{i,j} 的贡献，其中 i 和 j 只是 t 的任意两个角点。这是通过对 t 的角点进行一次更内部的循环来完成的，角点在整个网格节点列表中的索引由 'J' 表示：

```
for(int i=0; i<4; i++){
 int I = (*runner())[i].getIndex();
 for(int j=0; j<4; j++){
 int J = (*runner())[j].getIndex();
 }
 }
```

要将 t 的贡献添加到 a_{i,j}，我们区分两种情况：如果构造矩阵中第 'I' 行已经存在，则该贡献通过行操作添加到其中：

```
T mass = fabs(det(S))/120.;
 if(i==j)mass *= 2.;
 if(item[I]){
 row<T> r(mass*gradient[j]*weight*gradient[i],J);
 *item[I] += r;
 }
```

如果另一方面第 'I' 行尚不存在，则必须使用“new”命令构造它：

```
else
 item[I] = new row<T>(mass*gradient[j]*weight*gradient[i],J);
```

接下来，我们还将 t 与 b 上的混合边界条件相关的贡献添加到矩阵元素 a_{i,j}。这是通过对 t 的角点 k~ 进行一次更内部的循环来完成的，该角点与外层循环中扫描的原始角点 i~ 和 j~ 共同构成 b 中的三角形 Δ(i~,j~,k~)：

```
for(int k=0; k<4; k++){
    int K = (*runner())[k].getIndex();
    if((i!=j)&&(j!=k)&&(k!=i)
    &&((xBoundary[I] * xBoundary[J]
    * xBoundary[K]==1) ||
    (xBoundary[I] * xBoundary[J]
    * xBoundary[K]==8)) {
```

这个“if”问题确保 Δ(i~,j~,k~) 确实是 b 中的边界三角形。该三角形对 a_{i,j} 的贡献现在使用三角形面积的事实进行计算

1/2 || (j~ - i~) × (k~ - i~) ||_2 .

其中 ‘×’ 表示三维中的向量积：

```
point3 jMinusi =
    (*runner())[j]() - (*runner())[i]();
point3 kMinusi =
    (*runner())[k]() - (*runner())[i]();
T boundaryTerm =
    l2norm(jMinusi&kMinusi) / 24.;
row<T> boundaryTermJ(boundaryTerm,J);
*item[I] += boundaryTermJ;
```

（参见第 24 章末尾的练习。）此外，相同的贡献也必须进入主对角线元素 a_{i,i}：

```
row<T> boundaryTermI(boundaryTerm,I);
*item[I] += boundaryTermI;
}
}
}
}
} // sum of stiffness, boundary, and mass matrices
```

这完成了刚度、边界和质量矩阵之和的构造

A^{(s)} + A^{(b)} + A^{(m)}.

# A.29 三维中的高阶基函数

这里我们定义了构造第 28.2 节中 56 × 56 矩阵 B 的构造函数。为此，我们使用第 1.17 节末尾定义的函数“C()”。

如果 B 要通过第 3.20 节中的直接方法求逆，则将其存储为第 3.14 节中的稠密动态矩阵是有意义的。这里，我们更倾向于将其实现为稀疏矩阵，以便利用当前的迭代方法。

由于构造函数必须是成员函数，它应首先在“sparseMatrix”类的代码块中声明如下：

```
sparseMatrix(char*);
```

请注意，构造函数采用一个虚拟字符串参数以区别于默认构造函数。以下是完整的定义：

```
template<class T>
sparseMatrix<T>::sparseMatrix(char*){
    item = new row<T>*[number = 56];
    for(int i=0; i<number; i++)
        item[i] = 0;
}
```

一旦 56 行都初始化为零（空）指针，矩阵元素就可以在嵌套循环中设置。外层循环遍历矩阵中的 56 列。事实上，该循环本身是一个三重循环，扫描 T^(5) 中的所有三元组（参见第 28.2 节）。按字典顺序对三元组 (i,j,k) ∈ T^(5) 进行排序的索引 ĵ_{i,j,k} 存储在整数变量 'J' 中：

```
int J = -1;
for(int i=0; i<=5; i++)
    for(int j=0; j<=5-i; j++)
        for(int k=0; k<=5-i-j; k++) {
            J++;
```

现在，为了遍历矩阵中的行，前 40 行被分为四个各十行的子集，与参考四面体 T 的四个角点处求值的偏导数相关联。扫描 10 行子集的每个内部循环本身被实现为一个三重循环，以扫描三元组 (l,m,n) ∈ T^(2)：

```
if((i==l)&&(j==m)&&(k==n)){
    T coef = factorial(i) * factorial(j) *
        factorial(k);
    if(item[I])
        item[I]->append(coef,J);
    else
        item[I] = new row<T>(coef,J);
}
```

此外，接下来的 10 行与在角点 (1,0,0) 处求值的偏导数相关。显然，在该角点处，(n,m,l) 次偏导数仅对 y 次幂恰好为 m、z 次幂恰好为 l 且 x 次幂至少为 n 的单项式非零：

```
if((i==l)&&(j==m)&&(k>=n)){
    T coef = factorial(i) *
        factorial(j) * C(k,n);
    if(item[10+I])
        item[10+I]->append(coef,J);
    else
        item[10+I] = new row<T>(coef,J);
}
```

类似地，接下来的 10 行与在角点 (0,1,0) 处求值的偏导数相关。显然，在该角点处，(n,m,l) 次偏导数仅对 x 次幂恰好为 n、z 次幂恰好为 l 且 y 次幂至少为 m 的单项式非零：

```
if((i>=l)&&(j>=m)&&(k==n)){
    T coef = factorial(i) *
        C(j,m) * factorial(k);
    if(item[20+I])
        item[20+I]->append(coef,J);
    else
        item[20+I] = new row<T>(coef,J);
}
```

类似地，接下来的 10 行与在角点 (0,0,1) 处求值的偏导数相关。显然，在该角点处，(n,m,l) 次偏导数仅对 x 次幂恰好为 n、y 次幂恰好为 m 且 z 次幂至少为 l 的单项式非零：

```
if((i>=l)&&(j==m)&&(k==n)){
    T coef = C(i,l) * factorial(j) *
        factorial(k);
    if(item[30+I])
        item[30+I]->append(coef,J);
    else
        item[30+I] = new row<T>(coef,J);
}
```

这完成了矩阵中的前 40 行。

