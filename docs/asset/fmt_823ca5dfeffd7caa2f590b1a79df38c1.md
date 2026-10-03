
最后，我们定义一元运算符`+`来返回复数的共轭数。这样，用户可以对任何数值类型的变量`t`编写`+t`，该类型可以是实数也可以是复数。事实上，如果`t`是实数，那么`+t`与`t`相同；另一方面，如果`t`是复数，那么`+t`就是`t`的共轭数。

```
complex operator+(const complex&c){
    return complex(c.re(),-c.im());
} // 复数的共轭
```

## 第 15 章 对象

到此为止，复数的算术运算结束。最后，我们定义一个将复数打印到屏幕上的函数：

```cpp
void print(const complex&c) {
    printf("%f, %f\n",c.re(),c.im());
} // 打印复数
```

## 15.34 练习题

1. 编写类`point3`，用于实现三维笛卡尔空间中的一个点。为该类编写构造函数、析构函数、赋值运算符和算术运算符。
2. 编写一个使用复数极坐标表示法的函数：

`c = r(\cos(\theta) + i \cdot \sin(\theta))`

计算它的平方根`\sqrt{c}`。（在这里`0 \le \theta < 2\pi`是与正 x 轴的夹角，参见第 5 章。）解可以在附录的第 28.5 节找到。
3. 在上一个练习中，`c`的极坐标表示中的角度`\theta`处于`0`到`2\pi`之间，因此`\sqrt{c}`在实轴正部分的角度`\theta/2`处于`0`到`\pi`之间。不幸的是，平方根函数在实轴正部分是不连续的。事实上，当`\theta`趋于`0^+`（`\theta > 0`）时，`\theta/2`趋于`0`，符合要求；但当`\theta`趋于`2\pi^-`（`\theta < 2\pi`）时，`\theta/2`趋于`\pi`，产生平方根的负值。为了修复这个问题，修改你的代码使得原始角度`\theta`处于`-\pi`到`\pi`之间，且`\theta/2`处于`-\pi/2`到`\pi/2`之间。当`\theta`趋于`0`时，无论`\theta > 0`还是`\theta < 0`，`\theta/2`都会趋于`0`。解可以在附录第 28.5 节末最后找到。
4. 实现极坐标复数：`complex`对象包含两个字段`r`和`theta`，用于存储极坐标表示中使用的参数`r \ge 0`和`0 \le \theta < 2\pi`。

`exp(\theta) = r(\cos(\theta) + i \cdot \sin(\theta))`

在此实现中重新定义构造函数、析构函数和赋值运算符。此外，实现并测试算术运算。
5. `complex`类的用户需要被告知上述修改吗？为什么？

## 第 16 章 向量与矩阵

线性代数中最重要的对象是向量和矩阵（第 9 章）。在这里我们实现了这些对象，以及使用它们的运算符。在程序中包含此代码的用户可以通过编写如`vector v`或`matrix m`的命令来定义向量和矩阵。

此外，下面定义的`*`运算符的不同版本允许用户编写如`v*v`、`v*m`和`m*m`的命令来执行向量乘以向量（内积）以及矩阵乘以矩阵（分别），这与相应的数学公式完全一致。

因此，通过目前的实现，用户可以像使用 C 中的标准对象一样使用向量和矩阵。这样，用户就可以按照其原始的数学精神来思考和编写向量与矩阵，而无需担心任何存储细节。这不仅有助于用简短、优雅且易于调试的代码实现复杂的算法，还能更好地理解对象的本质，并继续开发和改进使用它们的算法和应用。

## 16.1 面向对象编程中的归纳与演绎

在第 10 章第 10.1 节中，我们讨论了解决问题中的归纳与演绎原理。这一原理指出，为了解决一个特定问题，有时将其推广为一个更通用的问题并用更通用的术语来描述是有用的。在通用的术语和框架下，解决问题有时会容易得多，因为描述原始问题的、可能掩盖本质组成部分的技术细节被移出了视野。此外，从原始特定问题得到的通用问题可能有一套基于基础对象和思想的通用理论。

将原始特定问题推广为更通用的问题被称为归纳。一旦定义了通用的框架并开发了合适的理论，就可以解决通用问题。现在，原始问题的解立即作为特例获得。因此，结果是不仅原始问题按要求得到了解决，而且还开发了一个解决通用问题的通用理论。

## 第 16 章. 向量与矩阵

归纳与演绎原理也可以用于面向对象编程。然而，在这种情况下，没有给出显式的问题。相反，任务是定义并实现一个特定的对象及其有用函数。归纳原理指出，人们最好定义一个更通用的对象，从该对象可以作为特例获得所需的对象。

这种方法有助于更准确地定义通用对象。事实上，在对象的通用形式中，非实质性的细节被移开了，只留下了它的本质特征和属性。在通用实现中，这些特征和属性是用（成员）函数编写的，使对象看起来像它应该有的样子。一旦通用对象的实现完成，就可以作为特例获得所需的对象。

例如，考虑在笛卡尔平面上实现一个点的任务。在这种情况下，这样的点可以被视为一个具有两个坐标的向量。建议将原始任务推广为通用问题。

## 16.2 模板

使用归纳和演绎的一种强大工具是模板。事实上，人们可以写一个依赖于未指定参数、例如`n`的模板类。例如，如果用户想要定义二维向量，那么`n`被指定为`2`。向量的算术运算在通用`n`维向量上实现（如归纳）比在特定的二维或三维向量上实现更好。一旦以通用形式实现，通过设置`n=2`就可以很容易获得所需的形式。

## 16.3 向量对象

在这里用模板类实现了多维向量，该类使用整数`N`代表维度`n`。此外，模板类使用参数`T`代表分量的特定类型。例如，如果用户指定`T`为`float`或`double`，则实现了实值向量。另一方面，如果用户指定`T`为复数类，则实现了复值向量。

有了目前的`vector`类，不再需要像第 15 章中的`point`类那样实现笛卡尔平面上的点。事实上，通过将`N`设置为 2 并将`T`设置为`double`，就可以作为特例获得点。这种方法避免了许多不编程工作。

在下面的实现中，类和函数定义前的`template<class T, int N>`字表示它们确实带有两个参数：`T`用于指定向量分量的类型，`N`用于指定向量分的数量。在定义中，这些参数尚未指定。事实上，在`T`为未指定类型且`N`为未指定的自然数时（归纳阶段）定义该类和函数更容易。事实上，只有当用户稍后定义具体的`vector`对象时（在演绎阶段），`T`和`N`才被指定。

```cpp
template<class T, int N> class vector{
    T component [N];
```

私有数据字段`component`是一个包含`N`个`T`类型元素的数组。这里是公共成员的声明：一个接受`T`参数的构造函数，

```cpp
public:
    vector(const T&);
```

一个接受`T`、整数和字符串的构造函数：

```cpp
    vector(const T&,int, char*);
```

一个拷贝构造函数，

# 第 16 章 向量与矩阵

`vector(const vector&);`

一个赋值运算符，

`const vector& operator=(const vector&);`

以及一个接受`T`类型参数的赋值运算符：

`const vector& operator=(const T&);`

这些函数将在稍后定义。
接下来，我们将定义析构函数。该函数块是空的，因为数据字段`component`在标记其结束的`}`符号处自动销毁。

```
vector()
// // destructor
```

由于它的作用与 C++ 编译器提供的默认析构函数相同，因此该析构函数也被称为默认析构函数。
此外，`vector`中的各个分量是私有成员，我们只通过公有成员函数访问它们：

```cpp
const T& operator[](int i) const{
return component[i];
} //read component
```

得益于函数块前的保留关键字`const`，当前的`vector`对象免受任何意外更改的保护。毕竟，此运算符的目的仅仅是读取第`i`个条目，而不是修改它。事实上，第`i`个条目是通过引用而非值返回的，以避免对`T`类构造函数进行不调用，无论`T`是什么。此外，返回的条目在头文件中被声明为常量，因此它无法传递给任何可能更改其值的函数（无论是作为参数还是对象），而这种更改是没有意义的。

通过上述运算符，用户只需编写`v[i]`即可读取`vector`对象`v`中的第`i`个分量。这确实符合向量原始数学公式的精髓。
此外，这里有一个成员函数，用于将第`i`个条目设置为与`T`参数相同的值：

```cpp
void set(int i,const T& a)
component[i] = a;
} // change component
```

事实上，用户只有通过编写`v.set(i,a)`将此函数应用于当前对象`v`才能将`v`中第`i`个分量的值改为标量`a`。
此外，这里是一些成员更新运算符的声明，用于向当前向量添加一个向量：

## 16.4. 构造函数

`const vector& operator+=(const vector&);`

从当前向量中减去一个向量，

`const vector& operator-=(const vector&);`

将当前向量乘以一个标量，

`const vector& operator*=(const T&);`

将当前向量除以一个非零标量，

`const vector& operator/=(const T&);`

};
这结束了`vector`模板类的块。

## 16.4 构造函数

接下来，我们显式定义在上述类块中声明的成员函数。每个头部以`template<class T,int N>`开头，表示这是一个模板函数，尽管它是通用参数`T`和`N`（归纳阶段）定义的，但在用户实际调用时（推导阶段）需要对其进行显式指定。此外，头文件中函数名前的前缀`vector<T,N>:`表示这是一个（带有当前`vector`对象的）成员函数的定义，该函数实际上属于类块。

以下是接受标量参数`a`以设置分量值的构造函数：

```cpp
template<class T, int N>
vector<T,N>::vector(const T& a = 0){
  for(int i = 0; i < N; i++)
    component[i] = a;
  // constructor
```

这里有一个更复杂的构造函数，它不仅接受标量`a`，还接受整数`n`来构造第`nth`个单位向量，即除了第`nth`个分量（其值为`a`）之外，其他分量全为零的向量。

```cpp
template<class T, int N>
vector<T,N>::vector(const T& a = 0,int n,char*){
  for(int i = 0; i < n; i++)
    component[i] = 0;
    component[n] = a;
  // constructor of standard unit vector
```

# 第 16 章 向量与矩阵

为了构造单位向量`(1,0)`，用户可以直接编写`vector<double,2> x(1,0)`。第三参数告诉编译器调用的是这个构造函数。
同样，拷贝构造函数的定义如下：

```cpp
template<class T, int N>
vector<T,N>::vector(const vector<T,N>& v){
  for(int i = 0; i < N; i++)
    component[i] = v[i];
} // copy constructor
```

## 16.5 赋值运算符

赋值运算符定义如下：

```cpp
template<class T, int N>
const vector<T,N>& vector<T,N>::operator=(
  const vector<T,N>& v){
```

如果赋值是非简单的，参数`v`与当前对象不是同一个：

```cpp
if(this != &v)
```

则将`v`的分量一个个赋值给当前对象的相应分量：

```cpp
for(int i = 0; i < N; i++)
  component[i] = v[i];
```

最后，返回当前对象的常量引用，如`const vector<T,N>&`所示：

```cpp
return *this;
} // assignment operator
```

通过这种方式，用户可以编写`w=v`命令将向量`v`赋值给向量`u`和`w`，只要它们的维度相同。赋值运算符的另一个版本是它接受标量（而非向量）参数`a`并将其赋值给当前向量的所有分量：

```cpp
template<class T, int N>
const vector<T,N>::operator=(const T& a){
for(int i = 0; i < N; i++)
  component[i] = a;
  return *this;
} // assignment operator with a scalar argument
```

## 16.6 算术运算符

我们定义了类块中声明的成员更新。将向量参数`v`加到当前向量的`+=`运算符定义如下：

```cpp
template<class T, int N>
const vector<T,N>&operator+=(const vector<T,N>& v) {
  for(int i = 0; i < N; i++)
  component[i] += v[i];
  return *this;
} // adding a vector to the current vector
```

在此代码中，假设当前向量与作为参数的向量`v`相同。建议在函数开头通过`if`这一点，如果不是则发布错误消息。这些细节留给读者。
现在使用`+=`运算符来定义二进制`+`运算符，计算相同维度向量`u`和`v`的和：

```cpp
template<class T, int N>
vector<T,N>& operator+(const vector<T,N>&u, const vector<T,N>&v){
  return vector<T,N>(u) += v;
} // vector plus vector
```

事实上，作为成员函数，`+=`运算符确实可以接受临时向量`vector<T,N>(u)`（由拷贝构造函数返回）作为其当前向量，加上`v`并按值返回，如函数名前之前的头部中的`const vector<T,N>&`所示。`+`运算符是一个普通函数，用户只需编写`u + v`即可计算现有向量`u`和`v`（维度相同）的和。

# 第 16 章 向量与矩阵

向量算术运算符的实现（例如向量乘以标量等）留作练习。在后文中，我们假设这些运算符已经可用。
以下普通函数是返回参数负值的单运算符：

```cpp
template<class T, int N>
const vector<T,N>
operator-(const vector<T,N>&u) {
  return vector<T,N>(u) *= -1;
} // negative of a vector
```

通过这个单运算符，用户只需编写`-v`即可获得定义向量`v`的负值，就像标准数学公式一样。
以下普通函数返回两个向量的内积（定义在第 9 章第 9.14 节）：

```cpp
template<class T, int N>
const T
operator*(const vector<T,N>&u, const vector<T,N>&v){
  T sum = 0;
  for(int i = 0; i < N; i++)
    sum += (+u[i]) * v[i];
  return sum;
} // vector times vector (inner product)
```

事实上，如果`T`是`float`或`double`，那么`+u[i]`就是向量`u`中的第`i`个分量。另一方面，如果`T`是`complex`类，`+u[i]`是`u`第`i`个分量的共轭，符合需要。

上述函数也用于以下普通函数以返回向量的平方`l_2`范数：

```cpp
template<class T, int N>
T squaredNorm(const vector<T,N>&u) {
  return u*u;
} // squared l2-norm
```

同样，以下普通函数返回向量的`l_2`范数：

```cpp
template<class T, int N>
const T l2norm(const vector<T,N>&u) {
  return sqrt(u*u);
} // 12 norm
```

最后，这里是可以在屏幕上逐个分量打印向量的普通函数：

## 16.7 笛卡尔平面与空间中的点

归纳步骤（即实现通用的`N`维向量）现在已经完成。第 15 章中实现的`point`类不再需要了；事实上，它可以从`N`维向量中作为一个特例来获取，即在将`N`设置为 2 的推导中：

```cpp
typedef vector<double,2> point;
```
