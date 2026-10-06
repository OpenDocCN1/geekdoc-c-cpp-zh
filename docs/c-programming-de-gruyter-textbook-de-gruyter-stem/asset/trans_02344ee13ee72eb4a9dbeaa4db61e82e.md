

## 3 — 3 函数

源代码：

```cpp
//3_2.cpp
#include <iostream>
using namespace std;
double power (double x, int n);

int main()
{
    int i;
    int value = 0;
    char ch;

    cout << "Enter an 8 bit binary number ";
    for (i = 7; i >= 0; i--)
    {
        cin >> ch;
        if (ch == '1')
            value += int(power(2,i));
    }
    cout <<"Decimal value is "<<value<<endl;\n}
}

double power (double x, int n)
{
    double val = 1.0;
    while (n--)
        val *= x;
    return(val);
}
```

运行结果：

| Enter an 8 bit binary number 01101001 |
| Decimal value is 105 |

**示例 3.3：** 编写一个程序使用以下公式计算 $\pi$ 的值。

$\pi = 16 \arctan\left(\frac{1}{5}\right) - 4 \arctan\left(\frac{1}{239}\right)$

使用以下级数来计算数的反正切值：

持续累加直到级数中某一项的绝对值小于 $10^{-15}$。$\pi$ 和 $x$ 的类型均为 double。

$\arctan(x) = x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \dots$

源代码：

```cpp
// 3_3.cpp
#include<iostream>
using namespace std;
int main()
{
    double a, b;
    double arctan(double x);
    a=16.0*arctan(1/5.0);
    b=4.0*arctan(1/239.0);
    //Note：由于整数除法会舍入，
    // 1/5 和 1/239 的值均为 0。
    cout<<"PI="<<a-b<<endl;
}
double arctan(double x)
{
    int i;
    double r, e, f, sqr;
    sqr=x*x;
    r=0;
    e=x;
    i=1;
    while(e/i>1e-15)
    {
        f=e/i;
        r=(i%4==1) ? r+f : r-f;
        e=e*sqr;
        i+=2;
    }
    return r;
}
```

运行结果：

![](img/5618306d085ac1bac8275d6c4c5bbf2a_100_0.png)

示例 3.4：找到 11 到 999 之间的数字 $m$，使得 $m, m^2$ 和 $m^3$ 都是回文，然后输出 $m$。

回文数是指具有对称数字的数字。例如：121、676 和 94249 都是回文数。满足本题要求的的一个实例是：$m=11, m^2=121, m^3=1331$。

分析：要检查一个数字是否为回文数，可以通过连续除以10并取余来获取该数的每个数字。获取所有数字后，反转数字顺序得到一个新的数字，并将新数字与原数字进行比较。当且仅当原数字等于新数字时，原数字是回文数。

源代码：

```cpp
//3_4.cpp
#include <iostream>
using namespace std;
int main() {
    bool symm(long n) {
        long m;
        for(m=11;m<1000;m++)
            if (symm(m)&&symm(m*m)&&symm(m*m*m))
                cout<<"m="<<m<<" m*m="<<m*m<<" m*m="<<m*m*m<<endl;
    }
    bool symm(long n) {
        long i, m;
        i=n; m=0;
        while(i) {
            m=m*10+i%10;
            i=i/10;
        }
        return (m==n);
    }
    return 0;
}
```

运行结果：

| m=11 | m*m=121 | m*m*m=1331 |
| m=101 | m*m=10201 | m*m*m=1030301 |
| m=111 | m*m=12321 | m*m*m=1367631 |

## 3.1 函数的定义与使用

**示例 3.5：** 计算以下公式的值并输出结果。

$k = \begin{cases} \sin(r) + \sin(s) & \text{当 } r^2 \le s^2 \\ \sin(r \times s) & \text{当 } r^2 > s^2 \end{cases}$

这里 $r$ 和 $s$ 的值从键盘输入。$\sin x$ 的近似值使用以下公式计算：

$$\sin x = \frac{x^3}{3!} - \frac{x^5}{5!} + \frac{x^7}{7!} - \dots = \sum (-1)^{n-1} \frac{x^{2n-1}}{(2n-1)!}$$

计算精度为 $10^{-6}$。停止累加直到某一项的绝对值小于精度，累加值即为 $\sin x$ 的近似值。

源代码：

```cpp
//3_5.cpp
#include <iostream>
#include <cmath> //数学头文件 math 包含数学函数的声明
using namespace std;
int main()
{
    double k,r,s;
    double tsin(double x);
    cout<<"r=";
    cin>>r;
    cout<<"s=";
    cin>>s;
    if (r*r<=s*s)
        k=tsin(r)+tsin(s);
    else
        k=tsin(r*s);
    cout<<k<<endl;
}

double tsin(double x)
{
    double p=0.000001,g=0, t=x;
    int n=1;
    do {
        g=g+t;
        n++;
        t=-t*x/(2*n-1)/(2*n-2);
    } while(fabs(t)>=p);
    return g;
}
```

运行结果：

```
r=5
s=8
37781
```

示例 3.6：掷骰子游戏。

规则：骰子有 6 面。从键盘输入一个无符号整数作为种子。如果回合内点数是 7 或 11，则玩家胜；如果是 2、3 或 12，则玩家输；否则继续下一回合。

源代码：

```cpp
//3_6.cpp
#include <iostream>
#include <cstdlib>
using namespace std;
int rolldice(void);
int main()
{
    int gamestatus,sum,mypoint;
    unsigned seed;
    cout<<"Please enter an unsigned integer:";
    cin>>seed;//输入种子
    rand(seed); // 将种子传递给 rand
    sum=rolldice(); // 第一轮掷骰子得到点数
    switch(sum)
    {
        case 7:
        case 11:
            gamestatus=1; // 点数为 7 或 11 时玩家胜
            break;
        case 2:
        case 3:
        case 12:
            gamestatus=2; // 点数为 2、3 或 12 时玩家输
            break;
        default:
            mypoint=sum; // 记录记录点数
            break;
    }
    while(gamestatus==0)
    {
        sum=rolldice(); // 继续掷骰子
        if(sum==mypoint)
        {
            gamestatus=1; // 点数等于记录点数时玩家胜
        }
        else if(sum==7)
        {
            gamestatus=2; // 点数为 7 时玩家输
        }
        // 否则进入下一回合
    }
    if(gamestatus==1)
        cout<<"player wins"<<endl;
    else if(gamestatus==2)
        cout<<"player loses"<<endl;
    return 0;
}

int rolldice(void)
{
    int die1,die2,worksum;
    die1=1+rand()%6;
    die2=1+rand()%6;
    worksum=die1+die2;
    cout<<"player rolled "<<die1<<"++"<<die2<<'='<<worksum<<endl;
    return worksum;
}
```

