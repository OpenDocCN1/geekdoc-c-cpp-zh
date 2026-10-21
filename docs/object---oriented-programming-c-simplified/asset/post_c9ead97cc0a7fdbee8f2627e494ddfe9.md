
It is used as follows :

```cpp
d1 = -d; // equivalent to d1 = d.operator-();
```

See few programs given below :

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

The program is almost same as the previous program with a little difference. In the program we have overloaded pre ++ operator. So, in the operator ++ function first num is incremented then assigned to num of temporary object. As a result both d1 and d2 get the value 31 for the num.

Note in the previous program if you write d2 = ++d1 then again the same operator ++ function would be called. Then how does the compiler distinguish between an overloaded pre++ and post ++ operator.

See the next program given below :

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

To distinguish between an overloaded pre and post ++, an int type argument is passed to the overloaded post ++ operator function. This int argument does not serve any purpose except helping the compiler to see the difference between a pre and post ++ operator function when this operator function is called implicitly. In the main when d2 = d1++ executes, post++ operator function will be called and in case of d3 = ++d1; pre++ operator function would be called.

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

In the main the statement -d1 is equivalent to d1.operator-(). The initial value of num for object d1 is 10. When -d1 executes it calls overloaded - operator function which reverses the sign of the num. This is the way the unary minus operator works. Note no argument is passed to the function. The function is simply called by the object d1.

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

The program is similar to the previous one with the change in overloaded operator function – which returns an object of demo class type. In the main when d2 = -d1 executes it becomes internally as d2 = d1.operator-(); in the function a temp object is created and after reversing the sign of num, it is assigned to num of temp. This temp is returned to d2 which contains -100 as num of d1 was 100.

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

Practically unary + does not serve any purpose i.e., writing +x does not affect the value of x. But in the program we have overloaded unary + operator to make a number positive, i.e., work as a function which finds absolute value of the number. In the main +d1 is equivalent to d1.operator+() which calls the operator+ function and checks the value of num. If it is positive, we do not change but if it is negative we make it positive.

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

The program is same as the previous one but instead of one data member we have taken two.

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

Now consider the case of overloading unary ++ operator overloaded using class.

```cpp
demo operator ++();
```

In main when we write d2 = d1++, it is internally equivalent to d2 = d1.operator++();

The same operator ++ overloaded using friend can be written as :

```cpp
friend demo operator ++ (demo d);
```

And **d2 = d1++** is equivalent to **d2 = operator++(d1).**

**Note :** In unary operators overloaded using class no argument is passed whereas overloaded using friend one argument is passed.

Now as we have understood that friend function can be used for overloading operators, the question arises why we need them when we can overload operators using operator function as member function of class. The answer is that in case of expressions written as **d1 + d2, d1 + 20, d1 * 3**, class operator functions will work but in case of expressions like **20 + d1, 10 * d1** etc., class operator functions will not work as left operand must be an object of the class. In such situations we can use friend function.

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

The declaration friend demo operator +(demo, int); tells the compiler that operator + is a friend function of the class which takes two arguments: one of class demo type and second as an int. In the main when d2 = d1 + 50 executes it is interpreted as d2 = operator+(d1, 50). This calls the operator + and passes d1 and 50 by value. Inside the function a temporary object is created which finds sum of T.num. This object is returned to main and assigned to d2.

The overloaded + function could be written as member function of the class.

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
