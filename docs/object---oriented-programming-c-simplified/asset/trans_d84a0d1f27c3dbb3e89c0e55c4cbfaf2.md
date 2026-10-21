

## 2.11 C++ 程序的编写风格

你的第一个程序可以用另外两种方式编写，这是一种较新的 C++ 程序编写风格。你所看到的程序被认为是旧式的 C++ 程序编写风格。新的风格是

```
#include <iostream>
using namespace std;
void main()
{
    cout << "hello C++" << endl;
}

or
#include <iostream>
    int main()
{
    std :: cout << "hello C++" << endl;
    return 0;
}
```

iostream.h 是头文件，iostream 也是一个头文件。区别仅仅在于 iostream 提供了全局命名空间（参考第 13 章）std，在其中声明了 cout 和 cin（稍后讨论）。如果你没有写 using namespace std，就必须写 std :: cout 和 std :: cin 来访问 cout 和 cin。函数 main 的返回类型可以是 void 也可以是 int。这并不会使你的程序出现错误。在 main 为 int 类型的情况下，main 必须返回一个值。我们将遵循旧式的程序编写风格。你可以选择任何一种风格你想要的，注意 main 函数与旧风格和新风格无关。使用 main 函数的方式由你自己决定，是采用旧风格还是新风格。

## 2.12 编程示例

```
/*PROG 2.2 WRITING MULTIPLE STATEMENTS WITH SINGLE COUT */
#include <iostream.h>
int main( )
{
    cout << "Hello NMIMS University" << endl
        << "Hello MPSTME Mumbai Campus" << endl
        << "Hello MPSTME Shirpur Campus" << endl;
    return 0;
}
```

OUTPUT :
Hello NMIMS University
Hello MPSTME Mumbai Campus
Hello MPSTME Shirpur Campus

![](img/ad5299318df8d4d7c6df5eaa86590ea3_55_0.png)

图 2.11. 程序 2.2 的输出屏幕。

EXPLANATION : 上述程序说明了可以用单个 cout 和多个 << 运算符编写多个语句的事实。endl 会换行。分号必须放在末尾。然而，如果你不想按上述方式编写，你也可以像下一个程序中那样使用多个 cout 语句编写。

```
/* PROG 2.3 THREE COUT STATEMENT IN A C++ PROGRAM */

#include <iostream.h>
int main()
{
    cout << "Hello NMIMS University" << endl;
    cout << "Hello MPSTME Mumbai Campus" << endl;
    cout << "Hello MPSTME Shirpur Campus" << endl;
    return 0;
}
```

OUTPUT :
Hello NMIMS University
Hello MPSTME Mumbai Campus
Hello MPSTME Shirpur Campus

![](img/ad5299318df8d4d7c6df5eaa86590ea3_55_1.png)

图 2.12. 程序 2.3 的输出屏幕。

EXPLANATION : 该程序不言自明。

```
/* PROG 2.4 DISPLAYING DIFFERENT TYPES OF CONTENTS */

#include <iostream.h>
void main()
{
    cout << 123 << endl;
    cout << 23.567 << endl;
    cout << 12345678 << endl;
    cout << 'P' << endl;
    cout << "Hari" << endl;
}

OUTPUT :
123
23.567
12345678
P
Hari
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_56_0.png)

图 2.13. 程序 2.4 的输出屏幕。

EXPLANATION : 该程序简单地显示了 int、char、double、char* 和 char 类型的各种常量。endl 是内置的操纵符，其作用类似于 ‘\n’。有关操纵符的更多内容请参见第 11 章。

```
/* PROG 2.5 WORKING WITH VARIABLES VER 1 */

#include <iostream.h>
void main()
{
    int x = 10;
    float y = 2.34f;
    char *s = "NMIMS UNIVERSITY";
    cout << "Value of x :" << x << endl;
    cout << "Value of y :=" << y << endl;
    cout << "Value of s :=" << s << endl;
}

OUTPUT :
Value of x :=10
Value of y :=2.34
Value of s :=NMIMS UNIVERSITY
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_57_0.png)

# 图 2.14. 程序 2.5 的输出屏幕。

EXPLANATION : 在程序中我们声明并初始化了 3 个变量 x、y 和 s，类型分别为 int、float 和 char*。注意 y 的值为 2.34f 而不是 2.34。浮点数后加上后缀 f 或 F 使其成为 float 数。如果不写，则该数被视为 double。显示变量值非常简单，如代码所示。只需写成 cout << variable_name。同样，对于连接，只需在变量前后使用 <<，例如 cout << "x=" << x << endl; 已声明但未初始化的变量包含垃圾值。

# /*PROG 2.6 WORKING WITH VARIABLES VER 2*/

```
#include <iostream.h>
void main()
{
    int x(10);
    float f(23.34);
    char ch('P');
    cout << "x=" << x << endl;
    cout << "f=" << f << endl;
    cout << "ch=" << ch << endl;
}

OUTPUT :
x=10
f=23.34
ch=P
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_58_0.png)

图 2.15. 程序 2.6 的输出屏幕

EXPLANATION : 在 C++ 中，所有内置数据类型都被视为类，而在 C 中它们被视为结构体。这里你可以假设 int 是一个类，x 是它的一个对象，我们通过调用构造函数来初始化 x。这与写 int x =10 相同，但给出的记法称为类构造函数记法。float 和 char 类型也适用同样的类比。

```
/*PROG 2.7 DYNAMIC INITIALIZATION OF VARIABLES */

#include <iostream.h>
void main()
{
    int num=20;
    cout<<"int num="<<num<<endl;
    double d=23.45;
    cout<<"double d="<<d<<endl;
    char ch='P';
    cout<<"char ch="<<ch<<endl;
    char*s="CPP";
    cout<<"char*s="<<s<<endl;
}

OUTPUT :
int num=20
double d=23.45
char ch=P
char*s=CPP
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_58_1.png)

图 2.16. 程序 2.7 的输出屏幕。

EXPLANATION : 该程序演示了变量可以在程序的任何地方声明和初始化的事实。在程序的任何地方动态初始化变量被称为动态初始化。

```
/* PROG 2.8 WORKING WITH VARIABLES INPUT FROM THE USER */

#include <iostream.h>
void main()
{
    int x;
    cout << "Enter a number" << endl;
    cin >> x;
    cout << "You have entered" << endl;
    cout << "x := " << x << endl;
}

OUTPUT :

Enter a number
40
You have entered
x :=40
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_59_0.png)

图 2.17. 程序 2.8 的输出屏幕。

EXPLANATION : 要从键盘读取用户数据，我们有对象 cin。它代表标准输入流。其语法为

```
cin >> var1 >> var2 >> var2...... >> var n
```

输入的值从左到右赋值，即第一个值赋给 var1，以此类推。这里我们只有一个 int 类型的变量 x。我们通过写 cin >> x 从用户处获取变量 x 的输入。随后使用 cout 将同一个变量显示出来。cin 是 iostream_with_assign 类的对象，>> 被称为 get from 或提取运算符。

# /*PROG 2.9 INPUT MIX DATA FROM USER */

```
#include <iostream.h>
void main()
{
    int x;
    float y;
    char ch;
    cout<<"Enter an int, char and"
        <<" a float value "<<endl;
    cin>>x>>ch;
    cin>>y;
    cout<<"You entered"<<endl;
    cout<<"Int value x :="<< x<<endl;
    cout<<"float value y :="<< y<<endl;
    cout<<"char value ch :="<< ch<<endl;
}
```

# OUTPUT :

Enter an int, char and a float value
15 h 12.45
You entered
Int value x :=15
float value y :=12.45
char value ch :=h

![](img/ad5299318df8d4d7c6df5eaa86590ea3_60_0.png)

图 2.18. 程序 2.9 的输出屏幕

# EXPLANATION :

在程序中我们有 3 个变量 x 为 int 类型，y 为 float 类型，ch 为 char 类型。这 3 个变量不是通过单个 cin 语句 cin>>x>>ch>>y 读取的。相反，我们通过写 cin>>x>>ch 读取了 int 和 char 类型的数据，然后通过写 cin>>y 读取了下一个数据，即 float 变量 y。

```
/*PROG 2.10 TAKING STRING DATA FROM USER */

#include <iostream.h>
void main()
{
    char s[15];
    cout << "Enter your name" << endl;
    cin >> s;
    cout << "Hello " << s << endl;
}
```

# OUTPUT :

Enter your name
Hari
Hello Hari

![](img/ad5299318df8d4d7c6df5eaa86590ea3_61_0.png)

图 2.19. 程序 2.10 的输出屏幕。

# EXPLANATION :

要从用户读取字符串，我们创建一个大小为 15 的字符数组 s。使用 cin >> s 我们接受了字符串 s。注意 cin 会在输入字符串中遇到第一个空白字符时停止，即遇到空格或制表符。所以如果你写 Hari Pandey，只有 Hari 会被接受到 s 中。

```
/* PROG 2.11 FINDING LIMITS OF INTEGRAL DATA TYPES */

#include <iostream.h>
#include <limits.h>
void main()
{
    cout << "CHAR_MIN    := " << CHAR_MIN << endl;
    cout << "CHAR_MAX    := " << CHAR_MAX << endl;
    cout << "INT_MIN     := " << INT_MIN << endl;
    cout << "INT_MAX     := " << INT_MAX << endl;
    cout << "SHRT_MIN    := " << SHRT_MIN << endl;
    cout << "SHRT_MAX    := " << SHRT_MAX << endl;
    cout << "LONG_MIN    := " << LONG_MIN << endl;
    cout << "LONG_MAX    := " << LONG_MAX << endl;
