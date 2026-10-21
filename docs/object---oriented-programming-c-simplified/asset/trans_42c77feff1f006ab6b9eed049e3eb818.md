

```
LENGTH := 4
STRING IS := HARI LIKE C++
LENGTH := 13
```

**说明** : 在默认构造函数中，我们动态创建了一个大小为 1 个字符的字符串，长度为 0。当执行 s1 = string ("HARI"); 时，会调用构造函数 string::string(char s[])，此时 s 包含 "HARI"；在构造函数内部，首先计算 s 的长度并赋给 len。然后我们动态分配大小为 len + 1 的内存。该内存被分配后，返回的第一个内存单元的地址被赋给指针 sname。在函数 show 中显示 len 和 sname 后，我们通过编写 delete sname 来删除 sname，从而释放 sname 指向的内存。

```cpp
/* PROG 7.21 CONCATENATION OF TWO STRINGS */

#include <iostream.h>
#include <string.h>
#include <conio.h>
class string
{
        char *sname;
        int len;
public :
        string( )
        {
                len=0;
                sname = new char [len + 1];
                *sname = '\0';
        }

        string(char s[ ])
        {
                len = strlen(s);
                sname = new char[len + 1];
                strcpy(sname, s);
        }

        friend string concate(string, string);

        void show( )
        {
                cout << "String := " << sname << endl;
        }
};
```

```cpp
string concat(string A, string B)
{
 string temp;
 temp.len = A.len + B.len +1;
 temp.sname = new char[temp.len+1];
 strcpy(temp.sname, A.sname);
 strcat(temp.sname, " ");
 strcat(temp.sname, B.sname);
 return temp;
}
```

```cpp
void main ()
{
 string s1,s2,s3;
 clrscr ();
 s1=string("Hari");
 s1.show ();
 s2=string("Pandey");
 s2.show ();
 s3=concat(s1,s2);
 s3.show ();
 getch ();
}
```

OUTPUT :

```
String := Hari
String := Pandey
String := Hari Pandey
```

说明 : 这里我们只解释函数 concat。

```cpp
string concat(string A, string B)
{
 string temp;
 temp.len = A.len + B.len +1;
 temp.sname = new char[temp.len+1];
 strcpy(temp.sname, A.sname);
 strcat(temp.sname, " ");
 strcat(temp.sname, B.sname);
 return temp;
}
```

当执行行 s3 = concate (s1, s2); 时，A.sname 等于 "Hari"，A.len = 4，B.sname 等于 "Pandey"，B.len = 6。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_343_0.png)

```
s1 = string ("Hari")
len = strlen ("Hari")
len = 4 (index 0 – 3)
```

### 图 7.10. 通过 strlen ( ) 函数实现字符串长度。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_343_1.png)

```
s2 = string ("Pandey")
len = strlen(s2);
len = 6 (index 0 – 5)
```

### 图 7.11. strlen ( ) 函数的物理实现。

在函数 concate 中，第一行创建对象 temp。在下一行我们将 A.len、B.len 和 1 个额外的空间相加，用于在 "Hari" 和 "Pandey" 之间添加空格。因此 temp 的 len 变为 4 + 6 + 1 = 11。下一行为 temp.sname 分配内存。在下一行，使用 strcpy( ) 函数将 A.sname 即 "Hari" 复制到 temp.sname。接下来，使用 strcat 将一个空格 " " 串联到当前包含 "Hari" 的 temp.sname。现在 temp.sname 变为 "Hari"。

在下一行，使用 strcat 将 B.sname 串联到 temp.sname，结果 temp.sname 包含 "Hari Pandey"。temp 对象被返回并赋给 s3。

A.len = 4  
B.len = 6  
temp.len = 10 + 1 = 11

![](img/ad5299318df8d4d7c6df5eaa86590ea3_343_2.png)

### 图 7.12. 通过应用 new 操作符分配空间。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_343_3.png)

```
strcpy (temp.sname, A.sname)
strcpy (temp.sname, "Hari")
```

### 图 7.13. 将字符串 "Hari" 复制到 temp. sname。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_344_0.png)

### 图 7.14. *应用 `strcat()` 用于串联空格后。*

![](img/ad5299318df8d4d7c6df5eaa86590ea3_344_1.png)

`s3 = strcat(s1, s2)`  
`strcat(temp.sname, B.sname);`

### 图 7.15. *将 string1 与 string2 串联后。*

```cpp
/*PROG 7.22 CONSTRUCTING OBJECTS DYNAMICALLY */

#include <iostream.h>
#include <conio.h>

class demo
{
    public :
        demo( )
        {
            cout << "Constructor called" << endl;
        }
};
void main( )
{
    clrscr( );
    demo *ptr = new demo( );
    getch( );
}
```

OUTPUT :

```
Constructor called
```

说明 : new 操作符可用于动态创建对象。创建指针不会创建对象。对于语句 `new demo ( )`，对象通过从堆分配内存并调用类的默认构造函数来构造。

它也可以写成：

```cpp
demo *ptr;
{
    ptr= new demo ();
}
```

甚至在 main 中简单地写 new demo (); 也是可行的。

```cpp
/* PROG 7.23 CONSTRUCTING OBJECTS DYNAMICALLY VER 2 */

#include <iostream.h>
#include <conio.h>

class demo
{
public :
    demo()
    {
        cout<<"DEFAULT CONSTRUCTOR"<<endl;
    }
    demo (int x)
    {
        cout<<"ONE INT ARGUMENT CONSTRUCTOR"<<endl;
        cout<<"X = "<<x<<endl;
    }
    demo (float f)
    {
        cout<<"ONE FLOAT ARGUMENT CONSTRUCTOR"<<endl;
        cout<<"f :="<<f<<endl;
    }
    demo (int x, char y)
    {
        cout<<"ONE INT AND ONE CHAR ARGUMENT CONSTRUCTOR"<<endl;
        cout<<"x :="<<x<<"\t"<<"y :="<<y<<endl;
    }
    demo(char *p)
    {
        cout<<"ONE CHAR* ARGUMENT CONSTRUCTOR"<<endl;
        cout<<"p :="<<p<<endl;
    }
};
```

```cpp
void main()
{
    clrscr();
    new demo();
    new demo(10);
    new demo(10.35f);
    new demo(20,'P');
    new demo("DYNAMIC");
    getch();
}
```

OUTPUT :

```
DEFAULT CONSTRUCTOR
ONE INT ARGUMENT CONSTRUCTOR
X = 10
ONE FLOAT ARGUMENT CONSTRUCTOR
f :=10.35
ONE INT AND ONE CHAR ARGUMENT CONSTRUCTOR
x :=20 y :=P
ONE CHAR* ARGUMENT CONSTRUCTOR
p :=DYNAMIC
```

说明 : 在程序中有 5 个构造函数。一个是默认的，其余是带参数的。在 main 中我们通过动态创建对象来调用每个构造函数。注意我们没有创建代表对象的指针变量，如 demo *ptr=new demo (); 当我们以后想使用对象时该语法是有效的。在程序中我们只是向你展示如何动态调用构造函数，因此我们没有将任何 new 调用返回的地址存储到 demo 类的指针中。

```cpp
/* PROG 7.24 CONSTRUCTING OBJECT DYNAMICALLY */

#include <iostream.h>
#include <conio.h>

class demo
{
public :
    demo()
    {
        cout<<"DEFAULT CONSTRUCTOR"<<endl;
    }
};
```

```cpp
void main( )
{
    demo *ptr = new demo [5];
    getch( );
}
```

OUTPUT :

```
DEFAULT CONSTRUCTOR
DEFAULT CONSTRUCTOR
DEFAULT CONSTRUCTOR
DEFAULT CONSTRUCTOR
DEFAULT CONSTRUCTOR
```

说明 : 在程序中我们动态创建了数组对象。第一个对象是 ptr [0]，第二个是 ptr [1]，以此类推。每个对象创建时都会调用默认构造函数。

## 7.7 析构函数

析构函数是类的成员函数，其名称与类名相同，但前面加上波浪号 ~。析构函数的目的是在对象不再需要或超出作用域时销毁对象。作为析构函数的一个非常小的例子，请看下面给出的程序：

```cpp
/*PROG 7.25 DEMO OF DESTRUCTOR VER 1*/
#include <iostream.h>
#include <conio.h>

class demo
{
public :
    demo( )
    {
        cout << "Constructor called\n";
    }
    ~demo( )
    {
        cout << "Destructor called" << endl;
    }
};
```

```cpp
void main()
{
    clrscr();
    demo d;
    getch();
}
```

OUTPUT :

```
Constructor called
Destructor called
```

说明 : 当执行 demo d; 时，它调用类的默认构造函数并打印 Constructor called。对象 d 的作用域是它可用的区域/位置，在上面的程序中作用域是整个 main 函数。demo d; 是函数 main 中唯一的语句，当编译器找到 main 的结束大括号 i.e., } 时，它会调用类的析构函数来销毁对象 d 并打印 Destructor called。代码如下：

```cpp
~demo()
{
    cout << "Destructor called " << endl;
}
```

是类 demo 的析构函数。

### 析构函数的特性

- 1. 名称与类名相同，但前面加上 ~ 符号。
- 2. 析构函数在对象超出作用域后立即自动调用。
- 3. 析构函数用于销毁对象。
- 4. 一旦为对象调用了析构函数，该对象将不再可供将来引用。
- 5. 析构函数可用于清理工作，例如关闭文件、释放动态分配的内存等。在析构函数中关闭文件是一个好主意，因为用户可能会忘记关闭与对象关联的文件。但当对象超出作用域时，析构函数会被调用，析构函数中编写的所有代码都会执行，这将始终导致文件关闭且不会有数据丢失。当在构造函数中使用 new 分配内存时，我们必须始终在析构函数中使用 delete 来释放内存。
- 6. 与构造函数类似，析构函数没有返回类型，因此它们不能返回值。
- 7. 析构函数没有显式或隐式类别。它们始终由编译器隐式调用。
- 8. 析构函数永远不能接受任何参数。

