
char MyName[];
cout << "a:" << a << endl;
cout << "b:" << b << endl;
cout << "Your name please:";
cin >> MyName;
cout << "Welcome dear " << MyName << " to the world of C++!";
}
Output:
a: 110
b: 0.11
Your name please: Saurabh
Welcome dear Saurabh to the world of C++!

The keyword cin is used for input in C++. The operator >> is used to separate the variables being input or output. A whitespace is used to separate items corresponding to different variables on the standard input device. The shift right operator >> is overloaded by C++ for this purpose. It is also called input operator or extraction operator. Program Code A.3 uses cin and cout for accepting two integers from the user and then displaying the sum of the two input numbers.

```
//A sample C++ program for illustrating cin and cout
#include<iostream.h>
main()
{
int a, b;
cout << "Enter values of a & b:";
cin >> a >> b;
cout << a << " + " << b << " = " << a + b;
}
Output:
Enter values of a & b: 5 6
5 + 6 = 11
```

An advantage of I/O in C++ is that it is format-free, that is, the programmer is not required to use formatting symbols to specify the type and order of items being input or output. Similar to other C++ operators, I/O operators can also be overloaded.

## A.3 FUNCTIONS IN C++

There are two kinds of functions in C++, namely regular functions and member functions. Member functions are those that are associated with a specific C++ class. Both types of functions are similar in all features excluding their scope.

A function consists of a function name, a list of arguments (input), a return type (output), and a body (code that implements a function). In Program Code A.4, Max is the function name, float a and float b are the list of arguments, where float is the return type, and the statements between { and } form the body of the function. Similarly, Square() is a function with int a as argument and int as the return type. Here, SayHello() is another function that has no argument, and it does not return any value, so its return type is void.

```
PROGRAM CODE A.4
// A sample C++ program-function
void SayHello()
{
cout << "Hello, welcome to the world of C with classes";
}
int Square(int a)
{
return a * a;
}
float max(float a, float b)
{
if(a > b)
return a;
else
return b;
}
void main()
{
int x, y, z;
SayHello();
cout << endl;
cout << "Enter number";
cin >> x;
cout << "Square of " << x << " is " << Square(x);
cout << "\nEnter two integers";
cin >> y >> z;
cout << "Maximum between " << y << " and " << z << " is " << max(y, z);
}
Output:
Hello, welcome to the world of C with classes
Enter number 5
Square of 5 is 25
Enter two integers 9 4
Maximum between 9 and 4 is 9
```

All functions in C++ return a value. If a function is not meant to return anything, we use void to denote its return type. A value is returned from a function by using the return statement. The return statement must return a value that is of the same type as the function's return type or should be converted to the desired type. The function terminates when a return statement is encountered. A function is invoked by supplying the actual arguments. Some examples are as follows:

- A call to function max(55.23, 76.89) returns 76.89.
- A call to function Square(5) returns 25.
- A call to function SayHello displays the message “Hello, welcome to the world of C with classes”.

### A.3.1 Inline Function

An inline function is declared by adding the keyword inline to the function definition as in Program Code A.5. Function PrintLine() is an inline function, whereas function PrintLine(int n, char ch) is not.

```
PROGRAM CODE A.5
// A sample C++ program-inline function
inline void PrintLine()
{
    cout << "---------";
    cout << endl;
}
void PrintLine(int n, char ch)
{
    for(i = 1; i <= n; i++)
        cout << ch;
    cout << endl;
}
// calling function
void main()
{
    PrintLine();
    PrintLine(10, 'S');
}
Output:
---------
SSSSSSSSSS
```

The inline keyword instructs the compiler that any calls to the inline function PrintLine() must be replaced by the body of the called function. This eliminates the overhead from performing a function call and copying arguments when the program is executing. When a member function is defined within a class definition as in Program Code A.6, it is automatically made inline.

The objective of the inline and const keywords is to avoid the use of preprocessor directives such as #define. This preprocessor directive has been traditionally used to perform macro substitution. A macro is similar to a function except for the difference that functions are called whereas macros are substituted. Excessive use of preprocessor directives makes it hard to use programming tools such as debuggers and profilers (used for debugging) efficiently.

The use of an inline function is beneficial for shorter code. However, as inline function calls are replaced by function definitions, this expansion results in larger code in case of lengthy functions. The compiler may ignore the demand to make a function inline in some cases when a function is recursive or it contains static variables or loop, switch, or goto statements.

```
PROGRAM CODE A.6
// A sample C++ program-inline function
#include<iostream.h>
class ABC
{
    int a, b, c;
public:
    void GetData()
    {
        cin >> a >> b >> c;
    }
};
void ABC :: ShowData()
{
    cout << a << "\t" << b << "\t" << c;
}
```

Here, ShowData() is a member function whose code is written outside the class definition. The function GetData() is defined inside the class definition, and hence is considered as an inline function. If the user wishes to define a function outside the class and still wants to make it an inline function, it can be done by explicitly instructing the compiler to do so, as shown in Program Code A.7.

```
PROGRAM CODE A.7

// A sample C++ program with inline function outside class
#include<iostream.h>
class ABC
{
    int a, b, c;
    public:
        void GetData()
        {
            cin >> a >> b >> c;
        }
};

inline void ABC :: ShowData()
{
    cout << a << "\t"<< b << "\t" << c;
}
```

We have discussed that an inline function call is replaced by its code, similar to macro expansion. However, there is one major difference between an inline function and a macro. Let us consider the code in Program Code A.8.

```
PROGRAM CODE A.8

// A sample C++ program with macro and inline function
#include<iostream.h>
#define Square1(x) x * x
inline int Square2(int x)
{
    return x * x;
}
int main()
{
    cout << "\n Using macro" << Square1(5 + 5);
    cout << "\n Using inline function" << Square2(5 + 5);
}
Output:
Using macro 30
Using inline function 100
```

If we observe the output of the code, we see that the expected output is correctly provided by the inline function and not by the macro. This difference makes inline functions far superior to macros.

## A.4 C++ CLASS AND ABSTRACT DATA TYPE

Classes in C++ are a natural evolution of the C notation struct. C++ also has the concept of structures. The only difference between a structure and a class in C++ is that, by default, the members of a class are private, whereas the members of a structure are public. Object-oriented programming encapsulates data (attributes) and functions (behaviour) into packages called classes.

### A.4.1 Class

A class is a user-defined data type whose variables are objects. It is created using the keyword class. A class is similar to a blue print. Based on a blue print, a builder can build one or more houses. Similarly, based on a class, a programmer can create one or more objects. One class can be reused many times to make many objects of the same class. Classes enable the programmer to model objects that have certain attributes (data members) and behaviour (operations). A sample class definition is given in Program Code A.9.

```
// A sample C++ class definition
class Time
{
 private:
 int Hour;
 int Minute;
 int Second;
 public:
 Time();
 void SetTime(int, int, int);
 void DisplayTime();
};
