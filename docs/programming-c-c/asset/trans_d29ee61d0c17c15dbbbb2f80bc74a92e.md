

## 46. 写一个C程序来声明并初始化一个联合体（union）。

```c
#include <stdio.h>

// union declaration
union pack{
    char a;
    int b;
    double c;
};

int main() {
    union pack p; // 对象/变量声明
    printf("\nOccupied size by union: %d\n", sizeof(p));

    // 逐个给成员赋值，它会覆盖上一个值
    p.a='A';
    printf("\nValue of a:%c\n", p.a);

    p.b=10;
    printf("\nValue of b:%d\n", p.b);

    p.c=12345.6790;
    printf("\nValue of c:%f\n", p.c);

    // 看看，如果同时赋值赋值会发生什么？
    p.a='A';
    p.b=10;
    p.c=12345.6790;

    // 在这里，所有成员都将访问 p c 的最后一个值
    printf("\nValue of a:%c, b:%d, c:%f\n", p.a,p.b,p.c);

    return 0;
}
```

输出
Occupied size by union pack: 8
Value of a:A
Value of b:10
Value of c:12345.67900
Value of a:,-377957122, c:12345.67900

## 47. 写一个C++程序来实现实现函数重载。

```cpp++
#include<iostream>
using namespace std;

int absolute(int);
float absolute(float);

int main() {
    int a = -5;
    float b = 5.5;

    cout << "Absolute value of " << a << " = " << absolute(a) << endl;
    cout << "Absolute value of " << b << " = " << absolute(b) << endl;
    return 0;
}

int absolute(int var) {
    if (var<0) {
        var = -var;
        return var;
    }
    return var;
}

float absolute(float var){
    if (var<0.0) {
        var = -var;
        return var;
    }
    return var;
}
```

输出
Absolute value of -5 = 5
Absolute value of 5.5 = 5.5

## 48. 写一个C++程序使用封装计算矩形的面积。

```cpp
#include<iostream>

using namespace std;

class Rectangle
{
    int length;
    int breadth;
public:
    void setDimension(int l, int b)
    {
        length = l;
        breadth = b;
    }
    int getArea()
    {
        return length * breadth;
    }
};

int main()
{
    int x,y;
    Rectangle rt;
    cout<<"Enter the length of the rectangle:";
    cin>>x;
    cout<<"Enter the breadth of the rectangle:";
    cin>>y;
    rt.setDimension(7, 4);
    cout<<rt.getArea() <<endl;
    return 0;
}
```

输出
Enter the length of the rectangle:30
Enter the breadth of the rectangle:20
600

## 49. 写一个C++程序使用数据抽象相两个数。

```cpp
#include <iostream>
using namespace std;
class Sum
{
    private: int x, y, z; // 私有变量
public:
    void add()
    {
        cout<<"Enter two numbers: ";
        cin>>x>>y;
        z= x+y;
        cout<<"Sum of two number is: "<<<<z<<endl;
    }
};

int main()
{
    Sum sm;
    sm.add();
    return 0;
}
```

输出:
Enter two numbers:
6
Sum of two number is: 9

## 50. 写一个C++程序重载二元运算符。

```cpp
#include <iostream>
using namespace std;
class A {
    int x;
    public:
    A(){}
    A(int i){
        x=i;
    }
    void operator+(A);
    void display();
};

void A ::operator+(A a){
    int m = x+a.x;
    cout<<"The result of the addition of two objects is : "<<m;
}
int main(){
    int x,y;
    cout<<"Enter the First number : ";
    cin>>x;
    cout<<"Enter the Second number : ";
    cin>>y;
    A a1(5);
    A a2(4);
    a1+a2;
    return 0;
}
```

输出:
Enter First Number: 3
Enter Second Number: 6
The result of the addition of two numbers is: 9

![](img/967bcdbdba6f2e1f56642982e8b39e66_294_0.png)

www.himpub.com

![](img/967bcdbdba6f2e1f56642982e8b39e66_294_1.png)

ISBN: 978-93-89652-30-7 ESM 0823

