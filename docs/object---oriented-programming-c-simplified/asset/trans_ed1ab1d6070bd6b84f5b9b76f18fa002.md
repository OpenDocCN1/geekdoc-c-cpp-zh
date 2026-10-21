

function was called. This saves time as there is no control transfer, no saving and popping back from stack-frame. So inline function executes faster than normal function. But at the place of inline function call, the code is expanded. If you have called inline function from 100 places in your program, the code will be expanded 100 places in your program thus increasing program size. So a trade-off between program size and execution efficiency is there. The general syntax of defining the inline functions as:

```
inline return type function_name (parameters)
{
    function definition;
}
```

## Some Important Points About Inline Function

- 1. Inline function is a request to the compiler thus inline function may not work as inline some times. In this regard they differ from macro, which work as macro always.
- 2. Inline function executes faster than normal function.
- 3. Strict type checking is performed for variables that are passed as arguments, which is not done in case of macro.
- 4. Inline function does not produce side effects whereas macro does.
- 5. All inline functions must be defined prior to their use.
- 6. Inline function does not work as inline when code contains loops, recursions, goto, switch, static variable etc.
- 7. They are used where function definition are small so calling cost and overhead for normal functions can be minimized.

```
/*PROG 5.17 DEMO OF INLINE FUNCTION VER 1*/

#include <iostream.h>
#include <conio.h>

inline void show()
{
    cout << "Hello from inline show\n";
}

void main()
{
    clrscr();
    show();
    getch();
}
```

OUTPUT :
Hello from inline show

EXPLANATION : The function show is inline so when it is called in the main it is simply expanded in the main. That is, all the statements written in the function show appear at the place of function call. Here we are having just one cout statement so it appear through we have written cout statement within main itself similar to macro.

```
/*PROG 5.18 DEMO OF INLINE FUNCTION VER 2*/

#include <iostream.h>
#include <conio.h>

inline void show( );

void main( )
{
    show( );
}
inline void show( )
{
    cout << "Hello from inline show\n";
}

OUTPUT :
Hello from inline show
```

EXPLANATION : An inline function has to be defined before it can be used. But the above program works fine in Visual Studio C++ compiler. However, in Turbo C 3.0 on executing the program makes system halts. There is no compilation error in Turbo C3.0.

```
/*PROG 5.19 SQUARE OF A NUMBER USING INLINE FUNCTION VER 1*/

#include <iostream.h>
#include <conio.h>

inline int square(int x)
{
    return x*x;
}

void main( )
{
```

```
{
 int num,snum;

clrscr();
cout << "Enter a number \n";
cin >> num;
cout << "Square of " << num << " is " << square(num) << endl;
getch( );
}
```

OUTPUT :

```
Enter a number
8
Square of 8 is 64
Square of 8 is 64
```

EXPLANATION : When the function is called as square (num), the function call is expanded in line as num*num. Rest is easy to understand.

```
/*PROG 5.20 SQUARE OF A NUMBER USING INLINE FUNCTION VER 2*/
#include <iostream.h>
#include <conio.h>
inline int square (int x)
{
return x*x;
}
void main ()
{
int s1 = square (2+3);
int s2 = square (3*4-5 + 6/2);
int s3 = square (+ +s1);
clrscr ();
cout << "s1 = " << s1 << endl;
cout << "s2 = " << s2 << endl;
cout << "s3 = " << s3 << endl;
}
```

```
getch();
}
```

## OUTPUT :

s1 = 26

s2 = 100

s3 = 676

## EXPLANATION :

Before expanding the function as function call is encountered compiler first computes the expression written as argument and make a single argument. So square (2+3) first turned into square (5) then expanded, similarly square (3*4-5+6/2) turned into square (10) and finally square (+ +s1) turned into square (26).

## /*PROG 5.21 SQR OF A NUMBER USING MACRO*/

```
#include <iostream.h>
#define SQR(x) (x*x)
#include <conio.h>

void main()
{
    int s1 = SQR(2 + 3);
    int s2 = SQR(3*4 - 5 + 6/2);
    int s3 = SQR(+ +s1);

    clrscr();
    cout << "s1 = " << s1 << endl;
    cout << "s2 = " << s2 << endl;
    cout << "s3 = " << s3 << endl;
    getch();
}
```

## OUTPUT :

s1 = 13

s2 = 41

s3 = 156

## EXPLANATION :

The side effect of macro can be seen in the above program. When macro SQR is expanded all three statements appear as :
    int s1 = 2 + 3*2 + 3;

int s2= 3*4-5*6/2*3*4-5+6/2;
int s3=++s1 * ++s1;
Now,
s1= 2+6+3=11;
s2= 12-5+3*3*4-5+3;
s2= 12+36+3-10;
s2=41
Due to pre increment twice and same value is used in the expression so s3= 13 * 13 = 169.

```
/*PROG 5.22 FINDING CUBE OF A NUMBER USING INLINE FUNCTION*/

#include <iostream.h>
#include <conio.h>

inline int cube(int x)
{
    return x*x*x;
}

void main()
{
    int num;
    clrscr();

    cout<<"Enter a number \n";
    cin>>num;
    cout<<"Cube of"<<num<<"is"<<cube (num)<<endl;

    getch();
}
OUTPUT :
Enter a number

12

Cube of 12 is 1728
```

EXPLANATION : The program is self-explanatory.

```
/*PROG 5.23 MAXIMUM OF TWO NUMBERS USING INLINE FUNCTION */

#include <iostream.h>
#include <conio.h>

inline int max(int x,int y)
{
    return x>y ? x :y;
}

void main()
{
    int n1,n2;

    clrscr();

    cout<<"Enter two numbers \n";
    cin>>n1>>n2;

    int m=max(n1,n2);

    cout<<"Max="<<m<<endl;
    getch();
}

OUTPUT :
Enter two numbers
12
45
Max=45
```

EXPLANATION : At the place of function call max (n1, n2), function is explained as return x>y ? X : y, value of n1 and n2 is assigned to x and y.

## 5.9 FUNCTION OVERLOADING

Overloading refers to use of same thing for different purpose. Function overloading refers to creating numbers of functions with the same name which performs different tasks. Function overloading is also known as function polymorphism. Function overloading relieves us from remembering so many functions names with type of arguments they take. In function overloading we can create number of functions with the same name but either number of arguments or type of arguments must be different. We provide few examples:

- 1. int sum (int);
      float sum(float);
      double sum(double);

Here, we have declared three functions with the same name sum. Each function takes just one parameter but all are of different types. That is number of parameters in all overloaded function sum is same but type of parameter is different.

- 2. void show(int,int);
      Void show(int);
      Void show(int,int,int);

Here number of parameters a re not same in show functions but type is same.

- 3. void show(int,char);
      void show (char,int,float);
      void show(int);
      int show(int,int);
      float show(char,char,char);

Here we have a mix of overloaded show functions. Some have same number of arguments but type is different and some have same type of argument but numbers of argument are different.

When we have number of overloaded functions in a program, which function to call is determined by either checking type of argument or number of argument. Note return type does not play any role in function overloading as which function to call is determined by checking type and number of argument a function accepts. When control is transferred to function and function is about to return after execution then return type comes to play.

In function overloading compiler first tries to find an exact match. If exact match is not find then integral promotion/ demotion is used. User defined conversion methods may be used also in case a class object is to be converted to any built-in type or vice-versa.

## /*PROG 5.24 DEMO OF FUNCTION OVERLOADING VER 1*/

```
#include <iostream.h>
#include <conio.h>

void main( )
{
    void show(int);
    void show(float);
    void show(char);
    void show(char*);

    int x =10;
    float y =23.45;
    char ch = 'p';
```

```
char * s ="overload";

clrscr( );
show(x);
show(y);
show(ch);
show(s);
getch( );
}

void show(int x)
{
    cout << "int show x =" << x << endl;
}

void show(float y)
{
    cout << "float show y =" << y << endl;
}

void show(char ch)
{
    cout << "char show ch =" << ch << endl;
}

void show(char*s)
{
    cout << "char *s show s =" << s << endl;
}

OUTPUT :
int show x      =10
float show y    = 23.45
char show ch    = p
char *s show s = overload
```

EXPLANATION : In the program we have functions show overloaded 4 times. The function takes a single parameter but each parameter is different in each function as can be seen from the program. In the main 4 variable of type int, char, float and char * type are generated and show is called with these parameters. Each parameter is passed to show and show is called 4 times. The compiler depending upon type of argument to function show calls the respective

