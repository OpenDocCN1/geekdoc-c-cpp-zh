
```cpp
for(int i = 0; i < nRows; i++)
for(int j = 0; j < nCols; j++)
pM[i][j] = i*j;
cout << "pM[" << i << "][" << j << "] = " << pM[i][j] << " ";
cout << endl endl;
```

```cpp
//memory clean up
for(int i = 0; i < nRows; i++)
delete[] pM[i];
delete[] pM;
return 0;
```

这段代码将产生类似于下面的输出：

The value of pM is 0x001150

The address for pM[0] is 0x001150

The address for pM[1] is 0x001154

The value of pM[0] is 0x001160

The address of pM[0][0] is 0x001160

The address of pM[0][1] is 0x001168

The address of pM[0][2] is 0x001170

The value of pM[1] is 0x001180

The address of pM[1][0] is 0x001180

The address of pM[1][1] is 0x001188

The address of pM[1][2] is 0x001190

代码列表 3.4 显示了一个 2x3 的双精度变量矩阵。这是通过获取一个可以存储即接收指向双精度浮点数指针内存地址的指针实现的。第一个循环为矩阵的两行中的每一行执行了内存分配。我们程序产生的输出确认了上述图中指示的内容：`pM` 指向即持有指针 `M[0]` 的地址，而 `M[0]` 又指向 `M[0]`，以此此类推。具体来说，第二个 `for` 循环证明了内存是行与行连续布局的。通常情况下，由于行与行之间的内存块之间存在间隙，我们的数组中的内存位置并不是连续的或无法保证连续。事实上，在 `pM[0]` 内存块与从 `pM[1]` 开始的内存块之间似乎存在间隙。实际上，这是 C++ 的一个特性，它始终为指针提供一个一次到最后的内存块。这块额外的内存可以被指向但不能被延迟。代码列表 3.4 证明了以指针指针格式存储的数据可以像任何其他数组一样进行操作。要为指针 `pM` 的第 `i, j` 个内存位置赋值，请使用 `pM[i][j]` 语法。列表中的最后一个循环演示了如何释放指针指针存储的内存。这种情况在技术上是不必要的，因为所有内会在程序终止时自动释放。但通常情况下，可能存在许多位于 `main` 调用的其他函数之外的情况。

如果 C++ 语言只允许将源代码放在 `main` 函数体内，限制将会很大。我们从第 2 章知道情况并非如此，在程序中包含其他函数是可能的。为了实现这一点，必须在 `main` 代码之前提供函数的原型或定义。这可以通过将原型放在与 `main` 相同的文件中，或者通过使用 `#include` 指令来实现。我们目前关注第一种方案。函数的通用结构如下：

```cpp
returnType functionName(arguments){
    body of function
    return statement
}
```

在这里，`returnType` 可以是任何基本数据类型。`return` 语句中的值必须与 `returnType` 的类型相同。下面的代码列表是一个简单的程序，它可以在 `main` 体内调用一个平方函数，对通过 2.3 节引入的输入流 `cin` 从 shell 界面提供的某些数值进行平方。

代码列表 3.5 square.cpp

```cpp
//square.cpp
#include <iostream>

using namespace std;

double square(double x);

int main() {
    double x;
    cout << "Enter a number ";
    cin >> x;
    cout << square(x) << endl;
    return 0;
}

double square(double x) {
    return x*x;
}
```

注意在 `main` 中使用之前为 `square` 提供的原型。如果没有这样做，并且没有在 `main` 之前给出 `square` 的定义，将生成类似下面的编译器错误：

```
square.cpp: In function int main() {
square.cpp:10: error: 'square' was not declared in this scope
```

编译 ` -Wall square.cpp` 会产生，例如：

```bash
$ g++ -Wall square.cpp -o square
./square
Enter a number 4
16
./square
Enter a number 1.278
1.63328
```

# 函数

它的名称本身就带有解引用的意思。输出的最后两行是通过将 `k` 和 `j` 交换到等号的左右两侧的，结果现在 `i` 的值发生了变化，但内存位置没有改变。

C++ 的另一个很有用特性是它允许函数重载。这意味着，只要参数类型不同，就允许两个或多个函数具有相同的名称。下面的代码通过对平方计算程序的修改说明了这一点。

```cpp
//squareOverload.cpp
#include <iostream>

using namespace std;

double square(double x);
int square(int x);

int main(){
    double x;
    cout << "Enter a number ";
    cin >> x;
    cout << square(x) << endl;
    int y;
    cout << "Enter an integer ";
    cin >> y;
    cout << square(y) << endl;
    return 0;
}

double square(double x){
    cout << "From double version" << endl;
    return x*x;
}

int square(int x){
    cout << "From int version" << endl;
    return x*x;
}
```

下面程序的输出验证了正在调用适当的 `square` 版本来处理 `double` 和 `int` 参数类型的情况。

```bash
$ g++ -Wall squareOverloaded.cpp -o squareOverloaded
$ ./squareOverloaded
Enter a number 12.9
From double version
166.41
Enter an integer 12
From int version
144
```

> 注意，在重载函数时，只有参数类型的差异是重要的。返回类型的差异将会被报告为编译错误。特别是，像这样的函数：

```cpp
int square(double x){
    return (int)(x*x);
```

在我们的平方程序中使用它，虽然在概念上可能是合理的，但会产生错误，编译器会我们这个函数歧义了第一个具有 double 参数和返回类型的 `square` 函数。

# C++ 概述

## 3.7 类、对象和方法

C++ 相对于 C 的强大之处在于它在定义新的用户创建的数据类型方面的灵活性。在某种程度上，这种功能在 C 中已经通过创建数据结构或结构体 `struct` 而存在。基本上，结构体是各种数据类型的聚合，可以包含数组、字符、整数等的混合体。结构体的组件被称为

C++ 通过允许数据结构包含函数或方法来泛化了结构体概念，因为这些方法在这些语境下通常是这样使用的。这种泛化被称为类 `class`，正如第 1 章所述，类的特定实例被称为对象 `objects`。

为了在 C++ 中定义类，我们使用通用类的语法框架：

```cpp
class className {
private:
    成员的声明，方法原型/定义
public:
    成员的声明，方法原型/定义
};
```

注意注意 `};` 必须出现在类定义的末尾。`public` 和 `private` 关键字决定了类和函数如何访问类成员。基本上，私有成员和方法供类内部使用，除某些特殊情况外，不能被其他类或函数访问或使用。特别是，类方法可以访问并更改其所属类的私有成员，但不能访问另一个类的成员。除非在类声明中通过将它们放在 `public:` 行之后进行显式指定，否则方法和类成员均被视为私有。因此，没有必要显式地使用 `private:` 语句。

澄清和简化类概念最简单的方法是通过示例。下面的代码列表扩展了我们的 `square.cpp` 程序，以计算给定双精度的整数幂。与我们之前的做法不同，现在的实现通过创建类 `Power` 使用了面向对象编程 OOP 方法。

# 列表 3.6 power.cpp

```cpp
//power.cpp
#include <iostream>

using namespace std;

class Power{
    int k;//integer
public:
    Power(int k);
    double xToK(double x);
};

Power::Power(int k){
    if(k >= 1)
        k = k;
    else
        cout << "The power must be an integer >= 1!" << endl;
}
```

```cpp
double Power::xToK(double x){
    double y = 1;
    for(int i = 1; i <= k; i++)
        y = x*y;
    return y;
}

int main(){
    int k;
    double x;
    cout << "Enter an integer power ";
    cin >> k;
    Power* p = new Power(k);
    cout << "Enter a number to raise to this power ";
    cin >> x;
    cout << p->xToK(x) << endl;
    cout << "Enter another number to raise to this power ";
    cin >> x;
    cout << p->xToK(x) << endl;
    delete p;
    return 0;
}
```

列表 3.6 带来了一个类的原型描述，其性质与我们在列表 3.5 中为函数 `square` 所做的相似。如果它提供了足够的信息让程序员使用该类及其方法而无需看到类实现的实际细节，这也被称为类接口 class interface。成员函数的详细定义在这些原型之外，通过使用类名结合作用域运算符 `::` 提供。`double` 的 `k` 次幂是通过使用成员函数迭代计算的。通常，要使用指针调用类方法，我们使用 `p->method()` 语法，这在第 36 和 39 行所示。

# 类、对象与方法

`include` 指令。在第 2 章中我们讨论了头文件，它是实现 C++ 标准库各个部分的手段。我们将对这部分进行扩展，即创建我们自己的头文件，以便其他程序能够访问我们为各种目的而创建的代码。

基本上，一个类的头文件应该由该类的原型或声明组成。因此，对于 `Power` 类，头文件的构建基本上是使用 `Power.cpp` 列表中第 6 到 12 行的内容完成的。这里关于包含保护 include guards 有一个细微的注意事项，在给出头文件的具体代码列表之前，我们需要先处理这个问题。

头文件提供了类与其他使用该类的程序之间的连接介质，它们被包含在任何使用了类成员的程序中。因此，当多个程序组合在一起时，某个头文件在最终编译过程中可能会被包含多次。编译器会将此视为类的重复定义，并标记为错误。包含保护提供了一种避免此类问题的方法。其步骤是：使用预处理器在第一次遇到头文件时条件性地定义一个变量。一旦定义，预处理器如果通过任何其他程序的 `include` 指令再次遇到该头文件，将会忽略它。

下面给出了一个带有包含保护的 `Power` 类头文件列表。当预处理器第一次遇到该头文件时，变量 `POWER_H` 被定义，文件中的代码被处理。后续任何其他包含该头文件的请求将使 `#ifndef POWER_H` 结果为 `false`，文件的其余部分将被忽略。

```cpp
//Class.h
#ifndef POWER_H
#define POWER_H

class Power{
    int K;//整数幂次

public:
    Power() : K(1);//默认构造函数
    Power(int k) : K(k); 
    double xToTheK(double x);
};
#endif
```

除了包含保护之外，我们还通过在头文件中提供默认构造函数的定义不仅仅是声明将其内联 inline。在类声明内部定义的任何函数自动都是内联的，其效果是编译器会在原地展开它即直接使用函数体，而不是通过函数调用。对于小型函数，这可以提高程序的运行速度。

`Power` 类成员函数的定义现在放在一个单独的文件 `powerClass.cpp` 中，其内容如下：

```cpp
//powerClass.cpp
#include <iostream>
#include "PowerClass.h"

using namespace std;

Power::Power(int k){
    if(k != 1)
        K = k;
    else
        cout << "The power must be an integer >= 1!" << endl;
}
```

# 58 C++ 概览

```cpp
double Power::xToTheK(double x){
  double y = 1;
  for(int i = 1; i <= K; i++)
    y = x*y;
  return y;
}
```

注意，这里使用了 `include` 指令来引入包含在 `Class.h` 中的 `Power` 类原型。使用引号 `"" 而不是 `< >` 告诉预处理器开始从当前目录查找头文件。

最后，是一个实际使用 `Power`类的程序：

```cpp
//powerClassDriver.cpp
#include <iostream>
#include "powerClass.h"

using namespace std;

int main(){
  int k;
  double x;
  cout << "Enter an integer power ";
  cin >> k;
  Power powObj(k);
  cout << "Enter a number to raise to this power ";
  cin >> x;
  cout << powObj.xToTheK(x) << endl;
  return 0;
}
```

观察发现，`Power` 类的头文件已包含在此驱动程序中，并且现在正在使用一个 `Power` 对象。

# 杂题

因此，该对象感知到自己的内存位置，以及何时或何可以直接访问该信息。这在分配类型操作符例如 `=`, `+=` 等时特别有用，这些运算符在对象使用动态分配内存时可以正常工作。我们将在下一节中探讨这一特定问题。现在，让我们集中在理解简单设置下此指针的属性。

列表 3.8 对此指针进行了一些实验。

列表 3.8 thisEx.cpp

```cpp
//thisEx.cpp
#include <iostream>

using namespace std;
class X{
public:
    int K;
    X();
    X(int k){K = k;}
    X* getThis() {return this;}
    X& getThisRef(){return *this;}
};
int main(){
    X w(0);
    cout << "w address = " << &w << endl;
    cout << "w value = " << w.K << endl;

    X* x = w.getThis();
    cout << "x value = " << x->K << endl;
    x->K = 1;
    cout << "w.K = " << w.K << endl;

    X& y = w.getThisRef();
    cout << "y address = " << &y << y.K << endl;
    y.K += 1;
    cout << "w.K = " << w.K << endl;

    X z = *w.getThis();
    cout << "z address = " << &z << endl;
    z.K = 1;
    cout << "w.K = " << w.K << endl;
    return 0;
}
```

创建了一个具有一个公共成员 K 和两个方法的简单类。其中一个类方法 `getThis` 返回此指针的值，而另一个方法 `getThisRef` 返回一个从类 X 构造的对象的引用。由于返回引用的方式，引用方法的语法有点微妙。这是一个指向对象地址的指针，这一事实意味着解引用后的指针 `*this` 就是对象本身。因此，为了返回一个对象的引用，我们对 `*this` 进行解引用，而函数的返回类型即 `&X` 规定了引用的地址是 `*this` 的地址：即 `this` 的值。
