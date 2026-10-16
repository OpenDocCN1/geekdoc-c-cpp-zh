
+   **sqrt(x)** 平方根；**x** 必须是非负的
+   **cos(x)** 余弦
+   **sin(x)** 正弦
+   **tan(x)** 正切
+   **acos(x)** 反余弦；结果是非负的
+   **asin(x)** 反正弦；返回最接近 0 的结果
+   **atan(x)** 反正切
+   **sinh(x)** 双曲正弦
+   **cosh(x)** 双曲余弦
+   **tanh(x)** 双曲正切
+   **exp(x)** 以 e 为底的指数
+   **log(x)** 自然对数，以 e 为底；**x** 必须是正数
+   **log10(x)** 以 10 为底的对数

存在接受 **float**、**double**、**long double** 和 **complex**（§40.4）参数的版本。
对于每个函数，返回类型与参数类型相同。
错误通过将 <cerrno> 中的 **errno** 设为 **EDOM**（表示定义域错误）或 **ERANGE**（表示值域错误）来报告。例如：

```
void f()
{
errno = 0; // clear old error state
sqrt(-1);
if (errno==EDOM) cerr << "sqrt() not defined for negative argument";
pow(numeric_limits<double>::max(),2);
if (errno == ERANGE) cerr << "result of pow() too large to represent as a double";
}
```

由于历史原因，少数数学函数位于 <cstdlib> 而非 <cmath> 中：**更多数学函数（§iso.26.8）**

+   **n2=abs(n)** 绝对值；**n** 是 **int**、**long** 或 **long long**；**n2** 与 **n** 类型相同
+   **n2=labs(n)** “长绝对值”；**n** 和 **n2** 是 **long**
+   **n2=llabs(n)** “长长绝对值”；**n** 和 **n2** 是 **long long**
+   **p=div(n,d)**
+   **p=ldiv(n,d)** 用 **d** 除 **n**；**p** 是 {商，余数}；**n** 和 **d** 是 **long**
+   **p=lldiv(n,d)** 用 **d** 除 **n**；**p** 是 {商，余数}；**n** 和 **d** 是 **long long**

**l*()** 版本的存在是因为 C 不支持重载。**ldiv()** 函数的结果分别是 **struct** **div_t**、**ldiv_t** 和 **lldiv_t**。这些 **struct** 具有实现定义类型的成员 **quot**（商）和 **rem**（余数）。

针对*特殊数学函数*[C++Math,2010]，有一个单独的 ISO 标准。实现可以将这些函数添加到 <cmath> 中：

## 数学特殊函数（可选）

+   **assoc_laguerre() assoc_legendre() beta() comp_ellint_1() comp_ellint_2()**
+   **comp_ellint_3() cyl_bessel_i() cyl_bessel_j() cyl_bessel_k() cyl_neumann() ellint_1()**
+   **ellint_2()**
+   **ellint_3() expint() hermite() laguerre() legendre() riemann_z eta() sph_bessel()**

+   z1/z2 除法
+   z1==z2 相等
+   z1!=z2 不等
+   norm(z) abs(z) 的平方
+   conj(z) 共轭：{z.re, −z.im}
+   polar(x,y) 根据极坐标 (rho,theta) 构造复数
+   real(z) 实部
+   imag(z) 虚部
+   abs(z) 到 (0,0) 的距离：sqrt(z.re*z.re+z.im*z.im)；也称为 rho
+   arg(z) 与正实轴的夹角：atan2(z.im/z.re)；也称为 theta
+   out<<z 复数输出
+   in>>z 复数输入

标准数学函数（§40.3）也可用于复数。注意，complex 不提供 < 或 %。更多细节参见 §18.3。

## 40.5 数值数组：valarray

许多数值计算工作依赖于相对简单的一维浮点值向量。特别是，这类向量受到高性能机器架构的良好支持，依赖这类向量的库被广泛使用，而且对使用这类向量的代码进行非常激进的优化在许多领域被认为是必不可少的。来自 <valarray> 的 valarray 是一个一维数值数组。它为数组类型提供了通常的数值向量算术运算，并支持切片（slice）和步长（stride）：

+   valarray<T>
+   slice
+   slice_array<T> gslice
+   gslice_array<T> mask_array<T> indirect_array<T>

### 数值数组类（§iso.26.6.1）

+   类型为 T 的数值数组
+   类似 BLAS 的切片（起点、长度和步长）；§40.5.4
+   由切片标识的子数组；§40.5.5
+   广义化为描述矩阵的切片
+   由广义切片标识的子矩阵；§40.5.6
+   由掩码标识的数组子集；§40.5.2
+   由索引列表标识的数组子集；§40.5.2

valarray 的基本思想是为密集多维数组提供类似 Fortran 的功能，并带来类似 Fortran 的优化机会。这只有通过编译器和优化供应商的积极支持，以及在 valarray 提供的非常基础的功能之上增加更多库支持才能实现。到目前为止，并不是所有实现都做到了这一点。

## 40.5.1 构造函数与赋值

通过 valarray 构造函数，我们可以从辅助数值数组类型和单个值初始化 valarray：

### valarray<T> 构造函数（§iso.26.6.2.2）

```
valarray va {}; valarray with no elements
valarray va {n}; valarray of n elements with value T{}; explicit
valarray va {t,n}; valarray of n elements with value t
valarray va {p,n}; valarray of n elements with values copied from [p:p+n) valarray va {v2};
valarray va {a};
```

移动和拷贝构造函数
用 a 中的元素构造 va；
a 可以是 slice_array、gslice_array、mask_array 或 indirect_array；元素个数与 a 中的元素个数相同。

```
valarray va {args}; Construct from the initializer_list {args};
the number of elements is the number of elements in {args} va.~valarray() Destructor
```

例如：

```
valarray<double> v0; valarray<float> v1(1000);
// placeholder,we can assign to v0 later // 1000 elements with value float()= =0.0F
```

```
valarray<int> v2(-1,2000);
valarray<double> v3(100,9.8064);
// 2000 elements with value -1
// bad mistake: floating-point valarraysize
valarray<double> v4 = v3; // v4 has v3.size() elements
valarray<int> v5 {-1,2000}; // twoelements
```

在两个参数的构造函数中，值位于元素个数之前。这与标准容器（§31.3.2）的约定不同。

拷贝构造函数中参数 valarray 的元素个数决定了结果 valarray 的大小。

大多数程序需要来自表或输入的数据。除了初始化列表之外，还有一个构造函数可以从内置数组复制元素来支持这一点。例如：

```
void f(const int * p, int n) {
const double vd[] = {0,1,2,3,4}; const int vi[] = {0,1,2,3,4};
valarray<double> v1{vd,4}; valarray<double> v2{vi,4}; valarray<double> v3{vd,8};
valarray<int> v4{p,n};
}
// 4elements: 0,1,2,3
// type error:vi is not pointer to double // undefined: too few elements in initializer // p had better point to at least n ints
```

valarray 及其辅助设施是为高速计算而设计的。这体现在对用户的一些限制以及赋予实现者的一些自由上。基本上，valarray 的实现者可以使用你能想到的几乎所有优化技术。valarray 操作被假定为没有副作用（当然，除了对它们显式参数的影响），valarray 被假定为无别名（alias-free），并且只要保持基本语义，就允许引入辅助类型和消除临时对象。没有范围检查。valarray 的元素必须具有默认的拷贝语义（§8.2.6）。

赋值可以是另一个 valarray、一个标量或 valarray 的一个子集：

### valarray<T> 赋值（§iso.26.6.2.3）

va2=va 拷贝赋值：va2.size() 变为 va.size()
va2=move(va) 移动赋值：va 变为空
va=t 标量赋值：va 的每个元素都是 t 的副本
va={args} 从初始化列表 {args} 赋值；va 的元素个数变为 {args}.size()
va=a 从 a 赋值；a.size() 必须等于 va.size()；a 可以是 slice_array、gslice_array、mask_array 或 indirect_array
va@=va2 对 va 的每个元素执行 v[i]@=va2[i]；@ 可以是 /、%、+、-、^、&、|、<< 或 >>
va@=t 对 va 的每个元素执行 v[i]@=t；@ 可以是 /、%、+、-、^、&、|、<< 或 >>

valarray 可以被赋给另一个相同大小的 valarray。正如所料，v1=v2 会将 v2 的每个元素复制到 v1 中对应的位置。如果 valarray 大小不同，则赋值的结果未定义。

除了这种常规赋值之外，还可以将标量赋给 valarray。例如，v=7 将 7 赋给 valarray v 的每个元素。这可能会让一些程序员感到惊讶，最好将其理解为运算符赋值操作的一种偶尔有用的退化情况。例如：

```
valarray<int> v {1,2,3,4,5,6,7,8};
v *=2; // v={2,4,6,10,12,14,16}
v=7; // v={7,7,7,7,7,7,7,7}
```

## 40.5.2 下标操作

下标操作可用于选择 valarray 的一个元素或其中的一个子集：

valarray<T> 下标操作（§iso.26.6.2.4、§iso.26.6.2.5）
t=va[i] 下标：t 是 va 第 i 个元素的引用；无范围检查
a2=va[x] 子集：x 是 slice、gslice、valarray<bool> 或 valarray<size_t>

每个 operator[] 都返回来自 valarray 的一个元素子集。返回类型（表示子集的对象类型）取决于参数类型。

对于 const 参数，结果包含元素的副本。对于非 const 参数，结果持有元素的引用。由于 C++ 不直接支持引用数组（例如，我们不能说 valarray<int&>），实现将以某种方式模拟这一点。这可以高效地完成。下面按顺序给出一个包含示例的详尽列表（基于 §iso.26.6.2.5）。在每种情况下，下标描述了要返回的元素，且 v1 必须是具有适当长度和元素类型的 valarray：

+   - 一个 const valarray 的切片：

```
valarray<T> operator[](slice) const;// copyofelements
// ...
const valarray<char> v0 {"abcdefghijklmnop",16};
```
