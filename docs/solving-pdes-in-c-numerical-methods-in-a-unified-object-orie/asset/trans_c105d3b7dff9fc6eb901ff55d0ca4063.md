

而不是对其的引用，正如在函数名之前出现的单词“double”（而不是“double&”）所指示的那样。

实现只读运算符的另一种可能策略是定义返回的变量为 double 的常量引用：

```
const double& operator[](int i) const{
    return coordinate[i];
} // read-only ith coordinate
```

如果坐标本身是复制成本很高的庞大对象，则这种方法更可取：这里，然而，由于它们只是“double”对象，无论是通过值返回还是通过常量引用返回都没有区别。

“operator[]”函数也可以按如下方式实现为“读写”运算符：

```
double& operator[](int i) {
    return coordinate[i];
} // read/write ith coordinate (risky)
```

此版本返回对第 'i' 个坐标的非常量引用，该引用甚至可以从既不是“point”类的成员也不是友元的普通函数中进一步更改。使用此版本，只有当“point”对象 'P' 为非常量时，才能进行形如“P[i]”的调用；否则，其第 'i' 个坐标为常量，不能作为非常量引用，以免通过它被更改。因此，在打开函数块的 '{' 字符之前的保留字“const”缺失：这表明当前对象可以被函数更改，因此不能为常量。

然而，后一种版本有些危险，因为坐标可能会被无意中更改，从而破坏原始的“point”对象。因此，此版本必须谨慎使用，并且仅在必要时使用。

也可以使用括号定义“operator()”而不是“operator[]”。此时，“point”对象 'P' 中的第 'i' 个坐标读作“P(i)”而不是“P[i]”。在这里，两种风格之间没有实质性区别。然而，在其他情况下，“operator()”可能更有用，因为它可以接受任意数量的参数，而“operator[]”必须恰好接受一个参数。

“point”模板类中剩下的唯一工作是显式定义上面声明的拷贝构造函数。此任务将在下面讨论并完成。

“point”模板类必须有一个拷贝构造函数，因为编译器提供的默认拷贝构造函数做错了。事实上，此拷贝构造函数只是将复制对象的每个数据字段复制到构造的对象中。由于“point<>”模板类中的字段是一个数组，它包含一个“double”变量的地址。因此，默认拷贝构造函数只是将此地址复制到构造对象的相应字段中，并且没有创建新数组，并且两个对象在其数据字段中具有相同的数组。结果是，构造的对象并不是真正的新对象，而仅仅是对旧对象的引用，这绝对不是所需的结果。下面的代码中的拷贝构造函数，另一方面，确实创建了一个与旧对象具有相同数据的新对象，正如所要求的。

定义之前的“template<int N>”一词表示这是一个模板函数。函数名之前的“point<N>::”前缀表示这是一个成员函数的定义：

在下一节中，我们提供此模板类的更完整版本，其中包含许多有用的函数，从中可以获得二维和三维点作为特例。

## 2.18 示例：向量对象

在本节中，我们介绍实现 N 维向量空间的“vector<T,N>”模板类，其中每个向量具有 N 个类型为 'T' 的分量。此类中实现的算术运算符为处理向量提供了一个有用且方便的框架。二维和三维点对象也可以作为特例获得。

除了非常短的运算符和函数外，大多数运算符和函数仅在下面的类块内部声明，其实际定义稍后放在其外部。函数名前面的“vector<T,N>::”前缀表示定义了成员函数。函数定义之前的前缀“template<class T, int N>”表示这是一个模板函数，使用尚未指定的类型 'T' 和整数 'N'：

```
#include<stdio.h>
template<class T, int N> class vector{
    T component[N];
public:
    vector(const T&);
    vector(const vector&);
    const vector& operator=(const vector&);
    const vector& operator=(const T&);
```

到目前为止，我们仅声明了构造函数、拷贝构造函数以及带标量和向量参数的赋值运算符。实际定义将在后面提供。接下来，我们定义析构函数。实际上，析构函数不包含任何命令。实际的销毁由函数结束时调用的默认析构函数完成：

```
~vector(){
} // destructor
```

由于向量中的分量是私有类成员，我们需要公共函数来访问它们。然后这些函数甚至可以从非成员和非友元函数中调用：

```
const T& operator[](int i) const{
    return component[i];
} //read ith component

void set(int i,const T& a){
    component[i] = a;
} // change ith component
```

在这里我们声明更多将在后面定义的成员算术运算符：

```
template<class T, int N>
const vector<T,N>&
operator+(const vector<T,N>&u, const vector<T,N>&v) {
    return vector<T,N>(u) += v;
} // vector plus vector
```

以下是按常见数学公式对向量进行操作的单目运算符：+v 与 v 相同，-v 是 v 的负值。

```
template<class T, int N>
const vector<T,N>&
operator+(const vector<T,N>&u) {
    return u;
} // positive of a vector
```

```
template<class T, int N>
const vector<T,N>&
operator-(const vector<T,N>&u) {
    return vector<T,N>(u) *= -1;
} // negative of a vector
```

以下函数返回两个向量的内积和一个向量的平方和：

```
template<class T, int N>
const T
operator*(const vector<T,N>&u, const vector<T,N>&v) {
    T sum = 0;
    for(int i = 0; i < N; i++)
        sum += u[i] * v[i];
    return sum;
} // vector times vector (inner product)
```

```
template<class T, int N>
T squaredNorm(const vector<T,N>&u) {
    return u*u;
} // sum of squares
```

最后，这里有一个将向量打印到屏幕的函数：

```
template<class T, int N>
void print(const vector<T,N>&v) {
    printf("(");
    for(int i = 0; i < N; i++) {
        printf("v[%d]=", i);
        printf(v[i]);
    }
    printf(")\n");
} // printing a vector
```

模板类“vector<T,N>”及其函数现在已完成。二维和三维点类可以从中作为特例获得：

```
typedef vector<double,2> point;
typedef vector<double,3> point3;
```

“typedef”命令为名称长且复杂的类型提供简短方便的名称。这样，“point”是二维向量的简写，“point3”是三维向量的简写。在下面，我们展示如何使用“point”类进一步派生“complex”类的另一种实现。

## 2.19 继承

在第 2.16 节中，我们定义了实现复数的“complex”类。隐藏在“complex”对象中的数据是两个“double”字段，用于存储其实部和虚部。在本节中，我们介绍一种略有不同的实现，使用复数作为二维笛卡尔平面中点的几何解释，其中 x 坐标表示实部，y 坐标表示虚部。例如，可以写

```
class complex{
    point p;
public:
    complex(const point&P):p(P){}

    complex(const complex&c):p(c.p){}

    const complex&operator=(const complex&c){
        p=c.p;
        return *this;
    }

    const complex&operator+=(const complex&c){
        p+=c.p;
        return *this;
    }
};
```

等等。此实现使用“has a”方法：“complex”对象有一个“point”字段来包含数据。在这种方法中，必须显式编写“complex”类中所需的功能。

上述方法并不完全自然。从数学上讲，复数并不“拥有”任何点，而是“是”二维笛卡尔平面中的一个点。这引导我们使用 C++ 中可用的“is a”方法。在这种方法中，“complex”对象实际上是一个带有一些额外功能或函数的“point”对象。这种方法在这种情况下更符合面向对象编程的精神，因为它允许人们将复数精确地实现为它们在数学上的样子：具有一些额外代数特征的笛卡尔平面中的点。

