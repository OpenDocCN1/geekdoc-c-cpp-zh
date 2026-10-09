
```cpp
// 使用不动点迭代法求解方程的
// 函数：
double findRoot(double (*f)(double), double x0, int n) {
    // 方程根的初始近似值：
    double x=x0;
    // 进行迭代：
    for(int k=1; k<=n; k++) {
        x=f(x);
    }
    // 函数的返回值：
    return x;
}

// 这些函数决定了方程：
double f(double x) {
    return 0.5*cos(x);
}
double g(double x) {
    return exp(-x);
}
double h(double x) {
    return (x*x+6)/5;
}
// 用于求解方程
// 并测试根的函数：
void test(double (*f)(double), double x0, string eq) {
    // 迭代次数：
    int n=100;
    // 用于保存方程根的变量：
    double z;
    cout << "The root of the equation " << eq << ":\t";
    // 找到方程的根：
    z=findRoot(f,x0,n);
    // 输出结果：
    cout<<z<<endl;
    cout<<"Testing the root:\t"; // 测试根：
    cout<<z << " = " << f(z)<<endl;
    for (int k=1; k<=50; k++) {
        cout<<"-";
    }
    cout<<endl;
}

// 程序的主函数：
int main() {
    // 求解方程：
    test(f,0,"x=0.5cos(x)");
    test(g,0,"x=exp(-x)");
    test(h,1,"x=(x*x+6)/5");
    return 0;
}
```

# 第9章 数学问题

这里是程序的输出：

程序的输出（见列表 9.1）

方程 x=0.5cos(x) 的根: 0.450184

测试根: 0.450184 = 0.450184

方程 x=exp(-x) 的根: 0.567143

测试根: 0.567143 = 0.567143

方程 x=(x*x+6)/5 的根: 2

测试根: 2 = 2

为了求解方程，我们在程序中描述了 `findRoot()` 函数。该函数的第一个参数是一个指向确定要解方程的函数指针。该函数必须有一个类型为 `double` 的参数，并且必须返回 `double` 类型。`findRoot()` 函数的第二个参数决定了方程根的初始近似值。第三个参数定义了计算根时执行的迭代次数。

我们在程序中解了三个方程。这些方程由函数 `f()`、`g()` 和 `h()` 决定。我们将这些函数名作为第一个参数传递给函数 `findRoot()`。`findRoot()` 函数本身在 `test()` 函数中被调用。

找到方程的根后，我们会测试它的正确性。为此，我们打印计算出的根 `x`，然后打印在根点确定方程的函数值 `q(x)`。理想情况下，这些值应该是相等的。

> 注意：
>
> 这里我们不考虑可以使用不动点迭代法求解方程的条件。

## 二分法

二分法用于求解形式为 $f(x) = 0$ 的代数方程。如果已知根局限于某个区间 $a \le x \le b$ 内，且函数 $f(x)$ 在区间边界处的符号不同（这意味着 $f(a)f(b) < 0$），我们就可以应用该方法。

算法如下：我们在区间的中心点 $x = (a+b)/2$ 处计算函数 $f(x)$。然后找到函数值与中心点符号相同的边界。将边界移动到区间的中心。结果是搜索根的区间缩短了一倍，且函数 $f(x)$ 在新区间边界处的符号不同。因此，我们的情况与最初几乎相同，但根的定位区间缩短了一倍。

列表 9.2 包含了通过二分法求解方程的程序。

## 列表 9.2. 二分法

```cpp
#include <iostream>
#include <cmath>
#include <string>
using namespace std;
// 使用二分法
// 求解方程的函数：
double findRoot(double (*f)(double),double a,
double b, double dx) {
    // 用于保存根的变量：
    double x=(a+b)/2;
    // 计算根：
    while((b-a)/2>dx) {
        // 如果根在左边界：
        if (f(a)==0) {
            return a;
        }
        // 如果根在右边界：
        if (f(b)==0) {
            return b;
        }
        // 如果：
        if (f(a)*f(x)<0) {
            // 将边界移动到区间的中心：
            a=x;
        } else {
            b=x;
        }
        // 计算新的点：
        x=(a+b)/2;
    }
// 函数的返回值：
    return x;
}
// 决定方程的函数：
double f(double x) {
  return 0.5*cos(x);
}
double g(double x) {
  return exp(-x);
}
double h(double x) {
  return (x*x+6)/5;
}
// 求解方程
// 并测试根的函数：
void test(double (*f)(double), double x0, string eq) {
  // 捕获异常：
  try {
    // 用于保存根的变量：
    double z;
    cout << "The root of the equation " << eq << ":\t";
    // 找到方程的根：
    z=findRoot(f,x0,n); 
    // 输出结果：
    cout<<z<<endl;
    cout<<"Testing the root:\t"; // 测试根：
    cout<<z << " = " << f(z)<<endl;
  } catch (const char* e) {
    // 输出错误：
    cout<<e<<endl;
  }
}
```
