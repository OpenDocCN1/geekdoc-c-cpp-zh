

它使用如下：

```cpp
d1 = -d; // equivalent to d1 = d.operator-();
```

参见下面给出的几个程序：

```cpp
/*PROG 8.9 OVERLOADING ++ VER 1*/
#include <iostream>
#include <conio.h>
class demo
{
	int num;
public :
	demo(){}
	demo (int x)
	{
		num = x;
	}
	demo operator ++ ( )
	{
		demo temp;
		temp.num = num;
		num++;
		return temp;
	}
	void show(char *s)
	{
		cout << "num of object" << s << "=" << num << endl;
	}
};
void main ( )
{
	clrscr( );
	demo d1(20), d2;
	d2 = d1++;
	d1.show("d1");
	d2.show("d2");
	getch( );
}
```

```cpp
temp.num = num;
    return temp;
}
void show(char *s)
{
    cout << "NUM OF OBJECT" << s << " :=" << num << endl;
}
};
void main()
{
    clrscr();
    demo d1(30), d2;
    d2 = ++d1;
    d1.show("d1");
    d2.show("d2");
    getch();
}
```

### OUTPUT

```
NUM OF OBJECT d1 :=31
NUM OF OBJECT d2 :=31
```

### EXPLANATION

该程序几乎与之前的程序相同，只是有一点不同。在程序中我们重载了前置 ++ 运算符。因此，在 operator ++ 函数中，首先递增 num，然后将其赋给临时对象的 num。结果 d1 和 d2 的 num 都得到值 31。

注意在之前的程序中如果写 d2 = ++d1 则仍会调用同一个 operator ++ 函数。那么编译器如何区分重载的前置 ++ 和后置 ++ 运算符呢。

参见下面给出的下一个程序：

```cpp
/* PROG 8.11 OVERLOADING PRE ++ AND POST ++ IN THE SAME PROGRAM */

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    demo(){}

demo (int x)
{
    num = x;
}
demo operator ++(int)
{
    demo temp;
    temp.num = num;
    num++;
    return temp;
}
demo operator ++( )
{
    demo temp;
    num++;
    temp.num = num;
    return temp;
}
void show(char *s)
{
    cout << "NUM OF OBJECT" << s << " = " << num << endl;
}
};
void main()
{
    clrscr();
    demo d1(30), d2, d3;
    d2 = d1++;
    d3 = ++d1;
    d1.show("d1");
    d2.show("d2");
    d3.show("d3");
    getch();
}
```

### OUTPUT

```
NUM OF OBJECT d1 = 32
NUM OF OBJECT d2 = 30
NUM OF OBJECT d3 = 32
```

### EXPLANATION

为了区分重载的前置和后置 ++，会向重载的后置 ++ 运算符函数传递一个 int 类型参数。此 int 参数除了帮助编译器在该运算符函数被隐式调用时区分前置和后置 ++ 运算符函数外，没有其他用途。在 main 中当执行 d2 = d1++ 时，会调用后置 ++ 运算符函数，而在 d3 = ++d1; 的情况下会调用前置 ++ 运算符函数。

```cpp
/* PROG 8.12 OVERLOADING UNARY - OPERATOR VER 1 */

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    demo(int x)
    {
        num = x;
    }
    void operator -()
    {
        num = -num;
    }
    void show()
    {
        cout << "num = " << num << endl;
    }
};
void main()
{
    clrscr();
    demo d1(10);
    cout << "Before" << endl;
    d1.show();
    -d1;
    cout << "After" << endl;
    d1.show();
    getch();
}
```

### OUTPUT

```
Before
num = 10
After
num = -10
```

### EXPLANATION

在 main 中语句 -d1 等价于 d1.operator-()。对象 d1 的 num 初始值为 10。当执行 -d1 时，它会调用重载的 - 运算符函数，该函数反转 num 的符号。这就是一元减运算符的工作方式。注意没有参数传递给函数。函数只是由对象 d1 直接调用。

```cpp
/* PROG 8.13 OVERLOADING UNARY - OPERATOR VER 2 */

#include <iostream.h>
#include <conio.h>
class demo
{
    int num;
public :
    demo() {}
    demo(int x)
    {
        num = x;
    }
    demo operator -()
    {
        demo temp;
        temp.num = -num;
        return temp;
    }
    void show(char *s)
    {
        cout << " Num of object" << s << " =" << num << endl;
    }
};
void main()
{
    demo d1(100), d2;
    d2 = -d1;
    d1.show("d1");
    d2.show("d2");
    getch();
}
```

### OUTPUT

```
Num of object d1 = 100
Num of object d2 = -100
```

### EXPLANATION

该程序与前一个程序相似，只是重载的运算符函数发生了变化——它返回 demo 类类型的对象。在 main 中当执行 d2 = -d1 时，内部等价于 d2 = d1.operator-()；在函数中创建一个临时对象，并在反转 num 符号后将其赋给 temp 的 num。此 temp 被返回给 d2，其中包含 -100，因为 d1 的 num 为 100。

```cpp
/* PROG 8.14 OVERLOADING UNARY + OPERATOR VER 1 */

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    demo(int x)
    {
        num = x;
    }
    void operator + ( )
    {
        num = num > 0 ? num : -num;
    }
    void show( )
    {
        cout << "num = " << num << endl;
    }
};
void main( )
{
    clrscr( );
    demo d1(-100);
    cout << "Before" << endl;
    d1.show( );
    +d1;
    cout << "After" << endl;
    d1.show();
    getch();
}
```

### OUTPUT

```
Before
num = -100
After
num = 100
```

### EXPLANATION

实际上一元 + 没有任何作用，即写 +x 不会影响 x 的值。但在程序中我们重载了一元 + 运算符使其使数字为正，即作为一个函数工作以求出数字的绝对值。在 main 中 +d1 等价于 d1.operator+()，它调用 operator+ 函数并检查 num 的值。如果它是正数，我们不改变它；如果它是负数，我们使其为正。

```cpp
/* PROG 8.15 OVERLOADING UNARY + OPERATOR VER 2 */

#include <iostream.h>
#include <conio.h>

class demo
{
    int dx, dy;
public :
    demo(int x, int y)
    {
        dx = x;
        dy = y;
    }
    void operator + ()
    {
        dx = dx > 0 ? dx : -dx;
        dy = dy > 0 ? dy : -dy;
    }
    void show()
    {
        cout << "dx=" << dx << endl;
        cout << "dy=" << dy << endl;
    }
};
void main()
{
    clrscr();
    demo d1(-10, 20);
    cout << "Before" << endl;
    d1.show();
    +d1;
    cout << "After" << endl;
    d1.show();
    getch();
}
```

### OUTPUT

```
Before
dx=-10
dy=20
After
dx=10
dy=20
```

### EXPLANATION

该程序与前一个程序相同，只是我们取了两个数据成员而不是一个。

```cpp
/* PROG 8.16 OVERLOADING INDIRECTION OPERATOR '*' */

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;

public :

    demo(int x)
    {
        num = x;
    }
    int operator *()
    {
```

现在考虑使用类重载一元 ++ 运算符的情况。

```cpp
demo operator ++();
```

在 main 中当我们写 d2 = d1++ 时，它在内部等价于 d2 = d1.operator++()。

使用友元重载的同一个 operator ++ 可以写成：

```cpp
friend demo operator ++ (demo d);
```

并且 **d2 = d1++** 等价于 **d2 = operator++(d1).**

**注意：** 使用类重载的一元运算符不传递参数，而使用友元重载时传递一个参数。

现在既然我们已经了解可以使用友元函数来重载运算符，就出现了为什么我们需要它们的问题，因为我们可以使用类的成员函数作为运算符函数来重载运算符。答案是对于写成 **d1 + d2, d1 + 20, d1 * 3** 这样的表达式，类运算符函数会工作，但在 **20 + d1, 10 * d1** 等左操作数为类对象的情况，类运算符函数将无法工作。在这种情况下我们可以使用友元函数。

```cpp
/*PROG 8.17 OVERLOADING BINARY + OPERATOR USING FRIEND VER 1*/

#include <iostream.h>
#include <conio.h>
class demo
{
    int num;
    public :
    demo( ){ }
    demo(int x)
    {
        num = x;
    }
    friend demo operator +(demo, int);
    void show(char *s)
    {
        cout << "num of object " << s << " = " << num << endl;
    }
};
demo operator +(demo T, int x)
{
    demo temp;
    temp.num = T.num + x;
    return temp;
}
void main()
{
    clrscr();
    demo d1(100), d2;
    d2 = d1 + 50;
    d1.show("d1");
    d2.show("d2");
    getch();
}
```

### OUTPUT

```
num of object d1 =100
num of object d2 =150
```

### EXPLANATION

声明 friend demo operator +(demo, int); 告诉编译器 operator + 是类的友元函数，它接受两个参数：一个为 demo 类类型，第二个为 int。在 main 中当执行 d2 = d1 + 50 时，它被解释为 d2 = operator+(d1, 50)。这会调用 operator + 并按值传递 d1 和 50。在函数内部创建一个临时对象，该对象求出 T.num 的和。此对象被返回到 main 并赋给 d2。

重载的 + 函数也可以写成类的成员函数。

```cpp
/*PROG 8.18 OVERLOADING BINARY + OPERATOR USING FRIEND VER 2*/

#include <iostream.h>
#include <conio.h>
class demo
{
    int num;
public :
    demo (){}
    demo(int x)
    {
        num = x;
    }
    friend demo operator *(int, demo);
    void show(char *s)
    {
        cout << "num" << s << "=" << num << endl;
    }
};
```

