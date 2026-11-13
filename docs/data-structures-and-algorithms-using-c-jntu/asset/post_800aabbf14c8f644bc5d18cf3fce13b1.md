
- The member variables and functions that are declared as public can be accessed by the members outside the class.

- The access specifier protected works similar to the keyword private. It is frequently used in inheritance, which is discussed in the Chapter 2.

**Syntax of access specifiers:** The keyword private, public and protected are followed by a colon (:).

```
class Class-name
{
private or public or protected:
members;
}
```

### Program 1.8

```
/* Program for private and public access specifier*/
#include<iostream.h>
#include<conio.h>
class Shape
{
private:
int a,b; // private section
void display()
{
cout<<"a="<<a<<"b="<<b;
}
public: // public section
void sum()
{
a=10, b=20; //using private numbers.
cout<<"sum="<<a+b;
}
}
void main()
{
clrscr();
Shape s;
//s.a=10; //private variables not accessible.
//s.b=20; //private variables not accessible.
//s.display(); //private member function not accessible.
s.sum(); //calling public member function.
}
```

### Output

Sum : 30

In Program 1.8, the variables a, b and the method display() are defined in the private section and the method sum() is defined in the public section. The object s is created for the class shape. The object s cannot be used to initialize private variables directly. When it is used, the compiler gives an error message as shape::a is not accessible, i.e. the private members are not accessible outside the class, and the private member function display() also cannot be accessed directly by the object. Using the public member function sum(), the private data members are accessed and the addition operation is performed on them.

The private member function can be accessed by the public member functions. The member function can also be defined outside the class, and then their prototype must be declared inside the class.

### Program 1.9

```
#include<iostream.h>
class Shape
{
 int a,b;
 void set_val() //private function.
 {
 a=10,b=20;
 }
 void display()
 {
 cout<<"a="<<a<<"\n"<<"b="<<b;
 }
 public:
 void sum() //public section
 {
 set_val(); //call to private Functions..
 display();
 cout<<"\nSum="<<a+b;
 }
 void sub(void);
};
void Shape::sub()
{
 a=30;
 b=10;
 cout<<"\nSubtraction="<<a-b;
}
void main()
{
 Shape s;
//s.set_val(); //not accessible
 s.sum();
 s.sub();
}
```

### Output

a=10
b=20
Sum=30
Subtraction=20

In Program 1.9, the method set_val() declared in the private section, and methods sum() and sub() are declared in the public section. The method sub() is defined outside the class that performs subtraction on a and b. The private method set_val() is accessed by making a call to it in the public member function sum().

## 1.5 CLASS SCOPE

Identifiers such as variable name, function name, typedef in C++ can be used only in certain areas of a program. This area is called the “scope” of the identifier. Scope determines the lifetime and visibility of an identifier. It also determines whether the identifier clashes with another identifier in any other parts of the program. There are five kinds of scope.

- a. Local scope: Variables declared within a function or blocks have local scope, i.e. they are accessed only within in that block. If the same variable is used in more than one function then each function, defines a new scope for it. Blocks can also be nested. A name declared in a block is local to that and to all the blocks contained in it. The formal arguments to a function will have local scope and are treated as if they belong to the outermost block.

```
{
 int i;
}
```

Here i has local scope, because it is declared inside a block enclosed by braces and it is never accessible since no code accesses it before closing the braces.

- b. Function scope: Labels are those that have function scope and they can be accessed only within the function but not outside of that function.

- c. File scope: When an identifier is not part of a function or class definition, then it is said to have file scope. File scope is the outermost scope in the program and it encloses both local and class scope. Variables defined at the file scope are called global variables.

- d. Class scope: Every C++ class defines a unique scope for its members called the class scope, i.e. data members and member functions have class scope.

```
class A
{
 int a;
 public:
 void b();
}
```

Here the variable a and function b() must be accessed, so that the compiler determines its class. Accessing a class member is done in three ways:

- i. Using (.dot) operator:
- obj.a,
- obj.b()

- ii. Using -> operator:
- ptr->a
- ptr->b()

- iii. Using :: (scope access) operator:
- A::a
- a::b()

- e. Prototype scope: Variables declared in a function prototype are visible only to the end of the prototype.

```
void val(int a, float b, char c)
```

The above prototype declares three names and they go out of scope at the end of the prototype.

## 1.6 STATIC CLASS MEMBERS

Every variable in C++ program is associated with a unit of storage in memory. C++ has two kinds of storage classes: automatic and static. Static members will be accessed using .(dot) or -> operators. Unlike normal class members, static members may be directly accessed by applying :: scope access operator to the class name. It is not necessary to create objects for accessing the static members.

### 1.6.1 Static Member Variables

When objects are created for a class, each object will have its own copy of members of class. The member functions are created ones, and all the objects will share them. There is no separate copy of every function of each object. Like member functions, the member variables can also be made common by using the keyword static. It makes the variables persist from the point of execution in which they are created until the program is terminated.

By declaring the member variables as static, only one copy of the variables is created and it is shared by all the objects of that class. Every static variable must be initialized to zero, the scope of the static variables is within the class. A static variable may be global to a particular transaction unit or global to a class. The general form is as follows:

```
static variable-declaration;
static function-definition;
```

### Program 1.10

```
#include<iostream.h>
#include<conio.h>
class Sum
{
static int a;
int b;
public:
void add()
{
b=0;
a++;
b++;
cout<<"a="<<a<<"\tb="<<b;
};
int Sum::a=9; //initialization of static variable
void main()
{
    Sum s1,s2;
    cout<<"\nvalues of a&b in object s1";
    s1.add();
    cout<<"\nvalues of a&b in object s2";
    s2.add();
}
```

### Output

values of a&b in object s1 a=10 b=0
values of a&b in object s2 a=11 b=0

In Program 1.10, the class sum has two variables—one is static and the other is non-static. The static variables are accessed by the public member functions of the class. Only one copy of data variable is created. Because it is declared to be static, and objects s1 and s2 share it, any change made to the static variable reflects in other objects.

### 1.6.2 Static Member Function

The member function in a class can also be defined as static, when the functions are declared as static, they can only access the static member variables and functions static member functions do not have access to nonstatic functions. Static member functions are invoked by using the class name and they can also be invoked by using objects. The scope of the static method is global within the class.

### Program 1.11

```
#include<iostream.h>
class Sum
{
    static int a;
    public:
    static void set()
    {
    a=10;
    }
    static void display()
    {
    cout<<"\na="<<a;
    }
};
int Sum::a=0;
void main()
{
Sum::set();
Sum::display();
}
```

### Output

A=10

In Program 1.11, the class sum is declared with one static data member and two static member functions. The static data members are accessed through static member functions only. The static functions are called by using the class name and scope access operators such as Sum::set() and Sum::display().
Static member functions can also be declared as private and they are accessed through public static functions. Static values declared as public can be initialized in the main() function like a normal variable by using the class name and the scope access operator.

### Program 1.12

```
#include<iostream.h>
#include<conio.h>
int a=20;
class Sum
{
private:
 static void set()
 {
 b++;
 }
public:
 static int c,b;
 static void display()
 {
 set();
 cout<<"\nb value is = "<<b;
 }
};
int Sum::b=70;
void main()
{
 int b=30;
 cout<<"\nClass variable="<<Sum::b;
 cout<<"\nGlobal variable"<<::a;
 cout<<"\nLocal variable"<<b;
 Sum::display();
}
