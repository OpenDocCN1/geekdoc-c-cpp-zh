
Argument values Received by the function:10 Hello World
Argument values Received by the function:10.2 H

In Program 2.34, X and Y are the two different template types. These template types are used to define a and b input arguments of generic_fun. When generic_fun<10,20.2> is called X becomes integer data type, and the Y becomes float data type. When a,b are called by the generic_fun, the values of a and b will be echoed on to the screen.

## 2.7.1.1 Generic Functions can be Overloaded

Overloading a template function with a normal function: As methods are overloaded generic function can also be overloaded, whenever new logic is required to perform the same functionality for any of the data type.

### Program 2.35

```
/*Explicitly Overloading Generic Functions*/
#include<iostream.h>
#include<conio.h>
template<class X,class Y>void generic_fun(X a,Y b)
{
cout<<"\nA="<<a<<" B="<< b;
}
void generic_fun( int a,int b)
{
int sum=a+b;
cout<<"\nSum="<<sum;
}
void main()
{
clrscr();
generic_fun(10,20); /*int generic_fun will be called*/
generic_fun(10,20.2); /*generic generic_fun will be called*/
generic_fun("Hello"," World");
}
```

### Output

```
Sum=30
A=10 B=20.2
A=Hello B=World
```

In Program 2.35, the template generic_fun will be called for all the data types except when generic_fun is called with two integer arguments. Here the template function generic_fun is overloaded with generic_fun(int,int) function. Whenever generic_fun(int,int) is called void generic_fun(int a,int b) will be called. For all the other data types, the template function generic_fun will be called.

Overloading a template function with another template function: As template functions are overloaded with the normal functions, a generic function can be overloaded with another template function. Depending upon the number of arguments, a generic function will be called. In Program 2.36, generic_fun(X a, b) template function is overloaded with another template function generic_fun(X a,Y b). When generic_fun(10); is called, the template function generic_fun(X a) will be called. When generic_fun(10,20.2) is called, the second overloaded template function generic_fun(X a, Y b) will be called.

### Program 2.36

```
/*Explicitly Overloading Generic Functions*/
#include<iostream.h>
#include<conio.h>
template<class X>void generic_fun( X a)
{
cout<<"\nA="<<a;
}
template<class X,class Y>void generic_fun(X a,Y b)
{
cout<<"\nA="<<a<<" B="<<b;
}
void main()
{
clrscr();
generic_fun(10); /*first template generic_fun will be called*/
generic_fun(10,20.2);/*Second template generic_fun will be called*/
generic_fun("Hello","World");/*Second template generic_fun will be called*/
}
```

### Output

```
A=10
A=10 B=20.2
A=Hello B=World
```

## 2.7.1.2 Standard Parameters can Be Used with the Template Function

A template function can be defined with the constants and predefined standard parameters. In Program 2.37, height is a constant parameter, the template function volume_of_cube(X l, X b) can use the standard parameter. The program is written with height as constant value 8, and the volume of a cube whose height is 8 can be computed with the generic function volume_of_cube(X l, X b).

### Program 2.37

```
/*Using Standard Parameters with Template Functions, For demonstrating constants can be mixed with the generic data type*/
#include<iostream.h>
#include<conio.h>
const int height=8; /*Here Height of the volume is fixed*/
template<class X>void volume_of_cube(X l,X b)
{
X volume=l*b*height;
cout<<"\nVolume of Cube where has constant height as '8' is:"<< volume;
}
void main()
{
clrscr();
volume_of_cube(10,20);
}
```

### Output

```
Volume of Cube where has constant height as '8' is:1600
```

## 2.7.2 CLASS TEMPLATES

As generic functions are possible, defining the generic classes is also possible with templates. Generic classes are very useful for writing a program with the same logic for more number of data types.

The general form of a template class is as follows:

```
template<class template-type>class class-name
{
//definition of the template class
}
```

The general form of a class template with more parameters is as follows:

```
template<class template-type1,class template-type2,...>class class-name
{
//definition of the template class
}
```

Here template-type can be of any data type, and any number of class template-types can be defined in the template class definition.

An object for the template class can be created using the general form below:

```
Class-name<data type>object;
```

Operations of the stack can be generalized for all the data types. So, instead of writing different classes with different data types, a single generic class stack program can be applied for all the data types (Program 2.38).

### Program 2.38

```
/*Generic Class*/
#include<iostream.h>
#include<conio.h>
template<class T>class A
{
T a,b,sum;
public:
void setAB(T x,T y)
{
a=x;
b=y;
sum=a+b;
}
void showAB()
{
    cout<<"\nA="<<a<<" B="<<b<<" SUM="<<sum;
}
};
void main()
{
    A<int>obj_int;
    A<float>obj_float;
    clrscr();
    obj_int.setAB(10,20);
    obj_int.showAB();
    obj_float.setAB(0.1,0.2);
    obj_float.showAB();
}
```

### Output

```
A=10 B=20 SUM=30
A=0.1 B=0.2 SUM=0.3
```

```
/*Generic Class*/
```

### Program 2.39

```
#include<iostream.h>
#include<conio.h>
template<class T1,class T2>class SUM
{
    T1 a;
    T2 b;
    public:
    SUM(T1 x,T2 y)
    {
        a=x;
        b=y;
    }
    void show()
    {
        cout<<"\nSum of "<<a<<", "<<b<<"="<<(a+b);
    }
};
void main()
{
    clrscr();
    SUM<int> obj1(10,20);
    SUM<float> obj2(0.1,0.2);
    obj1.show();
    obj2.show();
}
```

### Output

![](img/45784b9f0334626143002ec0d63692fd_106_0.png)

In Program 2.39, SUM is a class to find the addition of two numbers. The generic class helps the developer to use the same generic template class for the sum of two integers and the sum of two float values. The same SUM class is used to create obj1 with integers and the obj2 with floats to find the generic problem of the addition of two numbers.

A generic class can have default argument types and with the default values.

## 2.8 RECURSION

Recursion is a technique of calling a function by itself. Sometimes a function calling itself may produce bugs, but when its technique is correctly used it is very powerful. Recursion can be easily understand with a fact() function whose operation is to find the factorial of a number. The non recursive technique of fact() appears as follows:

Non-recursive or iterative way of fact():

```
int fact(int n)
{
 int i,result;
 result=1;
 for(i=1;i<=n;i++)
 result=result*i;
 return(result);
}
```

In the above program, the loop in the non-recursive fact() function executes from 1 to n and multiplies each number.

Recursive way of fact():

### Program 2.40

```
#include<iostream.h>
int factorial( int n )
{
 int n;
 int result ;
 cout<<"enter an integer";
 cin>>n;
 result=fact( n);
 cout<<"Factorial of "<<n<<" is "<<result;
 return 0;
}

int fact( int n)
{
 if(n==1) return 1;
 else
 return n*fact(n-1); //call by itself.
}
```

### Output

```
Enter an integer
5
Factorial of 5 is:120
```

In Program 2.40, the operation of the recursive fact() is somewhat complex, when fact() is called with an argument as 1 the function returns 1, otherwise it returns the value of n*fact(n-1). If value is 5, fact is called for the first time with 5 as an argument and second time it is called with an argument of 4 and third time with an argument 3 and so on until n is equal to 1. Each call of fact() stores the value of n while calling itself with another value of n.

When a function calls itself, a new set of local variables and arguments is allocated, and the function code executes with these variables. A recursive call does not create a new copy of function but a new a copy of values being operated are created. Every recursive function must be ended, otherwise it will call itself forever. The statement if(n==1) in the program does this, when the n value becomes 1 the program terminates.

The main advantage of the recursive function is that they can be used to implement several algorithms in the simplest way. The implementation of the quick sort is difficult using the iteration way. Thus, some may think that recursion is easier to iteration.

## SUMMARY

- Robustness, adaptability and reusability are goals of an object-oriented design.
- Abstraction, encapsulation and modularity are principles of an object-oriented design.
- Constructors are used for initializing objects. Destructors are used to destroy objects.
- Default constructors, parameterized constructors and copy constructors are the types of constructors.
- Constructor overloading is a technique of defining more than one constructor with the same name.
- Operator overloading changes the meaning of the predefined operators.
- Inheritance derives a new class from the already existing class. Access to base class members is controlled through public, private and protected access specifiers.
- The derived class will have the members of the base class based on the declaration type such as private, public or protected and the access specifier at the time of inheriting the base class.
- Single inheritance and multiple inheritance are the basic classifications of inheritance.
- Inheritance can be further divided into various types: hierarchical inheritance, single-level inheritance, multi-level inheritance, hybrid inheritance and multipath inheritance.
- When the access specifier of the base class is public, all the public members of the base class are accessible to the derived class.
- When the access specifier of the base class is private, then all the public, protected members of the base class become private members of the derived class.
- All the public and protected members of the base class become protected members of the derived class when the access specifier of the base class is protected. All the private members of the base class are not accessible by the derived class.
- Delegation is a mechanism in which the object of one class is used as a member of another class.
- Polymorphism defines one interface with many forms.
