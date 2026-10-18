
declared, much the same way as initialization of an ordinary variable.\nFor example,

```cpp
int m = 20;
float x = 5.75;
```
```

are valid initialization statements for basic data types.

Similarly, when a variable of built-in type goes out of scope, the compiler automatically destroys the variable. But it has not happened with the objects we have so far studied. It is therefore clear that some more features of classes need to be explored that would enable us to initialize the objects when they are created and destroy them when their presence is no longer necessary.

C++ provides a special member function called the constructor which enables an object to initialize itself when it is created. This is known as *automatic initialization* of objects. It also provides another member function called the *destructor* that destroys the objects when they are no longer required.

## 6.2 Constructors

**A constructor is a ‘special’ member function whose task is to initialize the objects of its class.** It is special because its name is the same as the class name. The constructor is invoked whenever an object of its associated class is created. It is called constructor because it constructs the values of data members of the class.

A constructor is declared and defined as follows:

```cpp
// class with a constructor
class integer
{
    int m, n;
public:
    integer(void); // constructor declared
    ...
    ....
};
integer :: integer(void) // constructor defined
{
    m = 0; n = 0;
}
```

When a class contains a constructor like the one defined above, it is guaranteed that an object created by the class will be initialized automatically. For example, the declaration

```cpp
integer int1; // object int1 created
```

not only creates the object int1 of type integer but also initializes its data members m and n to zero. There is no need to write any statement to invoke the constructor function (as we do with the normal member functions). If a ‘normal’ member function is defined for zero initialization, we would need to invoke this function for each of the objects separately. This would be very inconvenient, if there are a large number of objects.

A constructor that accepts no parameters is called the *default constructor*. The default constructor for **class A** is **A::A( )**. If no such constructor is defined, then the compiler supplies a default constructor. Therefore a statement such as

```
A a;
```

invokes the default constructor of the compiler to create the object a.

The constructor functions have some special characteristics. These are:

- They should be declared in the public section.
- They are invoked automatically when the objects are created.

- They do not have return types, not even void and therefore, and they cannot return values.
- They cannot be inherited, though a derived class can call the base class constructor.
- Like other C++ functions, they can have default arguments.
- Constructors cannot be **virtual**. (Meaning of virtual will be discussed later in Chapter 9.)
- We cannot refer to their addresses.
- An object with a constructor (or destructor) cannot be used as a member of a union.
- They make ‘implicit calls’ to the operators **new** and **delete** when memory allocation is required.

Remember, when a constructor is declared for a class, initialization of the class objects becomes mandatory.

## 6.3 Parameterized Constructors

The constructor **integer()**, defined above, initializes the data members of all the objects to zero. However, in practice it may be necessary to initialize the various data elements of different objects with different values when they are created. C++ permits us to achieve this objective by passing arguments to the constructor function when the objects are created. The constructors that can take arguments are called *parameterized constructors*.

The constructor **integer()** may be modified to take arguments as shown below:

```cpp
class integer {
    int m, n;
public:
    integer(int x, int y); // parameterized constructor
    ....
    ....
};
```

When a constructor has been parameterized, the object declaration statement such as

```
integer int1;
```

may not work. We must pass the initial values as arguments to the constructor function when an object is declared. This can be done in two ways:

- By calling the constructor explicitly.
- By calling the constructor implicitly.

The following declaration illustrates the first method:

```cpp
integer int1 = integer(0,100); // explicit call
```

This statement creates an integer object int1 and passes the values 0 and 100 to it. The second is implemented as follows:

```cpp
integer int1(0,100); // implicit call
```

This method, sometimes called the shorthand method, is used very often as it is shorter, looks better and is easy to implement.

Remember, when the constructor is parameterized, we must provide appropriate arguments for the constructor. Program 6.1 demonstrates the passing of arguments to the constructor functions.

## Program 6.1  Class with Constructors

```cpp
#include <iostream>
using namespace std;
class integer
{
int m, n;
public:
integer(int, int); // constructor declared

void display(void)
{
cout << “ m = “ << m << “\n”
cout << “ n = “ << n << “\n”
}
};
integer :: integer(int x, int y) // constructor defined
{
m = x; n = y;
}
int main( )
{
integer int1(0,100); // constructor called implicitly
integer int2 = integer(25, 75); // constructor called explicitly
cout << “\nOBJECT1” << “\n”
int1.display( );
cout << “\nOBJECT2” << “\n”
int2.display( );
return 0;
}
```

The output of program 6.1 would be:

```
OBJECT1
m = 0 n = 100

OBJECT2
```

m = 25
n = 75

The constructor functions can also be defined as **inline** functions.
Example:

```cpp
class integer
{
int m, n;
public:
integer(int x, int y)  // inline constructor
{
m = x; y = n;
}
. . . .
};
```

The parameters of a constructor can be of any type except that of the class to which it belongs. For example,

```cpp
class A
{
. . . .
. . . .
public:
A(A);
};
```

is illegal.

However, a constructor can accept a *reference* to its own class as a parameter. Thus, the statement

```cpp
Class A
{
. . . .
. . . .
```

public:
A(A&);
};

is valid. In such cases, the constructor is called the _copy constructor_.

## 6.4 Multiple Constructors in a Class

So far we have used two kinds of constructors. They are:

+   integer( ); // No arguments
+   integer( int ); // Two arguments

In the first case, the constructor itself supplies the data values and no values are passed by the calling program. In the second case, the function call passes the appropriate values from main( ).C++ permits us to use both these constructors in the same class. For example, we could define a class as follows:

```cpp
class integer
{
int m, n;
public:
integer( ){m=0; n=0;} // constructor 1
integer( int a, int b)
{m = a; n = b;} // constructor 2
integer( integer & i)
{m = i.m; n = i.n;} // constructor 3
};
```

This declares three constructors for an integer object. The first constructor receives no arguments, the second receives two integer arguments and the third receives one integer object as an argument. For example, the declaration

```
integer l1;
```

would automatically invoke the first constructor and set both **mand** and **n of I1** to zero. The statement

```
integer I2(20,40);
```

would call the second constructor which will initialize the data members **mand** and **n of I2** to 20 and 40 respectively. Finally, the statement

```
integer I3(I2);
```

would invoke the third constructor which copies the values of I2 into I3. In other words, it sets the value of every data element of I3 to the value of the corresponding data element of I2. As mentioned earlier, such a constructor is called the *copy constructor*. We learned in Chapter 4 that the process of sharing the same name by two or more functions is referred to as function overloading. Similarly, when more than one constructor function is defined in a class, we say that the constructor is overloaded.

Program 6.2 shows the use of overloaded constructors.

## Program 6.2  Overloaded Constructors

```cpp
#include <iostream>
using namespace std;
class complex
{
float x, y;
public:
complex( ) { }  // *constructor no arg*
complex(float a) {x = y = a;}  // *constructor-one arg*
complex(float real, float imag)  // *constructor-two args*
{x = real; y = imag;}
friend complex sum(complex, complex);
```
