
```cpp
#include <iostream>
using namespace std;
// 基类：
template<class X> class BaseClass{
private:
    // 字段：
    X value;
public:
    // 构造函数：
    BaseClass(X val) {
        set(val);
    }
    // 方法为字段赋值：
    void set(X val) {
        value=val;
    }
    // 方法获取字段值：
    X get() {
        return value;
    }
};
// 第一个派生类：
class Alpha : public BaseClass<int>{
public:
    // 构造函数：
    Alpha():BaseClass<int>(0) {}
};
// 第二个派生类：
classclass Bravo : public BaseClass<char>{
public:
    // 构造函数：
    Bravo(char s):BaseClass<char>(s) {}
};
// 程序的 main 函数：
int main() {
    // 第一个派生类对象：
    Alpha objA;
    // 与对象进行操作：
    cout<<"The object objA: "<<objA.get()<<endl;
    objA.set(100);
    cout<<"The object objA: "<<objA.get()<<endl;
    // 第二个派生类对象：
    Bravo objB('A');
    // 与对象进行操作：
    cout<<"The object objB: "<<objB.get()<<endl;
    objB.set('B');
    cout<<"The object objB: "<<objB.get()<<endl;
    return 0;
}
```

程序的输出如下：

| 输出 |
| :--- |
| 对象 objA: 0 |
| 对象 objA: 100 |
| 对象 objB: A |
| 对象 objB: B |

我们描述带有模板参数 `X` 的模板类 `BaseClass`。该类有一个类型为 `X` 的私有字段 `value`。公共方法 `set()` 为字段赋值，公共方法 `get()` 返回字段的值。该类还包含一个带有单个参数的构造函数。传递给构造函数的值决定了字段 `value` 的值。在这种情况下，我们调用 `set()` 方法。

`Alpha` 和 `Bravo` 类继承自 `BaseClass`。当我们创建 `Alpha` 类时，使用 `int` 类型作为 `BaseClass` 的模板参数。对于 `Bravo` 类，我们使用 `char` 类型作为 `BaseClass` 的模板参数。`Alpha` 和 `Bravo` 类都有构造函数。对于 `Alpha` 类，它的构造函数调用了带有零值的 `BaseClass<int>` 类构造函数。`Bravo` 类构造函数调用了带有字符参数的 `BaseClass<char>` 类构造函数。在 `main()` 函数中，我们创建并使用了 `Alpha` 和 `Bravo` 类的对象。

# 整数模板参数

模板类中的参数作为类型标识符的表示。模板类可以使用整数模板参数。我们以描述标准模板参数的方式描述这些参数。接下来，我们考虑一个示例。在程序12中，我们创建了模板类 `Polynomial`。我们需要这个类来实现多项式并对它们进行某些操作（例如，多项式的乘法、加法、减法以及计算导数）。

## 细节

| 描述 |
| :--- |
| 为了理解程序的组织原理，我们需要回顾多项式这类数学对象的特征。 |
| $n$ 次多项式是形式为 $P_n(x) = a_0 + a_1x + a_2x^2 + \dots + a_nx^n$ 的函数依赖。 |
| 多项式的系数个数比多项式的次数多1。 |
| 多项式在点 $x$ 的值由和 $a_0 + a_1x + a_2x^2 + \dots$ 给出。 |
| 项式 $P_n(x)$ 的导数 $P'_n(x)$ 是 $n-1$ 次多项式，由表达式 $P'_n(x) = a_1 + 2a_2x + 3a_3x^2 + \dots + na_{n-1}x^{n-1}$ 决定。 |
| 如果我们将多项式乘以一个数字 ($k$)，得到一个新的多项式，其系数乘以该数字：$kP_n(x) = ka_0 + ka_1x + ka_2x^2 + \dots + ka_nx^n$。 |
| 当计算多项式的和（或差）时，我们应该加上（或减去）相同索引系数（对应于参数 $x$ 的相同幂）。 |

程序最重要的部分是模板类 `Polynomial`。模板参数决定了类对象所实现的多项式的次数。我们还在类中同时使用了普通方法和运算符方法。同样，我们在程序中使用了模板运算符函数。现在，让我们考虑这个程序。

# 列表 7.12. 整数模板参数

```cpp
#include <iostream>
using namespace std;
// 用于实现多项式的模板类
template<int power> class Polynomial{
private:
    // 私有字段是一个带有系数的数组。
    // 数组的大小比多项式的次数大 1：
    double a[power+1];
public:
    // 无参数构造函数：
    Polynomial() {
        // 填充数组：
        for(int k=0;k<=power;k++) {
            a[k]=0;
        }
    }
    // 带有一个参数的构造函数：
    Polynomial(double* nums) {
        // 拷贝：
        for(int k=0;k<=power;k++) {
        }
    }
};
```

# 第 7 章

## 模板函数与类

```cpp
a[k]=nums[k];
}
}
// 该方法打印数组的元素：
void getAll() {
  cout<<"| "";
  for(int k=0;k<power;k++) {
    cout<<a[k]<<" | "";
  }
  cout<<endl;
}
// 用于调用对象的运算符方法：
double operator() (double x) {
  double s=0,q=1;
  for(int k=0;k<power;k++) {
    s+=a[k]*q;
    q*=x;
  }
  return s;
}
// 用于对象索引的运算符方法：
double &operator[] (int k) {
  return a[k];
}
// 用于计算多项式
// 积的模板运算符方法：
template<int n> Polym<power+n>
operator*(Pol<n> pol) {
  // 模板类的局部对象：
  Pol<power+n> tmp;
  // 计算多项式的系数
  // 也就是乘积的结果：
for(int i=0;i<=power;i++) {
    for(int j=0;j<n;j++) {
        tmp[i+j]+=a[i]*pol[j];
    }
  }

  // 方法的结果：
  return tmp;
}

// 用于计算多项式
// 和的模板运算符方法：
template<int n> Polynomial<power>n?n:power>
operator+(Polynomial<n> pol) {
    int i;
    // 模板类的局部对象：
    Polynomial<power>n?n:power> tmp;
    // 计算多项式的系数
    // 也就是方法的结果：
    for(i=0;i<=power;i++) {
        tmp[i]+=a[i];
    }
    for(i=0;i<=n;i++) {
        tmp[i]+=pol[i];
    }
    // 方法的结果：
    return tmp;
}

// 用于计算数字与多项式
// 相乘结果的模板运算符函数：
template<int power> Polynomial<power>
operator*( Polygon<power> pol, double r) {
  // 模板类的局部对象：
  Polygon<power> tmp;
  // 计算多项式的系数，
  // 也就是函数的结果：
  for(int k=0; k<=power; k++) {
    tmp[k]=pol[k]*r;
  }
  // 函数的结果
  return tmp;
}

// 用于计算数字与多项式
// 相乘结果的模板运算符函数：
template<int power> Polygon<power>
operator*(double r, Polygon<power> pol) {
  // 将多项式乘以数字：
  return pol*r;
}

// 用于计算两个多项式差的模板运算符函数：
template<int m, int n> Polygon<(m>n?m:n)>
operator-(Polygon<m> x, Polygon<n> y) {
  // 将第一个多项式加上
  // 乘以 -1 的第二个多项式：
  return x+(-1)*y;
}

// 用于计算多项式导数的模板函数：
template<int power> Polygon<power-1>
Diff(Polygon<power> pol) {
  // 模板类的局部对象：
  Polygon<power-1> tmp;
  // 计算多项式的系数，
  // 也就是函数的结果：
  for(int k=0;k<=power-1;k++) {
    tmp[k]=pol[k+1]*(k+1);
  }

  // 函数的结果
  return tmp;
}

// 程序的主函数：
int main() {
    // 带有系数的数组：
    double A[]={1,2,-1,1};
    double B[]={1,3,0,2,-1,1};
    // 多项式的参数
    double x=2;
    // 第一个多项式
    Polynom<3> P(A);
    cout<<"The polynomial P:\t";
    // 第一个多项式的系数：
    P.getAll();
    cout<<"The value P("<<x<<") = " << "";
    // 第一个多项式在点处的值：
    cout<<P(x)<<endl;
    cout<<"The polynomial P':\t";
    // 多项式导数的
    // 系数：
    Diff(P).getAll();
    cout<<"The value P('<<x<<") = " << "";
    // 导数在点处的值：
    cout<<Diff(P)(x)<<endl;
    // 第二个多项式：
    Polynom<5> Q(B);
    cout<<"The polynomial Q:\t";
    // 第二个多项式的系数：
    Q.getAll();
    cout<<"The value Q("<<x<<") = " << "";

    // 第二个多项式在点处的值：
    cout<<Q(x)<<endl;

    cout<<"The polynomial P*Q:\t";
    // 多项式乘积的
    // 系数：
    (P*Q).getAll();
    cout<<"The value (P*Q)("<<x<<") = " << "";

    // 多项式乘积在
    // 点处的值：
    cout<<(P*Q) (x)<<endl;

    cout<<"The polynomial P+Q:\t";
    // 多项式和的系数：
    (P+Q).getAll();
    cout<<"The value (P+Q)("<<x<<") = " << "";

    // 多项式和在点处的值：
    cout<<(P+Q) (x)<<endl;

    cout<<"The polynomial Q-P:\t";
    // 多项式差的系数：
    (Q-P).getAll();
    cout<<"The value (Q-P)("<<x<<") = " << "";

    // 多项式差在
    // 点处的值：
    cout<<(Q-P) (x)<<endl;

    return 0;
}
```

# 注意

在程序中，我们使用了填充法（tabulation）。

我们从程序的程序的输出：

| 描述 | 输出 |
| :--- | :--- |
| The polynomial P: | \| 1 | 2 | -1 | 1 | |
| The value P(2) = | 1 |
| The polynomial P': | \| 2 | -2 | -2 | |
| The value P'(2) = | -6 |
| The polynomial Q: | \| 1 | 3 | 0 | 2 | -1 | 1 | |
| The value Q(2) = | 7 |
| The polynomial P*Q: | \| 1 | 5 | 5 | 3 | -3 | 1 | |
| The value (P*Q)(2) = | 25 |
| The polynomial P+Q: | \| 2 | 5 | -1 | 3 | -1 | 1 | |
| The value (P+Q)(2) = | 11 |
| The polynomial Q-P: | \| 0 | 2 | 1 | 1 | -1 | 1 | |
| The value (Q-P)(2) = | 5 |

幂。因此，我们比较了幂和 n。较大者决定了生成的多项式的幂次。

在该方法中，语句 `Polynomial<n>power?:n:power>` 创建了一个局部对象。对于对象 `tmp`，系数的初始值为零。我们将它们累加到对象 `pol`（该方法的参数）的相应系数以及数组 `a` 的元素上。为了实现这一操作，我们使用了两个循环语句。在我们“填充”对象 `tmp` 之后，我们将其作为方法的的结果返回。

除了 `Polynomial` 类之外，我们还在程序中描述了几个模板函数。模板函数 `operator*()` 处理了多项式与一个数字的乘法运算。该函数返回一个 `Polynomial<power>` 类的对象，其中 `power` 是模板函数的参数。该运算符函数有两个参数。第一个参数 `pol` 是 `Polynomial<power>` 类的对象。第二个参数 `r` 是一个 `double` 类型的数字。在函数内部，语句 `Polynomial<power> tmp` 创建了一个局部对象。为了计算系数，我们使用一个循环语句。语句 `tmp[k]=pol[k]*r` 为索引为 `k` 的系数赋一个值。该值是系数 `pol[k]` 与数字 `r` 的乘积。系数计算完成后，我们返回对象 `tmp` 作为函数的结果。

值得一提的是，此函数处理了我们用一个对象（多项式）乘以一个数字的情况。如果我们想用数字乘以对象，就必须创建运算符函数的另一个版本。我们确实这么做了。这个版本的函数与第一个区别在于参数的顺序（现在第一个参数是数字 `r`，第二个参数是对象 `pol`）。为了避免程序代码的重复，我们在函数使用了表达式 `return pol*r`。换句话说，我们通过调用将对象乘以数字的函数，计算出了处理数字乘以对象的这一函数的结果。

**我们在模板运算符函数 `operator-()` 中也使用了类似的技巧，该函数计算两个对象（多项式）之间的差。

## 细节 (Details)

我们按照如下方式计算多项式 $Q_m(x)$ 和 $P_n(x)$ 的差。我们将多项式 $P_n(x)$ 乘以 $-1$，并将其加到多项式 $Q_m(x)$ 上。换句话说，我们使用了等式 $Q_m(x) - P_n(x) = Q_m(x) + (-1)P_n(x)$。

该函数有两个整数模板参数 $m$ 和 $n$（多项式的幂次）。它返回一个 `Polynomial<m>n>` 类的对象（生成的多项式的幂次是 $m$ 和 $n$ 中的最大值）。函数的参数 **x** 和 **y** 分别是 `Polynomial<m>` 和 `Polynomial<n>` 类的对象。函数的结果通过表达式 `x+(-1)*y` 计算。在这里，我们将对象乘以数字并将对象相加。我们之前已经定义了这些操作。

带有模板整数参数 `power`（多项式的幂次）的模板函数 `Diff()` 从多项式计算导数。它返回一个 `Polynomial<power-1>` 类的对象。在这里我们考虑到导数多项式的幂次比求导多项式的幂次小1。参数 `pol`（求导的多项式）是 `Polynomial<power>` 类的对象。在函数中，我们创建了 `Polynomial<power-1>` 类的局部对象 `tmp`。我们通过循环语句计算对象的系数。之后，函数返回对象 `tmp` 作为结果。

在程序的主函数中，我们声明并初始化了两个数值数组 `A` 和 `B`。语句 `Polynomial<3> P(A)` 和 `Polynom<5> Q(B)` 创建了对象，我们将它们等同于多项式。我们对这些对象进行乘法、加法、减法运算，并计算了它们的导数。

> 注意 (Notes)

> 在程序的主函数中，我们声明并初始化了两个数值数组 `A` 和 `B`。语句 `Polynomial<3> P(A)` 和 `Polynom<5> Q(B)` 创建了对象，我们将它们等同于多项式。我们对这些对象进行乘法、加法、减法运算，并计算了它们的导数。

# 列表 8.1 使用结构体
