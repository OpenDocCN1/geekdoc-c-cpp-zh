

## 6.13 使用矩阵库进行均值方差分析

让我们现在考虑如何在 C++ 中实现均值方差分析。如使用 Matlab 所示，计算是相对简单的矩阵表达式。要在 C++ 中实现计算，最好的方法是使用线性代数类来处理计算。为了说明目的，我们将展示两个不同矩阵类的用法，Newmat 和 IT++。这些类在附录中有更详细的描述，并附有如何获取和安装它们的参考。

在 C++ 代码 6.1 和 C++ 代码 6.2 中，我们展示了如何使用这两个类进行基本的均值方差计算，计算均值和标准差。请注意矩阵和向量乘法的执行方式与使用 Matlab 相似。还请注意两个类之间的一个重要区别。在 IT++ 中，元素索引从零开始，这是通常的 C++ 方式。因此，在 IT++ 示例中访问元素 tmp(0,0) 时，我们获取的是第一个元素。在 Newmat 中，默认索引从一开始，这是 Matlab 的方式。因此，在 Newmat 示例中访问 tmp(1,1) 时，我们也获取的是第一个元素。这提醒我们要仔细阅读文档，像这样混合使用库时，“偏一”错误是非常常见的情况。

```
#include <cmath>
using namespace std;

#include <itpp/itbase.h>
using namespace itpp;

double mv_calculate_mean(const vec& e, const vec& w){
  vec tmp = e.transpose()*w;
  return tmp(0);
};

double mv_calculate_variance(const mat& V, const vec& w){
  mat tmp = w.transpose()*V*w;
  return tmp(0,0);
};

double mv_calculate_av_stdev(const mat& V, const vec& w){
  double var = mv_calculate_variance(V,w);
  return sqrt(var);
};
```

C++ 代码 6.1：使用 IT++ 进行均值方差计算

### 示例

均值方差计算。

\(\mathbf{e} = \begin{bmatrix} 0.05 \\ 0.1 \end{bmatrix}\)

\(\mathbf{V} = \begin{bmatrix} 1.0 & 0.0 \\ 0.0 & 1.0 \end{bmatrix}\)

计算投资组合的均值、方差和标准差

\(\mathbf{w} = \begin{bmatrix} 0.5 \\ 0.5 \end{bmatrix}\)

```
#include <cmath>
using namespace std;

#include "newmat.h"
using namespace NEWMAT;

double mv_calculate_mean(const Matrix& e, const Matrix& w){
    Matrix tmp = e.t()*w;
    return tmp(1,1);
};

double mv_calculate_variance(const Matrix& V, const Matrix& w){
    Matrix tmp = w.t()*V*w;
    return tmp(1,1);
};

double mv_calculate_std_dev(const Matrix& V, const Matrix& w){
    double var = mv_calculate_variance(V,w);
    return sqrt(var);
};
```

C++ 代码 6.2：使用 Newmat 进行均值方差计算

### C++ 程序：

```
cout << "Simple example of mean variance calculations " << endl;
Matrix e(2,1);
e(1,1)=0.05; e(2,1)=0;
Matrix V(2,2);
V(1,1)=1.0; V(2,1)=0.0;
V(1,2)=0.0; V(2,2)=1.0;
Matrix w(2,1);
w(1,1)=0.5;
w(2,1)=0.5;
cout << " mean " << mv_calculate_mean(e,w) << endl;
cout << " variance " << mv_calculate_variance(V,w) << endl;
cout << " stdev " << mv_calculate_std_dev(V,w) << endl;
```

### C++ 程序输出：

```
Simple example of mean variance calculations
mean 0.075
variance 0.5
stdev 0.707107
```

在 C++ 代码 6.4 和 C++ 代码 6.3 中，我们展示了如何为给定的要求收益率计算均值方差最优投资组合。这是权重没有约束的情况，我们直接使用解析解。

```
#include "newmat.h"
using namespace NEWMAT;
ReturnMatrix mv_calculate_portfolio_given_mean_unconstrained(const Matrix& e,
                                 const Matrix& V,
                                 const double& r){
  int no_assets=nRows();
  Matrix ones = Matrix(no_assets,1); for (int i=0;i<no_assets;++i) ones.element(i,0) = 1;
  Matrix Vinv = V.i(); // inverse of V
  Matrix A = (ones.t()*Vinv*e); double a = A.element(0,0);
  Matrix B = e.t()*Vinv*e; double b = B.element(0,0);
  Matrix C = ones.t()*Vinv*ones; double c = C.element(0,0);
  double d = b*c - a*a;
  Matrix Vinv1=Vinv*ones;
  Matrix Vinve=Vinv*e;
  Matrix g = ((Vinv1*b - Vinve*a)*(1.0/d));
  Matrix h = (Vinv*e - Vinv1*a)*(1.0/d);
  Matrix w = r * g + h*r;
  w.Release();
  return w;
};
```

C++ 代码 6.3：使用 Newmat 计算给定预期收益的无约束前沿投资组合

### 示例

均值方差计算。

\(\mathbf{e} = \left[ \begin{array} { c } { 0.05 } \\ { 0.1 } \\ \end{array} \right]\)

\(\mathbf{V} = \left[ \begin{array} { c c } { 1.0 } & { 0.0 } \\ { 0.0 } & { 1.0 } \\ \end{array} \right]\)

找到收益率为 \(r = 0.075\) 的最优最小方差投资组合。

C++ 程序：

```
cout << "Testing portfolio calculation " << endl;
Matrix e(2,1);
e(1,1)=0.05; e(2,1)=0.1;
Matrix V(2,2);
V(1,1)=1.0; V(2,1)=0.0;
V(1,2)=0.0; V(2,2)=1.0;
double r=0.075;
Matrix w = mv_calculate_portfolio_given_mean_unconstrained(e,V,r);
cout << "suggested portfolio: ";
cout << " w1 = " << w(1) << " w2 = " << w(2,1) << endl;
```

C++ 程序输出：

```
Testing portfolio calculation
suggested portfolio: w1 = 0.5 w2 = 0.5
```

```
#include <itpp/itbase.h>
using namespace itpp;

mat mv_calculate_portfolio_given_mean_unconstrained(const vec& e, 
                                                    const mat& V, 
                                                    const double& r){
    int no_assets=e.size();
    vec one=ones(no_assets);
    mat Vinv = inv(V); // inverse of V
    mat A = e.transpose()*Vinv*e;
    double a = A(0,0);
    mat B = transpose(one)*Vinv*e;
    double b = B(0,0);
    mat C = one.transpose()*Vinv*one;
    double c = C(0,0);
    double d = b*c-a*a;
    mat Vinv1=Vinv*one;
    mat Vinve=Vinv*e;
    mat g = ((Vinv*e - Vinv*one*a)*(1.0/d));
    mat h = ((Vinv*one*b - Vinv*e*a)*(1.0/d));
    mat w = g + h*r;
    return w;
}
```

C++ 代码 6.4：使用 IT++ 计算给定预期收益的无约束前沿投资组合

## 第 7 章

## 期货算法。

### 目录

- 7.1 期货合约定价 . . . . . . . . . . . . . . . . . . . . 81

在此，我们讨论用于估值期货合约的算法。

## 7.1 期货合约定价。

无分红资产的期货价格是该资产当前价格的未来值。

$f_t = e^{r(T-t)}S_t$

```
#include <cmath>
using namespace std;
double futures_price(const double& S,
                     const double& r,       // current price of underlying asset
                     const double& time_to_maturity) { // risk free interest rate
    return exp(r*time_to_maturity)*S;
};
```

C++ 代码 7.1：期货价格

### 示例

设 S = 100，r = 10%。到期时间为半年的合约的期货价格是多少？

C++ 程序：

```
double S=100; double r=0.10; double time=0.5;
cout << " futures price = " << futures_price(S,r, time) << endl;
```

C++ 程序输出：

```
futures price = 105.127
```

## 第 8 章

## 二叉树期权定价

### 目录

| 8.1 期权 | 82 |
| 8.2 定价 | 82 |
| 8.3 多期二叉树定价 | 85 |

## 8.1 期权

期权及其他衍生品定价是现代金融的主要“成功故事”之一。期权是一种衍生证券，该证券的现金流是某些 *其他* 证券价格的函数，通常称为基础证券。看涨期权是一种权利，但不是义务，在一定时间内以特定价格（称为行权价 $K$）购买给定数量的基础证券。看跌期权是一种权利，但不是义务，在一定时间内以商定的行权价 *出售* 给定数量的基础证券。如果期权只能在特定日期（时间间隔为一天）行权（使用），则该期权称为欧洲期权。如果期权可以在直到特定日期的整个时间段内使用，则该期权称为美式期权。

$C_T = \max(0, S_T - K)$
$P_T = \max(0, K - S_T)$

期权定价的挑战在于确定期权权利金 $C_0$（看涨期权价格）和 $P_0$（看跌期权价格）。

## 8.2 定价

所有定价都使用衍生品的现金流是基础证券价格的直接函数这一事实。因此，定价可以相对于基础证券的价格进行 *相对* 定价。要对期权进行定价

