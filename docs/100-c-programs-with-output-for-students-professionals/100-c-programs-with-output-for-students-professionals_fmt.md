
# 100+ 带输出的 C++ 程序：学生与专业人士精选

# 前言

## 关于作者

Aniket O. Pataskar 出自印度奥兰格巴德。他是一名 IT 软件工程师，拥有多种语言编程和 Mac OSX 系统方面的工作经验。此外，他对各种社会事务也充满兴趣。在不断的努力下，他完成了这本书。

作者在软件开发、iOS（iPhone、iPad & iPod）及 Android 应用开发，以及多媒体（如动画、数字电影制作、视频编辑、视觉特效和音频编辑）方面也拥有技能。他在 Udemy 市场上也有自己的在线课程。

# 本书献给

我的家人，感谢他们一如既的爱与支持，以及对我的信任。我想将本书献给那位不断激励我做事的神。

没有你们的爱与理解，这本书是不可能实现的。

从心深处感谢你们。

## 目录

94. 编写程序显示 C++ 17 中的构造函数 174

95. 编写一个关于排序的程序 175

96. 编写一个程序演示 C++ 中的二分查找算法 176

97. C++ 中的命名空间可以嵌套吗？编写该程序。178

98. 编写一个使用嵌套 for 循环查找 2 到 100 之间质数的程序 180

99. 编写一个使用嵌套 if 语句的程序 181

100. 编写一个演示嵌套 switch 语句的程序 182

101. 预测以下 C++ 程序的输出。（1 到 15 个程序）183

## 1. Hello World C++ 示例程序

```cpp
#include<iostream>
#include<conio.h>

//标准命名空间声明
using namespace std;

// 主函数
int main()
{
    // 标准输出语句
    cout<<"My First C++ Program";

    // 等待输出屏幕
    getch();

    // 主函数返回语句
    return 0;
}
```

### 输出

```text
My First C++ Program
```

## 2. C++ 中的 `if` 语句示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;
int main()
{
     // 变量声明
    int a;

    // 获取输入值
    cout<<"Enter the Number :";
    cin>>a;

     // If 条件检查
    if(a > 10)
    {
         // 条件成功执行块
        cout<<a<<" Is Greater than 10";
    }

     // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Enter the Number :15

15 Is Greater than 10
```

## 3. C++ 中的 `if..else` 语句示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

int main()
{
    // 变量声明
    int a;

    // 获取输入值
    cout<<"Enter the Number :";
    cin>>a;

    // If 条件检查
    if(a > 10)
    {
        // 条件成功执行块
        cout<<a<<" Is Greater than 10";
    }
    else
    {
        // 条件失败执行块
        cout<<a<<" Is Less than/Equal 10";
    }

    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出 1

```text
Enter the Number :20

20 Is Greater than 10
```

### 输出 2

```text
Enter the Number :5

5 Is Less than/Equal 10
```

## 4. C++ 中的 `For` 循环示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

int main()
{
    // 变量声明
    int a;

    // 获取输入值
    cout<<"Enter the Number :";
    cin>>a;

    // for 循环块
    for (int counter = 1; counter <= a; counter++)
    {
        cout<<"Execute "<<counter<<" time"<<endl;
    }

    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Enter the Number :5

Execute 1 time

Execute 2 time

Execute 3 time

Execute 4 time

Execute 5 time
```

## 5. C++ 中的 `While` 循环示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

int main()
{
    // 变量声明
    int a;

    // 获取输入值
    cout<<"Enter the Number :";
    cin>>a;

    int counter = 1;
    // while 循环块
    while (counter <= a)
    {
        cout<<"Execute "<<counter<<" time"<<endl;
        counter++;
    }

    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Enter the Number :4

Execute While 1 time

Execute While 2 time

Execute While 3 time

Execute While 4 time
```

## 6. C++ 中的 `Do While` 循环示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

int main()
{
    // 变量声明
    int a;

    // 获取输入值
    cout<<"Enter the Number :";
    cin>>a;

    int counter = 1;
    // do while 循环块
    do {
        cout<<"Execute Do While "<<counter<<" time"<<endl;
        counter++;
    } while (counter <= a);

    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Enter the Number :6

Execute Do While 1 time

Execute Do While 2 time

Execute Do While 3 time

Execute Do While 4 time

Execute Do While 5 time

Execute Do While 6 time
```

## 7. C++ 构造函数示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

class Example {
    // 变量声明
    int a,b;
public:

    // 构造函数
    Example() {
        // 在构造函数中赋值
        a=10;
        b=20;
        cout<<"Im Constructor\n";
    }

    void Display() {
        cout<<"Values :"<<a<<"\t"<<b;
    }
};

int main() {
    Example Object;
    // 构造函数调用
    Object.Display();
    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Im Constructor

Values :10 20
```

## 8. C++ 带参数构造函数示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

class Example {
    // 变量声明
    int a,b;
public:

    // 构造函数
    Example(int x,int y) {
        // 在构造函数中赋值
        a=x;
        b=y;
        cout<<"Im Constructor\n";
    }

    void Display() {
        cout<<"Values :"<<a<<"\t"<<b;
    }
};

int main() {
    Example Object(10,20);
    // 构造函数调用
    Object.Display();
    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Im Constructor

Values :10 20
```

## 9. C++ 构造函数重载示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

class Example    {
    // 变量声明
    int a,b;
public:

    // 无参数的构造函数
    Example() {
        // 在构造函数中赋值
        a=50;
        b=100;
        cout<<"\nim Constructor";
    }

    // 带参数的构造函数
    Example(int x,int y) {
        // 在构造函数中赋值
        a=x;
        b=y;
        cout<<"\nim Constructor";
    }

    void Display() {
        cout<<"\nValues :"<<a<<"\t"<<b;
    }
};

int main()
{
  Example Object(10,20);
  Example Object2;
  // 构造函数调用
  Object.Display();
  Object2.Display();
  // 等待输出屏幕
  getch();
  return 0;
}
```

### 输出

```text
Im Constructor

Im Constructor

Values :10  20

Values :50  100
```

## 10. 查找质数的算法

### 算法

- 步骤 1：启动程序。
- 步骤 2：将类声明为 `Prime`。
- 步骤 3：使用整数成员参数。
- 步骤 4：从 `i=2` 到 `a/2` 执行以下操作。
- 步骤 5：检查 `a%i==0`，则将 `k` 设置为 `0` 并中断。
- 步骤 6：否则将 `k` 设置为 `1`。
- 步骤 7：将 `i` 值加 `1`。
- 步骤 8：检查 `k` 值是 `1` 还是 `0`。
- 步骤 9：如果是 `1`，则显示该值为质数。
- 步骤 10：否则显示该值不是质数。
- 步骤 11：停止程序。

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

// 类声明
class prime
{
  // 变量声明
  int a,k,i;
public:
  prime(int x)
  {
    a=x;
    k=1;
    for(i=2;i<=a/2;i++)
    {
      if(a%i==0)
      {
        k=0;
        break;
      }
      else
      {
        k=1;
      }
    }
  }

  void show()
  {
    if(k==1)
      cout<<"\n"<<a<<" is Prime Number.";
    else
      cout<<"\n"<<a<<" is Not Numbers.";
  }
};

// 主函数
int main()
{
  int a;
  cout<<"Enter the Number:";
  cin>>a;

  // 创建类对象
  prime obj(a);

  // 调用成员函数
  obj.show();
  getch();
  return 0;
}
```

### 输出

```text
Enter the Number:7

7 is Prime Number.
```

## 11. C++ 拷贝构造函数示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

class Example {
    // 变量声明
    int a,b;
public:

    // 带参数的构造函数
    Example(int x,int y) {
        // 在构造函数中赋值
        a=x;
        b=y;
        cout<<"\nIm Constructor";
    }

    void Display() {
        cout<<"\nValues :"<<a<<"\t"<<b;
    }
};

int main() {
    Example Object(10,20);

    // 拷贝构造函数
    Example Object2=Object;

    // 构造函数调用
    Object.Display();
    Object2.Display();

    // 等待输出屏幕
    getch();
    return 0;
}
```

### 输出

```text
Im Constructor

Values :10 20

Values :10 20
```

## 12. C++ 类和对象示例程序

```cpp
#include <iostream>
#include<conio.h>
using namespace std;

// 类声明
class person
{
// 访问修饰符
public:

// 变量声明
string name;
int number;
};

// 主函数
int main()
{
// 创建类对象
person obj;

// 为对象变量获取输入值
cout<<"Enter the Name :";
cin>>obj.name;

cout<<"Enter the Number : ";
cin>>obj.number;

// 显示输出
cout << obj.name << ": " << obj.number << endl;

getch();
return 0;
}
```

### 输出

```text
Enter the Name :Byron

Enter the Number :100

Byron: 100
```

## 13. C++ 质数判断示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

// 类声明
class prime
{
// 成员变量声明
int a,k,i;
public:
prime(int x)
{
a=x;
}

// 创建类对象
void calculate()
{
k=1;
{
for(i=2;i<=a/2;i++)
if(a%i==0)
{
k=0;
break;
}
else
{
k=1;
}
}
}
}

void show()
{
if(k==1)
cout<<"\nis Prime Number.";
else
cout<<"\nis Not Prime Numbers.";
}
;

// 主函数
int main()
{
int a;
cout<<"Enter the Number:";
cin>>a;

// 创建类对象
prime obj(a);

// 调用成员函数
obj.calculate();
obj.show();
getch();
return 0;
}
```

### 输出

```text
Enter the Number:10

10 is Not Prime Numbers.

Enter the Number:7

7 is Prime Numbers.
```

## 14. C++ 命名空间示例程序

```cpp
#include <iostream>

using namespace std;

// 命名空间 namespacefirst
namespace namespacefirst{
    int value = 5;
}

// 命名空间 namespacespacescond
namespace namespacespacescond{
    double value = 3.1416;
}

int main () {
    // 使用命名空间 namespacefirst变量
    cout << "namespacefirst value : " <<namespacefirst::value << endl;

    // 使用命名空间 namespacespacescond变量
    cout << "namespacescond value : "<<namespacescond::value << endl;
    return 0;
}
```

### 输出

```text
namespacefirst value : 5

namespacesecond value : 3.1416
```



## 15. C++ 查找质数示例程序

```cpp
#include<iostream>
#include<conio.h>
#include<math.h> // Math.h 用于 sqrt 函数

using namespace std;

int main()
{
    // 变量声明
int n;

    // 获取输入值
cout<<"Enter the Number :";
cin>>n;

cout<<"List Of Prime Numbers Below "<<n<<endl;
    // 用于查找质数的 for 循环块
    for (int i=2; i<n; i++)
        for (int j=2; j*j<=i; j++)
        {
            if (i % j == 0)
                break;
            else if (j+1 > sqrt(i))
                cout << i << endl;
        }
// 等待输出屏幕
getch();
return 0;
}
```

**输出：**

```
Enter the Number :50
List Of Prime Numbers Below 50
5
7
11
13
17
19
23
29
31
37
41
43
47
```

## 16. C++ 用另一种方法查找质数的示例程序

```cpp
#include<iostream>
#include<conio.h>
#include<math.h> // Math.h 用于 sqrt 函数

using namespace std;

int main()
{
    // 变量声明
    int n;

    // 获取输入值
cout<<"Enter the Number :";
cin>>n;

    // 用于查找质数的 for 循环块
    for (int i=2;i<n; i++)
    {
        bool prime=true;
        for (int j=2; j*j<=i; j++)
        {
            if (i % j == 0)
            {
                prime=false;
                break;
            }
        }
        if(prime) cout << i << endl;
    }

// 等待输出屏幕
getch();
return 0;
}
```

**输出：**

```
Enter the Number :50
List Of Prime Numbers Below 50
5
7
11
13
17
19
23
29
31
37
41
43
47
```

## 17. C++ 斐波那契数列示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

int main()
{
    // 变量声明
int counter, n;
long last=1,next=0,sum;
    // 获取输入值
cout<<"Enter the Number :";
cin>>n;

    // 斐波那契数列计算
    while(next<n)
    {
        cout<<last << " ";
        sum=next+last;
        next=last;
        last=sum;
    }

// 等待输出屏幕
getch();
return 0;
}
```

**输出：**

```
Enter the Number :30
1 2 3 5 8 13 21 34 55 89 144 233
```

## 18. C++ 递归阶阶乘示例程序

```cpp
#include<iostream>
#include<conio.h>

using namespace std;

// 函数
int main()
{
    // 变量声明
    int counter, n;

    // 获取输入值
cout<<"Enter the Number :";
cin>>n;

    // 阶乘函数调用
cout<<factorial(n);

    // 等待输出屏幕
getch();
return 0;
}

// 阶乘递归
long factorial(int n)
{
  if (n == 0)
    return 1;
  else
    return(n * factorial(n-1));
}
```

**输出：**

```
Enter the Number :6
6
```

## 19. C++ 命名空间阶乘示例程序

```cpp
#include <iostream>

using namespace std;

// 命名空间 namespacefirst
namespace namespacefirst{
    int value = 5;
}

// 命名空间 namespacespacescond
namespace namespacespacescond{
    double value = 3.1416;
}

int main () {
    // 使用命名空间 namespacefirst 变量
    cout << "namespacefirst value : " <<namespacefirst::value << endl;

    // 使用命名空间 namespacespacescond 变量
    cout << "namespacescond value : "<<namespacescond::value << endl;
    return 0;
}
```

**输出:**

```
namespacefirst value : 5
namespacesecond value : 3.1416
```



```cpp
#include <iostream>

using namespace std;

// 命名空间 namespacefirst
namespace namespacefirst {
    int value = 5;
}

// 命名空间 namespacespacescond
namespace namespacespacescond {
    double value = 3.1416;
}

int main() {
    // 使用命名空间 namespacefirst 变量
    cout << "namespacefirst value : " << namespacefirst::value << endl;

    // 使用命名空间 namespacespacescond 变量
    cout << "namespacescond value : " << namespacespacescond::value << endl;
    return 0;
}
```

```cpp
{
    line obj;
    float val1, val2;
    clrscr();
    cout << "Enter two values:";
    cin >> val1 >> val2;
    cout << "\n\nMultiplication value is:" << obj.mul(val1, val2);
    cout << "\n\nCube value is:" << obj.cube(val1) << "\t" << obj.cube(val2);
    getch();
}
```

# 输出

Enter two values: 5 7

Multiplication Value is: 35

Cube Value is: 25 and 343

## 25. 使用 C++ 编程进行二进制运算符重载的简单加法

```cpp
// 头文件
#include <iostream>
#include <conio.h>

// 标准命名空间声明
using namespace std;
```

```cpp
class overloading
{
    int value;

public:
    void setValue(int temp)
    {
        value = temp;
    }

    overloading operator+(overloading ob)
    {
        overloading t;
        t.value = value + ob.value;
        return t;
    }

    void display()
    {
        cout << value << endl;
    }
};
```

```cpp
// 主函数
int main()
{
    overloading obj1, obj2, result;
    int a, b;

    cout << "Enter the value of Complex Numbers a,b:";
    cin >> a >> b;

    obj1.setValue(a);
    obj2.setValue(b);

    result = obj1 + obj2;

    cout << "Input Values:\n";
    obj1.display();
    obj2.display();

    cout << "Result:";
    result.display();

    getch();
    return 0;
}
```

# 输出

Enter the value of Complex Numbers a,b:10

5

Input Values:

10

5

Result:15

## 26. 使用 C++ 编程进行多重继承的简单程序

为了使用多重继承查找学生详情。

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明基类 `student`。
- 步骤 3：声明并定义函数 `get()` 以获取学生详情。
- 步骤 4：声明另一个类 `sports`。
- 步骤 5：声明并定义函数 `getsm()` 以读取体育成绩。
- 步骤 6：创建派生自 `student` 和 `sports` 的类 `statement`。
- 步骤 7：声明并定义函数 `display()` 以计算总和和平均值。
- 步骤 8：声明派生类对象，调用函数 `get()`、`getsm()` 和 `display()`。
- 步骤 9：停止程序。

**程序：**

```cpp
#include <iostream.h>
#include <conio.h>

class student
{
protected:
    int rno, m1, m2;

public:
    void get()
    {
        cout << "Enter the Roll no :";
        cin >> rno;

        cout << "Enter the two marks :";
        cin >> m1 >> m2;
    }
};

class sports
{
protected:
    int sm; // sm = 体育成绩

public:
    void getsm()
    {
        cout << "\nEnter the mark :";
        cin >> sm;
    }
};

class statement : public student, public sports
{
    int tot, avg;

public:
    void display()
    {
        tot = m1 + m2 + sm;
        avg = tot / 3;

        cout << "\n\tRoll No : " << rno << "\tTotal : " << tot;
        cout << "\n\tAverage : " << avg;
    }
};

void main()
{
    clrscr();

    statement obj;
    obj.get();
    obj.getsm();
    obj.display();

    getch();
}
```

# 输出

Enter the Roll no: 100

Enter two marks

90

80

Enter the Sports Mark: 90

Roll No: 100

Total : 260

Average: 86.66

## 27. 使用 C++ 编程进行内联函数的简单程序

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明类。
- 步骤 3：声明并定义乘法和立方的内联函数。
- 步骤 4：声明类对象和变量。
- 步骤 5：读取两个值。
- 步骤 6：使用类对象调用内联函数。
- 步骤 7：返回值。
- 步骤 8：显示。
- 步骤 9：停止程序。

**程序：**

```cpp
#include <iostream.h>
#include <conio.h>

class line
{
public:
    inline float mul(float x, float y)
    {
        return x * y;
    }

    inline float cube(float x)
    {
        return x * x;
    }
};

void main()
{
    line obj;
    float val1, val2;

    clrscr();

    cout << "Enter two values:";
    cin >> val1 >> val2;

    cout << "\nMultiplication value is:" << obj.mul(val1, val2);
    cout << "\nCube value is:" << obj.cube(val1) << "\t" << obj.cube(val2);

    getch();
}
```

# 输出

Enter two values: 5 7

Multiplication Value is: 35

Cube Value is: 25 and 343

## 28. 使用 C++ 编程进行函数模板的简单程序

使用函数模板交换数字。

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明模板类。
- 步骤 3：声明并定义交换值的函数。
- 步骤 4：声明并定义获取值的函数。
- 步骤 5：读取值并调用相应的函数。
- 步骤 6：显示。
- 步骤 7：停止程序。

**程序：**

```cpp
#include <iostream.h>
#include <conio.h>

template <class t>
void swap(t& x, t& y)
{
    t temp = x;
    x = y;
    y = temp;
}

void fun(int a, int b, float c, float d)
{
    cout << "\na and b before swapping:" << a << "\t" << b;
    swap(a, b);

    cout << "\na and b after swapping:" << a << "\t" << b;
    cout << "\nc and d before swapping:" << c << "\t" << d;
    swap(c, d);

    cout << "\nc and d after swapping:" << c << "\t" << d;
}

void main()
{
    int a, b;
    float c, d;

    clrscr();

    cout << "Enter A,B values(integer):";
    cin >> a >> b;

    cout << "Enter C,D values(float):";
    cin >> c >> d;

    fun(a, b, c, d);
    getch();
}
```

# 输出

Enter A, B values (integer): 10 20

Enter C, D values (float): 50 10.80

A and B before swapping: 10 20

A and B after swapping: 20 10

C and D before swapping: 50 10.80

C and D after swapping: 10.80 50

## 29. 使用 C++ 编程进行函数重载的简单程序

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明类 `fn` 以及数据成员和成员函数。
- 步骤 3：从用户处读取选择。
- 步骤 4：选择 = 1，跳转到步骤 5。
- 步骤 5：使用一个整数参数的函数计算圆面积。
- 步骤 6：选择 = 2，跳转到步骤 7。
- 步骤 7：使用两个整数参数的函数计算矩形面积。
- 步骤 8：选择 = 3，跳转到步骤 9。
- 步骤 9：使用三个参数（两个整数和一个浮点数）的函数计算三角形面积。
- 步骤 10：选择 = 4，停止程序。

**程序：**

```cpp
#include <iostream.h>
#include <stdlib.h>
#include <conio.h>

#define pi 3.14

class fn
{
public:
    void area(int);            // circle
    void area(int, int);        // rectangle
    void area(float, int, int); // triangle
};

void fn::area(int a)
{
    cout << "Area of Circle:" << pi * a;
}

void fn::area(int a, int b)
{
    cout << "Area of rectangle:" << a * b;
}

void fn::area(float t, int a, int b)
{
    cout << "Area of triangle:" << t * a * b;
}

void main()
{
    int ch;
    int a, b, r;

    clrscr();

    fn obj;

    cout << "\n\tFunction Overloading\n";
    cout << "\n1.Area of Circle\n2.Area of Rectangle\n3.Area of Triangle\n4.Exit\n";
    cout << "Enter your Choice:";
    cin >> ch;

    switch (ch)
    {
    case 1:
        cout << "Enter Radius of the Circle:";
        cin >> r;
        obj.area(r);
        break;

    case 2:
        cout << "Enter Sides of the Rectangle:";
        cin >> a >> b;
        obj.area(a, b);
        break;

    case 3:
        cout << "Enter Sides of the Triangle:";
        cin >> a >> b;
        obj.area(0.5, a, b);
        break;

    case 4:
        exit(0);
    }

    getch();
}
```

## 30. 使用 C++ 编程进行友函数的简单程序

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明类 `base` 及其数据成员和成员函数。
- 步骤 3：使用函数 `get()` 从用户处读取 2 个输入。
- 步骤 4：在类内部声明友元函数 `mean(base ob)`。
- 步骤 5：在类外定义友函数并执行以下操作。
- 步骤 6：以浮点形式返回平均值 `(ob.val1 + ob.val2) / 2`。
- 步骤 7：停止程序。

**程序：**

```cpp
#include <iostream.h>
#include <conio.h>

class base
{
    int val1, val2;

public:
    void get()
    {
        cout << "Enter two values:";
        cin >> val1 >> val2;
    }

    friend float mean(base ob);
};

float mean(base ob)
{
    return float(ob.val1 + ob.val2) / 2;
}
```



```cpp
// 主函数
int main()
{
    overloading obj1,obj2,result;
    int a,b;

    cout<<"Enter the value of Complex Numbers a,b:";
    cin>>a>>b;
    obj1.setValue(a);
    obj2.setValue(b);

    result = obj1+obj2;

    cout<<"Input Values:\n";
    obj1.display();
    obj2.display();
    cout<<"Result:";
    result.display();
    getch();
    return 0;
}
```

**输出：**

```
Enter the value of Complex Numbers a,b:10
5
Input Values:
10
5
Result:15
```

## 26. 使用 C++ 编程进行多重继承的简单程序

为了使用多重继承查找学生详情。

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明基类`student`。
- 步骤 3：声明并定义函数`get()`以获取学生详情。
- 步骤 4：声明另一个类`sports`。
- 步骤 5：声明并定义函数`getms()`以读取体育成绩。
- 步骤 6：创建派生自`student`和`sports`的类`statement`。
- 步骤 7：声明并定义函数`display()`以计算总和和平均值。
- 步骤 8：声明派生类对象，调用函数`get()`、`getms()`和`display()`。
- 步骤 9：停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>

class student
{
protected:
    int rno,m1,m2;
public:
    void get()
    {
        cout<<"Enter the Roll no :";
        cin>>rno;
        cout<<"Enter the two marks :";
        cin>>m1>>m2;
    }
};

class sports
{
protected:
    int sm; // sm = 体育成绩
public:
    void getsm()
    {
        cout<<"\nEnter the mark :";
        cin>>sm;
    }
};

class statement:public student,public sports
{
    int tot,avg;
public:
    void display()
    {
        tot=(m1+m2+sm);
        avg=tot/3;
        cout<<"\n\tRoll No : "<<rno<<"\tTotal : "<<tot;
        cout<<"\n\tAverage : "<<avg;
    }
};

void main()
{
    clrscr();
    statement obj;
    obj.get();
    obj.getsm();
    obj.display();
    getch();
}
```

**输出：**

```
Enter the Roll no: 100
Enter two marks
90
80
Enter the Sports Mark: 90
Roll No: 100
Total : 260
Average: 86.66
```

## 27. 使用 C++ 编程进行内联函数的简单程序

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明类`line`。
- 步骤 3：声明并定义乘法和立方的内联函数。
- 步骤 4：声明类对象和变量。
- 步骤 5：读取两个值。
- 步骤 6：使用类对象调用内联函数。
- 步骤 7：返回值。
- 步骤 8：显示。
- 步骤 9：停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>

class line
{
public:
    inline float mul(float x,float y)
    {
        return(x*y);
    }
    inline float cube(float x)
    {
        return(x*x);
    }
};

void main()
{
    line obj;
    float val1,val2;
    clrscr();
    cout<<"Enter two values:";
    cin>>val1>>val2;
    cout<<"\nMultiplication value is:"<<obj.mul(val1,val2);
    cout<<"\nCube value is:"<<obj.cube(val1)<<"\t"<<obj.cube(val2);
    getch();
}
```

**输出：**

```
Enter two values: 5 7
Multiplication Value is: 35
Cube Value is: 25 and 343
```

## 28. 使用 C++ 编程进行函数模板的简单程序

使用函数模板交换数字。

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明模板类。
- 步骤 3：声明并定义交换值的函数。
- 步骤 4：声明并定义获取值的函数。
- 步骤 5：读取值并调用相应的函数。
- 步骤 6：显示。
- 步骤 7：停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>

template<class t>
void swap(t &x,t &y)
{
  t temp=x;
  x=y;
  y=temp;
}

void fun(int a,int b,float c,float d)
{
  cout<<"\na and b before swapping:"<<a<<"\t"<<b;
  swap(a,b);
  cout<<"\na and b after swapping:"<<a<<"\t"<<b;
  cout<<"\nc and d before swapping:"<<c<<"\t"<<d;
  swap(c,d);
  cout<<"\nc and d after swapping:"<<c<<"\t"<<d;
}

void main()
{
    int a,b;
    float c,d;
    clrscr();
    cout<<"Enter A,B values(integer):";
    cin>>a>>b;
    cout<<"Enter C,D values(float):";
    cin>>c>>d;
    fun(a,b,c,d);
    getch();
}
```

**输出：**

```
Enter A, B values (integer): 10 20
Enter C, D values (float): 50 10.80
A and B before swapping: 10 20
A and B after swapping: 20 10
C and D before swapping: 50 10.80
C and D after swapping: 10.80 50
```

## 29. 使用 C++ 编程进行函数重载的简单程序

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明类`fn`及其数据成员和成员函数。
- 步骤 3：从用户处读取选择。
- 步骤 4：选择=1，跳转到步骤 5。
- 步骤 5：使用一个整数参数的函数计算圆面积。
- 步骤 6：选择=2，跳转到步骤 7。
- 步骤 7：使用两个整数参数的函数计算矩形面积。
- 步骤 8：选择=3，跳转到步骤 9。
- 步骤 9：使用三个参数（两个整数和一个浮点数）的函数计算三角形面积。
- 步骤 10：选择=4，停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<stdlib.h>
#include<conio.h>
#define pi 3.14
class fn
{
public:
    void area(int); //circle
    void area(int,int); //rectangle
    void area(float ,int,int); //triangle
};

void fn::area(int a)
{
    cout<<"Area of Circle:"<<pi*a;
}
void fn::area(int a,int b)
{
  cout<<"Area of rectangle:"<<a*b;
}
void fn::area(float t,int a,int b)
{
  cout<<"Area of triangle:"<<t*a*b;
}
void main()
{
  int ch;
  int a,b,r;
  clrscr();
  fn obj;
  cout<<"\n\tFunction Overloading\n";
  cout<<"\n1.Area of Circle\n2.Area of Rectangle\n3.Area of Triangle\n4.Exit\n";
  cout<<"Enter your Choice:";
  cin>>ch;

  switch(ch)
  {
    case 1:
      cout<<"Enter Radius of the Circle:";
      cin>>r;
      obj.area(r);
      break;
    case 2:
      cout<<"Enter Sides of the Rectangle:";
      cin>>a>>b;
      obj.area(a,b);
      break;
    case 3:
      cout<<"Enter Sides of the Triangle:";
      cin>>a>>b;
      obj.area(0.5,a,b);
      break;
    case 4:
      exit(0);
  }
  getch();
}
```

## 30. 使用 C++ 编程进行友函数的简单程序

**算法：**

- 步骤 1：启动程序。
- 步骤 2：声明类`base`及其数据成员和成员函数。
- 步骤 3：使用函数`get()`从用户处读取 2 个输入。
- 步骤 4：在类内部声明友函数`mean(base ob)`。
- 步骤 5：在类外定义友函数并执行以下操作。
- 步骤 6：以浮点形式返回平均值`(ob.val1+ob.val2)/2`。
- 步骤 7：停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>
class base
{
    int val1,val2;
public:
    void get()
    {
        cout<<"Enter two values:";
        cin>>val1>>val2;
    }
    friend float mean(base ob);
};
float mean(base ob)
{
    return float(ob.val1+ob.val2)/2;
}
```

（注：由于您提供的原始文本在第 30 题起始处代码块似乎被截断了，我已完全按照您提供的文本结构进行了翻译。）



```cpp
#include<iostream.h>
#include<conio.h>

class student
{
protected:
    int rno,m1,m2;
public:
    void get()
    {
        cout<<"Enter the Roll no :";
        cin>>rno;
        cout<<"Enter the two marks :";
        cin>>m1>>m2;
    }
};

class sports
{
protected:
    int sm; // sm = 体育成绩
public:
    void getsm()
    {
        cout<<"\nEnter the mark :";
        cin>>sm;
    }
};

class statement:public student,public sports
{
    int tot,avg;
    public:
    void display()
    {
        tot=(m1+m2+sm);
        avg=tot/3;
        cout<<"\n\tRoll No : "<<rno<<"\tTotal : "<<"tot;
        cout<<"\n\tAverage : "<<"avg;
    }
};

void main()
{
    clrscr();
    statement obj;
    obj.get();
    obj.getsm();
    obj.display();
    getch();
}
```

**输出:**

```txt
Enter the Roll no: 100
Enter two marks
90
80
Enter the Sports Mark: 90
Roll No: 100
Total : 260
Average: 86.66
```

## 27. 使用 C++ 编程进行内联函数的简单程序

**算法：**

- 步骤 1: 启动程序。
- 步骤 2: 声明类。
- 步骤 3: 声明并定义乘法和立方的内联函数。
- 步骤 4: 声明类对象和变量。
- 步骤 5: 读取两个值。
- 步骤 6: 使用类对象调用内联函数。
- 步骤 7: 返回值。
- 步骤 8: 显示。
- 步骤 9: 停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>

class line
{
public:
    inline float mul(float x,float y)
    {
        return(x*y);
    }
    inline float cube(float x)
    {
        return(x*x);
    }
};

void main()
{
    line obj;
    float val1,val2;
    clrscr();
    cout<<"Enter two values:";
    cin>>val1>>val2;
    cout<<"\nMultiplication value is:"<<obj.mul(val1,val2);
    cout<<"\nCube value is:"<<obj.cube(val1)<<"\t"<<obj.cube(val2);
    getch();
}
```

**输出:**

```txt
Enter two values: 5 7
Multiplication Value is: 35
Cube Value is: 25 and 343
```

## 28. 使用 C++ 编程进行函数模板的简单程序

使用函数模板交换数字。

**算法：**

- 步骤 1: 启动程序。
- 步骤 2: 声明模板类。
- 步骤 3: 声明并定义交换值的函数。
- 步骤 4: 声明并定义获取值的函数。
- 步骤 5: 读取值并调用相应的函数。
- 步骤 6: 显示。
- 步骤 7: 停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>

template<class t>
void swap(t &x,t &y)
{
  t temp=x;
  x=y;
  y=temp;
}

void fun(int a,int b,float c,float d)
{
  cout<<"\na and b before swapping:"<<a<<"\t"<<b;
  swap(a,b);
  cout<<"\na and b after swapping:"<<a<<"\t"<<b;
  cout<<"\nc and d before swapping:"<<c<<"\t"<<d;
  swap(c,d);
  cout<<"\nc and d after swapping:"<<c<<"\t"<<d;
}

void main()
{
    int a,b;
    float c,d;
    clrscr();
    cout<<"Enter A,B values(integer):";
    cin>>a>>b;
    cout<<"Enter C,D values(float):";
    cin>>c>>d;
    fun(a,b,c,d);
    getch();
}
```

**输出:**

```txt
Enter A, B values (integer): 10 20
Enter C, D values (float): 50 10.80
A and B before swapping: 10 20
A and B after swapping: 20 10
C and D before swapping: 50 10.80
C and D after swapping: 10.80 50
```

## 29. 使用 C++ 编程进行函数重载的简单程序

**算法：**

- 步骤 1: 启动程序。
- 步骤 2: 声明类 `fn` 及其数据成员和成员函数。
- 步骤 3: 从用户处读取选择。
- 步骤 4: 选择=1，跳转到步骤 5。
- 步骤 5: 使用一个整数参数的函数计算圆面积。
- 步骤 6: 选择=2，跳转到步骤 7。
- 步骤 7: 使用两个整数参数的函数计算矩形面积。
- 步骤 8: 选择=3，跳转到步骤 9。
- 步骤 9: 使用三个参数（两个整数和一个浮点数）的函数计算三角形面积。
- 步骤 10: 选择=4，停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<stdlib.h>
#include<conio.h>
#define pi 3.14
class fn
{
public:
    void area(int); //circle
    void area(int,int); //rectangle
    void area(float ,int,int); //triangle
};

void fn::area(int a)
{
    cout<<"Area of Circle:"<<pi*a;
}
void fn::area(int a,int b)
{
  cout<<"Area of rectangle:"<<a*b;
}
void fn::area(float t,int a,int b)
{
  cout<<"Area of triangle:"<<t*a*b;
}
void main()
{
  int ch;
  int a,b,r;
  clrscr();
  fn obj;
  cout<<"\n\tFunction Overloading\n";
  cout<<"\n1.Area of Circle\n2.Area of Rectangle\n3.Area of Triangle\n4.Exit\n";
  cout<<"Enter your Choice:";
  cin>>ch;

  switch(ch)
  {
    case 1:
      cout<<"Enter Radius of the Circle:";
      cin>>r;
      obj.area(r);
      break;
    case 2:
      cout<<"Enter Sides of the Rectangle:";
      cin>>a>>b;
      obj.area(a,b);
      break;
    case 3:
      cout<<"Enter Sides of the Triangle:";
      cin>>a>>b;
      obj.area(0.5,a,b);
      break;
    case 4:
      exit(0);
  }
  getch();
}
```

## 30. 使用 C++ 编程进行友函数的简单程序

**算法：**

- 步骤 1: 启动程序。
- 步骤 2: 声明类 `base` 及其数据成员和成员函数。
- 步骤 3: 使用函数 `get()` 从用户处读取 2 个输入。
- 步骤 4: 在类内部声明友函数 `mean(base ob)`。
- 步骤 5: 在类外定义友函数并执行以下操作。
- 步骤 6: 以浮点形式返回平均值 `(ob.val1+ob.val2)/2`。
- 步骤 7: 停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>
class base
{
    int val1,val2;
public:
    void get()
    {
        cout<<"Enter two values:";
        cin>>val1>>val2;
    }
    friend float mean(base ob);
};
float mean(base ob)
{
    return float(ob.val1+ob.val2)/2;
}
```

```cpp
void main()
{
    clrscr();
    base obj;
    obj.get();
    cout<<"\n Mean value is :"<<mean(obj);
    getch();
}
```

**输出：**

```txt
输入两个值: 10, 20
平均值是: 15
```

## 31. 使用 C++ 编程的多 Catch 异常处理简单程序

**算法：**

步骤 1: 启动程序。
步骤 2: 声明并定义函数 `test()`。
步骤 3: 在`try`块中检查值是否大于零。
- a. 如果值大于零，抛出该值并捕获相应的异常。
- b. 否则，抛出字符并捕获相应的异常。
步骤 4: 为函数 `test()` 读取整数和字符值。
步骤 5: 停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>
void test(int x)
{
    try
    {
        if(x>0)
            throw x;
        else
            throw 'x';
    }
    catch(int x)
    {
        cout<<"Catch a integer and that integer is:"<<x;
    }
    catch(char x)
    {
        cout<<"Catch a character and that character is:"<<x;
    }
}

void main()
{
    clrscr();
    cout<<"Testing multiple catches\n:";
    test(10);
    test(0);
    getch();
}
```

**输出:**

```txt
Testing multiple catches
Catch a integer and that integer is: 10
Catch a character and that character is: x
```

## 32. 使用 C++ 编程的除以零异常处理简单程序

**算法：**

步骤 1: 启动程序。
步骤 2: 声明变量 `a`,`b`,`c`。
步骤 3: 读取值 `a`,`b`,`c` 的值。
步骤 4: 在`try`块内部检查条件。
- a. 如果`((a-b)!=0)`，则计算`d`的值并显示。
- b. 否则，抛出异常。
步骤 5: 捕获异常并显示适当的消息。
步骤 6: 停止程序。

**程序：**

```cpp
#include<iostream.h>
#include<conio.h>
void main()
{
    int a,b,c;
    float d;
    clrscr();
    cout<<"Enter the value of a:";
    cin>>a;
    cout<<"Enter the value of b:";
    cin>>b;
    cout<<"Enter the value of c:";
    cin>>c;
    try
    {
        if((a-b)!=0)
        {
            d=c/(a-b);
            cout<<"Result is:"<<d;
        }
        else
        {
            throw(a-b);
        }
    }
    catch(int i)
    {
        cout<<"Answer is infinite because a-b is:"<<i;
    }
    getch();
}
```

**输出:**

```txt
Enter the value for a: 20
Enter the value for b: 20
Enter the value for c: 40
Answer is infinite because a-b is: 0
```

## 33. 使用 C++ 编程的构造函数简单程序

**算法：**

- 步骤 1: 启动程序。
- 步骤 2: 声明类 `Prime` 并带有数据成员和成员函数。
- 步骤 3: 考虑带有整数参数的构造函数 `Prime()`。
- 步骤 4: 调用函数 `calculate()` 并执行以下步骤。
- 步骤 5: 对于 `i=2` 到 `a` 执行。
- 步骤 6: 如果检查 `a%i==0`，则设置 `k=0` 并跳出。
- 步骤 7: 否则将 `k` 值置为 1。
- 步骤 8: 将 `i` 值加 1。
- 步骤 9: 检查 `k` 值是 1 还是 0。
- 步骤 10: 如果是 1，则显示该值 `a` 为素数。
- 步骤 11: 否则显示该值不是素数。
- 步骤 12: 停止程序。

```cpp
#include<iostream.h>
#include<conio.h>
class prime
{
    int a,k,i;
public:
    prime(int x)
    {
        a=x;
    }
    void calculate()
    {
        k=1;
        for(i=2;i<=a/2;i++)
        {
            if(a%i==0)
            {
                k=0;
                break;
            }
            else
            {
                k=1;
            }
        }
    }
    void show()
    {
        if(k==1)
            cout<<"\n\ta is Number.";
        else
            cout<<"\n\ta Not prime.";
    }
};

void main()
{
    clrscr();
    int a;
    cout<<"\n\Enter the Number:";
    cin>>a;
    prime obj(a);
    obj.calculate();
    obj.show();
    getch();
}
```

**输出:**

```txt
Enter the number: 7
Given number is Prime
```

## 34. 使用 C++ 编程的运算符重载简单程序

**算法：**

- 步骤 1: 启动程序。
- 步骤 2: 声明类。
- 步骤 3: 声明变量和成员函数。
- 步骤 4: 使用函数 `getValue()` 获取数字。
- 步骤 5: 定义运算符 `+` 加两个数字。
- 步骤 6: 定义运算符 `-` 减两个数字。
- 步骤 7: 定义显示函数。
- 步骤 8: 声明对象 `obj1`,`obj2` 和 `result`。
- 步骤 9: 使用 `obj1` 和 `obj2` 调用函数。
- 步骤 10: 通过调用运算符 `+` `-` 计算 `result` 对象的值。
- 步骤 11: 使用 `obj1` 和 `obj2` 调用显示函数。
- 步骤 12: 返回值。
- 步骤 13: 停止程序。

**程序：**



```cpp
#include<iostream.h>
#include<conio.h>
class complex
{
    int a,b;
public:
    void getValue()
    {
        cout<<"Enter the value of Complex Numbers a,b:";
        cin>>a>>b;
    }
    complex+(complex ob)
    {
        complex t;
        t.a=a+ob.a;
        t.b=b+ob.b;
        return(t);
    }
    complex-(complex ob)
    {
        complex t;
        t.a=a-ob.a;
        t.b=b-ob.b;
        return(t);
    }
    void display()
    {
        cout<<a<<"+"<<b<<"\n";
    }
};

void main()
{
    clrscr();
    complex obj1,obj2,result,result1;

    obj1.getValue();
    obj2.getValue();
    result = obj1+obj2;
    result1=obj1-obj2;
    cout<<"Input Values:\n";
    obj1.display();
    obj2.display();
    cout<<"Result:";
    result.display();
    result1.display();
    getch();
}
```

**输出:**

Enter the value of Complex Numbers a, b

4

5

Enter the value of Complex Numbers a, b

2

2

Input Values

4 + 5

2 + 2

Result

6 + 7

2 + 3

## 35. 使用 C++ 编程的结构体变量输入简单程序

```cpp
#include<iostream.h>
#include<stdio.h>

struct books
{
    char name[20],author[20];
} a[50];

int main()
{
    int i,n;
    cout<<"No Of Books[less than 50]:";
    cin>>n;
    cout<<"Enter the book details\n";
    cout<<"------------------------\n";

    for(i=0;i<n;i++)
    {
        cout<<"Details of Book "<<i+1<<"\n";
        cout<<"Book Name :";
        cin>>a[i].name;
        cout<<"Book Author :";
        cin>>a[i].author;
        cout<<"------------------------\n";
    }
    cout<<"==================\n";
    cout<<"S.No\t|Book Name\t|author\n";
    cout<<"=====================";
    for(i=0;i<n;i++)
    {
        cout<<"\n"<<i+1<<"\t"<<a[i].name<<"t"<<a[i].author;
    }
    cout<<"\n=====================";

    return 0;
}
```

**输出 :**

No Of Books[less than 50]:2

Enter the book details

Details of Book No 1

Book Name :Programming

Book Author :Dromy

Details of Book No 2

Book Name :C

Book Author :Byron

| S.No | Book Name | author |
|---|---|---|
| 1 | Programming | Dromy |
| 2 | C | Byron |

## 36. 使用 C++ 编程的写操作简单程序

算法：

- 步骤 1: 启动程序。
- 步骤 2: 声明变量。
- 步骤 3: 读取文件名。
- 步骤 4: 打开文件写入内容。
- 步骤 5: 写入文件到特定条件。
- 步骤 6: 停止程序。

程序：

```cpp
#include<iostream.h>
#include<stdio.h>
#include<conio.h>
#include<fstream.h>

void main()
{
    char c,fname[10];
    ofstream out;
    cout<<"Enter File name:";
    cin>>fname;
    out.open(fname);
    cout<<"Enter contents to store in file (Enter # at end):\n";
    while((c=getch())!='#')
    {
        out<<c;
    }
    out.close();
    getch();
}
```

**输出:**

Enter File name: one.txt

Enter contents to store in file (enter # at end)

Master of Computer Applications

## 37. 使用 C++ 编程的虚函数简单程序

算法：

- 步骤 1: 启动程序。
- 步骤 2: 声明基类 class。
- 步骤 3: 声明并定义虚函数 `show()`。
- 步骤 4: 声明并定义函数 `display()`。
- 步骤 5: 从基类创建派生类。
- 步骤 6: 声明并定义函数 `display()` 和 `show()`。
- 步骤 7: 创建基类对象和指针变量。
- 步骤 8: 使用基类对象和指针调用 `display()` 和 `show()` 函数。
- 步骤 9: 创建派生类对象并使用派生类对象和指针调用 `display()` 和 `show()` 函数。
- 步骤 10: 停止程序。

程序：

```cpp
#include<iostream.h>
#include<conio.h>
class base
{
public:
    virtual void show()
    {
        cout<<"\n Base class show:";
    }
    void display()
    {
        cout<<"\n Base class display:";
    }
};

class drive:public base
{
    public:
    void display()
    {
        cout<<"\n Drive class display:\n";
    }
    void show()
    {
        cout<<"\n Drive class show:\n";
    }
};

void main()
{
    clrscr();
    base obj1;
    base *p;
    cout<<"\n\t P points to base:\n";

    p=&obj1;
    p->display();
    p->show();

    cout<<"\n\n\t P points to drive:\n";
    drive obj2;
    p=&obj2;
    p->display();
    p->show();
    getch();
}
```

**输出:**

P 指向 Base

Base 类显示

Base 类显示

P 指向 Drive

Base 类显示

Drive 类显示

## 38. 使用 C++ 编程虚拟基类的简单程序

算法：

- 步骤 1: 开始程序。
- 步骤 2: 声明基类 `student`。
- 步骤 3: 声明并定义函数 `getnumber()` 和 `putnumber()`。
- 步骤 4: 创建虚拟继承自基类 `student` 的派生类 `test`。
- 步骤 5: 声明并定义函数 `getmarks()` 和 `putmarks()`。
- 步骤 6: 创建虚拟继承自基类 `student` 的派生类 `sports`。
- 步骤 7: 声明并定义函数 `getscore()` 和 `putscore()`。
- 步骤 8: 创建继承自 `test` 和 `sports` 的派生类 `result`。
- 步骤 9: 声明并定义函数 `display()` 以计算总和。
- 步骤 10: 创建派生类对象 `obj`。
- 步骤 11: 调用函数 `getnumber()`, `getmarks()`, `getscore()` 和 `display()`。
- 步骤 12: 停止程序。

程序：

```cpp
#include<iostream.h>
#include<conio.h>

class student
{
    int rno;
public:
    void getnumber()
    {
        cout<<"Enter Roll No:";
        cin>>rno;
    }
    void putnumber()
    {
        cout<<"\n\tRoll No:"<<rno<<"\n";
    };
};

class test:virtual public student
{
public:
    int part1,part2;
    void getmarks()
    {
        cout<<"Enter Marks\n";
        cout<<"Part1:";
        cin>>part1;
        cout<<"Part2:";
        cin>>part2;
    }

    void putmarks()
    {
        cout<<"\n\tMarks Obtained\n";
        cout<<"\n\tPart1:"<<part1;
        cout<<"\n\tPart2:"<<part2;
    }
};

class sports:public virtual student
{
public:
    int score;
    void getscore()
    {
      cout<<"Enter Sports Score:";
      cin>>score;
    }

    void postscore() {
      cout<<"\n\tSports Score is:"<<score;
    };
};

class result:public test,public sports {
  int total;
  public:
  void display() {
    total=part1+part2+score;
    putnumber();
    putmarks();
    postscore();
    cout<<"\n\tTotal Score:"<<total;
  }
};

void main() {
  result obj;
  clrscr();
  obj.getnumber();
  obj.getmarks();
  obj.getscore();
  obj.display();
  getch();
}
```

**输出：**

Enter Roll No: 200

Enter Marks

Part1: 90

Part2: 80

Enter Sports Score: 80

Roll No: 200

Marks Obtained

Part1: 90

Part2: 80

Sports Score is: 80

Total Score is: 250

## 39. 使用 C++ 编程一运算符重载的简单程序

编写一个使用一运算符重载查找复数的程序。

算法：

- 步骤 1: 开始程序。
- 步骤 2: 声明类。
- 步骤 3: 声明变量及其成员函数。
- 步骤 4: 使用 `getValue()` 函数获取两个数字。
- 步骤 5: 定义运算符 `++` 来增加值。
- 步骤 6: 定义运算符 `--` 来减小值。
- 步骤 7: 定义显示函数。
- 步骤 8: 声明类对象。
- 步骤 9: 调用函数 `getValue()`。
- 步骤 10: 通过增加类对象来调用运算符 `++` 并调用显示。
- 步骤 11: 通过减小类对象来调用运算符 `--` 并调用显示。
- 步骤 12: 停止程序。

程序：

```cpp
#include<iostream.h>
#include<conio.h>

class complex
{
    int a,b,c;
public:
    complex(){}
    void getValue()
    {
      cout<<"Enter the Two Numbers:";
      cin>>a>>b;
    }
    void operator++()
    {
      a++;
      b++;
    }
    void operator--()
    {
      a--;
      b--;
    }
    void display()
    {
      cout<<a<<"\t"<<b<<endl;
    }
};

void main()
{
  clrscr();
  complex obj;
  obj.getvalue();
  obj++;
  cout<<"Increment Number\n";
  obj.display();
  obj--;
  cout<<"Decrement Number\n";
  obj.display();
  getch();
}
```

**输出：**

Enter the two numbers: 3 6

Increment Number

4 7

Decrement Number

3 6

## 40. 使用 C++ 编程静态数据和成员函数的简单程序

算法：

- 步骤 1: 开始程序。
- 步骤 2: 声明类名为 `Stat`，并带有数据成员和成员函数。
- 步骤 3: 构造函数 `Stat()` 用于将 `count` 的值增加为 1 以分配变量。
- 步骤 4: 函数 `showcode()` 显示代码。
- 步骤 5: 函数 `showcount()` 显示计数值。
- 步骤 6: 停止程序。

程序：

```cpp
#include<iostream.h>
#include<conio.h>

class stat
{
    int code;
    static int count;

public:
    stat()
    {
        count++;
    }
    void showcode()
    {
        cout<<"\nCode:"<<code;
    }
    static void showcount()
    {
        cout<<"\nCount is:"<<count;
    }
};

int stat::count=0;

void main()
{
    clrscr();
    stat obj1,obj2;
    obj1.showcount();
    obj1.showcode();
    obj2.showcount();
    obj2.showcode();
    getch();
}
```

**输出：**

Count: 2

Code:

## 41. 使用 C++ 编程实现单继承的简单程序

算法：

- 步骤 1: 开始程序。
- 步骤 2: 声明基类 `emp`。
- 步骤 3: 定义函数 `get()` 以获取学号。
- 步骤 4: 创建派生类 `salary`。
- 步骤 5: 定义函数 `get1()` 以获取各项费用。
- 步骤 6: 定义函数 `calculate()` 以计算净薪。
- 步骤 7: 定义函数 `display()` 显示结果。
- 步骤 8: 创建派生类对象 `s`。
- 步骤 9: 调用函数 `get()`, `get1()`, `calculate()` 和 `display()`。
- 步骤 10: 停止程序。

程序：



```cpp
#include<iostream.h>
#include<conio.h>

class emp
{
public:
    int eno;
    char name[20],des[20];
    void get()
    {
        cout<<"Enter roll number:";
        cin>>eno;
    }
};

class salary:public emp
{
    float bp,hra,da,pf;
public:
    void get1()
    {
        cout<<"Enter basic pay:";
        cin>>bp;
        cout<<"Enter HR allowance:";
        cin>>hra;
        cout<<"Enter deness allowance:";
        cin>>da;
        cout<<"Enter PF fund:";
        cin>>pf;
    }
    void calculate()
    {
        np=bp+hra+da-pf;
    }
    void display()
    {
        cout<<"\nPayroll SYSTEM\n";
        cout<<"\neno\tname\tdes\tbp\thra\tda\tpf\tnp";
        cout<<"\n"%(eno<<"\t"%(name<<"\t"%(des<<"\t"%(bp<<"\t"%(hra<<"\t"%(da<<"\t"%(pf<<"\t"%(np;
    }
    float np;
};

void main()
{
    int i,n;
    salary s[10];
    clrscr();
    cout<<"Enter number of employees:";
    cin>>n;
    for(i=0;i<n;i++) {
        s[i].get();
        s[i].get1();
        s[i].calculate();
    }
    for(i=0;i<n;i++) {
        s[i].display();
    }
    getch();
}
```

## 输出

Enter number of employees:2

Enter roll number:101

Enter basic pay:5000

Enter HR allowance:1000

Enter dearness allowance:500

Enter PF fund:300

Enter roll number:102

Enter basic pay:6000

Enter HR allowance:1200

Enter dearness allowance:600

Enter PF fund:400

Payroll SYSTEM

101	ram	Manager	5000	1000	500	300	6200

102	sham	clerk	6000	1200	600	400	7400

## 42. 使用 C++ 编程拷贝构造简单程序

### 算法

- 步骤 1：开始程序。
- 步骤 2：声明类名为 `Copy`，带有数据成员和成员函数。
- 步骤 3：构造函数 `Copy()` 带参数以赋值值。
- 步骤 4：调用函数 `calculate()` 执行以下步骤。
- 步骤 5：对于 `i=1` 到 `var` 执行。
- 步骤 6：计算 `fact*i` 并赋值给 `fact`。
- 步骤 7：增加值为 1。
- 步骤 8：返回值 `fact`。
- 步骤 9：打印结果。
- 步骤 10：停止程序。

### 程序

```cpp
#include<iostream.h>
#include<conio.h>

class copy
{
    int var,fact;
public:
    copy(int temp)
    {
        var = temp;
    }
    double calculate()
    {
        fact=1;
        for(int i=1; i<=var; i++)
        {
            fact=fact*i;
        }
        return fact;
    }
};

void main()
{
    int n;
    clrscr();
    cout<<"Enter a number:";
    cin>>n;
    copy obj(n);
    cout<<"Factorial of "<<n<<" is "<<obj.calculate();
    getch();
}
```

### 输出

Enter a number:5

Factorial of 5 is 120

```cpp
for(int i=1;i<=var;i++)
{
    fact = fact * i;
    return fact;
}
void main()
{
    clrscr();
    int n;
    cout<<"\n\tEnter the Number : ";
    cin>>n;
    copy obj(n);
    copy cpy=obj;
    cout<<"\n\t"<<n<<" Factorial is:"<<obj.calculate();
    cout<<"\n\t"<<n<<" Factorial is:"<<cpy.calculate();
    getch();
}
```

### 输出

输入数字：5

阶乘为：120

阶乘为：120

## 43. 使用 C++ 编程读取文件操作的简单程序

读取文件内容的程序。

### 算法

- 步骤 1：启动程序。
- 步骤 2：声明变量。
- 步骤 3：获取要读取的文件。
- 步骤 4：使用 `ifstream(filename)` 检查文件是否存在。
- 步骤 5：如果文件存在，则检查文件结束条件。
- 步骤 6：读取文件内容。
- 步骤 7：打印文件内容。
- 步骤 8：停止程序。

### 程序

```cpp
#include<iostream.h>
#include<conio.h>
#include<fstream.h>
void main()
{
    char c,fname[10];
    clrscr();
    cout<<"Enter file name:";
    cin>>fname;
    ifstream in(fname);
    if(!in)
    {
        cout<<"File Does not Exist";
        getch();
        return;
    }
    cout<<"\n\n";
    while(in.eof()==0)
    {
        in.get(c);
        cout<<c;
    }
    getch();
}
```

### 输出

输入文件名：one.txt

## 44. 使用 C++ 编程读取与写入文件操作（将小写转换为大写）的简单程序

### 算法

- 步骤 1：启动程序。
- 步骤 2：声明变量。
- 步骤 3：读取文件名。
- 步骤 4：打开文件写入内容。
- 步骤 5：写入文件内容直到达到特定条件。
- 步骤 6：将文件内容以大写形式写入。
- 步骤 7：打开文件读取内容。
- 步骤 8：停止程序。

### 程序

```cpp
#include<fstream.h>
#include<stdio.h>
#include<ctype.h>
#include<string.h>
#include<iostream.h>
#include<conio.h>

void main()
{
    char c,u;
    char fname[10];
    clrscr();
    ofstream out;
    cout<<"Enter File Name:";
    cin>>fname;
    out.open(fname);
    cout<<"Enter the text(Enter # at end)\n"; //将内容写入文件
    while((c=getchar())!='#')
    {
        u=c-32;
        out<<u;
    }
    out.close();
    ifstream in(fname); //读取文件内容
    cout<<"\n\n\tThe File contains\n\n";
    while(in.eof()==0)
    {
        in.get(c);
        cout<<c;
    }
}
```

### 输出

输入文件名：two.txt

要存储在文件中的内容（在末尾输入 `#`）

```text
oops programming
```

文件包含

```text
OOPS PROGRAMMING
```

## 45. 两个两个整数相和的 C++ 程序

```cpp
#include <iostream.h>

main() {
    // 一个简单的 C++ 程序
    int x, y, sum;
    cout << "A program which adds two integers\n";
    cout << "Enter 1st integer: ";
    cin >> x;
    cout << "Enter 2nd integer: ";
    cin >> y;
    sum = x + y;
    cout << "Sum is " << sum << endl;

    return 0;
}
```

### 输出

一个将两个整数相和的程序

输入第一个整数：3

输入第二个整数：4

和为 7

## 46. 输出整数、浮点数和字符的 C++ 程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int x = 10;
    float y = 10.1;
    char z = 'a';
    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
    cout << "z = " << z << endl;
    getch();
}
```

此程序为整数 `x`、浮点数 `y` 和字符 `z` 定义了预定义值。

这三个值使用 `cout` 命令输出。

### 输入

此程序没有从用户的输入。

### 输出

```text
x = 10
y = 10.1
z = a
```

## 47. 计算两个整数之和、差、积、商的 C++ 程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int x = 10;
    int y = 2;
    int sum, difference, product, quotient;
    sum = x + y;
    difference = x - y;
    product = x * y;
    quotient = x / y;
    cout << "The sum of " << x << " + " << y << " is " << sum << endl;
    cout << "The difference of " << x << " - " << y << " is " << difference << endl;
    cout << "The product of " << x << " * " << y << " is " << product << endl;
    cout << "The quotient of " << x << " / " << y << " is " << quotient << endl;
    getch();
}
```

此程序为两个整数定义了预定义值。

这两个值的和、差、积、商被计算出来，然后使用 `cout` 命令输出。

### 输出

10 + 2 的和为 12。

10 - 2 的差为 8。

10 * 2 的积为 20。

10 / 2 的商为 5。

## 48. 输入两个整数并计算它们的和和平均值的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int x,y;
    int sum;
    float average;
    cout << "Enter integers: ";
    cin>>x>>y;
    sum=x+y;
    average=sum/2;
    cout << "The sum of " << x << " and " << y << " is " << sum << endl;
    cout << "The average of " << x << " and " << y << " is " << average << endl;
    getch();
}
```

此程序从用户处通过屏幕输入 `x` 和 `y`。

这两个整数的和和平均值被计算出来，并使用 `cout` 命令输出。

### 输入

```text
8 6
```

### 输出

8 和 6 的和为 14。

8 和 6 的平均值为 7。

## 49. 输入速度、加速度和时间并使用公式 `v = u + a * t` 打印最终速度的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int v,u,a,t;
    cout << "Enter the velocity, acceleration, time as integers : " << endl;
    cin>>u>>a>>t;
    v=u+a*t;
    cout << "The final velocity is " << v << endl;
    getch();
}
```

此程序从用户处通过屏幕输入速度、加速度和时间。

最终速度使用公式 `v = u + a * t` 计算，然后使用 `cout` 命令输出。

### 输入

```text
20 10 5
```

### 输出

最终速度为 70。

## 50. 输入你的年龄并打印是否应该在 10 年级的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int age;
    cout << "Enter age : " << endl;
    cin>>age;
    if(age==16)
    {
        cout << "Your age is " << age << " years." << endl;
        cout << "You are of the right age for joining 10 !" << endl;
    }
    else
    {
        cout << "Your age is " << age << " years." << endl;
        cout << "You are not of the right age for joining 10 !" << endl;
    }
    getch();
}
```

此程序从用户处通过屏幕输入年龄。

程序使用 `IF-ELSE` 命令告诉用户是否应该进入 10 年级。

### 输入

```text
15
```

### 输出

你的年龄是 15 岁。

你不是进入 10 年级的年龄！

## 51. 输入整数并打印它是否大于或小于 100 的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main(){
    clrscr();
    int x;

    cout << "Enter an integer : " << endl;
    cin>>x;

    if(x>100)
    {
        cout << x << " is greater than 100." << endl;
    }
    else
    {
        cout << x << " is less than 100." << endl;
    }
    getch();
}
```

此程序从用户处通过屏幕输入整数 `x`。

程序使用 `IF-ELSE` 命令告诉用户该整数是大于 100 还是小于 100。

使用 `cout` 命令输出结果。

### 输入

```text
74
```

### 输出

74 小于 100。

## 52. 输入整数并输出其 15 倍的程序

```cpp
#include <iostream.h>
#include <conio.h>

int main()
{
    clrscr();
    int x;
    cout << "Enter an integer less than 185 : ";
    cin>>x;
    cout << "The first 15 multiples of " << x << " are : ";
    for(int y=1;y<16;y++)
    cout << "\n" << x << " x " << y << =" << x*y;

    getch();
    return 0;
}
```

此程序从用户处通过屏幕输入整数 `x`。

它随后计算该整数的前 15 倍数，并使用 `cout` 命令输出。

### 输入

```text
12
```

### 输出

12 的前 15 倍为：

```text
12x1=12
```



12x2=24

12x3=36

12x4=48

12x5=60

12x6=72

12x7=84

12x8=96

12x9=108

12x10=120

12x11=132

12x12=144

12x13=156

12x14=168

12x15=180

12x4=48

12x5=60

12x6=72

12x7=84

12x8=96

12x9=108

12x10=120

12x11=132

12x12=144

12x13=156

12x14=168

12x15=180

## 53. 输入两个整数并打印它们的商和余数的程序

```cpp
#include <iostream.h>
#include <conio.h>
int main()
{
  clrscr();
 int x,y,quotient,remainder;
  cout << "Enter 2 integers greater than 0 : ";
  cin>>x>>y;
  quotient=x/y;
  remainder=x-(quotient*y);
  cout << "Quotient of " << x << " & " << y << " = " << quotient << "\n";
  cout << "Remainder" << " = " << remainder << "\n";
  getch();
  return 0;
}
```

该程序从用户处获取两个整数`x`和`y`。然后它计算它们的商和余数，并使用`cout`命令输出它们。

输入：

23 4

输出：

Quotient of 23 & 4 = 5

Remainder = 3

## 54. 输入一个整数并判断是偶数还是奇数的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
clrscr();
int x;
cout << "Enter an integer : ";
cin>>x;
if(x%2==0)
cout << "The number " << x << " is even.";
else
cout << "The number " << x << " is odd.";
getch();
}
```

该程序从用户处获取一个整数`x`。然后它确定该整数是奇数还是偶数，并使用`cout`命令输出相应的信息。

输入：

86

输出：

The number 86 is even.

## 55. 修改前景颜色并在屏幕上画圆的程序

```cpp
#include <conio.h>
#include <graphics.h>
#include <stdlib.h>
#include <stdio.h>

void main (int DETECT,
{
int gdriver=DETECT,gmode,errorcode;//请求自动检测。
int mid,y,x;
// 初始化图形和局部变量。
initgraph(&gdriver,&gmode,"d:\bc3\bgi");
// 读取初始化结果。
errorcode=graphresult();
if(errorcode!=grOk)
// 发生错误。
{
printf("Graphics error occurred: %s \n",grapherrormsg(errorcode));
printf("Press any key to stop : ");
getch();
exit(1); // 由于错误终止程序。
}
/*更改前景颜色。
注意：按回车键退出最后一个屏幕，因为它是黑色的，
可能看起来程序已经停止运行。*/
for(x=15;x>=0;x--)
{
setcolor(x);
}
20+(x*40),200,50);/*每次改变 x 坐标，以便圆圈不重叠。*/
get();
}
cleardevice(); // 在图形模式下清除屏幕。
circle(200,200,50);
get();
closegraph();
}
```

该图形程序使用`setcolor`命令将屏幕上的前景颜色从白色逐渐变为黑色，依次绘制该前景颜色的圆。

## 56. 画两个矩形并填充其中一个的程序

```cpp
#include <iostream.h>
#include <conio.h>
#include <graphics.h>
#include <ctype.h>
#include <stdlib.h>
#include <stdio.h>

void main()
{
clrscr();
int gd = DETECT,gm,errorcode; // 请求自动检测。

// 初始化图形和局部变量。
initgraph(&gd,&gm,"d:\bc3\bgi"); // 图形驱动程序的安装路径

// 读取初始化结果。
errorcode = graphresult();

// 发生了错误。
if (errorcode != grOk)
{
cout << "Graphics error occured : \n" << grapherrormsg(errorcode) << endl;
cout << "Press any key to stop : ";
getch();
exit(1);
}

/*绘制一个左上角顶点在 (300, 300)
且右下角顶点在 (600, 400) 的矩形*/
rectangle(300, 300, 600, 400);
rectangle(100, 100, 200, 200);
floodfill(150, 150, WHITE); // 填充第一个矩形的示例
getch();
closegraph();
}
```

该图形程序绘制两个矩形，但仅使用`fill`命令将其中一个填充为白色。

## 57. 输入三个整数并输出最大的程序

```cpp
#include <iostream.h>
#include <conio.h>
int main()
{
clrscr();
int x,y,z,biggest;
cout << "Enter 3 integers : ";
cin>>x>>y>>z;
if(x>y && x>z)
biggest=x;
else if(y>x && y>z)
biggest=y;
else
biggest=z;
cout << "The largest integer is " << biggest;
getch();
return 0;
}
```

该程序从屏幕输入获取三个整数`x`, `y`和`z`。然后它确定最大的值并输出它。

## 58. 输入一个整数并打印其平方的程序

```cpp
#include <iostream.h>
#include <conio.h>
void main()
{
clrscr();
int x;
cout << "Enter an integer : ";
cin>>x;
cout << "The square of " << x << " is " << x*x << endl;
getch();
}
```

该程序获取一个整数并计算并打印它的平方。

## 59. 修改屏幕颜色的程序

```cpp
#include <conio.h>
#include <graphics.h>

void main (int DETECT,
{
int gdriver=DETECT,gmode,errorcode;
initgraph(&gdriver,&gmode,"d:\bc3\bgi");
errorcode=graphresult();
if(errorcode!=grOk)
{
printf("Graphics error occurred: %s \n",grapherrormsg(errorcode));
exit(1);
}
for(x=15;x>=0;x--)
{
setcolor(x);
}
closegraph();
}
```

该图形程序逐渐改变颜色。

## 60. 输入三个整数并输出商和余数的程序

```cpp
#include <iostream.h>
#include <conio.h>
int main()
{
clrscr();
int x,y,z,quotient,remainder;
cout << "Enter 3 integers greater than 0 : ";
cin>>x>>y>>z;
quotient=x/y;
remainder=x-(quotient*y);
cout << "Quotient of " << x << " & " << y << " = " << quotient << "\n";
cout << "Remainder" << " = " << remainder << "\n";
getch();
return 0;
}
```

## 61. 输入一个整数并打印其后继程序的

```cpp
#include <iostream.h>
#include <conio.h>
void main()
{
clrscr();
int x;
cout << "Enter an integer : ";
cin>>x;
cout << "The successor of " << x << " is ";
value(x);
getch();
}

void value(int x)
{
x++;
cout << x << "." << endl;
}
```

## 62. 输入一个整数并输出该整数立方方的程序

```cpp
#include <iostream.h>
#include <conio.h>
int cube(int x);

void main()
{
clrscr();
int a;
cout << "Enter an integer : ";
cin>>a;
cout << "The cube of " << a << " is : " << cube(a) << endl;
getch();
}

int cube(int x)
{
int y;
y=x*x*x;
return(y);
}
```

输出：

8 的立方方是：512

## 63. 输入字符串并找到其长度的程序

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

void main()
{
  clrscr();
  int length;
  char x[81]; //允许用户输入最多 80 个字符。
  cout << "Enter the string : " << endl;
  cin>>x;
  length=strlen(x);
  cout << "The length of the string " << x << " is " << length << "." << endl;
  getch();
}
```

该程序从用户处获取一个字符串`x`。然后它使用`strlen`函数确定字符串的长度。最后使用`cout`命令输出该长度。

输入：

goldfish

输出：

字符串 goldfish 的长度为 8。

## 64. 在不同用例之间切换的程序

```cpp
#include <iostream>
#include <conio.h>
int main()
{
  clrscr();
  int choice;
  cout << "1. Talk" << endl;
  cout << "2. Eat" << endl;
  cout << "3. Play" << endl;
  cout << "4. Sleep" << endl;
  cout << "Enter your choice : " << endl;
  cin>>choice;
  switch(choice) {
    case 1 : cout << "You chose to talk...talking too much is a bad habit." << endl;
    break;
    case 2 : cout << "You chose to eat...eating healthy foodstuff is good." << endl;
    break;
    case 3 : cout << "You chose to play...playing too much everyday is bad." << endl;
    break;
    case 4 : cout << "You chose to sleep...sleeping enough is a good habit." << endl;
    break;
    default : cout << "You did not choose anything...so exit this program." << endl;
  }
  getch();
}
```

该程序获取用户的选择作为屏幕输入。根据用户的选择，它在不同的用例之间切换。然后使用`cout`命令输出适当的消息。

输入：

```
3
```

输出：

你选择了玩耍……每天玩得太多是不好的。

## 65. 输入本金、利率和时间并打印单利的程序

```cpp
#include <iostream.h>
#include <conio.h>
```

```cpp
void main()
{
clrscr();
int x;
float sinterest,principal,rate,time;
for(x=4;x>=0;x--)
{
cout << "Enter the principal, rate & time : " << endl;
cin>>principal>>rate>>time;
sinterest=(principal*rate*time)/100;
cout << "Principal = $" << principal << endl;
cout << "Rate = " << rate << "%" << endl;
cout << "Time = " << time << " years" << endl;
cout << "Simple Interest = $" << sinterest << endl;
}
getch();
}
```

该程序从用户处获取本金、利率和时间作为屏幕输入。程序使用`FOR`循环执行 5 次。它使用公式 I = PTR/100 计算单利。然后使用`cout`命令输出本金、利率、时间以及单利。

输入：

1000 5 3

输出：

Principal = $1000

Rate = 5%

Time = 3 years

Simple Interest = $150

## 66. 输入整数并打印是否是质数还是合数的程序

```cpp
#include <iostream.h>
#include <conio.h>
#include <process.h>

void main()
{
  clrscr();
  int num1,x;
  cout << "Enter an integer : " << endl;
  cin>>num1;
  for(x=2;x<num1;x++)
{
    if(num1%x==0)
    {
      cout << num1 << " is a composite number." << endl;
      getch();
      exit(0);
    }
    else
    {
      cout << num1 << " is a prime number." << endl;
      getch();
      exit(0);
    }
  }
}
```

该程序从用户处获取一个整数`num1`。然后它确定该整数是质数还是合数。最后通过写入`cout`流输出适当的消息。

输入：

23

输出：

23 是一个质数。

## 67. 输入销售额并打印代理佣金的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
clrscr();
long int svalue;
float commission;
cout << "Enter the sale value : " << endl;
cin>>svalue;
if(svalue<=10000)
{
commission=svalue*5/100;
cout << "For a total sale value of $" << svalue << ", ";
cout << "the agent's commission is $" << commission;
}
getch();
}
```

该程序从用户处获取总销售额作为屏幕输入。程序通过`IF-ELSE`命令计算代理佣金，如下：

- 销售额小于等于 $10000 时，佣金为 5%

- 销售额小于等于 $25000 时，佣金为 10%

- 销售额大于 $25000 时，佣金为 20%

然后使用`cout`命令输出账单。

输入：

26000

输出：

销售额为 $26000 的代理佣金为 $5200

## 68. 输入读数并输出客户账单的程序



```cpp
#include <iostream.h>
#include <conio.h>

int main()
{
    clrscr();
    long int units, charge = 0;
    float total;
    const int rent = 25;

    cout << "Enter the number of units : ";
    cin >> units;

    if (units > 200)
        charge = (units - 200) * 20 + 150 * 40 + 50 * 60;
    else if (units > 50)
        charge = (units - 50) * 40 + 50 * 60;
    else
        charge = units * 60;

    total = 0 * charge + rent;

    cout << "You have used " << units << " units.";
    cout << "Your total bill is $" << total;

    getch();
    return 0;
}
```

该程序从用户处获取用电量作为屏幕输入。

它根据以下标准计算客户的电话账单：

- 强制费用 $25
- 前 50 个单位每单位 60 分分
- 接下来的 150 个单位每单位 40 分分
- 200 个单位以上每单位 20 分分

然后使用`cout`命令输出账单。

输入：

250

输出：

你使用了 250 个单位。

总账单为 $125

# 69. 查找今年截至目前的天数的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int day, month, total;
    int days_per_month[12] = {31, 28, 31, 30, 31, 30, 31, 30, 31, 30, 31};

    cout << "Enter the month : " << endl;
    cin >> month;
    cout << "Enter the day : " << endl;
    cin >> day;

    total = day;

    for (int x = 0; x < month - 1; x++)
        total += days_per_month[x];

    cout << "The number of days in this year till date = " << total << endl;

    getch();
}
```

该程序从用户处获取当前的日期和月份。

它计算今年截至目前的总天数，并使用`cout`命令输出。

输入：

612

输出：

今年截至目前的天数为 163

# 70. 计算斐波那契数列的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int a, b, x, y, num1, ct;
    a = 0;
    b = 1;

    cout << "Enter the number of terms (less than 25) : " << endl;
    cin >> num1;

    cout << a << endl;
    cout << b << endl;

    for (ct = 1; ct <= num1 - 2; ct++)
    {
        x = a + b;
        cout << x << endl;
        y = a;
        a = b;
        b = x;
    }

    getch();
}
```

该程序从用户处获取斐波那契数列的项数`num1`（小于 25）作为屏幕输入。

然后它计算斐波那契数列并使用`cout`命令打印出来。

输入：

12

输出：

0

1

2

3

5

8

13

21

34

55

89

# 71. 输入整数并根据公式打印其总值的程序

# `x - 1/3!x^3 + 1/5!x^5 - 1/7!x^7 + 1/9!x^9`

```cpp
#include <iostream.h>
#include <conio.h>
#include <math.h>

int main()
{
    clrscr();
    float factorial = 1;
    float num, tot, term, total;
    int i, n = 20, index, j = 1;

    cout << "Enter a single-digit integer : \n";
    cin >> num;

    tot = num;
    total = num;

    for (i = 2, index = 3; i <= n; i++, index += 2)
    {
        for (j = 1, factorial = 1; j <= index; j++)
            factorial *= j;

        tot = tot * pow((double)(-1), (double)(2 * i - 1)) * num * num;
        term = tot / factorial;
        total += term;
    }

    cout << "Total = " << total << endl;

    getch();
    return 0;
}
```

该程序从用户处获取一个整数`num`作为屏幕输入。

然后它根据公式`x - 1/3!x^3 + 1/5!x^5 - 1/7!x^7 + 1/9!x^9`计算该整数的总值。

然后它使用`cout`命令输出最终答案。

# 输入：

3

# 输出：

Total = 0.14112

## 72. 将天数转换为年和周的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int days, years, weeks, num1;

    cout << "请输入天数 : " << endl;
    cin >> days;

    years = days / 365;
    num1 = days - (years * 365);

    weeks = days / 7;
    num1 = days - (weeks * 7);

    cout << days << " days = " << endl;
    cout << weeks << " weeks OR = " << endl;
    cout << years << " years." << endl;

    getch();
}
```

该程序从用户处通过屏幕输入天数。

它将天数转换为年和周，并使用`cout`命令输出。

输入：

789

输出：

789 days =

112 weeks OR

2 years.

## 73. 求解二次方程根的程序

```cpp
#include <iostream.h>
#include <conio.h>
#include <math.h>

int main()
{
    clrscr();
    float a, b, c, d, root1, root2;

    cout << "输入三个系数 a, b, c : " << endl;
    cin >> a >> b >> c;

    if (!a)
    {
        if (!b)
        {
            cout << "ax^2 + bx + c = 0 中 a 和 b 都不能为 0" << "\n";
        }
        else
        {
            d = -c / b;
            cout << "线性方程的解为 : " << d << endl;
        }
    }
    else
    {
        d = b * b - 4 * a * c;

        if (d > 0)
            root1 = (-b + sqrt(d)) / (2 * a);
            root2 = (-b - sqrt(d)) / (2 * a);

        cout << "第一个根 = " << root1 << endl;
        cout << "第二个根 = " << root2 << endl;
    }

    getch();
    return 0;
}
```

该程序从用户处通过屏幕输入三个系数`a`、`b`和`c`的值。

然后它使用公式`ax^2 + bx + c = 0`确定二次方程的根。

最后使用`cout`命令输出这两个根。

# 输入：

4 4 -3

# 输出：

第一个根 = 0.5

第二个第二个根 = -1.5

## 74. 输入整数并以反转形式输出的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    long int num1, num2, rnum = 0;

    cout << "输入一个整数 : " << endl;
    cin >> num1;

    num2 = num1;

    do
    {
        rnum = rnum * 10;
        int digit = num1 % 10;
        rnum += digit;
        num1 /= 10;
    }
    while (num1);

    cout << "你输入的整数是 " << num2 << "." << endl << endl;
    cout << "反转后的整数是 " << rnum << "." << endl << endl;

    getch();
}
```

该程序从用户处通过屏幕输入整数`num1`。

它使用`cout`命令输出该整数的反转形式。

输入：

# 输出：

你输入的整数是 987。

反转后的整数是 789。

## 75. 统计句子中单词数和字符数的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    int count = 0;
    int countwd = 1;

    cout << "输入你的小写句子: " << endl;

    char ch = 'a';

    while (ch != 'a')
    {
        ch = getch();

        if (ch == ' ')
            countwd++;
        else
            count++;
    }

    cout << "\n 单词数 = " << countwd << endl;
    cout << "字符数 = " << count - 1 << endl;

    getch();
}
```

该程序从用户处通过屏幕输入一个句子。

然后它使用`WHILE`循环确定句子中的单词数和字符数，并使用`cout`命令输出。

输入：

this is a nice program

输出：

Words = 5

Characters = 18

## 76. 编写程序获取员工工资作为屏幕输入

该程序从用户处通过屏幕输入员工工资。

然后它根据以下标准扣除所得税：

- 工资超过 15000 扣 30% 税；
- 工资在 7000 到 15000 之间扣 20% 税；
- 工资低于 7000 扣 10% 税。

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    float salary, itax, nsalary;

    cout << "输入员工的工资 : ";
    cin >> salary;

    if (salary > 15000)
        itax = salary * 0.3;
    else if (salary >= 7000)
        itax = salary * 0.2;
    else
        itax = salary * 0.1;

    nsalary = salary - itax;

    cout << "工资 = " << salary << endl;
    cout << "所得税 = " << itax << endl;
    cout << "税后工资 = " << nsalary << endl;

    getch();
}
```

输入：

12000

输出：

工资 = 12000

所得税 = 2400

税后工资 = 9600

## 77. 求解正方矩阵主对角线元素和的程序

```cpp
#include <iostream.h>
#include <conio.h>

int main()
{
    clrscr();
    int n, i, j;
    int matrix[10][10];
    int sum = 0, sum2 = 0;

    cout << "输入矩阵的阶数 : ";
    cin >> n;

    cout << "输入矩阵元素 : " << endl;

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            cin >> matrix[i][j];

            if (i == j)
                sum += matrix[i][j];

            if (i + j == n - 1)
                sum2 += matrix[i][j];
        }
    }

    cout << "主对角线元素和 = " << sum << endl;
    cout << "副对角线元素和 = " << sum2 << endl;

    getch();
    return 0;
}
```

该程序要求用户输入矩阵的阶数以及矩阵元素。

如果矩阵是方阵，它会计算主对角线和副对角线的元素和。

## 78. 将双位十进制数转换为二进制数的程序

```cpp
#include <iostream.h>
#include <conio.h>

void octobin(int);

void main()
{
    clrscr();
    int a;

    cout << "输入双位十进制数 : ";
    cin >> a;

    octobin(a);
}

void octobin(int oct)
{
    long bnum = 0;
    int A[6];
    int a1, a2, quo, rem, x;

    a2 = oct / 10;
    a1 = oct % 10;

    // 转换第一位。
    for (x = 0; x < 3; x++)
    {
        quo = a1 / 2;
        rem = a1 % 2;
        A[x] = rem;
        a1 = quo;
    }

    // 存储第二位的余数。
    for (x = 3; x < 6; x++)
    {
        quo = a2 / 2;
        rem = a2 % 2;
        A[x] = rem;
        a2 = quo;
    }

    // 从余数获取二进制数。
    for (x = 5; x >= 0; x--)
    {
        bnum *= 10;
        bnum += A[x];
    }

    cout << "十进制数 " << oct << " 的二进制数是 " << bnum << endl;
}
```

## 79. 识别输入是符号、数字还是字符的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();

    char charac;

    cout << "输入你的字符 : " << endl;
    cin >> charac;

    if (((charac >= 'A') && (charac <= 'Z')) ||
        ((charac >= 'a') && (charac <= 'z')))
        cout << "你输入的 " << charac << " 是字符。" << endl;
    else if ((charac >= '0') && (charac <= '9'))
        cout << "你输入的 " << charac << " 是数字。" << endl;
    else
        cout << "你输入的 " << charac << " 是符号。" << endl;

    getch();
}
```

你的输入`#`是一个符号。

## 80. 使用 IF 语句输入三个整数并输出最小整数的程序

```cpp
#include <iostream.h>
#include <conio.h>

int main()
{
    clrscr();
    int x, y, z, smallest;

    cout << "Enter 3 integers: ";
    cin >> x >> y >> z;

    smallest = x;

    if (y < smallest)
        smallest = y;

    if (z < smallest)
        smallest = z;

    cout << "The smallest integer out of the 3 integers you typed ";
    cout << x << " , " << y << " & " << z << " is : "
         << "\n" << smallest << "\n";

    getch();
    return 0;
}
```

该程序从用户处获取三个整数`x`、`y`和`z`。

然后它确定这三个数中的最小值，并使用`cout`命令将其打印出来。

# 输入：

82 78 86

# 输出：

你输入的 3 个整数 82, 78 & 86 中最小的整数是：

78

## 81. 输入一个句子并输出句子中大写和小写辅音、大写和小写元音数量程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
    clrscr();
    char line[80];
    int number_of_vowels, uc, lc, uv, lv;

    uc = lc = uv = lv = 0;

    cout << "Enter your sentence : " << endl;
    cin.getline(line, 80);

    for (int x = 0; line[x] != '\0'; x++)
    {
        if (line[x] == 'A' || line[x] == 'E' || line[x] == 'I' ||
            line[x] == 'O' || line[x] == 'U')
            uv++;
        else if (line[x] == 'a' || line[x] == 'e' || line[x] == 'i' ||
                 line[x] == 'o' || line[x] == 'u')
            lv++;
        else if (line[x] > 65 && line[x] <= 90)
            uc++;
        else if (line[x] >= 97 && line[x] <= 122)
            lc++;
    }

    // 打印输出。
    cout << "Uppercase Consonants = " << uc << "," << endl;
    cout << "Lowercase Consonants = " << lc << "," << endl;
    cout << "Uppercase Vowels = " << uv << "," << endl;
    cout << "Lowercase Vowels = " << lv << "," << endl;

    number_of_vowels = uv + lv;
    cout << "Number of vowels = " << number_of_vowels << endl;

    getch();
}
```

该程序从用户处获取一个句子。

它计算大写和小写辅音、大写和小写元音的数量以及元音的总数。

然后使用`cout`命令进行输出。

# 输入：

These programs are truly AMAZING

# 输出：

大写辅音 = 5.

小写辅音 = 13.

大写元音 = 3.

小写元音 = 7.

元音总数 = 10

## 82. 打印杨辉三角前 10 行的程序

```cpp
#include <iostream.h>
#include <conio.h>
#include <iomanip.h>

long triangle(int x, int y);

int main()
{
    clrscr();
    const lines = 10;
```



```cpp
for (int i=0;i<lines;i++)

  for (int j=1;j<=lines-i;j++)

    cout << setw(2) << " ";

for (int j=0;j<=i;j++)

  cout << setw(4) << triangle(i,j);

cout << endl;

getch();

}

long triangle(int x,int y)

{

  if(x<0||y<0||y>x)

    return 0;

  long c=1;

  for (int i=1;i<=y;i++,x--)

    c=c*x/i;

  return c;

}
```

该程序不从用户处获取任何屏幕输入。它只是使用`cout`命令打印杨辉三角的前十行。

## 输入

此程序不需要用户输入。

## 输出

1 10 45 120 210 252 210 120 45 10 1

## 83. 在一维数组中输入10个整数并按升序打印数组的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()

{

clrscr();

int array[10],t;

for(int x=0;x<10;x++)

{

cout << "Enter Integer No. " << x+1 << " : " << endl;

cin>>array[x];

}

for (x=0;x<10;x++)

{

for(int y=0;y<9;y++)

{

if(array[y]>array[y+1])

{

t=array[y];

array[y]=array[y+1];

array[y+1]=t;

}

}

}

cout << "Array in ascending order is : ";

for (x=0;x<10;x++)

cout << endl << array[x];

getch();

}
```

该程序从用户处获取十个整数并存储在一维数组中。

它将这些整数按升序排序并使用`cout`命令输出。

## 输入

43

67

53

21

6

78

92

48

8

## 输出

升序数组为：

6

8

21

43

48

53

67

78

## 84. 计算4x4矩阵和的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
clrscr();
int x,y;
int A[4][4],sum=0;
cout << "Enter elements of 4x4 matrix" << endl;
for(x=0;x<4;x++)
{
for(y=0;y<4;y++)
{
cout << "A[" << x << "][" << y << "] : ";
cin>>A[x][y];
}
}
for(x=0;x<4;x++)
{
for(y=0;y<4;y++)
{
sum+=A[x][y];
}
}
cout << "Sum of elements of 4x4 matrix is " << sum;
getch();
}
```

该程序从用户处获取4x4矩阵的元素。

它计算矩阵所有元素的和并输出。

## 输入

1 1 1 1

1 1 1 1

1 1 1 1

1 1 1 1

## 输出

4x4矩阵元素的和为 16

## 85. 摄氏度转换为华氏度及反之的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
clrscr();
int choice;
float ctemp,ftemp;
cout << "1.Celsius to Fahrenheit" << endl;
cout << "2.Fahrenheit to Celsius" << endl;
cout << "Choose choice : " << endl;
cin>>choice;
if(choice==1)
{
cout << "Enter Celsius : ";
cin>>ctemp;
ftemp=(ctemp*9/5)+32;
cout << "Temperature in Fahrenheit is " << ftemp;
}
else if(choice==2)
{
cout << "Enter Fahrenheit : ";
cin>>ftemp;
ctemp=(ftemp-32)*5/9;
cout << "Temperature in Celsius is " << ctemp;
}
getch();
}
```

该程序从用户处获取选择以在摄氏度和华氏度之间转换。

它根据选择执行转换并输出结果。

## 输入

1

100

## 输出

华氏度为 212

## 86. 输入字符并输出其ASCII码的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
clrscr();
char charac;
int num1;
cout << "Enter a character : ";
cin>>charac;
num1=(int)charac;
cout << "ASCII code for " << charac << " is " << num1;
getch();
}
```

该程序从用户处获取任何字符。

它找到并输出其ASCII码。

## 输入

a

## 输出

a的ASCII码为 97

## 87. 输入字母并输出后两个字母的程序

```cpp
#include <iostream.h>
#include <conio.h>

void main()
{
clrscr();
char charac;
cout << "Enter your letter : ";
cin>>charac;
cout << "The next 2 letters are : " << endl;
cout << (char)(charac+1) << endl;
cout << (char)(charac+2) << endl;
getch();
}
```

该程序从用户处获取一个英文字母`charac`。

它确定它的前后的两个字母并打印出来。

## 输入

x

## 输出

x后面的两个字母是：

y

z

## 88. 在C++中不使用循环和递归打印1到100的程序

```cpp
#include <iostream>
using namespace std;

template<int N>
class PrintOneToN
{
public:
    static void print()
    {
        PrintOneToN<N-1>::print(); // 注意，这不是递归
        cout << N << endl;
    }
};

template<>
class PrintOneToN<1>
{
public:
    static void print()
    {
        cout << 1 << endl;
    }
};

int main()
{
    const int N = 100;
    PrintOneToN<N>::print();
    return 0;
}
```

该程序使用模板特化来打印从1到100的数字，而不使用循环或标准递归（注意：逻辑实际上使用了模板递归，这是一种不同的技术）。

## 89. 显示`getline`作用的简单C++程序

```cpp
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string str;
    int t = 4;
    while (t--)
    {
        // 从标准输入读取一行到str
        getline(cin, str);
        cout << str << " " : "newline" << endl;
    }
    return 0;
}
```

该程序展示了`getline`函数如何工作以读取包含空格的整行。

### 输入

This

is

Geeks

for

### 输出

This : newline

is : newline

Geeks : newline

for : newline

上面的输入和输出看起来良好，但当输入之间有空行时可能会出现问题。

### 输入

This

is

Geeks

for

### 输出

This : newline

: newline

is : newline

: newline

它没有打印最后2行。原因是`getline()`会在遇到回车键时停止读取，即使没有读到任何字符也是如此。因此，即使第三行是空的，`getline()`也会将其视为单独的一。进一步观察第二行的问题。

### 修改后的代码

```cpp
// 一个简单的 C++ 程序，使用 getline 读取
// 带有空行的输入
```

```cpp
#include <iostream>
#include <cstring>
using namespace std;
int main()
{
    string str;
    int t = 4;
    while (t--)
    {
        getline(cin, str);

        // 只要存在空行，就继续读取
        // 新的一行
        while (str.length()==0 )
            getline(cin, str);

        cout << str << " " : "newline" << endl;
    }
    return 0;
}
```

### 输入

This

is

Geeks

for

### 输出

This : newline

is : newline

Geeks : newline

for : newline

## 90. 在 C/C++ 中以不同行且不使用大括号打印二维矩阵的方法？

```cpp
#include<iostream>
using namespace std;

int main()
{
    int m = 2, n = 3;
    int mat[3][] = { {1, 2, 3},
    {4, 5, 6},

    for (int i = 0; i < m; i++)
    for (int j = 0; j < n; j++)

    // 如果 j != n-1 则打印 ' ',否则打印 '\n'
    cout << mat[i][j] << " "\n"[j == n-1];

    return 0;
}
```

### 输出

1 2 3

4 5 6

## 91. 演示友元类（friend Class）的简单完整的 C++ 程序

```cpp
#include <iostream>
class A {
private:
    int a;
public:
    A() { a=0; }
    friend class B;    // 友元类
};
```

```cpp
class B {
private:
    int b;
public:
    void showA(A& x) {
    // 因为 B 是 A 的友元，它可以访问
    // A 的私有成员
    std::cout << "A::a=" << x.a;
}
};
```

```cpp
int main() {
    A a;
    B b;
    b.showA(a); 
    return 0;
}
```

### 输出

A::a=0

## 92. 演示另一个类的友元函数（friend function）的简单完整的 C++ 程序

```cpp
#include <iostream>

class B;

class A
{
public:
    void showB(B&);
}

class B
{
private:
    int b;
public:
    B() { b = 0; }
    friend void A::showB(B& x); // 友元函数
}
void A::showB(B& x)
{\ // 因为 show() 是 B 的友元，它可以
// 访问 B 的私有成员
std::cout << "B::b = " << x.b;
}

int main()
{
    A a;
    B x;
    a.showB(x);

return 0;
}
```

### 输出

B::b = 0

## 93. 演示全局友元（global friend）的简单完整的 C++ 程序

```cpp
#include <iostream>
```

```cpp
class A
{
    int a;
public:
    A() {a = 0};
    friend void showA(A&); // 全局友元函数
};
```

```cpp
void showA(A& x) {
    // 因为 showA() 是友元，它可以访问
    // A 的私有成员
    std::cout << "A::a=" << x.a;
}
```

```cpp
int main()
{
    A a;
    showA(a);
    return 0;
}
```

### 输出

A::a = 0

## 94. 编写一个展示 C++ 构造函数（Constructors）的程序

```cpp
#include<iostream>
using namespace std;
```

```cpp
class Point
{
private:
    int x, y;
public:
    /**构造函数****/
    Point(int x1, int y1) { x = x1; y = y1; }

    int getX() { return x; }
    int getY() { return y; }
};
```

```cpp
int main()
{
    Point p1(10, 15); // 在处调用构造函数

    // 让我们访问构造函数赋值的值
    cout << "p1.x = " << p1.getX() << ", p1.y = " << p1.getY();

    return 0;
}
```

### 输出

p1.x = 10, p1.y = 15

## 95. 编写一个关于排序的程序

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

void show(int a[])
{
    for(int i = 0; i < 10; ++i)
    cout << '\t' << a[i];
}

int main()
{
    int a[10]={1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
    cout << "\n 排序前的数组是：";
    show(a);

    sort(a, a+10);

    cout << "\n 排序后的数组是：";
    show(a);

    return 0;
}
```

### 输出

排序前的数组是：1	5	8	9	6	7	3	4	2	0

排序后的数组是：

## 96. 编写一个演示 C++ 二分查找（Binary Search）算法的程序

```cpp
#include <iostream>
#include <algorithm>
```

```cpp
using namespace std;
```

```cpp
void show(int a[], int arraysize)
{
    for(int i = 0; i < arraysize; ++i)
    cout << '\t' << a[i];
}
```

```cpp
int main()
{
    int a[]={1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
    int arraysize = sizeof(a) / sizeof(a[0]);
    cout << "\n数组是：";
    show(a, arraysize);

    sort(a, a+10);

    cout << "\n 排序后的数组是：";
    show(a, arraysize);

    cout << "\n 假设要在数组中查找 2：";
    if (binary_search(a, a + 10, 2))
        cout << "\n找到了元素 2";
    else
        cout << "\n未找到元素 2";

    return 0;
}
```

（输出略）

## 97. C++ 中可以嵌套命名空间（namespaces）吗？

```cpp
#include <iostream>
namespace outer {
    namespace inner {
        void display() {
            std::cout << "来自嵌套命名空间!";
        }
    }
}
int main() {
    outer::inner::display();
    return 0;
}
```

### 输出

来自嵌套命名空间！

## 98. 使用`for`循环编写一个寻找2到100之间质数的程序



```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 2; i <= 100; i++) {
        bool isPrime = true;
        for (int j = 2; j <= i / j; j++) {
            if (i % j == 0) {
                isPrime = false;
                break;
            }
        }
        if (isPrime) {
            cout << i << " ";
        }
    }
    return 0;
}
```

输出：

2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97

## 99. 编写一个使用嵌套 `if` 语句的程序

```cpp
#include <iostream>
using namespace std;
int main() {
    int num = 10;
    if (num > 0) {
        if (num >= 10) {
            cout << "数字大于等于 10" << endl;
        } else {
            cout << "数字在 1 到 10 之间" << endl;
        }
    } else {
        cout << "数字为负数" << endl;
    }
    return 0;
}
```

输出：

数字大于等于 10

## 100. 编写一个演示嵌套 `switch` 语句的程序

```cpp
#include <iostream>

using namespace std;
int main ()
{
  int a = 100;
  int b = 200;

  switch(a) {
    case 100:
      cout << "这是外部 switch 的一部分" << endl;
      switch(b) {
        case 200:
          cout << "这是内部 switch 的一部分" << endl;
      }
      break;
  }
  cout << "a 的确切值是：" << a << endl;
  cout << "b 的确切值是：" << b << endl;
  return 0;
}
```

（注：原文 `switch` 输出存在语法错误；上述逻辑代表了预期的结构。）

输出：

这是外部 `switch` 的一部分

这是内部 `switch` 的一部分

`a` 的确切值是：100

`b` 的确切值是：200

## 程序 2

```cpp
#include<iostream>

using namespace std;
class Base1 {
public:
    Base1()
    { cout << "Base1's constructor called" << endl; }
};

class Base2 {
public:
    Base2()
    { cout << "Base2's constructor called" << endl; }
};

class Derived: public Base1, public Base2 {
public:
    Derived()
    { cout << "Derived's constructor called" << endl; }
};

int main()
{
    Derived d;
    return 0;
}
```

### 输出

Base1's constructor called

Base2's constructor called

Derived's constructor called

在多重继承的情况下，基类的构造函数总是按照从左到右的派生顺序被调用，而析构函数则按反顺序调用。

## 程序 3

```cpp
#include<iostream>
using namespace std;

class A {
public:
  A(int ii = 0) : i(ii) {}
  void show() { cout << "i = " << i << endl; }
private:
  int i;
};

class B {
public:
  B(int xx) : x(xx) {}
  operator A() const { return A(x); }
private:
  int x;
};

void g(A a)
{ a.show(); }

int main() {
  B b(10);
  g(b);
  g(20);
  getchar();
  return 0;
}
```

### 输出

i = 10

i = 20

由于类 `A` 中存在转换构造函数，整数值可以赋值给 `A` 类对象，函数调用 `g(20)` 可以正常工作。此外，类 `B` 中重载了转换运算符，因此我们可以使用 `B` 类对象调用 `g()`。

## 程序 4

```cpp
#include<iostream>
using namespace std;

class base {
  int arr[10];
};

class b1: public base { };

class b2: public base { };

class derived: public b1, public b2 { };

int main(void)
{
    cout<<sizeof(derived);
    getchar();
    return 0;
}
```

### 输出

如果整数占用 4 字节，那么结果是 80。

## 程序 5

```cpp
#include<iostream>

using namespace std;
class P {
public:
    void print()
    { cout << "Inside P::"; }
};

class Q : public P {
public:
    void print()
    { cout << "Inside Q::"; }
};

class R: public Q {
};

int main(void)
{
    R r;

    r.print();
    return 0;
}
```

### 输出

Inside Q

在 `R` 类中没有定义 `print` 函数。因此，它会在继承层次中进行查找。`print()` 在 `P` 类和 `Q` 类中都存在，应该调用哪一个呢？其是：如果存在多级继承，则函数会在继承层次中线性向上搜索，直到找到匹配的函数为止。

## 程序 6

```cpp
#include<iostream>
#include<stdio.h>

using namespace std;

class Base
{
public:
    Base()
{
        fun(); //注意: fun() 是虚函数
    }
    virtual void fun()
{
  cout<<"\nBase Function";
}
};

class Derived: public Base
{
public:
  Derived(){
  virtual void fun()
  {
    cout<<"\nDerived Function";
  };
};

int main()
{
  Base* pBase = new Derived();
  delete pBase;
  return 0;
}
```

### 输出

Base Function

请参见以下 C++ 标准的解释。

当从构造函数（包括数据成员的成员初始化列表）或析构函数中直接或间接调用虚函数，且该调用所作用的对象是正在构造或销毁的对象时，所调用的函数是定义在构造函数或析构函数类中或其某个基类中的函数，而不是在构造函数或析构函数的派生类中覆盖的函数，或在最派生对象的某个基类中覆盖的函数。

由于这种行为上的差异，建议不要在对象构造或销毁期间调用该对象的虚函数。

## 程序 7

```cpp
#include<iostream>
using namespace std;

int x = 10;
void fun()
{
    int x = 2;
    {
    int x = 1;
    cout << ::x << endl;
    }
}

int main()
{
    fun();
    return 0;
}
```

### 输出

10

如果作用域解析运算符放在变量名之前，则引用的是全局变量。因此，如果从上述程序中删除以下行，编译将失败：

```cpp
int x = 10;
```

## 程序 8

```cpp
#include<iostream>
using namespace std;
class Point {
private:
    int x;
    int y;
public:
    Point(int i, int j); // 构造函数
};

Point::Point(int i = 0, int j = 0) {
    x = i;
    y = j;
    cout << "Constructor called";
}

int main() {
    Point t1, t2;
    return 0;
}
```

### 输出

Constructor called.

如果我们仔细观察语句 `Point t1, t2;`，可以看到只有对象被构造了。`t2` 只是一个指针变量，而不是对象。

## 程序 9

```cpp
#include<iostream>
using namespace std;

class Point {
private:
    int x;
    int y;
public:
    Point(int i = 0, int j = 0); // 普通构造函数
    Point(const Point& t); // 拷贝构造函数
};

Point::Point(int i, int j) {
    x = i;
    y = j;
    cout << "Normal Constructor called\n";
}

Point::Point(const Point& t) {
    y = t.y;
    cout << "Copy Constructor called\n";
}

int main() {
    Point t1, t2;
    t1 = Point(10, 15); // 构造函数调用
    t2 = Point(t1); // 拷贝构造函数调用
    Point t3 = t1; // 拷贝构造函数调用
}
```

（注：原文中程序 9 的输出部分似乎在提供的文本中被截断或混淆，此处根据逻辑翻译对应内容）

*纠正：提供的原始文本中程序 9 的输出部分似乎与程序 10-13 混合在一起了。以下按照原文逻辑顺序翻译：*

### 输出

Normal Constructor called

Copy Constructor called

Normal Constructor called

Copy Constructor called

Normal Constructor called

Constructor called

Constructor called

Constructor called

Normal Constructor called

Copy Constructor called

Normal Constructor called

Copy Constructor called

Normal Constructor called

Normal Constructor called

Normal Constructor called

（由于原始文本中程序 9 到 10-13 的输出错乱，以下是基于代码逻辑的翻译与对齐）

## 程序 10

```cpp
#include<iostream>
using namespace std;

class Test {
    int value;
public:
    Test (int v = 0) {value = v;}
    int getValue() { return value; }

int main() {
  const Test t;
  cout << t.getValue();
  return 0;
}
```

### 输出

编译错误。

常量对象不能调用非 `const` 函数。上述代码可以通过将 `getValue` 改为 `const` 或将 `t` 改为非常量。以下是带有 `getValue const` 的修改后程序，它可以正常工作并输出 0。

```cpp
#include<iostream>
using namespace std;

class Test {
  int value;
public:
  Test (int v = 0) { value = v; }
  int getValue() const { return value; }
}

int main() {
  const Test t;
  cout << t.getValue();
  return 0;
}
```

## 程序 11

```cpp
#include<iostream>
using namespace std;

class Test {
public:
    Test();
};

Test::Test() {
    cout<<"Constructor \n";
}

int main()
{
    cout<<"Start \n";
    Test t1();
    cout<<"End \n";
    return 0;
}
```

### 输出

Start

End

注意 `Test t1();` 并不是构造函数调用。编译器认为这是一个不接收参数的函数声明。

## 程序 12

```cpp
#include<iostream>
using namespace std;

class Base {
public:
    Base();
};

Base::Base() {
    static int a = 10;
    return a;
}

int main() {
    int &y = Base();
    y = 30;
    cout<<y;
    return 0;
}
```

### 输出

40

程序正常工作，因为 `a` 是静态的。`Base()` 返回后，`a` 的内存位置依然有效。

## 程序 13

```cpp
#include<iostream>

using namespace std;

class Test {
    int &t;
public:
    Test (int &x) { t = x; }
    int getT() { return t; }
};

int main()
{
    int x = 20;
    Test t1(x);
    cout << t1.getT() << " ";
    x = 30;
    cout << t1.getT() << endl;
    return 0;
}
```

### 输出

由于 `Test` 中的 `t` 是引用，必须使用初始化列表进行初始化。以下是修改后的程序。它可以正常工作并输出 `"20 30"`。

```cpp
#include<iostream>

using namespace std;

class Test {
    int &t;
public:
    Test(int &x):t(x) { }
    int getT() { return t; }
};

int main() {
    int x = 20;
    Test t1(x);
    cout << t1.getT() << " " << endl;
    x = 30;
    cout << t1.getT() << endl;
    return 0;
}
```

## 程序 15

```cpp
#include <iostream>

using namespace std;

class Complex
{
private:
    double real;
    double imag;
public:
    // 默认构造函数
    Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}

    // 比较两个复数的方法
    bool operator == (Complex rhs) {
        return (real == rhs.real && imag == rhs.imag)? true : false;
    }
};
```

```cpp
int main()
{
    // 一个复数对象
    Complex com1(3.0, 0.0);

    if (com1 == 3.0) {
        cout << "Same";
    } else {
        cout << "Not Same";
        return 0;
    }
}
```

### 输出

Same

## 注意事项
