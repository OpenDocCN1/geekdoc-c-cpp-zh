
int main ()
{
    try
    {
        long double*array=new long double[100000000000000000];
    }
    catch (exception& e)
    {
        cout << "Here is an error: " << e.what()<< endl;
    }

    return 0;
}
```

Output

Here is an error: std::bad_alloc

We can throw our pre-decided error, in addition we can also decide what to show for what() function.

Consider the following program:

```
#include <iostream>
#include <exception>
using namespace std;
class myexception: public exception
{
    virtual const char* what() const throw()
    {
        return "My exception occured";
    }
}
myexample;
int main ()
{
    try
    {
        throw myexample;
    }
    catch (exception& e)
    {
        cout << e.what() << endl;
    }

    return 0;
}
```

Output

My exception occurred

![](img/5340985153962870d4e4a3b9453b9146_249_0.png)

## Namespaces

Is it possible to define two same variables with different data types?

Consider the following program:

```
#include<iostream>
int main()
{
    int var=3;
    float var=5;
    cout<<var;
}
```

This program will display an error saying “[Error] conflicting declaration ‘float var’”.

But it is possible to define two variables with the same name using namespaces!

To declare a namespace, we use the following syntax:

```
namespace namespace_name
{
//statements
}
```

After writing the above line, whatever we write those are parts of this namespace.

If we are in another namespace then we use resolution operator (::) to access the elements of that namespace.

Consider the following program:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int var=3;
}
namespace ns2
{
    float var=5;
}
int main()
{
    cout<<ns1::var<<endl;
    cout<<ns2::var;
}
```

Output

3

5

However, remember that Turbo C++ does not support **namespace** keyword. If you are using Turbo C++ then various programs implemented in this chapter will not work. You should immediately leave that and switch to a compiler of Borland C++. You can switch to Dev C++, Code block and various other popular compilers. All of these are free and easy to use.

Here, you see to access each element, we used resolution operator (::). This is a tedious work to use this operator each element. Hence the keyword **using** is used.

### using keyword

This is a multipurpose keyword. It has two uses, one is to access a namespace in a program another is to use a variable of a particular namespace in the program.

### For accessing the namespace

The syntax of using:

```
using namespace namespace_name;
```

Once we declare the above statement, further statements are considered to belonging to that namespace, until and unless another such a statement like above is encountered.

Consider the following program:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
    int b=2;
}
namespace ns2
{
    float a=3.33;
    double b=4.44;
}
int main()
{
    using namespace ns1;
    cout<<a<<endl;
    cout<<b;
}
```

Output
1
2

### For using the elements of a particular namespace

Here the syntax is:

```
using namespace_name::element_name;
```

Consider the following program:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
    int b=2;
    int add(int x,int y){return x+y;}
}
namespace ns2
{
    float a=3.33;
    double b=4.44;
    int add(int x,int y){return 2*x+y;}
}
int main()
{
    using ns1::a;
    using ns1::b;
    using ns1::add;
    cout<<a<<endl;
    cout<<b<<endl;
    cout<<add(a,b);
}
```

Output
1
2
3

### Using multiple namespaces simultaneously

Namespaces also allows us to use multiple namespaces simultaneously. We can say the compiler to use a variable of one namespace and other variable of another namespace.

Consider the following program:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
    int b=2;
}
namespace ns2
{
    float a=3.33;
    double b=4.44;
}
int main()
{
    using ns1::a;
    using ns2::b;
    cout<<a<<endl;
    cout<<b;
}
```

Output

1

4.44

Here, you see ns1::a is not a namespace rather it is a variable. So, we cannot use using namespace ns1::a; Here, a is from ns1 and b is from ns2.

Now consider the following program:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
}
namespace ns2
{
    float a=3.33;
}
int main()
{
    using namespace ns1;
    cout<<a<<endl;
    using namespace ns2;
    cout<<a<<endl;
}
```

This program will generate an error since including a namespace does not mean removing the previous one. So, the variable a is ambiguous. However, the namespace remains valid in the entire block only not outside the block. So, you can write the above program in following way:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
}
namespace ns2
{
    float a=3.33;
}
int main()
{
    {
        using namespace ns1;
        cout<<a<<endl;
    }
    {
        using namespace ns2;
        cout<<a<<endl;
    }
}
```

Output
1
3.33

### Namespaces aliases

One of the amazing features of namespace is that its alias can be created. So, after creating an alias the old name and new name both can be used.

The syntax for renaming the namespace is:

```
namespace new_name=old_name;
```

Consider the following program:

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
}
namespace ns2=ns1;
int main()
{
    using namespace ns1;
    cout<<a<<endl;
    using namespace ns2;
    cout<<a;
}
```

Output

1
1

This time the variable a is not ambiguous.

![](img/5340985153962870d4e4a3b9453b9146_257_0.png)

## Templates

Templates, also called "generics" or "parameterized types", enable you to construct a family of related functions or classes. It is used when you need to write lots of nearly identical things. This is a special feature of C++ comes under its property **code reuse and recycle**. Here, you will see how to reuse a code efficiently.

Suppose we define a function as follows:

```
int random(int a, int b)
{
    return a+b+sizeof(int);
}
```

A very simple function , right! Now, suppose we not only want the above function for integer but also for double, short and long double data types in our program. Here comes a problem, we shall have to define four different functions for each corresponding data type. Is there not any way to reduce this task? Here templates are useful.

At first we see our tedious program then we shall simplify it using templates:

```
#include<iostream>
using namespace std;
short random(short a,short b)
{
    return a+b+sizeof(short);
}
int random(int a,int b)
{
    return a+b+sizeof(int);
}
double random(double a,double b)
{
    return a+b+sizeof(double);
}
long double random(long double a,long double b)
{
    return a+b+sizeof(long double);
}

int main()
{
    short xa=5,ya=6;
    int xb=5,yb=6;
    double xc=5,yc=6;
    long double xd=5,yd=6;
    short p=random(xa,ya);
    int q=random(xb,yb) ;
    double r=random(xc,yc);
    long double s=random(xd,yd);
    cout<<p<<endl<<q<<endl<<r<<endl<<s<<endl;
}
```

| Output on 64 bit compiler | Output on 32 bit compiler |
| :--- | :--- |
| 13 | 13 |
| 15 | 13 |
| 19 | 19 |
| 27 | 21 |

You have now understood that while defining the templates, we have to work for data types not the values. We can say that we shall define a template which takes data types as arguments and work on the values irrespective of its data type.

There are two types of templates

- 1. Function templates
- 2. Class templates

### Function templates

Function templates can be defined in two ways, i.e. by using two different keywords class and typename. Both can be used in same way.

The syntax of declaring a template is as follows:

```
template <typename identifier> function_declaration;
```

Another syntax which very popular is:

```
template <class identifier> function_declaration;
```

So, examples of declarations can be:

```
template <class myDataType> myDataType GetMax(myDataType a, myDataType b);
```

```
template <typename myDataType> myDataType GetMax(myDataType a, myDataType b);
```

A function template can be defined like other functions but instead of using int, float etc. we use myDataType everywhere.

So, the corresponding definition of random function defined above will be:

```
template <typename T>

T random(T a, T b)

{
     return a+b+sizeof(T);
}
```

However, remember that Turbo C++ does not support typename keyword. If you are using Turbo C++ then various programs implemented in this chapter will not work as Turbo C++ are not updated. You should immediately leave that and switch to a compiler of Borland C++. You can switch to Dev C++, Code block and various other popular compilers. All of these are free and easy to use.

We can also create objects in a function definition. So the above snippet can also be written as:

```
template <typename T>

T random(T a, T b)
```
