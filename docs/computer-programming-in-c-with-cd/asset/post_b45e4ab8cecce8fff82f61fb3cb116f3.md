
```
x=1
y=2
Program Over
```

In Listing 10, the NumberInitialization class is created that has a constructor called NumberInitialization() to initialize the private members of the class.

Some characteristics of constructors are given as follows:

- Constructors are functions but their names must be the same as that of their class names.
- Constructors are intended to initialize the members of the class when an instance of that class is created.
- Constructors are invoked automatically when the objects are created.
- Similar to functions, constructors can have default arguments.
- Constructors do not have return types, therefore, they cannot return values.
- Constructors cannot be inherited.
- Constructors cannot be `virtual`.
- Multiple constructors for the same class can be defined. They must have different parameters to distinguish them.
- Constructors make implicit call to the `new` and `delete` operators when memory allocation is required.
- The address of a constructor cannot be used to refer to other constructors.
- A constructor cannot be invoked explicitly as a member function of a class using the dot(.) operator.

You can create the following types of constructors in a class:

- Default constructor
- Parameterized constructor
- A constructor with default arguments
- Inline constructor
- Copy constructor
- Dynamic constructor

Let's now discuss each of these constructors in detail.

## Creating a Default Constructor

In C++, a constructor is the first member of a class that is invoked automatically when an object of the class is created. This means that whenever an object of a class is created, the constructor of the class is invoked. However, what would happen when you do not declare a constructor in a class? In that case, the C++ compiler creates a constructor for your class. This compiler created constructor is called the `default constructor`. A default constructor is a constructor that either has no parameter, or has parameters with default values.

You can create a default constructor in a class by simply adding a constructor without any argument and providing the same name as the class name, in the public section of the class. When you declare an instance (an object) of a class, whether you use that object or not, constructor of the class is invoked automatically. Listing 11 shows an example of creating a default constructor in a class (you can find this example in the DefaultConstructor.cpp file on the CD in the code\chapter6 folder):

### Listing 11: Creating a Default Constructor

```cpp
#include<iostream.h>

class NumberInitialization
{
    int x,y;
    public:
    NumberInitialization();
};
NumberInitialization::NumberInitialization()
{
    cout<<"Default constructor calling"<<endl;
    x=0;
    y=0;
    cout<<"x="<<x<<endl;
    cout<<"y="<<y<<endl;
}

int main()
{
    NumberInitialization n1;
    cout<<"Program Over\n";
    return 0;
}
```

### Output

```
Default constructor calling
x=0
y=0
Program Over
```

The NumberInitialization class has a constructor, called NumberInitialization(), with no parameter to initialize the data members, x and y, of the class. Such kind of constructors are called default constructors.

After creating a default constructor, let’s discuss how to code a parameterized constructor within a class.

## Creating a Parameterized Constructor

Similar to a function, you can pass arguments to a class constructor. Constructors with arguments are called **parameterized constructors**. In C++, a constructor with arguments can co-exist with another constructor without any argument. This concept is called constructor overloading.

![](img/8a6886c00caa6a1651a6c0e62bff341f_364_0.png)

> You learn more about constructor overloading later in this chapter.

Listing 12 shows an example of a constructor with parameters (you can find this example in the ParameterizedConstructor.cpp file on the CD in the code\chapter6 folder).

### Listing 12: Creating a Parameterized Constructor

```cpp
#include<iostream.h>

class NumberInitialization
{
    int x,y;
public:
    NumberInitialization();
    //Default constructor prototype
    NumberInitialization(int a, int b);
    //Parameterized constructor prototype
};

NumberInitialization::NumberInitialization()
{
    cout<<"Default constructor calling"<<endl;
    x=0;
    y=0;
    cout<<"x="<<x<<endl;
    cout<<"y="<<y<<endl;
}

NumberInitialization::NumberInitialization(int a, int b)
{
    cout<<"Parameterized constructor calling"<<endl;
    x=a;
    y=b;
    cout<<"x="<<x<<endl;
    cout<<"y="<<y<<endl;
}

int main()
{
    NumberInitialization n1;
    NumberInitialization n2(23,33);
    cout<<"Program Over\n";
    return 0;
}
```

### Output

```
Default constructor calling
x=0
y=0
Parameterized constructor calling
x=23
y=33
Program Over
```

The NumberInitialization class has two constructors: one of these is a default constructor - NumberInitialization(), and other is a parameterized constructor - NumberInitialization(int a, int b). When an object, n1, of the NumberInitialization class is created, the default constructor of the class initializes the data members, x and y, with the value zero (0). However, the n2 object invokes the parameterized constructor of the NumberInitialization class, as shown in the following code snippet:

```cpp
NumberInitialization n2(23,33);
```

In the preceding code snippet, the parameterized constructor initializes the data members, x and y, with the values 23 and 33, respectively.

## Creating a Constructor with Default Arguments

You can also define a constructor with default arguments. Listing 13 shows a constructor with default arguments in a class (you can find this example in the ConstructorDefaultArgs.cpp file on the CD in the code\chapter6 folder):

### Listing 13: Creating a Constructor with Default Arguments

```cpp
#include<iostream.h>

class MyClass
{
  public:
  MyClass(int a=100, int b=10);
};

MyClass::MyClass(int a, int b)
{
  cout<<"This constructor has default arguments"<<endl;
  cout<<"Parameters are:"<<a<<" and "<<b<<endl;
}

int main()
{
    MyClass o1();
    MyClass o2(78);
    MyClass o3(45, 56);
    return 0;
}
```

### Output

```
This constructor has default arguments
Parameters are:78 and 10
This constructor has default arguments
Parameters are:45 and 56
```

In Listing 13, the MyClass class has a parameterized constructor, also called MyClass, which has the a and b variables as its parameters of int types. These variables, a and b, are storing the numeric values 100 and 10, respectively with its corresponding object (o3). Now, consider the following code snippet:

```cpp
MyClass o1();
MyClass o2(78);
MyClass o3(45, 56);
```

In the preceding code snippet, the first statement assigns the default values, 100 and 10, to the variables a and b, respectively. The second statement overrides the default value of the variable a to 78 and assigns the value 10 to the variable b. However, the third statement overrides the default values of both variables a and b, respectively. These values override the default arguments or default value and the missing arguments must be the trailing ones.

You must remember that the constructor having default arguments can be called with either one argument or no arguments. When it is called with no arguments, it becomes a default constructor. When both these forms are used in a class, it causes error. Listing 14 shows ambiguity for C++ compiler between a default constructor and a constructor with default arguments (you can find this example in the AmbiguityConstructors.cpp file on the CD in the code\chapter6 folder):

### Listing 14: Creating Ambiguity for C++ Compiler

```cpp
#include<iostream.h>

class MyClass
{
    public:
    MyClass();
    MyClass(int x, int y);
    MyClass(float a=100.0f, float b=10.0f);
};

MyClass::MyClass()
{
    cout<<"Default constructor calling"<<endl;
}
MyClass::MyClass(int x, int y)
{
    cout<<"Parameterized constructor calling"<<endl;
    cout<<"Parameters are:"<<x<<" and "<<y<<endl;
}
MyClass::MyClass(float a, float b)
{
    cout<<"This constructor has default arguments"<<endl;
    cout<<"Parameters are:"<<a<<" and "<<b<<endl;
}

int main()
{
    MyClass o1;              //Compiler causes ambiguity here
    MyClass o2(23,45);
    MyClass o3(45.6f);
    return 0;
}
```

In Listing 14, the MyClass class has three constructors: MyClass(), MyClass(int x, int y), and MyClass(float a =100.0f, float b=10.0f). The MyClass() constructor is a default constructor, the MyClass(int x, int y) constructor is a parameterized constructor, and the MyClass(float a =100.0f, float b=10.0f) constructor has default arguments. In the main() function, the following code snippet causes an ambiguity for C++ compiler:

```cpp
MyClass o1;
```

The reason for this ambiguity is that the C++ compiler does not know whether to invoke the MyClass() constructor or the MyClass(float a=100.0f, float b=10.0f) constructor of the MyClass class.

## Creating an Inline Constructor of a Class

Similar to an inline function, you can create an inline constructor. Listing 15 shows an example of an inline constructor in a class (you can find this example in the InlineConstructor1.cpp file in the CD in the code\chapter6 folder):

### Listing 15: Creating an Inline Constructor inside a Class

```cpp
#include <iostream.h>

class Volume {
    double len, wd, hgt;
    double result;
public:
```
