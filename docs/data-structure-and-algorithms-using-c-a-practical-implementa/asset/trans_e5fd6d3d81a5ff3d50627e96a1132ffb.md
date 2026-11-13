

## 4.2 C++ 中的访问说明符

顾名思义，这些是控制类成员的访问说明符。为了实现面向对象编程（OOP）的特性，类提供了三种不同的访问说明符，如下

- 私有（Private）
- 公有（Public）
- 保护（Protected）

这些也称为成员访问控制。

### 私有（Private）：

在私有组中声明的成员不允许在类外部使用；只有类的成员可以访问它们，这实现了数据隐藏。

### 公有（Public）：

在此类别中声明的成员允许在程序的任何地方使用。

### 保护（Protected）：

在单个类中使用时，此部分与私有类别相同。唯一的区别是，在继承情况下，这些成员可以传递给派生类。

## 4.3 类的声明

```
class class_name
{
private:
    data members;
    member functions();
public:
    data members;
    member functions();
protected:
    data members;
    member functions();
};
```

### 成员函数

类的成员函数是指其定义或原型位于类定义内部的函数，就像其他变量一样。它作用于其所属类的任何对象，并可以访问该对象的类的所有成员。

### 示例

```
class print
{
private:
    int x;
public:
    void display()
    {
        cout<<"\n Enter the number";
        cin>>x;
        cout<<"THE ENTERED NUMBER IS "<<x;
    }
};
```

函数 display() 被放在公有部分，因为只有通过它才能打印 x 的值，而 x 位于私有类别中，因此任何想要显示数字的人都必须使用 display()。这就是类的优势。

### 类与结构体的区别

| 类 | 结构体 |
| :--- | :--- |
| 使用关键字 class | 使用关键字 struct |
| 它提供继承和多态 | 它不提供这些概念 |
| 默认情况下，类的成员是私有的 | 默认情况下，结构体的成员是公有的 |
| 支持数据抽象 | 不支持 |

### 对象的声明

对象是类的实例。通过对象可以使用类的成员。

语法：class_name object_name;

### 访问类的成员

类的成员可以通过对象来访问，就像结构体一样。即：object_name.member_name；

### 以编程方式区分 PRIVATE、PUBLIC 和 PROTECTED

### 示例

```
class differ
{
private:
    int x;
public:
    int y;
protected:
    int z;
};

void main()
{
    differ obj;    // Declaration of the object
    cout<<"Enter a number for x";
    cin>>obj.x;    // Error, because x is private
    cout<<"Enter a number for y";
    cin>>obj.y;    // No Error, since y is public
    cout<<"Enter a number for z";
    cin>>obj.z;    // Error, because z is protected
}
```

## 4.4 C++ 中使用的一些操纵符

C++ 允许一些操纵符函数，用于在输出期间进行额外格式化。其中最常用的操纵符函数有

- endl
- setw()
- setfill()
- dec
- oct
- hex
- setprecision()

这些操纵符定义在 <iomanip.h> 中，因此在使用前必须包含 <iomanip.h>。

### endl

此操纵符用于换行。它的作用与 “\n” 相同。示例：cout<<"HELLO"<<endl<<"WEL COME";

输出
HELLO
WEL COME

### setw()

此操纵符用于在两个数字之间留出一些间隔。
示例：int x=5, y=4
cout<<x<<setw(5)<<y;

输出
5___4 _（下划线表示空格）

### setfill()

此操纵符用于用 setw() 操纵符提供的字符填充间隔。
示例：
int x=5, y=4;
cout<<setfill('$');
cout<<x<<setw(5)<<y;

输出
5$$$$4

### dec、oct、hex

这些操纵符用于以不同进制显示整数。
dec：以整数格式显示数字
oct：以八进制格式显示数字
hex：以十六进制格式显示数字

```
Ex:
void main()
{
    int x = 14;
    cout<<"DECIMAL"<<dec<<x;
    cout<<endl<<"OCTAL"<<oct<<x;
    cout<<endl<<"HEXADECIMAL"<<hex<<x;
}
```

输出
DECIMAL 14
OCTAL 16
HEXADECIMAL e

### setprecision()

此操纵符用于控制浮点数小数点后显示的位数。

```
Ex:
float x=5.23456;
cout<<setprecision(2)<<x;
cout<<endl<<setprecision(0)<<x;
cout<<endl<<setprecision(6)<<x;
```

### 输出

5.23
5.23456
5.23456

## 4.5 在类外部定义成员函数

我们已经知道，类由不同的数据成员和成员函数组成，当我们将成员函数的定义放在类内部时，类会变得复杂，并且也难以处理错误。

因此，最好在类内部声明成员函数，但在类外部提供定义。为了实现这一点，使用了作用域解析运算符。

在类外部定义成员函数的过程如下

```
Return_type class_name::function_name(data_type var1, data_type var2......)
{
    Body of function;
    Return value/variable/expression;
}
```

## 4.6 对象数组

与其他普通变量一样，对象也可以用作数组，其声明方式也与普通数组相同。

### 声明

```
class_name object[size];
```

### 示例

编写一个程序，输入 5 名学生的详细信息并显示它们。

```
class student
{
    char name[20], add[30];
    int roll, age;
public:
    void input();
    void print();
};
void student::input()
{
    cout<<endl<<"Enter the name and address";
    gets(name);
    gets(add);
    cout<<endl<<"Enter the roll and age";
    cin>>roll>>age;
}
void student::print()
{
    cout<<endl<<"NAME IS "<<name;
    cout<<endl<<"ADDRESS"<<add;
    cout<<endl<<"AGE IS "<<age;
    cout<<endl<<"ROLL IS"<<roll;
}
void main()
{
    student obj[5];
    int i;
    for(i=0; i<5; i++)
    {
        obj[i].input();
    }
    for(i=0; i<5; i++)
    {
        obj[i].print();
    }
}
```

## 4.7 对象指针

如果对象是指针，则可以使用间接运算符访问类的成员，如下所示

```
object_name->member_name;
```

### 示例：编写程序检查一个数是否为质数

```
#include <iostream.h>
class prime
{
private:
    int x;
public:
    void input();
    void check();
};
void prime::input()
{
    cout<<"Enter the number";
    cin>>x;
}
void prime::check()
{
    int i;
    for(i=2; i<=x; i++)
    {
        if(x%i==0)
            break;
    }
    if(i==x || x==1)
        cout<<"PRIME";
    else
        cout<<"NOT PRIME";
}
void main()
{
    prime *p;
    p->input();
    p->check();
}
```

## 4.8 内联成员函数

C++ 为其常规用户提供了使用 inline 关键字的功能。C++ 提供内联函数，编译器会将函数的代码直接写在调用处，而不是为函数生成目标函数并在每次需要时调用它。

当调用普通函数时，控制权总是从调用处转移到定义部分，这在执行一系列用于转移控制、保存寄存器、将值返回给调用函数以及安排值的指令时会花费更多额外时间。

为了避免这种情况，我们可以使用宏来替代该任务，例如：#define min(a,b) (a<b ? a:b)

这通过在程序中简单地文本替换表达式 min(a,b) (a<b ? a : b) 来节省函数调用的开销。

宏的主要缺点是它们不是真正的函数，因此在编译期间不会进行通常的错误检查。

因此，为了避免这种情况，C++ 引入了一种称为内联函数的新功能，它在调用时会内联展开。也就是说，当调用函数时，编译器用函数定义替换其调用。通常，inline 用于大小较小的函数。inline 不是命令，而是对编译器的请求，函数是否被视为内联取决于编译器，即使我们声明了 inline。

在 C++ 中，当我们在类体内部定义类的成员函数时，默认情况下这些函数会被视为内联函数，但当我们在类体外部定义函数时，则必须显式地将函数定义为 inline。

当我们在类内部定义成员函数时，C++ 编译器默认会将其视为内联函数，但当我们在类外部提供函数定义时，也可以通过 inline 关键字将其设置为内联。

```
inline return_type class_name::function_name(data_type var............)
{
    Body of function;
    Return(value/variable/expression);
}

