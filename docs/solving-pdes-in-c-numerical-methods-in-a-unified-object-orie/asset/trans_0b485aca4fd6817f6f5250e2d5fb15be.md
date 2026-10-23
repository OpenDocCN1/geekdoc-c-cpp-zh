

```cpp
template<class T>
const polynomial<T>
operator+(const polynomial<T>& p,
    const polynomial<T>&q) {
    polynomial<T> keep = p;
    return keep += q;
} // 两个多项式相加
```

## 24.3 标量乘法

下一个运算符将多项式与类型 ‘S’ 的对象相乘，该类型稍后由用户指定。（通常，‘S’ 只是一个普通的标量，不过，下面我们还会看到它也可以是一个更复杂的对象。）更准确地说，第一个参数（非常数多项式 ‘p’）与第二个参数（‘a’，它是类型 ‘S’ 的对象）相乘：

```cpp
template<class T, class S>
const polynomial<T>&
operator*=(polynomial<T>& p, const S&a){
    for(int i=0; i<=p.degree(); i++)
        p(i) *= a;
    return p;
} // 标量乘法
```

在上述循环中，使用 “operator()” 访问 ‘p’ 的系数，并利用与 ‘T’ 类相关的 "*=" 运算符将它们与 ‘a’ 相乘。借助上述函数，用户可以编写 "p *= d" 来将定义明确的多项式 ‘p’ 与任意类型的标量 ‘d’ 相乘。

现在使用上述函数来定义“标量乘多项式”和“多项式乘标量”乘法：

```cpp
template<class T, class S>
const polynomial<T>
operator*(const S&a, const polynomial<T>&p){
    polynomial<T> keep = p;
    return keep *= a;
} // 标量乘多项式
```

```cpp
template<class T, class S>
const polynomial<T>
operator*(const polynomial<T>&p, const S&a){
    polynomial<T> keep = p;
    return keep *= a;
} // 多项式乘标量
```

借助这些函数，用户可以编写 "p * d" 或 "d * p" 来获得定义明确的多项式 ‘p’ 与任意类型的标量 ‘d’ 的乘积。

## 24.5 多项式复合

在这里，我们计算给定多项式 p 和 q 的复合 p ∘ q，其定义为：

(p ∘ q)(x) ≡ p(q(x)).

为此，我们使用一种类霍纳（Horner）算法，其中 p 作用于多项式，而不仅仅是一个普通的标量：

```cpp
template<class T>
const polynomial<T>
operator&(const polynomial<T>&p,
    const polynomial<T>&q) {
```

局部多项式 "result" 初始化为一个常数多项式，其常数值与 'p' 中最高次 x 项的系数相同：

```cpp
polynomial<T> result(1,p[p.degree()]);
```

然后，在循环中反复更新 "result"，正如霍纳算法（第 5.8 节）那样：

```cpp
for(int i=p.degree(); i>0; i--){ 
    result *= q; 
    result += polynomial<T>(1,p[i-1]); 
} 
return result; 
} // 复合 p 和 q 的霍纳算法
```

## 24.6 递归霍纳代码

接下来，我们计算给定多项式 p（度数为 n）在给定自变量 x 处的值 p(x)。为此，我们使用递归公式：

p(x) = a₀ + x p₁(x),

其中 p₁ 是度数为 n − 1 的多项式。实际上，这个公式无非是递归情形下的霍纳算法。为了高效地实现它，诀窍在于避免显式地构造或存储 p₁。

实现上述想法的函数 "HornerArray" 已经被声明为 "polynomial" 类的成员函数，以允许其他成员函数调用它，这将在下面证明是有用的。此外，第三个参数 'x' 的类型已声明为模板类 'S'，由用户稍后指定。这提供了额外的灵活性，因为 'S' 可能与 'T' 不同：

```cpp
template<class T>
template<class S>
const T
polynomial<T>::HornerArray(T** const&p,
    int n, const S&x) const{
```

函数中的第一个参数 ‘p’ 代表度数为 ‘n’ 的多项式 p 中系数指针的数组。因此，"p+1" 只是度数为 "n−1" 的多项式 p₁ 中系数指针的数组，用于递归：

```cpp
return n ==0 ?
    *p[0]
    :
    *p[0] + x * HornerArray(p+1,n-1,x);
} // 递归霍纳代码
```

由于 "item" 字段在基类 "list" 中被声明为受保护的（而不是私有的），因此也可以从派生类 "polynomial" 访问它。下面定义的 "operator()" 函数利用此特性，将上述 "HornerArray" 函数应用于数组 "item"，以生成当前多项式在自变量 ‘x’ 处所需的值：

```cpp
template<class T>
template<class S>
const T
polynomial<T>::operator()(const S&x) const{
    return HornerArray(item,degree(),x);
} // 计算多项式的霍纳算法
```

使用此运算符，用户可以编写 "p(x)" 来获得定义明确的多项式 ‘p’ 在给定自变量 ‘x’ 处的值。

## 24.7 双变量多项式

要实现双变量多项式，只需指定 ‘T’ 本身为一个多项式即可。这里我们使用此实现来计算双变量多项式在给定自变量 x 和 y 处的值：

p(x,y) ≡ Σᵢ aᵢ(x) yⁱ

```cpp
template<class T>
template<class S>
const S
polynomial<T>::operator()(const S&x,
    const S&y) const{
    return (*this)(y)(x);
} // 计算 p(x,y)
```

此函数调用了第 24.6 节中原始的 "operator()" 两次。在第一次调用中，自变量 y 被用来获得单变量多项式 p(·,y)，其中 y 是一个固定数值。在第二次调用中，自变量 x 被用来计算所需的数值 p(x,y)。

## 24.10 单位区间上的积分

现在使用上述函数对单变量多项式在单位区间 [0,1] 上进行积分，使用公式：

$$\int_{0}^{1} p(x)dx = P(1) - P(0) = P(1),$$

其中 P 是在前一节中定义的定积分：

```cpp
template<class T>
const T
integral(const polynomial<T>&p) {
  return indefiniteIntegral(p)(1.);
} // 单位区间上的积分
```

实际上，在调用 "indefiniteIntegral" 计算 P 之后，调用 "operator()" 来计算所需的数值 P(1)。

## 24.11 单位三角形上的积分

现在考虑双变量多项式 p(x,y)。假设 x 是一个固定数值，因此 p(x,·) 实际上只是一个单变量多项式。设 P 为这个多项式的定积分（第 24.9 节）。因此，P ≡ P(x,y)，其中 x 是固定参数，y 是唯一变量。

现在我们使用 P 来计算 p 在图 5.5 中的单位三角形上的积分：

$$\int_{0}^{1}\int_{0}^{1-x} p(x,y)dy dx = \int_{0}^{1} P(x,1-x)dx.$$

下面的代码确实实现了该公式：

```cpp
template<class T>
const T
integral(const polynomial<polynomial<T> >&p) {
```

首先，我们使用接受两个 "double" 参数的构造函数来形成多项式 1−x：该多项式随后存储在一个名为 "oneMinusx" 的局部多项式对象中：

```cpp
polynomial<T> oneMinusx(1., -1.);
```

接下来，"indefiniteIntegral" 函数应用于原始多项式 `p` 以形成关于 y 的定积分（在上式中记为 P）。然后，第 24.6 节中的 "operator()" 应用于 P(x,y)（带有多项式参数 1−x），以用 1−x 替换 y 并生成 P(x,1−x)。实际上，"operator()" 的参数不仅可以是一个普通的标量，还可以是一个单变量多项式，因此第 24.6 节中的模板类 `S` 也被解释为一个单变量多项式。最后，原始的 "integral()" 版本应用于 P(x,1−x) 以在单位区间上进行积分：

```cpp
return
  integral(indefiniteIntegral(p)(oneMinusx));
} // 单位三角形上的积分
```

## 24.12 单位四面体上的积分

现在考虑三变量多项式 $p(x,y,z)$。假设 $x$ 和 $y$ 都是固定数值，因此 $p(x,y,z)$ 实际上只是一个单变量多项式。设 $P$ 为这个多项式的定积分（第 24.9 节）。因此，$P \equiv P(x,y,z)$，其中 $x$ 和 $y$ 是固定参数，$z$ 是唯一变量。

现在我们使用 $P$ 来计算 $p$ 在图 27.1 中的单位四面体上的积分：

$$\int_0^1\int_0^{1-x}\int_0^{1-x-y} p(x,y,z)\,dz\,dy\,dx = \int_0^1\int_0^{1-x} P(x,y,1-x-y)\,dy\,dx.$$

下面的代码确实实现了该公式：

```cpp
template<class T>
const T
integral(const
    polynomial<polynomial<polynomial<T> > >&p){
```

为了形成双变量多项式 $1-x-y$，我们将其写为：

$$1-x-y=(1-x)y^0+(-1)y^1.$$

因此，为了形成 $1-x-y$，我们必须使用接受两个多项式参数的构造函数：单变量多项式 $1-x$ 和常数多项式 $-1$。为了形成常数多项式 $-1$，我们调用接受整数参数 $1$（表示这是一个 0 次多项式）和“double”参数 $-1$（指定系数）的构造函数：

```cpp
polynomial<T> minus1(1,-1.);
```

另一方面，为了形成多项式 $1-x$，我们调用接受两个“double”参数的构造函数以指定两个系数：

```cpp
polynomial<T> oneMinusx(1.,-1.);
```

最后，为了形成所需的双变量多项式 $1-x-y$，我们调用接受两个单变量多项式 $1-x$ 和 $-1$ 的构造函数：

```cpp
polynomial<polynomial<T> >
oneMinusxMinusy(oneMinusx,minus1);
```

现在，将“indefiniteIntegral”函数应用于原始多项式 $p(x,y,z)$，以生成其关于 $z$ 的定积分（在上式中记为 $P(x,y,z)$）。然后，应用第 24.6 节中原始的“operator()”（其中 ‘S’ 和 ‘T’ 均为双变量多项式），在固定自变量 $z=1-x-y$ 处计算它，并生成双变量多项式 $P(x,y,1-x-y)$。最后，使用前一节的“integral()”版本，将此多项式在单位三角形上进行积分：

```cpp
return
    integral(indefiniteIntegral(p)(oneMinusxMinusy));
}   // 单位四面体上的积分
```

