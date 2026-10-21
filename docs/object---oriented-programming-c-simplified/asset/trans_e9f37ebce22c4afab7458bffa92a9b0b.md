

**说明：** 该程序不言自明。为了更好地理解，请参阅前一个程序的说明。

```cpp
/*PROG 11.30 DEMO OF BUILT-IN MANIPULATORS VER 5*/

#include <iostream.h>
#include <conio.h>

void main()
{
    int oct_enter;
    clrscr();
    cout<<"========================================"<<endl;
    cout<<"ENTER AN OCTAL VALUE \n";
    cout<<"========================================"<<endl;
    cin>>oct>>oct_enter;
    cout<<"========================================"<<endl;
    cout<<"HEX VALUE :="<<hex<<oct_enter<<endl;
    cout<<"========================================"<<endl;
    cout<<"DEC VALUE :="<<dec<<oct_enter<<endl;
    cout<<"========================================"<<endl;
    cout<<"OCT VALUE :="<<oct<<oct_enter<<endl;
    cout<<"========================================"<<endl;
    getch();
}
```

**输出：**

```text
========================================
ENTER AN OCTAL VALUE
========================================
17
========================================
HEX VALUE :=f
========================================
DEC VALUE :=15
========================================
OCT VALUE :=17
========================================
```

**说明：** 参见程序 11.28 的说明。

```cpp
/*PROG 11.31 DEMO OF BUILT-IN MANIPULATORS VER 5*/
#include <iostream.h>
#include <conio.h>

void main( )
{
	clrscr( );
	cout << "************************";
	endl(cout);
	cout << "FIRST LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	cout << "SECOND LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	cout << "THIRD LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	cout << "FOURTH LINE";
	endl(cout);
	cout << "************************";
	endl(cout);
	getch( );
}
```

**输出：**

```text
************************
FIRST LINE
************************
SECOND LINE
************************
THIRD LINE
************************
FOURTH LINE
************************
```

**说明：** 所有操纵符都以引用方式接收一个 `ostream` 类型的参数，因此我们可以将 `cout` 作为 `endl` 的参数传递。所以编写 `endl(cout);` 等价于编写 `cout<<endl;`。

## 11.5.1 创建自己的操纵符

除了使用 C++ 内置的操纵符之外，你还可以为了任何目的创建自己的操纵符。要创建不带任何参数的操纵符，语法如前所示：

```cpp
ostream & manip_name (ostream & mycout)
{
    _____________;
    _____________;
    _____________;
    return mycout;
}
```

所有用户定义的操纵符都必须以 `ostream` 类型的引用作为参数，并以 `ostream` 类型的引用作为返回值。由于使用该操纵符时我们传入的是 `cout` 的引用，因此操纵符实际执行的操作就好像直接操作 `cout` 一样。例如，考虑一个模拟双空格的操纵符：当我们使用它时，它会在流中先留下两个空格，然后继续。

```cpp
ostream & DS(ostream & mycout)
{
    mycout << " ";
    return mycout;
}
```

要使用它，我们可以这样写：**cout<<DS<<"hello"<<DS;**

这首先留下两个空格，打印 `hello`，然后再留下两个空格。如前所述，操纵符（无论是用户定义的还是内置的）的主要优点是，可以通过 **>>** 和 **<<** 方便地放入 **cin** 和 **cout** 流中。正是这一优点使操纵符广受欢迎。

为了便于理解，下面给出几个程序。

```cpp
/*PROG 11.32 CREATING YOUR OWN MANIPULATOR VER 1*/

#include <iostream.h>
#include <conio.h>

ostream & DS(ostream & mycout)
{
    mycout << " ";
    return mycout;
}

void main()
{
    clrscr();
    cout << "Before Applying manipulator";
    endl(cout);
    cout << "HELLO";
    endl(cout);
    cout << "After applying own manipulator";
    endl(cout);
    cout << DS << "HELLO" << DS;
    getch();
}
```

**输出：**

```text
Before Applying manipulator
HELLO
After applying own manipulator
    HELLO
```

**说明：** 在该程序中，下面给出的语句仅用于打印 `hello`：

```cpp
cout << "Before Applying manipulator";
    endl(cout);
    cout << "HELLO";
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_574_0.png)

图 11.18：用户自定义操纵符的逻辑实现

```cpp
/*PROG 11.33 CREATING YOUR OWN MANIPULATOR VER 2*/

#include <iostream.h>
#include <conio.h>

/* Manipulator for two spaces */
ostream & DSD(ostream & mycout)
{
    mycout << "  ";
    return mycout;
}

/*Manipulator for three spaces */
ostream & DST(ostream & mycout)
{
    mycout << "   ";
    return mycout;
}

void main( )
{
    clrscr( );
    cout << "Before Applying manipulator";
    endl(cout);
    cout << "HELLO";
    endl(cout);
    cout << "After applying own manipulator DSD";
    endl(cout);
    cout << DSD << "HELLO" << DSD;
    endl(cout);
    cout << "After applying own manipulator DST";
    endl(cout);
    cout << DST << "HELLO" << DST;
    getch( );
}
```

**输出：**

```text
Before Applying manipulator
HELLO
After applying own manipulator DSD
  HELLO
After applying own manipulator DST
   HELLO
```

**说明：** 该程序与上一个程序非常相似，唯一的区别是这里又声明了一个用户自定义操纵符，用于在所需字符串 **“HELLO”** 前放置三个空格。下图显示了操纵符的实际实现。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_576_0.png)

```cpp
/* PROG 11.34 CREATING YOUR OWN MANIPULATOR VER 3 */

#include <iostream.h>
#include <conio.h>
/* CREATION OF MANIPULATOR */
ostream & Rup(ostream & mycout)
{
        mycout << "Rs ";
        return mycout;
}
void main( )
{
        int money = 8000;
        clrscr( );
        cout << "==============================";
        endl(cout);
        cout << "AMOUNT IS SHOWN HERE";
        endl(cout);
        cout << "==============================";
        endl(cout);
        cout << Rup << money << "-/" << endl;
        cout << "==============================";
        endl(cout);
        getch();
}
```

**输出：**

```text
==================================
AMOUNT IS SHOWN HERE
==================================
Rs 8000/-
==================================
```

**说明：** 用户自定义操纵符 `Rup` 在 `cout` 语句中使用时只显示 “Rs”。它也可以这样使用：

```cpp
Rup (cout);
cout << money << endl;
```

因为 `Rup` 接受 `ostream` 类型的引用，而我们传入的是 `cout`。

```cpp
/* PROG 11.35 CREATING YOUR OWN MANIPULATOR VER 4 */

#include <iostream.h>
#include <conio.h>
#include <iomanip.h>
ostream & format(ostream & mycout)
{
    mycout << setw(8) << setfill('$');
    return mycout;
}

void main()
{
    int num1 = 1234;
    float num2 = 35.56;
    char *str = "HELLO";
    clrscr();
    cout << format << num1 << endl;
    cout << format << num2 << endl;
    cout << format << str << endl;
    getch();
}
```

**输出：**

```text
$$$1234
$$$35.56
$$$HELLO
```

`format` 操纵符与 `cout` 一起调用时会做两件事：将宽度设置为 8，并将填充字符设置为 `'$'`。对于 `num1`、`num2` 和 `str` 这三个数据，只需调用一次 `format` 即可设置宽度和填充字符 `'$'`。你可以根据需要选用任意格式化操纵符，并将其整合成自己的操纵符。

```cpp
/*PROG 11.36 CREATING YOUR OWN MANIPULATOR VER 5*/
#include <iostream.h>
#include <conio.h>

/*CREATION OF MANIPULATOR STARTS */

ostream & tab (ostream & mycout)
{
    mycout << "<t>";
    return mycout;
}

ostream & new_line(ostream & mycout)
{
    mycout << "\n";
    return mycout;
}

ostream & bell_alert(ostream & mycout)
{
    mycout << "\a";
    return mycout;
}

ostream & ver_tab(ostream & mycout)
{
    mycout << "\v";
    return mycout;
}

ostream & wel_mssg(ostream & mycout)
{
    mycout << "WELCOME";
    return mycout;
}
/* CREATION OF MANIPULATOR FINISH HERE */

void main()
{
    int a=5,b=6;
    char *name = "hari";
    clrscr();
    cout << "---------------------" << endl;
    cout << "DEMO OF TAB AND NEW LINE" << endl;
    cout << "---------------------" << endl;
    cout << a << tab << b << new_line;
    cout << endl;
    cout << "---------------------" << endl;
    cout << "DEMO OF VERTICAL TAB AND NEW LINE" << endl;
    cout << "---------------------" << endl;
    cout << a << ver_tab << b << new_line;
    cout << endl;
    cout << "---------------------" << endl;
    cout << wel_mssg << name << new_line;
    cout << endl;
    cout << "---------------------" << endl;
    cout << "DEMO OF BELL ALERT" << endl;
    cout << "---------------------" << endl;
    cout << bell_alert << a << tab << bell_alert << b << new_line;
    getch();
}
```

**输出：**

```text
----------------
DEMO OF TAB AND NEW LINE
----------------
5 6
----------------
DEMO OF VERTICAL TAB AND NEW LINE
----------------
5
```

