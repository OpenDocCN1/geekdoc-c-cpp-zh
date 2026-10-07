

# 84 C++ 概述

```
}
Matrix* m2 = new Matrix(3, 2, p);
cout << "Here is a matrix initialized by a pointer-to-pointer" << endl;
m2->printMatrix();
return 0;
}
```

该程序使用指向指针的存储方式创建了一个单位矩阵和一个带有非零对角线元素的矩阵。使用了 Matrix 对象和指向 Matrix 对象的指针，分别使用这两种情况对应的语法来表示矩阵。

与我们的 Matrix 类代码相关的 Makefile 可能如下所示：

```
simpleMat : simpleDriver.o simpleMatrix.o
 g++ -Wall simpleDriver.o simpleMatrix.o -o simpleMat
```

```
simpleMatrix.o : simpleMatrix.cpp simpleMatrix.h
 g++ -c -Wall simpleMatrix.cpp
```

```
simpleDriver.o : simpleDriver.cpp simpleMatrix.h
 g++ -c -Wall simpleDriver.cpp
```

执行我们的代码后的输出应为：

Here is an identity matrix

+   1 0
0 1

Here is a matrix initialized by a pointer-to-pointer

+   1 2
2 4
3 6

我们的类在功能方面的限制仅限于创建一个类对象。下一步是扩展这个骨架结构以创建功能，包括提供矩阵加法、乘法等方法。这可以通过运算符重载来实现，正如我们将演示的那样。但首先要处理我们类的**拷贝构造函数**概念。

我们最终希望将矩阵对象作为函数的参数或在赋值中（通过 `=`）进行使用。特别是，这意味着会出现创建矩阵对象副本的情况。这是通过 C++ 为每个类隐式默认拷贝构造函数实现的，除非显式定义了拷贝构造函数。隐式拷贝构造函数会对类的成员进行逐个元素的拷贝，这并不总是如愿的。

获取默认拷贝构造函数对我们 Matrix 类行为的示例可以通过尝试运行以下代码：

```cpp//copyEx.cpp
#include "simpleMatrix.h"
#include <iostream>
```

```cpp
using std::cout; using std::endl;
void g(Matrix A){};
```

```cpp
int main(){
Matrix m(2, 2, 1.);
```

# 矩阵与向量类

```cpp
g(m);
cout << "The destructor will now be called."
return 0;
}
```

在以下代码中天真地使用赋值运算符 `=` 会获得类似的结果：

```cpp//equalEx.cpp
#include "simpleMatrix.h"
#include <iostream>

using std::cout; using std::endl;

int main() {
    Matrix m1(1., 2, 2);
    Matrix m2;
    m2 = m1;
    cout << "The destructor will now be called." << endl;
    return 0;
}
```

具体来说，这两个程序中的任何一个都会产生运行时错误，输出如下语句：

```
The destructor will now be called
equalEx(17): malloc: error for object 0x10009
pointer being freed was not allocated
breakpoint in debug
```

这条消息是关于 C++ `new` 运算符底层内存分配问题。该问题可能源于尝试删除一个实际上并没有分配的指针（使用 C 函数 `free`）。这正是所发生的情况。

为了理解发生了什么，我们需要思考当对象超出作用域时析构函数何时触发：即当到达代码块的末尾时。对于第一个程序，创建了一个 Matrix 对象的副本按值传递给函数 `g`。当控制权返回 `main` 时，它超出作用域，析构函数删除与类相关的内存。但由于拷贝是逐个元素进行的，`pa` 指向的内存（即 `main` 中的 `pa`）实际上被删除了。当 `m` 在 `main` 结束超出作用域时，析构函数再次被调用并删除不再指向的内存。

第二个驱动程序 `equalEx.cpp` 也出现了类似的问题。在后者，当 `m2` 等于 `m1` 时，行为是创建一个 Matrix 对象的逐个元素拷贝 `m2`。在 `main` 结束时，`m2` 的析构函数同样通过删除分配给 `m1` 的内存而创建。当尝试删除对象 `m1` 的内存时，发生了错误。

上面的讨论明确了：当涉及动态内存时，必须有一个拷贝构造函数和一个重载的赋值运算符版本。让我们先处理创建拷贝构造函数的问题。

拷贝构造函数是一种特殊的构造函数，其参数是类类的常量引用。具体来说，对于 `Matrix` 类，可以使用以下代码实现拷贝构造函数：

```cpp
Matrix::Matrix(const Matrix& A){
    nRows = A.nRows;
    Cols = A.nCols;
    pA = new(std::nothrow) double*[nRows];
    pointerCheck();

    for(int i = 0; i < nRows; i++) {
    pA[i] = new(std::nothrow) double[nCols];
    pointerCheck(i);
}
```

如果将其包含在 Matrix 类方法的定义中，并在相关的头文件中插入 `Matrix(const Matrix& A);`，那么 `copyEx.cpp` 的输出将只是 `The destructor will now be called.`。显然，拷贝问题已经解决。

要处理 `Matrix` 类中使用赋值的问题，解决方案是沿着 3.8.3 节的定义赋值运算符的重载版本。我们矩阵类的重载赋值运算符的形式为 `Matrix& operator=(const Matrix& A);`。

这里，更通用地说，赋值运算符需要返回引用以允许在复合表达式中使用赋值。赋值运算符的定义可能如下：

```cpp
Matrix::operator=(const Matrix& A){
    if(this == &A) // 避免自赋值
        return *this;
    // 如果维度匹配，我们可以拷贝，否则……
    if(nRows != A.nRows||nCols != A.nCols){
        if(pA != nullptr) // 在释放内存之前检查
            ~Matrix();

        // 重新定义成员
        nRows = A.nRows;
        Cols = A.nCols;
        pA = new(std::nothrow) double*[nRows];
        pointerCheck();

        for(int i = 0; i < nRows; i++) {
            pA[i] = new(std::nothrow) double[nCols];
            pointerCheck(i);
        }
    }
}
```

```cpp
for(int i = 0; i < nRows; i++)
    for(int j = 0; j < nCols; j++)
        pa[i][j] = A.pa[i][j];

return *this;
}
```

这段代码与我们为拷贝构造函数使用的代码相似。主要区别在于它现在允许处理已存在的对象。在这种情况下，必须考虑到 `=` 左侧的 Matrix 将被运算符参数中的 Matrix `A` 的内容覆盖，这对应于 `=` 运算符右侧的内容。

