
### 15.6.4 To display trailing zeroes and decimal point in a floating point number : An Example

Consider the following statements:

```cpp
float a=54.210, b =25.00;
cout<<"a="<<a<<endl;
cout<<"b="<<b<<endl;
```

The cout statement will produce the output as

```text
a=54.21
b=25
```

Note that the trailing zeros do not appear in the output by default, 54.210 is printed as 54.21 by default. Also, the trailing decimal point does not appear in the output, that is, 25.00 is printed as just 25.

We can make the trailing zeros and decimal point to appear in the output value printed by setting the flag `ios::showpoint`

The statements

```cpp
float a=54.210, b =25.00;
cout.setf(ios::showpoint);
cout<<"a="<<a<<endl;
cout<<"b="<<b<<endl;
```

will produce the output as

```text
a=54.210
b=25.00
```

### 15.6.5 To display base of the number system in the output: An Example

Consider the statements below:

```cpp
int a=112;
cout.setf(ios::hex,ios::basefield);
cout<<"a="<<a<<endl;
```

The cout statement will print

```text
70
```

This is because 70 is hexadecimal representation of 112.

You can force C++ to print the base indicator of the number system at the beginning of the number by setting the flag `ios::showbase` as shown. The statements

```cpp
int a=112;
cout.setf(ios::hex,ios::basefield);
cout.setf(ios::showbase);
cout<<"a="<<a<<endl;
```

will generate the output as

```text
0x70
```

Note, the presence of 0x in the output, which represents that this is a hexadecimal number. Likewise, only symbol 0 (zero) would have been printed had it been an octal number.

### 15.6.6 Resetting flags

The flag once set remains in effect till the time it is reset. The function `unsetf()` is used to reset any flag in C++. For example, to reset the hex flag, you can invoke the function as follows:

```cpp
cout.unsetf(ios::hex);
```

This will stop giving hexadecimal outputs and the mode of the output will again return to default, which is the decimal number system.

## 15.7 Formatted I/O using Manipulators

`ios` functions are considered to be complex because of their syntax. Hence, to make programmers' lives easy, for each `ios` function, C++ offers an equivalent manipulator. The advantage of manipulators is that they have a simple syntax compared to the `ios` functions, and a call to the manipulators can be embedded within the `cout/cin` statement itself, rather than calling them separately using the `cout/cin` object.

Table 15.3 gives the list of I/O manipulators in C++ and their equivalent ios functions. All these manipulators except `endl` are defined in the header file **iomanip.h**. Hence, the program must include this header file before making use of these manipulators. `endl` unlike other manipulators is defined in the header file **iostream.h**.

The code below uses ios functions to set the precision as 8 and the width as 10, before printing the value of variable a.

```cpp
float a =20;
cout.precision(8);
cout.width(10);
cout.fill('$');
cout<<a;
```

**Table 15.3:** I/O manipulators

| I/O manipulator | Description |
|---|---|
| `setprecision(int pre)` | This is equivalent to the `precision()` function with 1 argument as described in ios functions |
| `setw(int width)` | This is equivalent to the `width()` function with 1 argument as described in ios functions |
| `setfill(char fillc)` | This is equivalent to the `fill()` function with 1 argument as described in ios functions |
| `endl` | Transfers the output cursor on the new line |

The same code can be written with equivalent manipulators as shown below:

```cpp
cout<<setprecision(8)<<setw(10)<<setfill('$')<<a;
```

This statement is exactly equivalent to that written using ios functions and will produce the same output as that of ios functions, as follows:

```text
$$$$$$$$20
```

## 15.8 Creating your Own Manipulator

You can also create your own manipulator rather than just using the built-in manipulators provided by C++. The following is the syntax to create custom manipulator:

```cpp
ostream& NameOfTheManipulator(Arguments)
{
/*Functionality of the manipulator*/
}
```

Consider the program below, it creates a manipulator for extended tab space and names it as ETAB, which is actually printing 3 tab spaces each time the manipulator is used.

```cpp
#include<iostream.h>
ostream& ETAB(ostream& t)
{
cout<<"\t\t\t";
return t;
}
void main()
{
cout<<"Hello"<<ETAB<<"Bye";
}
```

The function

```cpp
ostream& ETAB(ostream& t)
{
cout<<"\t\t\t";
return t;
}
```

contains a cout statement that prints 3 tab characters, hence, each time the manipulator is invoked it will print 3 consecutive TAB spaces.

> **NOTES**
>
> It is mandatory for the manipulator function to take an argument of ostream, if it is required to work with the cout object. This is because cout is an object of ostream.

The statement

```cpp
cout<<"Hello"<<ETAB<<"Bye";
```

in the program invokes the user-defined manipulator ETAB between Hello and Bye. Hence, there will be 3 TAB spaces printed between strings Hello and Bye as shown in the output of the code.

## 15.9 Passing Arguments to the Custom Manipulator

We have created a manipulator named ETAB in the previous section. This manipulator will always print 3 tab spaces when invoked. However, the number of tabs that we would want to print on the screen might not always be fixed as 3. Programmers would like to have an ability to configure the number of TABs that are printed by this manipulator. In such a case, we will have to create a manipulator that can take a parameter, which defines the number of TABs it should print. Such manipulators are called parameterized manipulators. One of the examples of parameterized manipulator is setprecision(int precision), which takes an integer argument to set the precision for floating point numbers or setw(int width), which takes width as a parameter to configure the output symbol spacing. Our requirement is that, we should be able to pass an integer parameter to the manipulator ETAB, to determine the actual number of TABs to be printed. For example, the statement

```cpp
cout<<"Hello"<<ETAB(5)<<"Bye";
```

should print 5 TABs between Hello and Bye since we have invoked the manipulator by passing integer constant 5.

Recall the format of creating user-defined manipulators in Figure 15.12, which supports passing custom arguments for parameterized manipulators. In this particular case, we need an additional parameter of type integer, which can give the number of TABs to be printed. Hence, we write the manipulator function, which takes an additional parameter named n

```cpp
ostream& NameOfTheManipulator (Arguments)
{
    /*Functionality of the manipulator*/
}
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_910_0.png)

```cpp
ostream& ETAB(ostream& p, int n)
{
        while (n>=1)
        {
                p<<"\t";
                n--;
        }
        return p;
}
```

```cpp
#include <iostream.h>
#include <iomanip.h>
class MyTab
{
private:
    ostream& (*ptrfn)(ostream&,int);
    int noOfTabs;
public:
    MyTab(ostream& (*arg1)(ostream&,int), int arg2)
    {
        ptrfn=arg1;
        noOfTabs=arg2;
    }
    friend ostream& operator<<(ostream& arg1, MyTab arg2);
};
ostream& ETAB(ostream& p, int n)
{
    while(n>=0)
    {
        p<<"\t";
        n--;
    }
    return p;
}
ostream& operator<<(ostream& arg1,MyTab arg2)
{
    return ETAB(arg1, arg2.noOfTabs);
}
MyTab ETAB(int n)
{
    return MyTab(ETAB,n);
}
void main()
{
    cout<<"Hello"<<ETAB(5)<<"World";
}
```

## 15.10 Character by Character Unformatted I/O Operations

The functions get() and put() are used to perform character by character I/O operations. This means that, they can only input/output one character at a time. Unlike insertion or extraction operators, which provide formatted input/output, get() and put() provide unformatted I/O operations in C++.
