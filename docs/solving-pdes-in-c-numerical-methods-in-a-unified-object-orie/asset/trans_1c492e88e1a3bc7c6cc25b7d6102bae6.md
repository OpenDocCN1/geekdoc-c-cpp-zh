
编译时维度尚不可知，因此不能使用第2章第18节的“vector”类。显然需要一种能在运行时确定维度的动态向量。

本节将提供所需的动态实现。在该实现中，“dynamicVector”对象的维度存储在一个私有数据成员中。因此，“dynamicVector”对象不仅包含向量的分量，还包含一个额外的整数来指定向量的维度。该整数的值可以在运行时根据需要设置。

由于实际维度在编译时未知，用于存储“dynamicVector”对象的内存无法在编译时分配。相反，内存分配在运行时使用保留字“new”完成。“new”函数为某个对象分配内存并返回该内存的地址。例如，

```
double* p = new double;
```

为“double”变量分配内存，并用其地址初始化一个名为“p”的指向double的指针。

当前实现灵活且动态，符合要求。模板仅用于指定分量的类型，而非分量的数量。这个数量确实是在运行时动态确定的。

“dynamicVector”类中的数据字段声明为“protected”，以便稍后定义的派生类可以访问它们。使用了两个数据字段：指示向量维度的整数“dimension”和指向向量分量的指针“component”。

由于维度尚不可用，“component”字段必须声明为指向T的指针，而不是像第2章第18节的“vector”类中那样声明为T的数组。只有在实际调用“dynamicVector”类的构造函数时，所需的内存才会被分配，“component”才会指向具体的分量数组：

```
#include<stdio.h>
template<class T> class dynamicVector{
protected:
    int dimension;
    T* component;
public:
    dynamicVector(int, const T&);
    dynamicVector(const dynamicVector&);
    const dynamicVector& operator=(const dynamicVector&);
    const dynamicVector& operator=(const T&);
```

上面只声明了构造函数和赋值运算符。实际定义将在后面给出。接下来，我们定义析构函数：

```
~dynamicVector(){
    delete [] component;
} // 析构函数
```

析构函数中使用的“delete[]”命令会删除整个数组“component”，并释放其占用的内存以供将来使用。注意，“dimension”字段不需要显式删除。因为它不是指针，所以会被C++编译器内置的默认析构函数隐式删除，该默认析构函数在每次调用上述析构函数结束时自动调用。

因为“dimension”字段是protected的，我们需要一个公共函数来从非“dynamicVector”派生类的普通类中读取它：

```
int dim() const{
    return dimension;
} // 返回维度
```

下面定义的“operator()”返回当前“dynamicVector”对象中第i个分量的引用。由于该引用非常量，用户可修改它。而“operator[]”返回常量引用，因此第i个分量只能通过它读取：

```
T& operator()(int i){
    return component[i];
} // 读/写第i个分量
```

```
const T& operator[](int i) const{
    return component[i];
} // 只读第i个分量
```

我们还声明了一些成员算术运算符，它们作用于当前的“dynamic Vector”对象。完整定义将在后面给出。

```
const dynamicVector& operator+=(const dynamicVector&);
const dynamicVector& operator-=(const dynamicVector&);
const dynamicVector& operator*=(const T&);
const dynamicVector& operator/=(const T&);
};
```

“dynamicVector”类的定义到此结束。

现在我们来定义上面仅声明过的函数。在下面定义的构造函数中，如果维度非零，则在初始化列表中为分量数组分配内存：该动态内存分配由“new”命令完成。该命令返回的地址存放在“component”字段中以供将来访问：

```
template<class T>
dynamicVector<T>::dynamicVector(
    int dim = 0, const T& a = 0)
    : dimension(dim), component(dim ? new T[dim] : 0){
for(int i = 0; i < dim; i++)
    component[i] = a;
} // 构造函数
```

拷贝构造函数中使用相同的方法：

```
template<class T>
dynamicVector<T>::dynamicVector(const dynamicVector<T>& v)
```

: dimension(v.dimension),
component(v.dimension ? new T[v.dimension] : 0){
  for(int i = 0; i < v.dimension; i++)
    component[i] = v.component[i];
} // 拷贝构造函数

接下来，我们定义赋值运算符：

```
template<class T>
const dynamicVector<T>&
dynamicVector<T>::operator=(const dynamicVector<T>& v){
  if(this != &v){
```

我们刚刚进入“if”块，它确保赋值运算符不会被形如“u = u”的无意义调用触发。现在，我们需要使当前向量的维度与参数向量“v”的维度相同：

```
if(dimension != v.dimension){
  delete [] component;
  component = new T[v.dimension];
}
```

这样，数组“component[]”的维度与数组“v.component[]”的维度相同，并且可以在一个标准循环中填充对应的值：

```
for(int i = 0; i < v.dimension; i++)
  component[i] = v.component[i];
dimension = v.dimension;
}
return *this;
} // 赋值运算符
```

这就完成了接受向量参数的赋值运算符的定义。接下来，我们定义接受标量参数的另一个赋值运算符。该标量被简单地赋给当前动态向量的所有分量：

```
template<class T>
const dynamicVector<T>&
dynamicVector<T>::operator=(const T& a){
  for(int i = 0; i < dimension; i++)
    component[i] = a;
  return *this;
} // 带标量参数的赋值运算符
```

接下来，我们实现一些有用的算术运算符：

```
template<class T>
const dynamicVector<T>&
dynamicVector<T>::operator+=( const dynamicVector<T>&v){
  for(int i = 0; i < dimension; i++)
```

```
```cpp
component[i] += v[i];
return *this;
} // 将dynamicVector加到当前向量上

template<class T>
const dynamicVector<T>
operator+(const dynamicVector<T>&u,
         const dynamicVector<T>&v){
  return dynamicVector<T>(u) += v;
} // dynamicVector加dynamicVector

template<class T>
const dynamicVector<T>
operator-(const dynamicVector<T>&u){
  return dynamicVector<T>(u) *= -1.;
} // dynamicVector的负向量
```
```

最后，这里有一个将动态向量打印到屏幕的函数：

```
```cpp
template<class T>
void print(const dynamicVector<T>&v){
  print("[");
  for(int i = 0; i < v.dim(); i++){
    printf("v[%d] = ",i);
    print(v[i]);
  }
  print("]\n");
} // 打印dynamicVector
```
```

一些算术运算的实现，如减法、乘法、标量除法和内积，留给读者作为练习。假设这些运算也可用，就可以编写各种向量操作如下：

```
```cpp
int main(){
  dynamicVector<double> v(3,1.);
  dynamicVector<double> u;
  u=2.*v;
  printf("v:\n");
  print(v);
  printf("u:\n");
  print(u);
  printf("u+v:\n");
  print(u+v);
  printf("u-v:\n");
  print(u-v);
  printf("u*v=%f\n",u*v);
  return 0;
}
```
```

## 3.3. 动态向量

## 3.4 列表

上述向量和动态向量都是作为类型为“T”的分量数组实现的。根据定义，C（以及其它编程语言）中的数组必须包含类型和大小都相同的分量。任何数组都不能包含占用不同内存量的分量。

然而，在许多应用中，需要使用大小各异的对象序列。例如，可能需要使用维度在编译时尚不可知的向量序列。这类应用不能再使用标准数组来存储向量，因为最终它们可能占用不同的大小。需要一种更灵活的数据结构。

![](img/1f293b0ceb2de964310ea7f941a1b580_132_0.png)

图3.1. 对象列表的示意图。箭头表示指针，圆点表示已构造的对象。i表示指针数组中的索引。

所需的数据结构实现在“list”类中，该类包含一个指向“T”对象的指针数组（见图3.1）。虽然“T”类型的对象可能具有不同的大小（例如，当“T”是“dynamicVector”时），但它们的地址只是占用固定内存量的整数，因此可以放在数组中。在运行时，具体的“T”类型对象被放置在数组中的地址处。例如，如果在编译时将“T”指定为“dynamicVector”，则列表中的“dynamicVector”对象的维度在运行时通过“dynamicVector”类的构造函数指定，然后放置在列表数组中包含的地址处。

列表的长度，即其中数组中指向“T”的指针的数量，也可以在运行时动态确定。与“dynamicVector”类一样，这是通过使用一个额外的整数字段来存储项的数量来实现的。因此，“list”类包含两个受保护的数据字段：“number”表示项数量，“item”存储它们的地址。详细实现如下：

