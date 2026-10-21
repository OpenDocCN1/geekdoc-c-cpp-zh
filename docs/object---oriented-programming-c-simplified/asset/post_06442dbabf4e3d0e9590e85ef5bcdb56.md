
version of the show function i.e., in case of show(x), show function of int version will be called and so on.

```
/*PROG 5.25 DEMO OF FUNCTION OVERLOADING VER 2*/

#include <iostream.h>
#include <conio.h>

void main()
{
    void show(int);
    void show(double);

    clrscr();

    show(23);
    show('p');
    show(2.5f);
    show(3.45);
    getch();
}

void show(int x)
{
    cout << "int show x=" << x << endl;
}

void show(double s)
{
    cout << "double show s=" << s << endl;
}

OUTPUT :
int show x=23
int show x=112
int show x=2.5
int show x=3.45
```

EXPLANATION : In the program we have just overloaded function show which takes a single parameter of int and double respectively. In function call show (23), int version of show is called as 23 is an integer. In function call show ('p'), int version of show is called why ? The compiler searches for an overloaded show function which takes a parameter of type char, but it fails as there is no such overloaded function we have written. So it does
integral promotion from char to integer and calls the int version of show function displaying ASCII value of `p`. Similarly in function call show (2.5f), compiler look for an overloaded function show which takes float type argument. If fails and overloaded function show with double type value is called.

```
/*PROG 5.26 DEMO OF FUNCTION OVERLOADING VER 3*/

#include <iostream.h>
#include <conio.h>

void main()
{
    void show(float);
    void show(double);

    clrscr();

    show(23);
    show(2.5f);
    show(3.45);

    getch();
}

void show(float x)
{
    cout << "float show x=" << x << endl;
}

void show(double s)
{
    cout << "double show s=" << s << endl;
}

OUTPUT :
ERROR
‘show’ : ambiguous call to overloaded function
```

EXPLANATION : The function call show (23) is ambiguous as there is no overloaded function show which takes an int type of value. Now compiler is in dilemma whether to call overloaded float version of show or overloaded double version of show as can be converted to float as well as to double.

## 180 Object-Oriented Programming C++ Simplified

```
/*PROG 5.27 DEMO OF FUNCTION OVERLOADING VER 4*/
#include <iostream.h>
#include <conio.h>

void main()
{
 void show(int);
 void show(float);

 clrscr();
 show('p');
 show(3.45);
 getch();
}

void show(float x)
{
 cout << "float show x = " << x << endl;
}

void show(int s)
{
 cout << "int show s = " << s << endl;
}
```

OUTPUT :
Error
'show' : ambiguous call to overloaded function

EXPLANATION : The error is clear as we have not defined an overloaded function show for the double data type. When function call show (3.45) is encountered compiler look for an overloaded function show which takes a single parameter of double type. But the error is not what we are thinking. The function call show ('p') calls the int version of show. In the function call show (3.45) as overloaded show for double data type was not written, int or float version of show can be called. Deciding this confuses the compiler and it generates the error. One more example of demotion is given.

```
/*PROG 5.28 DEMO OF FUNCTION OVERLOADING VER 5*/
#include <iostream.h>
#include <conio.h>

void main()
{
    void show(int);
    clrscr();
    show(5.47f);
    show(3.45);
    getch();
}

void show(int s)
{
    cout << "int show s=" << s << endl;
}

OUTPUT :
int show s=5
int show s=3
```

EXPLANATION : Demotion takes place from float to int in function call show (5.47f) and from double to int in function call show (3.45).

```
/*PROG 5.29 DEMO OF FUNCTION OVERLOADING VER 6*/

#include <iostream.h>
#include <conio.h>

void main()
{
    void show(float);
    void show(char);

    clrscr();
    show(4.76f);
    show(345);
    getch();
}
void show(char x)
{
    cout << "Char show x=" << x << endl;
}

void show(float s)
{
    cout << "int show s=" << s << endl;
}

OUTPUT :
Error
'show' : ambiguous call to overloaded function.
```

EXPLANATION : As there is no overloaded int version of show, the compiler is in confusion whether to demote int or char and call version of show or promote int to float and call float.

```
/*PROG 5.30 FUNCTION OVERLOADING MAX OF TWO NUMBERS */

#include <iostream.h>
#include <conio.h>

void main()
{
    int x,y, intmax;
    float f1,f2,fmax;
    char ch1,ch2,chmax;

    int max2(int,int);
    float max2(float,float);
    char max2(char,char);

    clrscr();
    cout << "Enter two integers \n";
    cin >> x >> y;

    cout << "Enter two floats\n";
    cin >> f1 >> f2;
    cout << "Enter two chars \n";
    cin >> ch1 >> ch2;

    intmax = max2(x,y);

    fmax = max2(f1,f2);

    chmax = max2(ch1,ch2);

cout << "Max of two int is "<<intmax<<endl;
cout << "Max of two float is "<<fmax<<endl;
cout << "Max of two char is"<<chmax<<endl;

getch();
}
int max2(int x,int y)
{
    return(x>y ?x :y);
}

float max2(float x,float y)
{
    return(x>y ?x :y);
}

char max2(char x,char y)
{
    return(x>y ?x :y);
}
```

### OUTPUT :

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

**EXPLANATION :** We have in the program three over of function max2 which takes two parameters of type int, char, and float and returns the maximum of two numbers. Depending upon type of parameter appropriate version of max2 function is called.

### 5.10 FUNCTION WITH DEFAULT ARGUMENTS

In C ++ it is possible for a function not to specify all its arguments. Some of the arguments may be specified their default values at the time of declaring the function. When a function
having default argument is called, compiler checks for the number and type of argument as well as was not specified during the function call, default value of that argument is assumed. In case we provide a new value, default argument is overridden.

For example :

```
void show (int x, int y = 20);
```

The function show takes two argument of int type out of which second argument from left is default. In case function is called as show (10), default value of y i.e., 20 is assumed. If function is called as show (10,100) than default value of y i.e., 20 is overridden. It is possible not to provide even the formal parameter names during function declaration i.e., we may declare the above function show as

```
void show (int, int = 20);
```

In a function with default argument, if one argument is default, all successive arguments must be default. We cannot provide default values in the middle of the arguments or towards left side. We provide few examples:

- 1. void fun(int x, int y = 20, int z=35);
- 2. void fun(int x, int y = 30, int z);
- 3. void fun(int x = 45, int y);

Out of three examples given only 1 is valid and 2 and 3 are invalid. In the 2 middle argument is default and the next argument z is not default. In the 3 first argument is default and next argument is not default.

```
/*PROG 5.31 DEMO OF FUNCTION WITH DEFAULT ARGUMENT VER 1*/

#include <iostream.h>
#include <conio.h>

void main( )
{
    void show(int x = 10);

    clrscr( );

    cout << "Called show with argument 20\n";
    show(20);

    cout << "Called show without argument \n";
    show( );

    getch( );
}
void show(int y)
{
    cout << "Argument to show was" << y << endl;
}

OUTPUT :
Called show with argument 20
Argument to show was20
Called show without argument
Argument to show was10
```

**EXPLANATION :** The function show takes just one argument of type int which is a default argument. Note default argument has to be specified in the function declaration. Writing it in function definition is optional. In the function call show (20), the default argument is overridden and y takes the value 20. In the function call show ( ) as no argument was specified, the compiler assumes default value 10 for y. Note argument name is declaration and definition are different, they may be same. Note function declaration can be written in the following manner too:

```
void show (int=10);
```

```
/*PROG 5.32 DEMO OF FUNCTION WITH DEFAULT ARGUMENTS VER 2*/

#include <iostream.h>
#include <conio.h>

void main( )
{
    void show(char* s = "Good Morning");
    clrscr( );
    show( );

    show("Good Evening");
    getch( );
}
void show(char *s)
{
    cout << "Argument to show was" << s << endl;
}

OUTPUT :
Argument to show was Good Morning
Argument to show was Good Evening
```
