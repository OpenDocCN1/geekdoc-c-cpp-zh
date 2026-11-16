

这里，函数 display() 获取的是局部变量的地址而非其值。因此，值的更改是永久的。

## 返回指针

指针也可用作返回类型。

请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int*change();
int main()
{
    int*b;
    b=change();
    cout<<*b;
}
int*change()
{
    int a=5;
    return(&a);
}
```

该程序将显示 5。

## 指针运算

指针遵循加法和减法，即地址可以增加、减少、相加甚至相减。

请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
int a=7,*b=&a;
cout<<b;
b++;
cout<<endl<<b;
}
```

输出（您的可能不同）

0x22fe44

0x22fe48

请注意，我们将 b 增加了 1，因此，这将增加相应数据类型（即 int）的一个内存块。因此，在 64 位编译器中将观察到 4 字节的增加，而在 32 位编译器中将观察到 2 字节的增加。

两个指针之间不能直接进行乘法或除法运算。

![](img/5340985153962870d4e4a3b9453b9146_95_0.png)

## 数组

数组是存储在相同数据类型的连续内存位置中的变量序列。它是存储大量变量的一种方法。假设我们要处理 500 个数字，那么声明或定义 500 个不同的变量是不可行的。因此，我们可以定义一个数组，例如 int num[500]；这里，num 的索引范围是 0 到 499。因此，我们现在可以使用 num[0] 到 num[499]。

### 数组声明与初始化

数组可以按以下方式声明和初始化：

```cpp
int a[2]={45,43};
int a[2]={43};
int a[]={34,54,65};
int a[]={43};
int a[23];
```

未初始化的数组包含垃圾值。

例如，假设我们想计算以下程序中 10 个数字的和

```cpp
#include<iostream>
using namespace std;
int main()
{
    int num[10]={5,7,8,3,2,1,2,4,3,15};
    int sum=0,i;
    for(i=0;i<10;i++)
    sum+=num[i];
    cout<<sum;
}
```

输出

50

这里，您可以看到为 num[i] 赋值的方法。要为某个数字（例如 num[3]）赋值，可以直接使用 num[3]=5；在上述程序中，我使用了线性赋值，即 5 赋给 num[0]，7 赋给 num[1]，……，15 赋给 num[9]。

## 边界检查

假设您声明了一个数组 int a[32]；然后您可以使用语句 a[95]=0；因为 C++ 不会检查边界。但是，不应这样做，因为这可能会导致程序崩溃。

例如，请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    int a[32];
    a[90]=0;
}
```

由于没有边界检查，该程序不会显示任何错误。因此，使用数组时要注意边界。但是，如果在初始化时越界，编译器会检测到它并报错。

例如，请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    int a[3]={1,2,4,5};
}
```

该程序将报错 "Too many initializers for int[3]"

## 将数组元素传递给函数

数组以与普通变量相同的方式传递给函数。

例如，请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
void disp1(int);
int main()
{
    int a[32],i;
    for(i=0;i<32;i++)
    {
        a[i]=i;
        disp1(a[i]);
    }
}
void disp1(int x)
{
    cout<<x<<endl;
}
```

这将在不同行上打印 0 到 31。

## 将整个数组传递给函数

整个数组也可以传递给函数。

方法 1：请考虑以下代码：

```cpp
#include<iostream>
using namespace std;
void disp(int*,int);
int main()
{
    int num[5]={3,2,0,1,4};
    disp(num,5);
}
void disp(int*x,int y)
{
    int i;
    for(i=0;i<y;i++,x++)
    cout<<*x;
}
```

这里，您可以看到我们只将 num 传递给了函数。在数组中，变量名实际上是其基地址。因此，num 等价于 &num[0]。然后使用指针运算，我们在 for 循环的第 3 条语句中增加了 x 的地址（x 实际上就是 num）。因此，输出将是 32014

方法 2：上述程序也可以写成：

```cpp
#include<iostream>
using namespace std;
void disp(int*,int);
int main()
{
    int num[5]={3,2,0,1,4};
    disp(num,5);
}
void disp(int*x,int y)
{
    int i;
    for(i=0;i<y;i++)
    cout<<*(x+i);
}
```

方法 3：请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
void disp(int&,int);
int main()
{
    int num[5]={3,2,0,1,4};
    disp(num[0],5);
}
void disp(int&x,int y)
{
    int i;
    for(i=0;i<y;i++,x++)
    cout<<x;
}
```

请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<main;
}
```

函数名也是函数本身的地址。该程序将显示 main() 函数的地址。

请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<cout;
}
```

该程序将显示 cout 宏的地址。

## 多维数组

数组可以是一维数组或多维数组。例如，int array[3][4][2]；

请考虑以下程序

```cpp
#include<iostream>
using namespace std;
int main()
{
    int num[3][2][5],i,j,k;
    for(i=0;i<3;i++)
        for(j=0;j<2;j++)
            for(k=0;k<5;k++)
                num[i][j][k]=i+j+k;
}
```

在此程序中，我们声明了一个三维数组并为其赋值。

二维数组也可以按以下方式初始化

```cpp
int num[4][2] = {{ 1214, 86 },{ 1612, 53 },{ 24, 8 },{ 22,8 }};
```

重要的是要记住，在初始化二维数组时，必须指定第二个维度，而第一个维度是可选的。

因此，以下声明：

```cpp
int num[2][3] = { 1, 3, 2, 4, 98, 78 };
int num[][3] = { 2, 4, 2, 4, 6, 5 };
```

是可接受的，而，

```cpp
int num[2][] = { 12, 34, 23, 45, 56, 45 };
int num[] [] = { 12, 34, 23, 45, 56, 45 };
```

会报错 "Array type has incomplete element type"

请考虑以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    int num[2][3]={{0,1,5},{6,7,8}};
    int i;
    for(i=0;i<2;i++)
    {
        cout<<"\nAddress of num["<<i<<"] is "<<num[i];
    }
}
```

运行此程序时，您会发现 num[0] 和 num[1] 的地址相差 12 字节。这意味着 num[0] 包含三个内存块 num[0][0]、num[0][1] 和 num[0][2]，然后 num[1] 的内存块开始。更令人惊讶的是，此程序显示每个维度比实际数组少一的数组都表示实际数组的地址。这意味着我们可以通过高效使用指针来访问多维数组的元素。

## 返回数组

数组也可以返回。我们可以使用指针或引用来返回数组。

### 方法 1：使用指针返回数组

可以使用指针返回整个数组。以下程序说明了这一点：

```cpp
#include<iostream>
using namespace std;
int*arr();
int main()
{
    int*a=arr();
    cout<<*a<<*(a+1)<<"\n";
}
int*arr()
{
    int num[2]={1,2};
    return num;
}
```

输出

12

### 方法 2：使用引用返回数组

可以使用引用返回数组。以下程序说明了此方法：

```cpp
#include<iostream>
using namespace std;
int&arr();
int main()
{
    int a=arr();
    cout<<a<<(a+1)<<"\n";
}
int&arr()
{
    int num[2]={1,2};
    return num[0];
}
```

输出

12

![](img/5340985153962870d4e4a3b9453b9146_104_0.png)

