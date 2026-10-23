
# 附录。部分习题解答

```cpp
if ((i==1)&&(k==0)) {
    T coef = 1. / power(2,j);
    if(item[43])
        item[43]->append(coef,J);
    else
        item[43] = new row<T>(coef,J);
}
```

类似地，接下来的两行对应于在 (0,0,1/2) 处求值的 x- 和 y-偏导数：

```cpp
if ((j==0)&&(k==1)) {
    T coef = 1. / power(2,i);
    if(item[44])
        item[44]->append(coef,J);
    else
        item[44] = new row<T>(coef,J);
}
if ((j==1)&&(k==0)) {
    T coef = 1. / power(2,i);
    if(item[45])
        item[45]->append(coef,J);
    else
        item[45] = new row<T>(coef,J);
}
```

此外，接下来的两行对应于边中点 (1/2,1/2,0)。该点处的法向导数是 z-偏导数与 x- 和 y-偏导数之和除以 $\sqrt{2}$：

```cpp
if(i==1) {
    T coef = 1. / power(2,j+k);
    if(item[46])
        item[46]->append(coef,J);
    else
        item[46] = new row<T>(coef,J);
}
if(!i&&(j||k)) {
    T coef = (j+k) / sqrt(2.) / power(2,j+k-1);
    if(item[47])
        item[47]->append(coef,J);
    else
        item[47] = new row<T>(coef,J);
}
```

类似地，接下来的两行对应于边中点 (1/2,0,1/2)。该点处的法向导数是 y-偏导数与 x- 和 z-偏导数之和除以 $\sqrt{2}$：

```cpp
if (j==1) {
    T coef = 1. / power(2,i+k);
    if(item[48])
        item[48]->append(coef,J);
    else
        item[48] = new row<T>(coef,J);
}
if(!j&&!(i||k)){
    T coef = (i+k) / sqrt(2.) / power(2,i+k-1);
    if(item[49])
        item[49]->append(coef,J);
    else
        item[49] = new row<T>(coef,J);
}
```

类似地，接下来的两行对应于边中点 (0,1/2,1/2)。该点处的法向导数是 x-偏导数与 y- 和 z-偏导数之和除以 $\sqrt{2}$：

```cpp
if (k==1) {
    T coef = 1. / power(2,i+j);
    if(item[50])
        item[50]->append(coef,J);
    else
        item[50] = new row<T>(coef,J);
}
if(!k&&!(i||j)){
    T coef = (i+j) / sqrt(2.) / power(2,i+j-1);
    if(item[51])
        item[51]->append(coef,J);
    else
        item[51] = new row<T>(coef,J);
}
```

最后四行对应于 T 的侧面中点。特别是，下一行对应于 (1/3,1/3,0) 处的法向导数（或 z-偏导数）：

```cpp
if (i==1) {
    T coef = 1. / power(3,j+k);
    if(item[52])
        item[52]->append(coef,J);
    else
        item[52] = new row<T>(coef,J);
}
```

此外，下一行对应于 (1/3,0,1/3) 处的法向导数（或 y-偏导数）：

```cpp
if(j==1){
    T coef = 1. / power(3,i+k);
    if(item[53])
        item[53]->append(coef,J);
    else
        item[53] = new row<T>(coef,J);
}
```

类似地，下一行对应于 (0,1/3,1/3) 处的法向导数（或 x-偏导数）：

```cpp
if(k==1){
    T coef = 1. / power(3,i+j);
    if(item[54])
        item[54]->append(coef,J);
    else
        item[54] = new row<T>(coef,J);
}
```

最后，最后一行对应于 T 最长边的中点 (1/3,1/3,1/3)。该点处的法向导数是 x-、y- 和 z-偏导数之和除以 $\sqrt{3}$：

```cpp
if(i||j||k){
    T coef = (i+j+k) / sqrt(3.) / power(3,i+j+k-1);
    if(item[55])
        item[55]->append(coef,J);
    else
        item[55] = new row<T>(coef,J);
}
```

这就完成了第 28.2 节中 $56 \times 56$ 矩阵 B 的构造函数。一旦线性系统 $B\mathbf{x} = \mathbf{I}^{(q)}$ 求解出未知向量 $\mathbf{x}$，就可以通过以下函数从 $\mathbf{x}$ 生成基函数 $p_q$（其中 $p_q$ 是三个变量的多项式，如第 24.8 节所述）：

```cpp
template<class T>
const polynomial<polynomial<polynomial<T> > > producePolynomial(const dynamicVector<T>&x) {
    polynomial<T> zero(1,0.);
    polynomial<polynomial<T> > Zero(1,zero);
    polynomial<polynomial<polynomial<T> > > p(6,Zero);
    int J = -1;
    for(int i=0; i<=5; i++){
        polynomial<polynomial<T> > A(6-i,zero);
        for(int j=0; j<=5-i; j++){
            polynomial<T> a(6-i-j,0.);
            for(int k=0; k<=5-i-j; k++){
                J++;
                a(k) = x[J];
            }
            A(j) = a;
        }
        p(i) = A;
    }
    return p;
} // 从 x 生成一个 5 次多项式
```

确实，在此函数中，按字典顺序列在 $\mathbf{x}$ 中的系数 $a_{i,j,k}$ 被放置到函数返回的三变量多项式的适当位置。

### A.30 三维网格中的边索引

这里我们为网格中每个四面体的六条边分配一个索引，以指示其在整个网格边列表中的位置。更准确地说，网格中的每条边被赋予两个连续的索引，用于索引与其中点处两个法向导数相关的两个自由度。

为此，每个四面体必须包含一个 56 个整数的数组，以存储其自由度在整个网格自由度列表中的索引。为此，必须如以下修改第 13.3 节中 "finiteElement" 类的代码块：

```cpp
template<class T, int N> class finiteElement{
    node<T>* vertex[N];
    int index[56];
public:
    int readMeshIndex(int i) const{
        return index[i];
    } // 只读索引

    int& meshIndex(int i){
        return index[i];
    } // 读/写索引
    ...
```

通过这种方式，在每个 "finiteElement" 对象中添加了包含 56 个整数的私有数组 "index"，以及公共函数 "readMeshIndex"（用于读取其中的条目）和 "meshIndex"（用于读/写其中的条目）。数组 "index" 将包含分配给当前四面体自由度的索引，以指示它们在整个网格自由度列表中的位置。

将上述数组 "index" 中的条目初始化为默认值 −1 也是一个好主意，可以通过在 "finiteElement" 类构造函数的末尾添加以下循环来实现：

```cpp
for(int i=0; i<56; i++)
    index[i] = -1;
```

类似地，最好在 "finiteElement" 类的拷贝构造函数和赋值运算符的末尾添加一个形式如下的循环：

```cpp
for(int i=0; i<56; i++)
    index[i] = e.index[i];
```

只有当有限元被嵌入到完整的网格中时，才应赋予 "finiteElement" 对象中数组 "index" 的条目更有意义的索引。这就是为什么下面的 "edgeIndexing" 函数（用于分配这些索引）必须是 "mesh" 类的成员，以便它可以应用于当前的 "mesh" 对象，从而为其中的边赋予有意义的索引。这也是为什么必须首先在 "mesh" 类的代码块中声明此函数：

```cpp
int edgeIndexing(int);
```

以下是该函数的实际定义。首先，它接受一个存储网格中节点总数的整数参数 "nodes"：

```cpp
template<class T>
int mesh<T>::edgeIndexing(int nodes) {
    int edges = 0;
```

局部整型变量 "edges" 统计网格中的边。现在，网格中的四面体在外层循环中被扫描：

```cpp
for(mesh<T>* runner = this; runner;
    runner=(mesh<T>*)runner->next) {
```

首先，在此循环中遇到的每个四面体中的每个顶点必须在数组 "index" 中分配 10 个条目，以存储与其相关的 10 个自由度的索引。幸运的是，这些顶点已经在全局节点列表中被索引。实际上，每个顶点在整个网格节点列表中的索引可以通过 "node" 类的公共 "getIndex" 函数读取：

此外，在上面的外层循环中遇到的每个四面体中，六条边在嵌套的内层循环中如下扫描。设四面体的四个顶点由数字 0, 1, 2 和 3 表示。然后，四面体的边按以下顺序扫描：

(0,1), (0,2), (0,3), (1,2), (1,3) 和 (2,3)。

换句话说，四面体中从顶点 $i$ 到顶点 $j$ 的边表示为 $(i,j)$，其中 $0 \le i < j \le 3$：

```cpp
int I = -1;
for(int i=0; i<3; i++)
    for(int j=i+1; j<=3; j++) {
        I++;
    }
```

在此嵌套循环中，整型变量 $I=0,1,2,3,4,5$ 统计当前四面体中的边。此外，现在使用一个更深层的内层循环来扫描网格中所有之前的四面体，以检查当前边 $(i,j)$ 是否已经在其中任何一个中被索引：

```cpp
for(mesh<T>* previous = this;
    previous&& (previous != runner)
    && (runner->item.readMeshIndex(40+2*I) < 0);
    previous=(mesh<T>*)previous->next) {
```

为了检查这一点，我们使用 "finiteElement" 类的 "operator<"，该运算符检查给定的节点是否确实作为给定有限元的顶点：

```cpp
int ni = runner->item[i] < previous->item;
int nj = runner->item[j] < previous->item;
if(ni&&nj) {
    ni--;
    nj--;
}
```

如果节点 $i$ 和 $j$ 确实被网格中的一个先前四面体共享，那么当前边 $(i,j)$ 也可以表示为 $(ni,nj)$，其中 "ni" 和 "nj" 是这些节点在此先前四面体四个顶点列表中的索引。此外，我们可以找到 $(ni,nj)$ 在此先前四面体六条边列表中的索引 $0 \le J < 6$：

