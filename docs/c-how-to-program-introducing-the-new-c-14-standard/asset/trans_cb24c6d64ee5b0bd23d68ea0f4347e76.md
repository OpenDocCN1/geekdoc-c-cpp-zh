

```cpp
// Fig. 6.12: fig06_12.cpp
// square function used to demonstrate the function
// call stack and activation records.
#include <iostream>
using namespace std;

int square(int); // prototype for function square

int main() {
    int a{10}; // value to square (local variable in main)

    cout << a << " squared: " << square(a) << endl; // display a squared
}

// returns the square of an integer
int square(int x) { // x is a local variable
    return x * x; // calculate square and return result
}
```

```text
10 squared: 100
```

**图 6.12** 用于演示函数调用栈和活动记录的 `square` 函数。

首先，操作系统调用 `main`——这会将一个活动记录*压入*栈中（如**图 6.13**所示）。活动记录告诉 `main` 如何返回操作系统（即转移到返回地址 `R1`），并包含 `main` 的局部变量（即 `a`，初始化为 `10`）的空间。

**步骤 1：** 操作系统调用 `main` 来执行应用程序

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_764_0.png)

```cpp
int main() {
    int a{10};
    cout << a * a << endl;
}
```

**图 6.13** 操作系统调用 `main` 执行程序后的函数调用栈。

在返回操作系统之前，函数 `main` 现在调用**图 6.12** 中第 12 行的函数 `square`。这会导致 `square` 的栈帧（第16–18行）被压入函数调用栈（**图 6.14**）。该栈帧包含 `square` 返回 `main` 所需的返回地址（即 `R2`），以及 `square` 的局部变量（即 `x`）的内存。

`square` 计算完其参数的平方后，需要返回 `main`——不再需要其变量 `x` 的内存。因此 `square` 的栈帧会从栈中*弹出*——给 `square` 提供在 `main` 中的返回位置（即 `R2`），并丢弃 `square` 的局部变量（**步骤 3**）。

**图 6.15** 展示了 `square` 的活动记录被*弹出*后的函数调用栈。

**步骤 2：** `main` 调用函数 `square` 来执行计算

```cpp
int main() {
    int a {10};
    cout << a << " squared: "
         << square(a) << endl;
}
```

```cpp
int square(int x) {
    return x * x;
}
```

返回位置 **R2**

`main` 调用 `square` 后的函数调用栈

栈顶

函数 `square` 的活动记录

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_765_0.png)

函数 `main` 的活动记录

**图 6.14** `main` 调用 `square` 执行计算后的函数调用栈。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_766_0.png)

```cpp
int main() {
    int a{10};
    cout << a << " squared: "
         << square(a) << endl;
}
```

```cpp
int square(int x) {
    return x * x;
}
```

**图 6.15** 函数 `square` 返回 `main` 后的函数调用栈。

函数 `main` 现在显示调用 `square` 的结果（图 6.12 中的第 12 行）。到达 `main` 的右花括号会导致其栈帧从栈中*弹出*，并给 `main` 提供返回操作系统所需的地址（即图 6.13 中的 `R1`）——此时，`main` 的局部变量（即 `a`）不再存在。

你现在已经看到了栈数据结构在实现支持程序执行的关键机制方面是多么有价值。数据结构在计算机科学中有许多重要应用。我们将在**第 15 章 标准库容器与迭代器**和**第 19 章 自定义模板化数据结构**中讨论栈、队列、列表、树和其他数据结构。

## 6.12 内联函数

从软件工程的角度来看，将程序实现为一组函数是好的，但函数调用涉及执行时开销。C++ 提供了**内联函数**来帮助减少函数调用的开销。在函数定义的返回类型前加上限定符 `inline`，会*建议*编译器在函数被调用的*每个*地方（在适当的时候）生成函数体代码的副本，以避免函数调用。这通常会使程序变大。编译器可以忽略 `inline` 限定符，并且除了*最小的*函数外，通常都会忽略。可复用的 `inline` 函数通常放在头文件中，以便其定义能被每个使用它们的源文件包含。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_767_0.png)

### 软件工程

**观察 6.7**

> *如果你更改了某个* `inline` *函数的定义，必须重新编译该函数的所有客户端。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_768_0.png)

### 性能提示 6.1

> *编译器可以对你不曾显式使用* `inline` *关键字的代码进行内联。当今的优化编译器非常复杂，因此最好将内联决策留给编译器。*

**图 6.16** 使用 `inline` 函数 `cube`（第9–11行）来计算立方体的体积。函数 `cube` 参数列表（第9行）中的关键字 `const` 告诉编译器，该函数*不会*修改变量 `side`。这确保了在计算过程中 `side` 的值*不会*被函数改变。（关键字 `const` 将在**第7–9章**中更详细地讨论。）

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_768_1.png)

### 软件工程

**观察 6.8**

> *应该使用* `const` *限定符来强制执行最小权限原则。利用这一原则进行正确的软件设计，可以大大减少调试时间和不当副作用，并使程序更易于修改和维护。*

```cpp
// Fig. 6.16: fig06_16.cpp
// inline function that calculates the volume of a cube.
#include <iostream>
using namespace std;

// Definition of inline function cube. Definition of function appears
// before function is called, so a function prototype is not required.
// First line of function definition acts as the prototype.
inline double cube(const double side) {
    return side * side * side; // calculate cube
}

int main() {
    double sideValue; // stores value entered by user
    cout << "Enter the side length of your cube: ";
    cin >> sideValue; // read value from user

    // calculate cube of sideValue and display result
    cout << "Volume of cube with side "
         << sideValue << " is " << cube(sideValue) << endl;
}
```

```text
Enter the side length of your cube: 3.5
Volume of cube with side 3.5 is 42.875
```

图 6.16 计算立方体体积的*内联*函数。

## 6.13 引用和引用参数

在许多编程语言中，向函数传递参数有两种方式：**按值传递**和**按引用传递**。当参数按值传递时，会生成参数值的*副本*，并将该副本（通过函数调用栈）传递给被调用的函数。对副本的更改*不会*影响调用方中原始变量的值。这防止了*意外副作用*，这些副作用会极大地阻碍正确、可靠软件系统的开发。到目前为止，本书中的每个参数都是按值传递的。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_770_0.png)

### 性能提示 6.2

> *按值传递的一个缺点是，如果要传递较大的数据项，复制该数据可能会消耗大量的执行时间和内存空间。*

### 引用参数

本节介绍引用参数——C++ 提供的执行按引用传递的两种方式中的第一种。通过*按引用传递*，调用方给予被调用的函数*直接访问调用方数据*并修改该数据的能力。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_771_0.png)

### 性能提示 6.3

> *按引用传递在性能方面有好处，因为它可以消除按值传递复制大量数据的开销。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_771_1.png)

### 软件工程

**观察 6.9**

> *按引用传递可能会削弱安全性；被调用的函数可能会破坏调用方的数据。*

在本节示例之后，我们将展示如何在*同时*实现保护调用方数据不被破坏的软件工程优势的同时，获得按引用传递的性能优势。

**引用参数**是其对应实参在函数调用中的*别名*。若要指示函数参数按引用传递，只需在函数原型中的参数类型后加上一个*与号*（&）；在列出参数时也使用同样的约定

