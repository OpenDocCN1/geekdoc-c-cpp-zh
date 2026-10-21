
输出：

Caught an int exception := 123

Caught a char exception := p

Caught a char* exception := NMIMS UNIVERSITY

![](img/ad5299318df8d4d7c6df5eaa86590ea3_685_0.png)

**图 14.17.** *程序 14.17 的输出屏幕*

**说明：** 语句 **void demo() throw(int, char, char*)** 指定函数 **demo** 可能抛出 **int、char** 和 **char\*** 类型的异常。使用 for 循环抛出所有指定类型的异常。所有抛出的异常都被各自的 **catch** 块捕获。

## 14.8 值得思考的要点

- 1. 异常是在程序中可能出现的运行时错误。
- 2. 如果异常未被处理，可能导致程序异常终止。
- 3. 为了处理异常，使用 try-catch 块。
- 4. 在编程术语中，异常被视为一个被抛出的对象。
- 5. 任何可能产生异常的代码或函数都放在 try 块中。通过使用关键字 throw 抛出异常。
- 6. 一个 try 块可以有多个 catch 块。
- 7. 在 try-catch 块嵌套的情况下，异常可以被重新抛出。要重新抛出异常，只需写 throw;
- 8. 函数可以通过在函数声明中指定来规定可以抛出什么类型的异常。
- 9. 用户自定义类的对象也可以作为异常被抛出。
- 10. 表达式 catch (...) 可用于捕获所有类型的异常。

## 练习

### A. 判断题：

- 1. throw 语句可用于抛出异常。
- 2. “throw”表达式创建一个指向异常对象的指针。
- 3. 抛出异常总是导致程序终止。
- 4. 可能产生运行时错误的代码放在 catch 块中。
- 5. 异常在编译期间产生。
- 6. 一组 catch 块可以与单个 try 块关联。

### B. 回答下列问题：

- 1. 什么是异常？
- 2. 我们如何处理异常？
- 3. 描述 try、catch 和 throw 的含义。
- 4. 我们如何捕获多个异常？
- 5. 我们如何捕获所有异常？
- 6. 解释 try-catch 的方法。
- 7. 我们如何限制一个函数只抛出特定类型的异常？
- 8. 如果抛出的异常未被捕获会怎样？

### C. 头脑风暴：

- 1. 编写一个程序，提示用户输入一个数字。如果数字不是偶数，则抛出异常。
- 2. 编写一个程序接受字符串。如果任一字符串不是以大写字母开头，则抛出异常。
- 3. 编写一个队列类，并包含所有必要的函数。每当队列为空且执行删除操作时，抛出一个 queue_empty 类的对象。类似地，每当队列满时，抛出 queue_full 类的异常。队列使用数组实现。
- 4. 编写一个程序，用 new 分配内存。如果没有足够的内存，则 new 返回 NULL。每当 new 返回 NULL 时，抛出异常。
- 5. 编写一个程序，将五个数字输入数组。每当输入一个大于 100 的数字时，抛出异常。
- 6. 有时使用异常最简单的方法是创建一个新类，其中异常类是其成员。尝试使用一个通过异常处理文件错误的类来实践这一点。创建一个 dofile 类，包含一个异常类以及读写文件的成员函数。此类的构造函数可以将文件名作为参数，并用该名称打开文件。你可能还需要一个成员函数将文件指针重置到文件开头。编写一个 main() 程序，提供相同的功能，但通过调用 dofile 类的成员来实现。

## 面向对象程序设计上机实验

实验1：演示函数重载特性的程序。

```
/*Program : Illustrating function overloading */

#include <iostream.h>
#include <conio.h>

void main()
{
    void show(int);
    void show(float);
    void show(char);
    void show(char*);

    int x = 10;
    float y = 23.45;
    char ch = 'p';

    char * s = "overload";

    clrscr();
    show(x);
    show(y);
    show(ch);
    show(s);
    getch();
}
```

```cpp
void show(int x)
{
	cout << "int show x=" << x << endl;
}
```

```cpp
void show(float y)
{
	cout << "float show y=" << y << endl;
}
```

```cpp
void show(char ch)
{
	cout << "char show ch=" << ch << endl;
}
```

```cpp
void show(char* s)
{
	cout << "char *s show s=" << s << endl;
}
```

```cpp
int show x=10
float show y=23.45
char show ch = p
char *s show s= overload
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_688_0.png)

在程序中，show 函数被重载了 4 次。从程序中可以看出，该函数只有一个参数，但每个函数中的参数类型各不相同。在 main 中，生成了 int、char、float 和 char* 类型的 4 个变量，并分别用这些参数调用 show。每个参数都传递给 show，show 被调用了 4 次。编译器根据调用 show 函数时参数的类型，调用相应的 show 函数版本，例如 show(x) 会调用 int 版本的 show 函数，以此类推。

```
/*Program : Function overloading max of two numbers */

#include <iostream.h>
#include <conio.h>

void main( )
{
    int x,y, intmax;
    float f1,f2,fmax;
    char ch1,ch2,chmax;

    int max2(int,int);
    float max2(float,float);
    char max2(char,char);

    clrscr( );
    cout << “Enter two integers \n”;
    cin >> x >> y;

    cout << “Enter two floats\n”;
    cin >> f1 >> f2;
    cout << “Enter two chars \n”;
    cin >> ch1 >> ch1;

    intmax=max2(x,y);

    fmax=max2(f1,f2);

    chmax=max2(ch1,ch2);

    cout << “Max of two int is ” << intmax << endl;
    cout << “Max of two float is ” << fmax << endl;
    cout << “Max of two char is” << chmax << endl;

    getch( );
}
int max2(int x,int y)
{
    return(x > y ? x : y);
}
```

```
float max2(float x,float y)
{
    return(x>y ?x :y);
}

char max2(char x,char y)
{
    return(x>y ?x :y);
}
```

输出：
Enter two integers
123 567
Enter two floats
12.34
56.78
Enter two chars
a g
Max of two int is 567
Max of two float is 56.78
Max of two char is g

![](img/ad5299318df8d4d7c6df5eaa86590ea3_690_0.png)

图 15.2. 程序的输出屏幕。

说明：在程序中，max2 函数有三个重载版本，分别接受 int、char 和 float 类型的两个参数，并返回两个数中的较大值。根据参数的类型，调用相应版本的 max2 函数。

实验2：演示各种运算符重载的程序。例如：二元运算符、一元运算符、new 和 delete 运算符等。

```
/*Program : Overloading binary + with class objects as argument */

#include <iostream.h>
#include <conio.h>
class demo_sum
{
    private :
        int num;
        static int count;
    public :
        void input()
        {
            cout << "Enter the number for" << "Object" << ++count << "\n";
            cin >> num;
        }
        void operator +(demo_sum temp)
        {
            int x;
            x = num + temp.num;
            cout << "Sum of two is " << x << endl;
        }
        void show()
        {
            cout << "The num is" << num << endl;
        }
};
int demo_sum ::count;
void main()
{
    clrscr();
    demo_sum d1,d2;
    d1.input();
    d1.show();
    d2.input();
    d2.show();
    d1 + d2;
    getch();
}
```

输出：
Enter the number forObject1
23
The num is23
Enter the number forObject2
45
The num is45
Sum of two is 68

![](img/ad5299318df8d4d7c6df5eaa86590ea3_692_0.png)

图 15.3. *程序的输出屏幕*

说明：函数

```
void operator + (demo_sum temp)
{
    int x;
    x = num + temp.num;
    cout << “sum of two is “ << x << endl;
}
```

重载了二元 + 运算符，并接受一个 **demo_sum** 类型的参数。在 **main** 中，语句 **d1+d2;** 在内部被解释为 **d1.operator +(d2)**，即 d1 调用该函数，并将 d2 作为参数传递给这个重载的二元 + 运算符函数。在函数内部，num 属于对象 **d1**（调用该函数的对象的成员，可以在函数内部直接使用，而无需用对象名加点运算符；其他使用 this 指针的语法将在后面讨论），而 **d2** 被复制到 **temp** 对象，因此 **temp.num** 是 **d2.num** 的一个副本。该函数计算总和并显示它。

```
/*Program : Overloading + and − in the same program */

#include <iostream.h>
#include <conio.h>
class demo_sum_sub
```

