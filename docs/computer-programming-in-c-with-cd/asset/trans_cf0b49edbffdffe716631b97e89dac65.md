

![](img/8a6886c00caa6a1651a6c0e62bff341f_616_0.png)

答案：

```cpp
#include<iostream.h>

class staff
{
    public:
        char EmployCode[10];
};

class Teacher :public staff
{
    int Experience;
    char Subjectname[30];
    public:
    void ReadTeacher()
    {
        cin>>Subjectname>>EmployCode>>Experience;
    }
};
class Typist :public staff
{
    int Speed;
    int Experience;
    public:
    void ReadTypist ()
    {
        cin>>Experience>>EmployCode>>Speed;
    }
};
class RegularTypist :public Typist
{
    int BasicSalary;
    public:
    void ReadRegularTypist ()
    {
        cin>>BasicSalary;
    }
};
class CasualTypist :public Typist
{
    int Duration;
    public:
    void ReadCasualTypist ()
    {
        cin>>Duration;
    }
};

class officer :public staff
{
    char Dept[15];
    char Grade;
    public:
    void Readofficer ()
    {
        cin>>EmployCode>>Grade>>Dept;
    }
};
```

## 问题20：编写一个程序，重载“+=”运算符，以将给定的两个距离（以英尺和英寸为单位）相加（孟买大学，2008年12月）

```cpp
#include <iostream.h>
#include <conio.h>

class overloading
{
        int Feet, Inches;
public:
overloading(int feet, int inches)
{
    Feet=feet;
    Inches=inches;
}
void operator += (overloading obj)
{
    Feet=Feet+obj.Feet;
    Inches=Inches+obj.Inches;
}
void Display()
{
    cout<<Feet<<"feet  "<<"and  "<<Inches<<"   inches"<<endl;
    cout<<endl<<endl;
}
};
void main()
{
    clrscr();
    overloading obj1(10,6),obj2(17,4);
    cout<<endl;
    obj1.Display( );
    obj2.Display( );
    obj2+=obj1;
    obj2.Display( );
    getche();
}
```

## 问题21：下面所示的是弗洛伊德三角形

```text
1
3
4          5          6
7          8          9          10
11--------------------------------15
-
-
-
-
-
79---------------------------------------------------------------91
```

编写一个面向对象的程序（使用类和对象）来打印这个三角形。（孟买大学，2007年6月）

答案：

```cpp
#include<iostream.h>

class FloydT
{
        public:
        void printFloydT();
};

void FloydT :: printFloydT()
{
        int i,j,k=1;

        for(i=1;k<=91;i++)
        {
                cout<<endl;

                for(j=1;j<=i;j++)
                {
                        cout << k ;
                        ++k;
                }
        }
}
void main()
{
        FloydT ft;
        ft.printFloydT();
}
```

## 问题22：编写一个面向对象的程序，用于通过一组点 (x,y) 拟合一条直线，其中 i = 1...........n。直线方程为 y=mx+c，m 和 c 的值由下式给出

$$m=\frac{n\sum(x_i y_i)-(\sum x_i)(\sum y_i)}{n(\sum x_i^2)-(\sum x_i)^2}$$

$$c=\frac{\sum y_i-m\sum x_i}{n}$$

> （孟买大学，2007年6月）

答案：

```cpp
#include<iostream.h>

#include<math.h>

class sline
{
    public:
        void calcm();
    private:
        int x[20], y[20],n;
    //assuming n<=20;
};

void sline :: calcm()
{
    int i, valx=0, valy=0,mulxy=0, xqsum=0, sumxq,m,c;
    for(i=0; i<=n;i++)
    {
        valx= valx+x[i];
        valy= valy+y[i];
        mulxy= mulxy + (x[i]*y[i]);
        xqsum=xqsum + pow(x[i],2);
    }
    sumxq= pow(valx,2);
    {
        m= (n*mulxy - valx*valy) / (n*xqsum -sumxq);
        cout<<m;
        c= (valy - m* valx)/i;
        cout<<c;
    }
}

void main()
{
sline s;
s.calm();
}
```

## 问题23：编写一个使用欧几里得算法来显示两个整数的最大公约数的面向对象程序。数字的最大公约数是能同时整除这两个数字的最大数。算法工作原理如下。

- i. 使用模运算符，用较大的数除以较小的数，求出余数。
- ii. 将较大的数变为较小的数，并将较小的数变为步骤 (i) 中的余数。
- iii. 重复此过程，直到余数为零。请包含用于数据输入、显示结果、默认构造函数和带两个参数的构造函数的成员函数。还要创建对象来引用这些成员函数。

（孟买大学，2007年6月）

答案：

```cpp
#include<iostream.h>
#include<math.h>

class gcd
{
        public:
                gcd();
                gcd(int, int);
        void gcdinput();
                void gcdcompute();
                void gcdoutput();

        private:
                int m,n,result;
};
gcd :: gcd()
{
        m=n=result=0;
}
gcd :: gcd(int x, int y)
{
        m=x;
        n=y;
        result=0;
}
void gcd :: gcdinput()
{
    cout<<"Enter First number";
    cin>> m;
    cout<<"Enter second number";
    cin>>n;
}
void gcd :: gcdcompute()
{
    int Remainder;
    int max, min;
    max=m > n ? m:n;
    min=m<n ? m:n;

    while (min!=0)
    {
        Remainder =max % min;
        max=min;
        min=Remainder;
    }

    result=max;

}
void gcd :: gcdoutput()
{
    cout<<" The gcd of two numbers is:";
    cout<< result << endl;
}

void main()
{
    gcd g;

    g.gcdinput();
    g.gcdcompute();
    g.gcdoutput();

}
```

## 问题24：开发一个类，其成员函数支持有理数的算术运算，即执行有理数的加法、减法、除法和乘法。所有成员函数都需要重载二元运算符。编写合适的 main 程序来演示二元运算符重载的各个方面。包含合适的构造函数和重载构造函数。有理数采用 a/b 的形式，其中 a 和 b 是整数常量。（孟买大学，2007年6月）

答案：

```cpp
#include<iostream.h>

#include<conio.h>
class rat
{
private:
int Num,Den;

public:
rat(int x=0, int y=1)
{
Num=x;
Den=y;
}

rat operator +( rat R)
{
rat temp;
temp.Num= Num*R.Den+ R.Num*Den;
temp.Den= R.Den* Den;
return temp;
}

void operator -(rat R)
{
Num= Num*R.Den-R.Num*Den;
Den= R.Den* Den;
}

void operator /(rat R)
{
Num= Num*R.Den ;
Den= R.Num* Den;
}

rat operator *(rat R)
{
rat temp;
temp.Num= Num*R.Num;
temp.Den= R.Den* Den;
return temp;
}

void display()
{
cout<<Num<<Den;
}
};

void main()
{
clrscr();
rat R1(2,3),R2(3,4),R3;
R3=R1+R2;
R3.display();
R1-R2;
R1.display();
R3=R1*R2;
R3.display();
R1/R2;
R1.display();

getch();
}
```

在矩阵加法中使用对象作为函数参数。编写合适的 main 程序来测试这些成员函数。

答案：

```cpp
#include<iostream.h>
#include<conio.h>

class matrix
{
int n,m;
int mat[10][10];
public:
void input();
void display();
void add(matrix obj,matrix obj1);
void mul(matrix obj,matrix obj1);
void Elimination();
void Transpose();

};
void matrix::input()
{
cout<<"\n Enter The Number of Rows: ";
cin>>m;
cout<<"\n Enter The Number of Columns: ";
cin>>n;
for(int i=0;i<m;i++)
for(int j=0;j<n;j++)
cin>>mat[i][j];
}
void matrix::display()
{
for(int i=0;i<m;i++)
{
cout<<endl;
for(int j=0;j<n;j++)
cout<<"\t"<<mat[i][j];
}
}

void matrix::Transpose()
{
if(m>n) { int temp=m; m=n; n=temp;}

for(int i=0;i<m;i++)
for(int j=i;j<n;j++)
{
int temp=mat[i][j];
mat[i][j]=mat[j][i];
mat[j][i]=temp;
}
}
void matrix::add(matrix obj,matrix obj1)
{
if((obj1.m==obj.m)&&(obj1.n==obj.n))
{
m=obj1.m;
n=obj1.n;
for(int i=0;i<obj1.m;i++)
for(int j=0;j<obj1.n;j++)
mat[i][j]=obj1.mat[i][j]+obj.mat[i][j];
}
else
cout<<"\n Cannot Add";
}
void matrix::mul(matrix obj,matrix obj1)
{
if(obj.n==obj1.m)
{
n=obj1.n;
m=obj1.m;
for(int i=0;i<m;i++)
for(int j=0;j<n;j++)
{
mat[i][j]=0;
for(int k=0;k<m;k++)
mat[i][j]+=obj.mat[i][k]*obj1.mat[k][j];
}
}
else
cout<<"\n Cannot Multiply ";
}
void matrix::Elimination( )
{
```

