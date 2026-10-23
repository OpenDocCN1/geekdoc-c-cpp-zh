

if(((*vertex[i])()[0]>0.)||((*vertex[i])()[1]>0.))
    return 1.;
return 1000.;
} // y-导数的系数

这些函数应根据第12章第5节中的指南用于刚度矩阵的计算。实际上，唯一的变化是第16章第5节中组装刚度矩阵的构造函数中的2 × 2矩阵“weight”，其中间也应包含因子 diag(P, Q)：

```
point diffX((*runner()).p(),0.);
point diffY(0.,(*runner()).q());
matrix2 diffCoef(diffX,diffY);
matrix2 S((*runner())[1]() - (*runner())[0](),
    (*runner())[2]() - (*runner())[0]());
matrix2 Sinverse = inverse(S);
matrix2 weight = abs(det(S)/2) *
    Sinverse * diffCoef * transpose(Sinverse);
```

我们将混合边界条件的纳入细节以及消除狄利克雷边界 Γ_D 上节点对应的方程留给读者（参见第 A.23 节和第 A.33 节）。至此刚度矩阵的定义完成。

为了不仅在区域内部而且在边界的圆形部分进行细化，我们还使用自动边界细化（第14章第7节）。为此，我们在第14章第8节的代码中引入一个额外的“if”问题，以确保自动边界细化仅在紧邻圆形边界段的边界边上使用。

自适应细化循环与上文第 A.21 节中的相同。至此扩散求解器的定义完成。

## A.23 线性弹性求解器

这里，我们展示如何实现第20章第8节中的自适应细化算法来求解线性弹性方程。首先，我们给出第20章第7节中描述的组装刚度矩阵的构造函数。代码与第16章第5节中的代码相似，只是第20章第7节中的三个块 A^(0,0)、A^(1,1) 和 A^(0,1) 需要构造。因此，第16章第5节代码中内层循环的主体在这里实际上重复了三次，使用三个不同的2 × 2矩阵：“diffCoef”构造 A^(0,0)，“diffCoef2”构造 A^(1,1)，以及“mixed”构造 A^(0,1)。

为了在 Γ_D 中的点处施加狄利克雷边界条件，我们定义一个名为“DirichletBoundary”的整数向量。对于 Γ_D 中的每个节点 i，“DirichletBoundary”中的第 i 个分量为零。“DirichletBoundary”中其余分量的值为1。现在，矩阵 A 由“DirichletBoundary”向量“掩蔽”，其含义是对于每个 i ∈ Γ_D，第 i 行和第 i 列被丢弃并替换为标准单位向量 e^(i)，其第 i 个分量值为1，其余分量为0。这导致对于每个 i ∈ Γ_D，刚度系统中的未知数 x_i 的方程是平凡的。

因此，用于弹性方程的刚度矩阵的组装构造函数如下：

```
template<class T>
sparseMatrix<T>::sparseMatrix(mesh<triangle>&m) {
item = new row<T>*[number = 2 * m.indexing()];
for(int i=0; i<number; i++)
item[i] = 0;
point gradient[3];
gradient[0] = point(-1,-1);
gradient[1] = point(1,0);
gradient[2] = point(0,1);
dynamicVector<int> DirichletBoundary(number,1);
for(const mesh<triangle>* runner = &m; runner; runner = (const mesh<triangle>*)runner->readNext()){
point diffX(1.,0.);
point diffY(0.,(1.-NU)/2.);
point diffX2((1.-NU)/2.,0.);
point diffY2(0.,1.);
matrix2 diffCoef(diffX,diffY);
matrix2 diffCoef2(diffX2,diffY2);
point mixedX(0.,NU);
point mixedY((1.-NU)/2.,0.);
matrix2 mixed(mixedX,mixedY);
matrix2 S((*runner())[1]() - (*runner())[0](),
    (*runner())[2]() - (*runner())[0]());
matrix2 Sinverse = inverse(S);
matrix2 weight = abs(det(S)/2) * Sinverse * diffCoef * transpose(Sinverse);
matrix2 weight2 = abs(det(S)/2) * Sinverse * diffCoef2 * transpose(Sinverse);
matrix2 weightMixed = abs(det(S)/2) * Sinverse * mixed * transpose(Sinverse);
for(int i=0; i<3; i++) {
int I = (*runner())[i].getIndex();
if((abs(squaredNorm((*runner())[i]()))-1.)<1.e-7 &&
((*runner())[i][0] <= -0.5)){
DirichletBoundary[I] = 0;
DirichletBoundary[I+number/2] = 0;
}
for(int j=0; j<3; j++) {
int J = (*runner())[j].getIndex();
if(j>=i){
if(item[I]){
row<T> r(gradient[j]*weight*gradient[i],J);
*item[I] += r;
}
else
item[I] = new row<T>(gradient[j]*weight*gradient[i],J);
}
}
}
}
}
```

```
if(item[I+number/2]){
    row<T> r(gradient[j]*weight2*gradient[i],
        J+number/2);
    *item[I+number/2] += r;
}
else
    item[I+number/2] =
        new row<T>(gradient[j]*weight2*gradient[i],
            J+number/2);
}
if(item[I]){
    row<T> r(gradient[j]*weightMixed*gradient[i],
        J+number/2);
    *item[I] += r;
}
else
    item[I] = new
        row<T>(gradient[j]*weightMixed*gradient[i],
            J+number/2);
}
}
for(int i=0; i<number; i++){
    if(DirichletBoundary[i])
        item[i]->maskItems(DirichletBoundary, (double)0.);
    else
        *item[i] = row<T>(1.,i);
}
// assemble stiffness matrix for linear elasticity
```

如第20章第7节所述，在使用上述构造函数构造矩阵 A 之后，应进一步通过以下方式修改它：

```
A += transpose(A) - diagonal(A);
```

至此刚度矩阵的定义完成。

接下来，我们实现第20章第8节中的自适应细化算法。为此，第14章第6节中“refine”函数中的“if”问题应修改为

```
if((item[i].getIndex() >= 0)&&
    (item[j].getIndex() >= 0)&&
    ((abs(v[item[i].getIndex()]) -
    v[item[j].getIndex()])>threshold)||
    (abs(v[item[i].getIndex()+v.dim()/2] -
    v[item[j].getIndex()+v.dim()/2])>threshold))){
    ...
```

这样就实现了第20章第8节中的准则。

接下来，我们实现第20章第9节中修改的多重网格算法。该算法原则上与第17章第8节中的相同，只是 A 的块对角部分

blockdiag(A^(0,0),A^(1,1))

用于构造粗网格以及 prolongation 矩阵 P 和 restriction 矩阵 R。为了得到这个块对角矩阵，我们在第 A.18 节的“createTransfer”函数开头插入几行代码。这些代码行从刚度矩阵 A 的当前副本中删除 A^(0,1) 和 A^(1,0) 块。 （当然，假设原始矩阵 A 也在其他地方保存，因此这些更改不会影响它。）结果是 A 所需的块对角部分，然后在“createTransfer”函数的其余部分中使用它来创建粗网格以及 prolongation 和 restriction 矩阵。

应插入到“createTransfer”函数开头的代码行如下：

```
dynamicVector<int> one(rowNumber(),1);
dynamicVector<int> two(rowNumber(),1);
for(int i=0; i<rowNumber()/2; i++)
    two(i) = 0;
for(int i=rowNumber()/2; i<rowNumber(); i++)
    one(i) = 0;
for(int i=0; i<rowNumber()/2; i++)
    item[i]->maskItems(one, (double)0.);
for(int i=rowNumber()/2; i<rowNumber(); i++)
    item[i]->maskItems(two, (double)0.);
```

至此线性弹性求解器所需的更改完成。实现自适应细化算法的循环基本上与第 A.21 节相同。

## A.24 与替代右端项的融合

这里我们修改原始的多重网格融合算法，使其使用第23章第23.10节中引入的替代右端项。为此，我们必须首先定义一个新的二进制算术运算符，该运算符将稀疏行加到动态向量上：

```
template<class T>&
const dynamicVector<T>&
operator+=(dynamicVector<T>&v, const row<T>&r){
    for(const row<T>* runner = &r; runner;
        runner = (const row<T>*)runner->readNext())
        v(runner->getColumn()) += runner->getValue();
    return v;
} // adding a row to a dynamic vector
```

有了这个运算符，用户可以写“v += r”来将 well-defined 的行 'r' 加到 well-defined 的动态向量 'v' 上。这样的命令在下面确实被使用。

