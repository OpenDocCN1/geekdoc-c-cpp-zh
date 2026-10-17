
```cpp
return *this;
}

Vector Vector::operator-(const Vector& v) const {
    if(nRows != v.nRows)
        cout << "Bad row dimensions in -!" << endl;
        exit(1);
    Vector temp(nRows);
    for(int i = 0; i < nRows; i++)
    temp.pA[i] = this->pa[i] - v.pa[i];
    return temp;
}

Vector& Vector::operator-=(const Vector& v) {
    if(nRows != v.nRows)
        cout << "Bad row dimensions in -=!" << endl;
        exit(1);
    for(int i = 0; i < nRows; i++)
    pa[i] -= v.pa[i];
    return *this;
}

Vector Vector::operator*(double b) const {
    Vector temp(nRows);
    for(int i = 0; i < nRows; i++)
    temp.pA[i] = b*pa[i];
    return temp;
}

double Vector::operator[](int i) const {
    return pa[i];
}
```

```cpp
void Vector::printVec() const {
  for(int i = 0; i < nRows; i++)
    cout << pA[i] << " " << endl;
}

Vector operator*(double b, const Vector& v){
  Vector B = v;
  return B*b;
}
```

# 附录 E

## ranGen 类

本附录提供了在第 8 章及其他地方使用的 `ranGen` 类“完整”版本。我们从下面的头文件开始。

### 列表 E.1 ranGen.h

```cpp
//ranGen.h
#ifndef RANGEN_H
#define RANGEN_H

enum unType {FM2, WH};
enum normType {BM, C};

class ranGen {
    unType T;
    normType NT;
    unsigned long seed1, seed2, seed3;
    double gCauchy(double x) const;
    double gInvCauchy(double u) const;
    double fNorm(double x) const;
public:
    ranGen(unType t = WH, normType nt = BM) : T(t), NT(nt) {}
    ~ranGen();
    void ranUnif(int n, double* pu);
    void ranNorm(int n, double* pNorm, double mu = 0,
        double sig = 1);
    void setSeed(unsigned long si);
};

#endif
```

有两种类型的均匀随机数生成器：Fishman-Moore II `FM2` 生成器和 Wichmann-Hill `WH` 生成器。它们被封装在 `ranUnif` 方法中。在 `ranNorm` 方法中，提供了柯西接受法 `C` 和 Box-Muller `BM` 方法作为生成随机数的选项。不同算法的选择通过指定符号常量 `FM2`、`WH` 和 `C` 完成，这些常量是使用 `enum` 枚举语句定义的。均匀分布生成器和正态分布生成器类型的默认选项 `WH` 和 `BM` 在类构造函数中设置。`ranNorm` 允许指定分布的均值和标准差，其默认值可产生正态分布。

其他类成员是三个用于生成器的无符号长型种子。这些值由用户通过仅接受一个 `unsigned long` 参数的公共 `setSeed` 方法设置。然后通过 FM2 生成器的整数形式为 WH 生成器设置另外两个种子。

方法的定义在接下来的列表中给出。

### 列表 E.2 ranGen.cpp

```cpp
//ranGen.cpp
#include "ranGen.h"
#include <iostream>
#include <cmath>

//匿名命名空间
namespace i {
    double pi = 2.**acos(0);
    double sqrtpi = sqrt(2.*pi);
    unsigned long a1 = 171, m1 = 30269, a2 = 172, m2 = 30307,
    a3 = 170, m3 = 30323, m4 = 2147483647, a5 = 630600616;
}

void ranUnif(int n, double* pu) {
    if (T == WH) {
        double temp = 0;
        for (int i=0; i<n; i++) {
            seed1=(a1*seed1)%m1;
            seed2=(a2*seed2)%m2;
            seed3=(a3*seed3)%m3;
            temp = ((double)seed1)/((double)m1) + ((double)seed2)/((double)m2)
                + ((double)seed3)/((double)m3);
            if(temp > 2.)
                if(temp > 1.) temp -= 1.
            pu[i] = temp;
        }
    } else {
        for (int i=0; i<n; i++) {
            seed1=(a4*seed1)%m4;
            pu[i]=((double)seed1)/((double)m4);
        }
    }
}

void ranNorm(int n, double* pNorm, double* mu) {
    double sig = 0;
    int nFill = 0, iAccept = 0, nReject = 0;
    if (NT != BM) {
        double spare = 0, mult = 0, Rsq = 0;
        while(nFill<n) {
            if(iAccept) { // 如果我们还有一个剩余，现在使用它
                pNorm[nFill] = spare;
                iAccept = 0;//下一次我们需要生成另一对
                nFill += 1;
            } else while(iAccept == 0){
                // 在 [-1, 1] 上生成两个均匀分布数
                ranUnif(2,pu);
                pu[0] = 2*pu[0] - 1;
                pu[1] = 2*pu[1] - 1;
                Rsq = pu[0]*pu[0] + pu[1]*pu[1];
                if(Rsq <= 1 && Rsq != 0){ // 接受结果
                    mult = sqrt(-2.*log(Rsq)/Rsq);
                    pNorm[nFill] = mu + sig*pu[0]*mult;
                    spare = mu + sig*pu[1]*mult;//将这个留到下一次
                    nFill += 1;
                }
            }
        }
    }
}
```

### RANGEN 类逻辑

（注：此处为代码片段的逻辑翻译说明，保持代码结构不变）

```cpp
// ... 内部逻辑 ...
```

```cpp
void ranGen::setSeed(unsigned long si) {
    if (T == WH){
        seed1 = si;
        seed2=(a4*seed1)%m4;
        seed3=(a5*seed2)%m3;
    } else
        seed1 = si;
}
```
