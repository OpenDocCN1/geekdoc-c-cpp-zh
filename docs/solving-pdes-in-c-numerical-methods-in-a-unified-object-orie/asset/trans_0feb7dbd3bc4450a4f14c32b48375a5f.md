

```
if(fabs(u[i]) < fabs(v[i]))
    maxuv(i) = v[i];
return maxuv;
} // maximum absolute value
```

现在，这个函数还用于实现包含 m 个向量的列表的 max() 函数，如上文第 23.9 节所示：

```
template<class T>
const T
max(const list<T>&l){
    T maxl = l[0];
    for(int i=1; i<l.size(); i++)
        maxl = max(maxl,l[i]);
    return maxl;
} // maximum modulus of list of vectors
```

现在，我们准备实现多重网格融合算法。这实际上是在下面的“fuse()”函数中完成的。该函数接受两个参数：向量列表“f1m”，它包含多个右端项向量 f^(1), f^(2), ..., f^(m)；以及多重网格对象“mg”，它包含对具有 Neumann 边界条件的拉普拉斯算子进行离散化的稀疏系数矩阵。

```
template<class T>
const dynamicVector<T>
fuse(const list<dynamicVector<T> >&f1m,
    const multigrid<T>&mg){
    dynamicVector<T> f = max(f1m);
    return mg.getNext() ?
        mg.getP() * (fuse(mg.getR() * f1m,
            *mg.getNext()))
        - mg.getR() * f / *mg.getNext()
    + f / mg
    :
    f / mg;
} // multigrid fusion algorithm
```

## 23.14 示例

在本示例中，使用了两幅 Lena 的模糊图像。每幅图像被划分为四个子方块。一幅图像在右上和左下子方块中存在模糊，包括 Lena 的眼睛和鼻子（图 23.1）。另一幅图像在左上和右下子方块中存在模糊，包括 Lena 的眉毛（图 23.2）。上文第 23.13 节实现的多重网格融合算法将这两幅图像融合成一幅没有任何模糊的清晰图像（图 23.3）。

![](img/1f293b0ceb2de964310ea7f941a1b580_576_0.png)

图 23.1：第一幅模糊图像，其中右上和左下子方块（包括 Lena 的眼睛和鼻子）是模糊的。

![](img/1f293b0ceb2de964310ea7f941a1b580_577_0.png)

图 23.2：第二幅模糊图像，其中右下和左上子方块（包括 Lena 的眉毛）是模糊的。

![](img/1f293b0ceb2de964310ea7f941a1b580_578_0.png)

图 23.3：多重网格融合算法将上述 Lena 的模糊图像融合成一幅清晰图像的结果。

# 第七部分

三维空间中的应用

# 第七部分：三维空间中的应用

在本部分中，我们同样使用当前的面向对象框架来实现三维有限元。所得到的四面体网格特别适合自适应细化。我们还实现了在网格边处具有连续梯度的高阶有限元。

然后，这些高级对象被用于求解复杂的非线性偏微分方程系统，包括三维空间中的 Navier–Stokes 方程、Maxwell 方程和 Helmholtz 方程。

当前的面向对象框架对于 Newton 迭代所需的线性化特别有用。实际上，在每次 Newton 迭代中组装并（隐式）求逆的刚度矩阵，其元素本身就是复杂的对象，而不是简单的标量。

当前的 Maxwell 求解器是当前 Stokes 求解器和 Helmholtz 求解器的组合。与这些问题相关的反问题也进行了讨论。最后，Maxwell 求解器还被修改为用作 Navier–Stokes 求解器。

# 第24章

# 三个独立变量中的
# 多项式

在本章中，我们以比第 5 章略为直接的方式重新实现一元和二元多项式。此外，我们还利用这一实现来实现三元多项式。而且，我们还实现了一些有用的运算符和函数，包括在图 27.1 中的单位四面体上的积分。这些函数对于本书后续线性和非线性偏微分方程的有限元离散化特别有用。

## 24.1 多项式对象

模板类“polynomial”派生自上文第 3.4 节中的“list”类：

```
template<class T> class polynomial:public list<T>{
```

由于基类“list”中的字段“number”和“item”仅被声明为 protected（而非 private），因此可以在下面的构造函数中访问和设置它们：

```
public:
    polynomial(int n=0){
        number = n;
        item = n ? new T*[n] : 0;
        for(int i=0; i<n; i++)
            item[i] = new T(0);
    }  // constructor
```

事实上，该构造函数首先隐式调用基类“list”的默认构造函数，将“number”和“item”字段初始化为零，然后修改这些字段，构造一个具有 n 个零系数的平凡多项式。

类似地，下面的构造函数构造一个具有 n 个系数且所有系数都等于 a 的多项式。

```
polynomial(int n, const T&a){
    number = n;
    item = n ? new T*[n] : 0;
    for(int i=0; i<n; i++)
        item[i] = new T(a);
}   // constructor with 'T' argument
```

如前所述，某些编译器（如 GNU 3.2 及更高版本）可能需要使用前缀 'this->' 来访问从基类“list”继承的字段 'number' 和 'item'：

```
this->number = n;
```

（另请参阅附录中 A.34 节的代码，以及本书网页 http://www.siam.org/books/cs09 上的代码，这些代码同样可以用新的 GNU 版本编译。）不过在后续内容中，我们不再费心添加这一前缀。

下一个构造函数构造一个具有两个系数 'a' 和 'b' 的多项式：

```
polynomial(const T&a, const T&b){
    number = 2;
    item = new T*[2];
    item[0] = new T(a);
    item[1] = new T(b);
}   // constructor with 2 'T' arguments
```

下面的析构函数仅隐式调用基类“list”的默认析构函数：

```
~polynomial(){
}   // destructor
```

下一个函数返回多项式的次数：

```
int degree() const{
    return number-1;
}   // degree of polynomial
```

下一个函数允许用户访问多项式中的第 i 个系数：

```
T& operator()(int i){
    return list<T>::operator()(i);
}   // read/write ith coefficient
```

实际上，利用这个函数，用户只需写 'p(i)' 即可访问已定义好的多项式 'p' 中的第 i 个系数。

以下成员函数在此仅作声明；其详细定义将在后面给出。请注意，传递给这些函数的参数类型为 'S'，它可能与 'T' 不同：

```
template<class S>
    const T
    HornerArray(T* const&, int, const S&) const;
template<class S>
    const T operator()(const S&) const;
template<class S>
    const S operator()(const S&, const S&) const;
template<class S>
    const S operator()(const S&,
        const S&, const S&) const;
};
```

至此，“polynomial”类的代码块就完成了。接下来，我们定义一些有用的多项式算术运算符。

## 24.2 多项式的加法

下面定义的“+=”运算符是一个普通的（非成员）函数，它接受两个多项式参数，并将第二个多项式加到第一个多项式上。这就是为什么只有第二个参数被声明为常量，而第一个参数不是常量。

```
template<class T>
const polynomial<T>&
operator+=(polynomial<T>& p, const polynomial<T>& q){
```

如果 'p' 的次数大于 'q' 的次数，则将 'q' 中的系数逐一加到 'p' 中相应的系数上：

```
if(p.degree() >= q.degree())
    for(int i=0; i<=q.degree(); i++)
        p(i) += q[i];
```

另一方面，如果 'q' 的次数大于 'p' 的次数，则不能像上面那样直接地将 'q' 加到 'p' 上。此时，必须递归调用“+=”运算符，并交换 'p' 和 'q' 的角色。然而，由于 'q' 是常量，必须先将其赋值给局部的非常量多项式“keepQ”，然后才能把 'p' 加进去：

```
else{
    polynomial<T> keepQ = q;
    p = keepQ += p;
}
return p;
}   // add a polynomial
```

利用这个运算符，用户可以写出类似“p += q”的命令，将已定义好的多项式‘q’加到已定义好的多项式‘p’上。此外，这个运算符还被用来定义‘+’运算符：

