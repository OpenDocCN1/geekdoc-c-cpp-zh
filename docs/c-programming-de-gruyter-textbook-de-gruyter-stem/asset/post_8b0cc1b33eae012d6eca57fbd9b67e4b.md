
# 4 Class and Object

4.8 Define a class Dog, which includes attributes like age and weight, and functions to operate on the attributes. Implement and test this class.

4.9 Design and test a class Rectangle whose attributes are coordinates of the left bottom point and the right top point. This class should be able to compute the area of the rectangle.

4.10 Define a class ‘employee’ for personnel management. Considering the generality, we only abstract attributes that everyone has: ID, sex, birth date, and PIN. Here, birth date should be declared as an embedded object of class ‘Date.’ Use member functions to realize input and display data. A constructor, destructor, copy constructor, inline member function, function with default values, and combination of classes must be used.

4.11 Define a class Rectangle with attributes length and width, and use a function member to compute area.

4.12 Define a class data type that can deal with char, integer, and float data types. Give its constructor.

4.13 Define a class Circle with data member radius, and use function member GetArea() to compute area. Create an object of Circle to test the code.

4.14 Define a class tree with data member age, function member grow(int years) which increases ages by years, and age() to display the value of ages.

4.15 Draw a UML diagram of Circle according to its source code in Example 4.3.

4.16 Draw UML diagrams to represent the inheritance relations among class ZRF, class SSH, and class Person according to the following code:

```cpp
class Person
{
public:
    Person(const Person& right);
    ~Person();
private:
    char Name;
    int Age;
};
```

```cpp
class ZRF : protected Person
{
};
```

```cpp
class SSH : private Person
{
};
```

4.17 In a course selection system of a college, there are two classes: class CourseSchedule and class Course. The relations between the two classes are: the parameters of the member functions of class CourseSchedule, add and remove, are objects of class Course. Please use UML to represent this dependency explicitly.

4.18 For a department personnel information system, we need to build a model for the relation between Department and Teacher. The relation can be described as: each Teacher belongs to 0 or multiple Departments, while each Department includes at least one Teacher. Please draw a UML diagram according to the above relation.

# 5 Data Sharing and Protecting

An important characteristic of C++ is that it is a language in which it is suitable to write large complex programs and enables data sharing and protection mechanisms. In this chapter we will introduce the concept of scope, visibility, and the lifetime of identifiers, as well as the sharing and protection mechanism of class members. At last we will introduce the multifile structure and compilation preprocessing directives, as is how we use several source files to organize large programs.

# 5.1 Scope and Visibility of Identifiers

Scope concerns the effective range of an identifier, while visibility concerns whether an identifier can be referenced. We know that a variable declared in a function can only be effective in this function, which is due to the restriction of the scope and visibility of variables. Scope and visibility are interrelated but different.

## 5.1.1 Scope

Scope is the region where an identifier is effective in the program body. The scopes of identifiers in C++ include function prototype scope, block scope (also termed local scope), class scope, and file scope.

### Function Prototype Scope

Function prototype scope is the smallest scope in a C++ program. In Chapter 3 we introduced how there must be a type specification of formal parameters in the function prototype. Function prototype scope is the effective area of formal parameters during the declaration of function prototype. The following is an example of a declaration of a function.

```cpp
double Area(double radius);
```

The effective area of identifier radius is between the two brackets of Area's parameter list, and you cannot reference this identifier in other places of the program. Therefore, the scope of identifier radius is called the function prototype scope. Since formal parameter type is the only factor that works in the formal parameter list of a function prototype, omitting the identifier will not affect the compiling and running results. Considering the readability of the program, we usually give each formal parameter identifier while declaring a function prototype.

### Block Scope

To understand block scope, let us first look at an example:

```cpp
void fun(int a) {
    int b(a);
    cin >> b;
    if(b>0) {
        int c;
        ...
    } // c's scope
}
```

Here, variable $b$ is declared inside function $fun()$, and is initialized by the value of $a$. Then variable $c$ is declared inside the $if$ statement. Both $b$ and $c$ have block scopes, though they belong to different block scopes. A block is a section of program that is enclosed in a pair of brackets. In this example, the block itself is a block; the branch body after the $if$ statement is a smaller block - an inclusive relationship. Identifiers declared in a block have a scope starting from the declaration and ending at the end of the block it is. Therefore, the scope of variable $b$ is from its declaration to the end of the block it is (i.e., the function body), and the scope of variable $c$ is from its declaration to the end of the block it is (i.e., the branch body). **A variable that has a local scope is also called a local variable.**

### Class Scope

A class can be viewed as a collection of named members, and member $M$ of class $X$ has a class scope. The access method of $M$ is:

If there is no declaration of local scope identifiers of the same name in $X$'s member functions, then we can access $M$ inside that function. That is, $M$ works in all kinds of functions. The use of class encapsulation is to limit the scope of data.

$Access$ through the expression $x.M$ or $x::M$, which is the most basic method to access object members in a program.

**Access $M$ through the expression $prt->M$, where $prt$ is a pointer that points to an object of class $X$.** More details about pointers are in Chapter 6.

Other access methods and the scope rules of classes and their objects in C++ will be discussed in the following chapters.

### File Scope

Declarations that appear in none of the scopes talked about have file scopes. The scope of this kind of identifier starts from the declaration point and ends at the end of the file. The global variables declared in Example 5.1 have file scope, and they are effective in the whole file.

**Example 5.1:** Examples of scope and visibility.

```cpp
//5_1.cpp
#include <iostream>
using namespace std;
int i; //global variable, file scope
int main()
{
    i=5; //initialize i of the file scope
    { //subblock 1
        int i; //local variable, local scope
        i=7;
        cout<<i<<endl; //output 7
    }
    cout<<i<<endl; //output 5
}
```

In this example, variable i declared before the main function has file scope, and its effective area is the whole file. We initialize i to 5 at the beginning of the main function, we declare a variable of the same name in block 1 and initialize it to 7. The first output result is 7, because the variable with local scope covers the variable with file scope that is, the variable with file scope becomes invisible (this is the visibility issue, which we will discuss later). When the program finishes executing block 1 and starts the second output, the output is the value of the variable with file scope, which is 5. **A variable with file scope is also called a global variable.**

## 5.1.2 Visibility

Now, let us look at the effective area of a variable from the perspective of an identifier reference — that is, the visibility of the identifier. When a program executes to one point, the identifier that can be referenced is the identifier that is visible at this point. To understand visibility, we first look at the relationship between different scopes. File scope is the largest scope, followed by class scope and local scope. Figure 5.1 describes the general relationship between scopes. Visibility represents what you can see when you “look” from inner scope to outer scope.

The general rules of scope visibility are:

+   You must first declare an identifier before referencing it.
- You cannot declare identifiers of the same name in the same scope.
