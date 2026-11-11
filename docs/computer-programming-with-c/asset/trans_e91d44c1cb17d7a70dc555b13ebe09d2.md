
```cpp
void output()
{
    cout<<str<<endl;
}
};
void main()
{
    cout<<"String Concat using operator overloading"<<endl;
    String s1("Computer");
    String s2("Programming");
    String s3;
    s3 = s1+s2;
    s3.output();
}
```

## 输出

String Concat using operator overloading
ComputerProgramming

## 演算过程

main() 中的第一条语句

```cpp
String s1("Computer");
```

通过调用动态构造函数并将字符串“Computer”作为参数传递给该构造函数，创建了一个 String 对象 s1。因此，对象 s1 的成员 str 现在将指向字符串“Computer”，如图 13.38 所示。

类似地，main() 中的第二行

```cpp
String s2("Programming");
```

通过调用动态构造函数并将字符串“Programming”作为参数传递给该构造函数，创建了一个 String 对象 s2。因此，对象 s2 的成员 str 现在将指向字符串“Programming”，如图 13.38 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_778_0.png)

**图 13.38：** 对象 s1 和 s2 的状态

语句 `s3 = s1+s2;` 将使用对象 s1 调用一个运算符函数，并将对象 s2 作为参数传递给该函数。这意味着，在运算符函数内部可以直接访问对象 s1 的成员 str，因为该函数是由对象 s1 本身调用的。此外，对象 s2 作为参数传递，并将被初始化为作为运算符函数一部分创建的形式参数 t，因此现在可以通过对象以 t.str 的形式访问 s2 的成员 str，如代码所示。

此外，我们在运算符函数内部创建一个指针 res，用于指向结果的 String，该结果应当是对象 s1 和 s2 中各自字符串的拼接。这意味着结果字符串的长度将是 s1 的字符串长度与 s2 的字符串长度之和。因此，我们使用下面的语句为结果分配内存：

```cpp
res = new char[strlen(str) + strlen(t.str) + 1];
```

进一步地，运算符函数内部使用的 strcat() 函数使指针 res 指向由对象 s1 的成员 str 和对象 s2 的成员 str 所指向字符串的拼接结果（"Computer" + "Programming" = "ComputerProgramming"）。同时，使用 new 创建 String 类的对象，并将其返回给 main() 函数。因此，对象 s3 现在包含 s1 和 s2 中字符串的拼接结果，如图 13.39 所示。

语句 s3.output(); 调用 output() 函数，以打印存储在对象 s3 中的结果字符串，这从 main() 函数的最后一行可以看到。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_779_0.png)

**图 13.39：** 对象 s3 的状态

## 测验

- 1. C++ 中的运算符重载有助于实现。
  - (a) 运行时多态
  - (b) 编译时多态
  - (c) 抽象
  - (d) a 和 c
  - (e) b 和 c
- 2. 下列哪个运算符不能被重载？
  - (a) +
  - (b) ++
  - (c) sizeof
  - (d) ->
- 3. 当要重载关系运算符时，运算符函数必须返回 ______ 值。
  - (a) 任意字符值
  - (b) 布尔值 0 或 1
  - (c) 任意整数值
  - (d) 运算符函数不应返回任何值
- 4. 运算符函数可以写成
  - (a) 类的成员函数
  - (b) 类的友元函数
  - (c) 全局函数
  - (d) 以上都不是
- 5. 下列哪一项不属于函数签名的一部分？
  - (a) 函数名称
  - (b) 函数接受的参数个数
  - (c) 参数的数据类型
  - (d) 函数的返回类型
- 6. 如果 o1 是类 Abc 的对象，那么在下列哪种表达式中必须创建全局运算符函数？
  - (a) o1*o2
  - (b) o1*9
  - (c) 9*o2
  - (d) 以上都不是
- 7. 函数重载有助于实现
  - (a) 封装
  - (b) 编译时多态
  - (c) 数据隐藏
  - (d) 运行时多态
- 8. 当通过将运算符函数创建为类的成员函数来重载二元运算符时，该运算符函数将接受多少个参数？
  - (a) 1
  - (b) 2
  - (c) 3
  - (d) 4
- 9. 当通过将运算符函数创建为全局函数来重载一元运算符时，该运算符函数将接受多少个参数？
  - (a) 1
  - (b) 2
  - (c) 3
  - (d) 4
- 10. 下列哪项陈述是正确的？
  - (a) 所有运算符函数都执行早期绑定。
  - (b) 所有运算符函数都执行晚期绑定。
  - (c) 要执行的绑定类型取决于我们编写的程序，运算符函数没有通用规则。
  - (d) 运算符函数不执行绑定。

## 错误查找练习

下面给出了一些程序，它们可能包含错误，也可能不包含错误。如果代码中存在错误，请改正错误，和/或确定输出。

### 程序 1

```cpp
#include<iostream.h>
class DATA
{
float a;
int b;
public:
        DATA()
        {
        a=0
        b=-10;
        }
        DATA(int p,int q)
        {
        a=p;
        b=q;
        }
        void add(DATA t)
        {
        DATA res;
        res.a=a+t.a;
        res.b=b+t.b;
        return res;
        }
        void output()
        {
        cout<<"a="<<a<<"b="<<b;
        }
};
void main()
{
DATA d1(10,20);
DATA d2,d3;
d3=d1+d3;
d3.output()
}
```

### 程序 2

```cpp
#include<iostream.h>
class DATA
{
float a;
public:
        void set_data(int p)
        {
        a=p;
        }
int operator<=(DATA t)
{
if(a>t.a)
{
return 0;
}
return 1;
}
void output()
{
cout<<"a="<<a<<"b="<<b;
}
};
void main()
{
DATA d1, d2,d3;
d1.set_data(10);
d2.set_data(20);
d3.set_data(30);
if(d1>d2)
{
cout<<"d1 is greater than d2"<<endl;
}
else
{
cout<<"d1 is not greater than d2" <<endl;
}
if(d1<=d3)
{
cout<<"d1 is less than or equal to d3" <<endl;
}
else
{
cout<<"d1 is greater than d3" <<endl;
}
}
```

### 程序 3

```cpp
#include<iostream.h>
class DATA
{
float a;
int b;
public:
DATA()
{
a=50
b=-100;
}
DATA(int p,int q)
{
a=p;
b=q;
}
DATA operator+()
{
DATA res;
res.a=a+d2.a;
res.b=b+d2.b;
return res;
}
void output()
{
cout<<"a="<<a<<"b="<<b;
}
};
void main()
{
DATA d1(10,20);
DATA d2,d3;
d3=d1+d3;
d3.output()
}
```

### 程序 4

```cpp
#include<iostream.h>
class DATA
{
float a;
int b;
public:
DATA()
{
a=50
b=-100;
}
DATA(int p,int q)
{
a=p;
b=q;
}
friend DATA operator+(DATA);
    void output()
    {
        cout<<"a="<<a<<"b="<<b;
    }
};
DATA operator+(DATA t)
{
DATA res;
res.a=a+t.a;
res.b=b+t.b;
return res;
}
void main()
{
DATA d1(10,20);
DATA d2,d3;
d3=d1+d3;
d3.output()
}
```

## 复习题

- 1. 请用适当的示例解释运算符重载。
- 2. 请解释二元运算符在有友元函数和无友元函数情况下的运算符重载。
- 3. 编写一个 C++ 程序，重载运算符 += 以将两个 Time 类对象相加。每个 Time 对象用分钟和秒表示。程序应从用户处接收两个 Time 对象作为输入，并打印 += 运算的结果。
- 4. 什么是运算符函数？请描述运算符函数及其创建语法和规则。
- 5. 编写一个 C++ 程序，创建包含成员 dd、mm、yy 的 Date 类。重载 ++ 和 -- 运算符以递增/递减 Date 对象的值。同时，在递增/递减日期时考虑闰年的情况。
- 6. 编写一个程序，重载运算符 +、− 和 *，分别用于执行 Matrix 对象的加法、减法和乘法。创建 Matrix 类，并通过将运算符函数编写为 Matrix 类的友元函数来重载运算符。
- 7. 编写一个 C++ 程序，重载 new 和 delete 运算符。
- 8. 什么是编译时绑定？请举例说明。

