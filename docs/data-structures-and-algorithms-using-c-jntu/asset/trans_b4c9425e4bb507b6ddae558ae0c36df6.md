

对象既保存数据，也保存操作数据的方法。

### 1.2.3 类成员

类成员包括成员变量（或数据变量）和成员函数（或方法）。类是成员变量和成员函数的组合。[方法与函数的区别在于，定义在类内部的函数称为方法。] 类可以使用访问说明符控制来自类外部对成员的访问。

类的成员可以通过该类的对象和点（.）运算符来访问。

### class Shape

```cpp
class Shape
{
    public:
    int a,b;
    void set()
    {
        - - - - -
    }
};
```

假设 s 是类 Shape 的对象，则类成员基于访问控制通过对象来访问，例如

```cpp
s.a=10, s.b=5 //calling the member-function using object s
```

### 程序 1.1

```cpp
#include<iostream.h>
#include<conio.h>
class Shape
{
    int a,b; //by default private
    public:
    void area()
    {
        cout<<"Enter a&b values:";
        cin>>a>>b;
        cout<<"a="<<a<<"b="<<b;
    }
};
void main()
{
    Shape s1;
    s1.area();
}
```

### 输出

```
Enter a&b values: 5 6
a=5 b=6
```

在程序 1.1 中，类 Shape 定义了变量 a、b 和一个操作变量的方法 area()。创建了对象 s1，它拥有变量 a 和 b 的副本。

## 1.3 I/O 流

流是输入/输出（I/O）设备的逻辑实体。流可以生成或消耗信息，并且直接与 I/O 子系统相关联。流直接连接到物理设备。每当对流执行读取或写入操作时，这些操作都会反映到物理 I/O 设备上。C++ 提供了一组丰富的 I/O 库。

C++ 中提供了两种不同的模板类。一种用于 8 位流，另一种用于 16 位流（宽字符）。类 ios 是 I/O 流的基类。当 C++ 程序加载到内存时，标准输入流（cin）、标准输出流（cout）、标准错误输出流（cerr）以及标准错误输出流的缓冲版本会自动打开。当通过键盘输入任何内容时，可以使用 cin 流收集输入流。当使用 cout 向标准输出流写入任何内容时，字符流将显示在标准输出（屏幕）上。如果在执行时或编译时识别出任何错误，则这些消息将通过 cerr 传递到屏幕。

### 格式化输入/输出

C++ 提供了两种定义输入或输出的方式：

- 1. 通过格式化 ios 类成员（标志）
- 2. 使用 I/O 操纵符

ios 类包含用于格式化 I/O 的不同状态标志。ios 标志可以设置或取消设置。当标志被设置时，I/O 事务期间将执行以下操作。

### ios 类中的不同标志：

- adjustfield：left、right 和 internal 字段统称为 adjustfield。
- basefield：oct、hex 和 dec 字段统称为 basefield。
- boolalpha：布尔值将由关键字 true 或 false 接受。
- dec：I/O 数值系统将设置为十进制。
- fixed：浮点数将以常规表示法显示。
- floatfield：科学计数法和固定字段统称为 floatfield。
- hex：I/O 数值系统将设置为十六进制。
- internal：数值将通过在任何符号和基字符之间插入空格来填充。
- left：输出左对齐。
- oct：I/O 数值系统将设置为八进制。
- right：输出右对齐。
- scientific：浮点数将以科学计数法显示。
- showbase：显示输出时将显示数值基数系统。
- showpoint：浮点值将显示小数点。
- showpos：在值之前显示正号或负号。
- skipws：在对流执行输入操作时用于跳过空白字符。
- unitbuf：插入操作后刷新 I/O 缓冲区。
- uppercase：字符将以大写显示。

### 设置 ios 格式标志：

ios 类成员函数 setf() 用于设置标志。setf 的一般用法如下：

```cpp
fmtflags setf(fmtflags flags);
```

### 程序 1.2

```cpp
#include<iostream.h>
void main()
{
 int a=10;
 cout.setf(ios::showpos);
 cout <<"\n" <<"a="<<a;
}
```

### 输出

```
a=+10
```

在程序 1.2 中，对于 cout 流，设置了 showpos 标志。因此，变量 a 的符号会被显示。

### 程序 1.3

```cpp
#include<iostream.h>
void main()
{
 float a=10.2;
 cout.setf(ios::showpos|ios::showpoint);
 cout <<"\n" <<"A="<<a;
}
```

### 输出

```
A=+10.200000
```

如果未设置 showpoint 标志，则将显示值 +10.2。因为设置了 showpoint 和 showpos 标志，值 10.2 显示为 +10.200000。程序 1.3 演示了可以通过使用管道符号（|）设置两个或多个标志。

取消设置 ios 标志：由于 setf() 用于设置 ios 的标志，因此 ios 类的 unsetf() 成员函数用于取消设置已设置的标志。一般形式如下：

```cpp
void unsetf(fmtflags flags);
```

程序 1.4 取消设置程序 1.3 中设置的标志。

### 程序 1.4

```cpp
#include<iostream.h>
#include<conio.h>
void main()
{
float a=10.2;
clrscr();
cout.setf(ios::showpos | ios::showpoint);
cout<<"After Setting the flags the 'a'="<<a;
cout.unsetf(ios::showpos | ios::showpoint);
cout<<"After Clearing the flags the 'a'="<<a;
}
```

### 输出

```
After Setting the flags the 'a'=+10.200000
After Clearing the flags the 'a'=10.2
```

ios 类的其他成员方法：类 ios 提供了其他成员函数 width()、precision() 和 fill()。width 函数可用于设置最小字段大小。precision 方法可用于设置浮点精度。此外，fill 方法允许开发者使用用户指定的字符修改默认填充值。width、precision 和 fill 方法的一般形式如下：

```cpp
streamsize width(streamsize w);
streamsize precision(streamsize p);
char fill(char ch);
```

### 程序 1.5

```cpp
#include<iostream.h>
#include<conio.h>
void main()
{
float a=10.123456;
clrscr();
cout.precision(2);
cout.width(10);
cout.fill('#');
cout<<a;
}
```

### 输出

```
#####10.12
```

从程序 1.5 可以观察到，因为宽度设置为 10 个字符，输出显示为 10 个字符宽。因为精度设置为 2 个字符，显示 10.12 而不是 10.123456。因为默认对齐方式是右对齐，五个空字符将由 # 字符填充。

输入和输出操纵符：输入/输出操纵符是 ios 的成员。可以使用操纵符成员函数来操作输入流和输出流。这些成员函数不接受输入参数。setiosflags 操纵符类似于 ios 类的 setf 成员函数。两个函数的作用相同。

### 程序 1.6

```cpp
#include<iostream.h>
#include<iomanip.h>
#include<conio.h>
void main()
{
 float a=10.2;
 clrscr();
 cout<<endl<<"After Setting the flags the 'a'="<<setiosflags (ios::showpos|
 ios::showpoint)<<a;
}
```

### 输出

```
After Setting the flags the 'a'=+10.200000
```

在程序 1.6 中，使用了 endl 和 setiosflags 操纵符。endl 操纵符用于换行打印。

### 程序 1.7

```cpp
#include<iostream.h>
#include<iomanip.h>
#include<conio.h>
void main()
{
 clrscr();
 cout<<setiosflags (ios::showbase);
 cout<<hex<<10<<endl;
 cout<<oct<<10<<endl;
}
```

### 输出

```
0xa
012
```

在这里，hex 和 setiosflags 操纵符用于操作 cout 输出流（程序 1.7）。当设置 showbase 标志时，数值将带有基数格式前缀，例如十六进制值带有 '0x' 前缀，八进制值带有 '0' 前缀，十进制值无前缀。第一个输出是带有 '0x' 前缀的 10 的十六进制值，第二个输出是带有 '0' 前缀的 10 的八进制值。

## 1.4 访问控制

访问说明符为类成员提供来自类外部的访问权限。访问说明符是以下关键字之一：
public、private 和 protected。

- 默认情况下，类的所有成员都是私有的，且无法在类外部访问。类的私有成员可以通过同类的公有成员来访问。

