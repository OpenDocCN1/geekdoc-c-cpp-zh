

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

在我们的平方程序中使用它，虽然在概念上可能是合理的，但会产生错误，编译器会我们这个函数“歧义”了第一个具有 double 参数和返回类型的 `square` 函数。

# C++ 概述

## 3.7 类、对象和方法

C++ 相对于 C 的强大之处在于它在定义新的用户创建的数据类型方面的灵活性。在某种程度上，这种功能在 C 中已经通过创建数据结构或结构体（struct）而存在。基本上，结构体是各种数据类型的聚合，可以包含数组、字符、整数等的混合体。结构体的组件被称为

C++ 通过允许数据结构包含函数或方法来泛化了结构体概念，因为这些方法在这些语境下通常是这样使用的。这种泛化被称为类（class），正如第 1 章所述，类的特定实例被称为对象（objects）。

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

澄清和简化类概念最简单的方法是通过示例。下面的代码列表扩展了我们的 `square.cpp` 程序，以计算给定双精度的整数幂。与我们之前的做法不同，现在的实现通过创建类 `Power` 使用了面向对象编程（OOP）的方法。

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

列表 3.6 带来了一个类的原型描述，其性质与我们在列表 3.5 中为函数 `square` 所做的相似。如果它提供了足够的信息让程序员使用该类及其方法而无需看到类实现的实际细节，这也被称为类接口（class interface）。成员函数的详细定义在这些原型之外，通过使用类名结合作用域运算符 `::` 提供。`double` 的 `k` 次幂是通过使用成员函数迭代计算的。通常，要使用指针调用类方法，我们使用 `p->method()` 语法，这在第 36 和 39 行所示。

