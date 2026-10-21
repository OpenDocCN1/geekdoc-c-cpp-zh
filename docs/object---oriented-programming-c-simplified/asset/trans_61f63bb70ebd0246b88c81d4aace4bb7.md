

# 面向对象程序设计 C++ 简化版

```
int & getsx ( )
{
return sx;
}
void shows( )
{
cout << "sx = " << sx << endl;
}
};
class first
{
int fx;
public :
first() {}
first(int x)
{
fx = x;
}
operator second ( )
{
second temp;
temp.getsx() = fx*fx;
return temp;
}
}
void showf ( )
{
cout << "fx = " << fx << endl;
}
};
void main ( )
{
clrscr ( );
first f(20);
second s(30);
cout << "Before conversion" << endl;
f.showf ( );
s.shows ( );
s = f;
cout << "After conversion" << endl;
f.showf ( );
s.shows ( );
getch( );
}
```

# OUTPUT :
Before conversion
fx=20
sx=30
After conversion
fx=20
sx=400

我们想要将类类型 first 的对象转换为类类型 second 的对象。因此在源类 first 中我们需要编写函数 operator second()，它将返回类类型 second 的对象。我们已在类 first 中完成了此操作。当语句 s=f 执行时，编译器会查找此转换函数。它找到了一个。在该函数中，我们找到了 fx 的平方并将其赋给了类 second 的 sx。注意 sx 是私有的，因此在位于类 first 中的函数 operator second() 中无法访问它。由于函数在类中，因此可以无问题地访问它。为了在 operator 函数 second 中获取 sx，我们通过编写一个返回 sx 引用的公共成员函数 getsx 来返回 sx 的引用。此引用获取值 fx*fx 和临时值。

```
/* PROG 8.36 DEMO OF TYPE CONVERSION ONE CLASS TYPE TO ANOTHER CLASS TYPE VER 2 */
#include <iostream.h>
#include <conio.h>

class first
{
 int fx;
 public :
 first(){}
 first (int x)
 {
  fx=x;
 }
 int getfx ( )
 {
  return fx;
 }
 void showf ( )
 {
  cout << "fx=" << fx << endl;
 }
};

class second
{
 int sx;
 public :
 second(){}
 second (int x)
 {
  sx=x;
 }
 int getsx ( )
 {
  return sx;
 }
 void shows ( )
 {
  cout << "sx=" << sx << endl;
 }
};

int main()
{
 first f(20);
 second s(30);
 cout << "Before conversion" << endl;
 f.showf();
 s.shows();
 s = f; // conversion
 cout << "After conversion" << endl;
 f.showf();
 s.shows();
 getch();
 return 0;
}
```

EXPLANATION : 该程序演示了将一个类类型对象转换为另一个类类型的第二种方法。同样，源类是 first，目标类是 second。这里在构造函数转换方法中，构造函数必须在目标类中定义。当 s = f 语句执行时，会调用 second(first obj) 构造函数，并通过按值调用机制将 f 赋给 obj。由于构造函数在类 second 中，我们无法访问私有成员 fx。为此，我们在类 first 中编写了公共成员函数 getfx，它返回 fx 的值。fx 的平方通过 getfx 间接赋给 sx。

```
/* PROG 8.37 DEMO OF TYPE CONVERSION ONE CLASS TYPE TO ANOTHER CLASS TYPE */

#include <iostream.h>
#include <conio.h>

class first
{
    int fx;
public :

    first() {}
    first(int x)
    {
        fx = x;
    }
    int getfx()
    {
        return fx;
    }
    void showf()
    {
        cout << "fx = " << fx << endl;
    }
};

class second
{
    int sx;
public :

    second() {}
    second(int x)
    {
        sx = x;
    }
    void operator = (first obj)
```

# 388 面向对象程序设计 C++ 简化版

```
{
  sx = obj.getfx() * obj.getfx();
}
void shows()
{
  cout << "sx=" << sx << endl;
};
void main()
{
  clrscr();
  first f(100);
  second s(200);
  cout << "Before Conversion" << endl;
  f.show();
  s.show();
  cout << "After Conversion" << endl;
  f.show();
  s.show();
  getch();
}
```

OUTPUT :

Before Conversion
fx=100
sx=200
After Conversion
fx=100
sx=200

![](img/ad5299318df8d4d7c6df5eaa86590ea3_407_0.png)

Figure 8.4. Output screen of the program 8.37

**EXPLANATION** : 该程序演示了将一个类对象转换为另一个类类型的第三种方法。在目标类 second 中编写了 `operator =` 函数，它接受一个类型为 first 的参数。当语句 `s = f` 执行时，它在内部被解释为 `s.operator = (f)`。其余部分不言自明。

```
/* PROG 8.38 TYPE CONVERSION CONVERTING HOUR TO MINUTES AND SECOND */

#include <iostream.h>
#include <conio.h>

class Hour
{
    unsigned int hr;

public:

    Hour(unsigned int x)
    {
        hr=x;
    }
    int gethr( )
    {
        return hr;
    }
    void showh( )
    {
        cout << "Hour =" << hr << endl;
    }
};
class secmin
{
    unsigned int sec, min;

public:

    secmin( ){ }
    secmin(Hour ob)
    {
        min = ob.gethr( )*60;
        sec = min*60;
    }
    void showsm( )
```

```
{
    cout << "Mins =" << min << endl;
    cout << "Secs =" << sec << endl;
}
};
void main()
{
    clrscr();

    Hour H(5);
    secmin sm;
    sm = H;

    H.showh();
    sm.showsm();
    getch();
}
```

# OUTPUT :

Hour =5
Mins =300
Secs =18000

![](img/ad5299318df8d4d7c6df5eaa86590ea3_409_0.png)

Figure 8.5. Output screen of program 8.38

# EXPLANATION :

类 Hour 包含一个数据成员 hr，用于保存输入的小时数。类 secmin 有一个构造函数，该构造函数具有 Hour 类的对象。当语句 sm =H 执行时，会调用 secmin 类的构造函数，并传递对象 H，该对象在变量 obj 中收集。在此构造函数内部，从 Hour 类对象计算分钟数和秒数。同样，由于 hr 是私有的，因此编写了一个返回 hr 的公共成员函数。

# 8.8 思考要点

- 1. 运算符重载是使运算符能够处理多种数据类型包括用户定义类型的机制。
- 2. 在 C++ 中使用关键字 operator 重载运算符。
- 3. 在 C++ 中只能重载已存在的运算符。
- 4. 运算符的重载不能改变运算符的优先级。
- 5. 可以使用 friend 关键字重载运算符。当左操作数不是类的对象时，它们是不可或缺的。使用 friend 重载二元运算符时，两个操作数都作为参数传递，而重载一元运算符时，只有一个参数传递给函数。
- 6. 我们不能重载以下运算符 :- ? : , . * , . : : 和 sizeof。
- 7. 不能使用 friend 重载 =, ->, 和 [ ] 运算符。
- 8. 为了将基本类型转换为类类型，在该类中创建该类型的一个参数构造函数。
- 9. 为了将类类型转换为任何基本类型，在类中创建以基本类型命名的运算符函数。
- 10. 为了将一个类类型对象转换为另一个类类型对象，可以使用构造函数或运算符方法。

# EXERCISE

# A. True and False :

- 1. Operator in C++ can be overloaded using the function named opt_overload.
- 2. The operator to be overloaded in C++, must already exist in the language.
- 3. All operators may be overloaded using friend functions.
- 4. The assignment operator cannot be overloaded.
- 5. The compiler won't give any error if* operator is overloaded to be perform summation.
- 6. A friend function cannot be used to overload the subscript operator [ ].
- 7. The precedence of an operator can be changed by overloading it.

# B. Answer the Following Questions :

- 1. What is operator overloading ?
- 2. Why do need operator overloading ?
- 3. What is the use of friend in operator overloading ?
- 4. What is the difference between postfix++ and prefix ++ ?
- 5. Can we change the precedence of operators using operator overloading ?
- 6. What are the operator overloading rules ?
- 7. Which operator cannot e overloaded by using friend ?
- 8. Which operator we cannot overload ?
- 9. Why we need type conversion ?
- 10. Explain two methods of conversion between objects of two different classes.

# C. Brain Drill :

- 1. Consider a class string where each objects contains an array of characters and the length of string. Write member function for
  (a) Initializing a string object either by a given string constant (e.g.,"dsdf") or by an integer indicating maximum size of string to be accommodated or by another string object.
  (b) Overloading the assignment operator overloading comparison operator = = so that string object may be compared with another string object and a constant string may be compared with other string object.
- 2. Write C++ program to overload a function named power( ) to allow the calculation of power of both ‘int’ and ‘float’ value.
- 3. Write a program to pass reference of object to operator function and change the contents of object. Use single object as source and destination.
- 4. Write a program to declare two classes Rupees and Dollar. Declare objects of both the classes and perform conversion between Rupees and Dollar using any of the conversion method.
- 5. Write a program using a class to convert square to square root and vice-versa. Write conversion methods between objects of two different class.
- 6. Write a program that substitutes an overloaded += operator for the overloaded + operator. This operator should allow statements like :
```
s1 + = s2;
```
Where s2 is added (concatenated) to s1 and the result is left in s1. The operator should also permits the results of the operation to be used in other calculations, as in
```
s3 = s1 + = s2;
```
- 7. For math buff only : Create a class Polar that represents the points on the plain as polar coordinates (radius and angle). Create an overloaded +operator for addition of two polar quantities. “Adding” two points on the plain can be accomplished by adding their X coordinates and then adding their Y coordinates. This gives the X and Y coordinates of the “answer”. Thus you will need to convert two sets of polar coordinates to rectangular coordinates, and them, and then convert the resulting rectangular representation back to polar.
- 8. Write a program that incorporates both the bMoney a class and the sterling class. Write conversion operators to convert between bMoney and strling, assuming that one pound (£1.0.0) equals fifty dollars ($50.00). This was the approximate exchange rate in the 19th century when British Empire was at its height and the pound-shillings-pence format was in use. Write a main( ) program that allows the user to enter an amount in either currency, and that then converts it to the other currency and displays the result. Minimize any modification to the existing bMoney and sterling classes.

