
由成员初始化器或体抛出的异常将导致执行永远无法到达体的结束右合大括号。相反，`catch`子句会被触发。由于构造函数体没有完成，对象不被认为已正确构造，最终对象的析构函数不会被调用。

构造函数`try`块的`catch`子句与普通函数`try`块的`catch`子句略有不同。到达构造函数`try`块的异常可能会转换为另一个异常（从`catch`子句抛出），但如果`catch`子句没有显式抛出异常，则到达`catch`子句的异常总是重新抛出。因此，没有办法确认从基类构造函数或成员初始化到构造函数抛出的异常：此类异常会传播到成员块，在这种情况下，对象的构造始终是不完整的。

如果不完整的对象抛出异常，构造函数仍负责防止内存（泛指资源）泄漏。有几种方法可以实现这一点：

- 如果构造函数定义了函数`try`，则构造函数句无法使用任何数据成员。相反，构造函数体本身必须确保内存被正确删除；
- 使用多继承时：如果初始基类已经构造，而后续类抛出异常，则初始基类对象会被析毁（因为它们已完全构造）；
- 使用组合时：已构造的对象会被析毁（因为它们已完全构造）；
- 使用原始指针应使用智能指针（参见第`18.4`节）来管理动态分配的内存。在这种情况下，如果构造函数在分配动态内存之前抛出异常，内存作为`shared_ptr`对象返回。
- 如果必须使用指针成员，则构造函数体应首先在成员初始化中初始化指针成员。然后在体中动态分配内存，重新分配指针成员。在这些情况下，指针处理必须嵌入`try`块中，允许构造函数在抛出异常之前释放已分配的内存，从而到达构造函数函数块的`catch`子句。最后的`catch`可以完成所需的任何操作（例如，写入日志）。示例：

```cpp
class Incomplete2 {
    Composed d_composed;
    char *d_cp; // 原始指针
    int *d_ip;
public:
    Incomplete2(size_t nChars, size_t nInts)
        try {
            d_composed(* arguments */); // 可能抛出异常
            d_cp(0);
            d_ip(0)
        {
            preamble(); // 可能抛出异常
            d_cp = new char[nChars]; // 可能抛出异常
            d_ip = new int[nInts]; // 可能抛出异常
            postamble(); // 可能抛出异常
        } catch (...)
        {
            delete[] d_cp; // 清理
            delete[] d_ip;
            throw; // 重新抛出异常
        }
    catch (...)
    {
        // 可能写入日志，但也抛出
        // 原始异常
    }
}
```

另一方面，C++支持构造函数委托，因此一个对象可能已经根据C++运行时系统完成了完全构造，但其（委托的）构造函数函数可能会抛出异常，如下例所示：

```cpp
1: #include <iostream>
2:   using namespace std;
3:
4: class Delegate
5: {
6:     char *d_p1;
7:     char *d_p2;
8:
9:
10:    public:
11:        Delegate()        // 成功 -> 对象已构造
12:            Delegate(0)
13:        {
14:            d_p2 = new char[10];
15:            cout << "default, throws...\n";
16:            throw 12; // 但被视为已构造
17:        }
18:    ~Delegate()
19:        {
20:            delete[] d_p1;
21:            delete[] d_p2;
22:            cout << "destructor\n";
23:        }
24:
25:    private:
26:        Delegate(int x)    // 完成 OK
27:
28:
29:            d_p1(0),
30:            d_p2(0)
31:        {
32:            cout << "delegated\n";
33:        }
34:    };
35: int main(){
36:   try
37:   {
38:       Delegate del;        // 抛出
39:
40:       cout << "never reached\n";
41:   } // del 的析构函数在这里被调用
42:   } catch (...)
43: }
```

这是`Delegate`设计者的责任，要确保抛出异常的默认构造函数不会使`Delegate(int x)`构造函数执行的操作失效。后构造函数由默认构造函数（第`12`行）调用，并且仅初始化第`6`和`7`行的数据成员（第`28, 29`行）。接下来，默认构造函数在分配某些内存后抛出异常（第`16`行）。事实上，异常可能在任何点抛出，但析构函数（第`18`行）无论如何都会调用（第`41`行）。如果抛出多个异常，`Delegate`可以定义一个枚举和一个枚举类型的数据成员，该数据成员被设置为指示下一个异常性质的枚举值（如果它抛出了的话），析构函数可以根据其类型处理异常。

## 10.13 析构函数中的 C++ 标准异常

根据 C 标准，析构函数不能离开其体体。为析构函数提供函数`try`块违反了标准：被函数块的`catch`子句捕获的异常已经离开了析构函数的体体。如果——在违反的情况下——为析构函数提供了函数`try`块且`try`块捕获了异常，则它会被重新抛出，就像在构造函数`try`块的`catch`子句中发生的情况一样。

异常离开析构函数体的后果尚未定义，可能会导致意外的行为。考虑以下示例：

假设一个木工做了一个单抽屉的柜子。柜子完成了，购买柜子的客户发现柜子可以按预期使用。客户对柜子很满意，让木工再做一个柜子，这次有两个抽屉。当第二个柜子完成后，客户把它带回家，并在第一次使用后感到非常惊讶。

奇怪的故事吗？考虑以下程序：

```cpp
int main() {
    try {
        {
            cerr << "Creating Cupboard1\n";
            Cupboard1();
            cerr << "Beyond Cupboard1 object\n";
        }
        catch (...) {
            cerr << "Cupboard1 behaves as expected\n";
        }
        try {
            {
                cerr << "Creating Cupboard2\n";
                Cupboard2();
                cerr << "Beyond Cupboard2 object\n";
            }
            catch (...) {
                cerr << "Cupboard2 behaves as expected\n";
            }
        }
    }
}
```

当这个程序运行时，它产生以下输出：

```
Creating Cupboard1
Drawer 1 used
Cupboard1 behaves as expected
Creating Cupboard2
Drawer 2 used
Drawer 1 used
terminate called after throwing an instance of 'int'
Abort
```

最后的`Abort`表示程序已中止，而不是显示`Cupboard2 behaves as expected`的消息。

让我们看看涉及的三个类。`Drawer`类没有特殊特征，除了析构函数抛出一个异常：

```cpp
class Drawer
{
    size_t d_nr;
    public:
        Drawer(size_t nr)
            : d_nr(nr) {}
        ~Drawer()
    {
        cerr << "Drawer " << d_nr << " used\n";
        throw 0;
    }
};
```

`Cupboard1`类没有任何特殊特征。它仅仅有一个组合的`Drawer`对象：

```cpp
class Cupboard1
{
    Drawer left;
    public:
        Cupboard1()
            : left(1) {}
};
```

`Cupboard2`构造方式类似，但它有两个组合的`Drawer`对象：

```cpp
class Cupboard2
{
    Drawer left;
    Drawer right;
    public:
        Cupboard2()
            : left(1), right(2) {}
};
```

## 10.13 析构函数中的异常

根据 C 标准，析构函数不能离开其体体。为析构函数提供函数`try`块违反了标准：被函数块的`catch`子句捕获的异常已经离开了析构函数的体体。如果——在违反的情况下——为析构函数提供了函数`try`块且`try`块捕获了异常，则它会被重新抛出，就像在构造函数`try`块的`catch`子句中发生的情况一样。

异常离开析构函数体的后果尚未定义，可能会导致意外的行为。

# 第 11 章 更多运算符重载

```cpp
size_t d_size;
int *d_data;
```

```cpp
public:
    IntArray(size_t size = 1);
    IntArray(IntArray const &other);
    ~IntArray();
    IntArray &operator=(IntArray const &other);
```

```cpp
// 重载的下标运算符：
int &operator[](size_t index); // 第一个
int const &operator[](size_t index) const; // 第二个
```

```cpp
void swap(IntArray &other); // 简单的实现
```

```cpp
private:
    void boundary(size_t index) const;
    int &operatorIndex(size_t index) const;
};
```

该类具有以下特点：

- 它的一个构造函数带有一个默认参数值的`size_t`参数，用于指定对象中`int`元素的数量。
- 该类内部使用指针来访问已分配的内存。因此，提供了必要的工具：拷贝构造函数、重载的赋值运算符和析构函数。
- 存在两个重载的下标运算符允许我们访问并修改非`const` `IntArray`对象的元素。

这两个运算符在哪里呢？
第一个重载的下标运算符`operator[]`可以返回一个非`const` `IntArray`对象的引用。该重载运算符的原型允许我们使用像`x[10]`这样的表达式作为右值或字面量。
对于非`const` `IntArray`，`operator[]`可用于检索和赋值值。非`const` `operator[]`成员函数的返回值是一个`int&`，允许在作为左值使用时修改元素；而`const` `operator[]`的返回值允许将返回值（例如一个二进制文件）写入到以下位置中：

```cpp
void writeValue(IntArray const &iarr, size_t idx){
    cout.write(reinterpret_cast<char *>(iarr[idx]));
}
```

如果没有无可赋值的内容，这种方案就会失效。考虑一下我们定义了`IntArray const stable(5)`的情况。这样的对象是一个`const`对象。编译器检测到这一点，如果存在非`const`版本，它将拒绝编译此定义。第二个重载的下标运算符会被编译器自动用于`const`对象。它用于检索而非值赋值。这当然正是我们使用`const`对象时所希望的。在这种情况下，成员仅根据其`const`属性进行重载。这种形式的函数重载早早在C++标准中引入（第`2.5`节和`7.7`节）。

## 11.1. 重载 'operator[]'

- 由于只有一个指针数据成员`data`，由对象分配的内存的析构是一个简单的`delete[]`操作。

现在，成员函数的实现（省略`swap`的简单实现，请参见第`9`章）如下：

```cpp
#include "intarray.h"
IntArray::IntArray(size_t size)
: d_size(size)
{
  if (d_size < 1)
    throw "IntArray: size of array must be >= 1";
  d_data = new int[d_size];
}
IntArray::IntArray(IntArray const &other)
: d_size(other.d_size),
  d_data(new int[d_size])
{
  memcpy(d_data, other.d_data, d_size * sizeof(int));
}
IntArray::~IntArray()
{
  delete[] d_data;
}
IntArray &IntArray::operator=(IntArray const &other)
{
  IntArray tmp(other);
  swap(tmp);
  return *this;
}
int &IntArray::operatorIndex(size_t index)
{
  boundary(index);
  return d_data[index];
}
int &IntArray::operator[](size_t index)
{
  return operatorIndex(index);
}
int const &IntArray::operator[](size_t index) const
{
  return operatorIndex(index);
}
```

# 第 11 章 更多运算符重载

```cpp
void IntArray::swap(IntArray &other)
{
    // 交换 *this 和 other 的 d_size 和 d_data 成员
}
```

```cpp
void IntArray::boundary(size_t index) const
{
    if (index < d_size)
        return;
    ostream out;
    out << "IntArray: boundary overflow, index = " <<
        index << ", should be < " << d_size << '\n';
    throw out.str();
}
```

注意`operator()`成员的实现：由于非`const`成员可以拥有`const`函数，且`const`函数的实现与非`const`成员函数的实现相同，因此`operator()`成员可以使用`operatorIndex(size_t index) const`进行内联定义。成员函数可以返回一个非`const`引用（或指针）值，引用对象的一个数据成员。当然，这是一个潜在的危险后门，可能会破坏数据隐藏性。然而，公共接口中的成员防止了这一点，因此两个公共`operator()`成员本身会安全地调用同一个`operatorIndex()`成员，该成员定义了一个私有后门。

## 11.11 多参数 'operator[]()'

考虑一个标准的二维数组。它有`nRows`行和`nCols`列。这样的数组是一维数组的推广：每行都由一个包含`nCols`个元素的数组组成。定义了一个类型`DoubleArray`，类似于上一节的`IntArray`，但包含的是`double`值而非`int`值，设计该类可以如下：

```cpp
class Matrix
{
    size_t nRows;
    size_t nCols;
    double **d_data;
public:
    Matrix(size_t nRows, size_t nCols);
};
```

并且它的构造函数分配`DoubleArrays`，每个都有`nCols`个元素并初始化为`0`：

```cpp
```
