![](Images/cover01411.jpeg)

PROGRAMMING IN C++

![](Images/image01299.jpeg)<map name="awmap1"><area shape="rect" href="http://www.pudhiyadesambook.blogspot.com" coords="249, 675, 537, 692"></map>

 Unit 1

 Object Oriented Programming  Paradigms

 Comparison of Programming  Paradigms

 Object Oriented  Languages

 Benefits of Object Oriented  Programming

 Comparison with  C

 Overview of  C++

 Pointers ,References and  Structures

 Functions - Scope and  Namespaces

 Source Files and  Programs

###  Procedure-oriented  Programming

The high level languages, such as BASIC, COBOL, C, FORTRAN are commonly known as Procedure Oriented Programming.

![](Images/image01300.jpeg)![](Images/image01301.jpeg)![](Images/image01302.jpeg)![](Images/image01303.jpeg)![](Images/image01304.jpeg)![](Images/image01305.jpeg)Using this approach, the problem is viewed in sequence of things to be done, like reading, processing and displaying or printing. To carry out these tasks the function concepts must be used.

![](Images/image01306.jpeg)![](Images/image01307.jpeg)

### Fig. Typical structure of Procedure Oriented Programs

 ![](Images/image01308.jpeg)This concept basically consists of number of statements and these statements are organized or grouped into  functions.

 While developing these functions the programmer must care about the data that is being used in various  functions.

 A multi-function program, the data must be declared as global, so that data can be accessed by all the functions within the program & each function can also have its own data called local data.

![](Images/image01309.jpeg)

### ![](Images/image01310.jpeg)Fig. Relationship of data and functions in procedural programming

 The global data can be accessed anywhere in the program. In large program it is very difficult to identify what data is accessed by which function. In this case we must revised about the external data and as well as the functions that access the global data. At this situation there is so many chances for an  error.

### Characteristics of Procedure-oriented Programming (C):

*   Emphasis is on doing things  (algorithms)
*   Larger programs are divided into smaller programs known  functions.
*   Most of the functions share global  data.
*   Data move openly around the system from function to  functions
*   Functions transforms data from one form to  another
*   Employs TOP-DOWN approach in program  design.

### ![](Images/image01311.jpeg)Object-oriented programming

 This programming approach is developed to reduce the some of the drawbacks encountered in the Procedure Oriented Programming  approach.

 The OOProgramming approach treats data as critical element and does not allow the data to flow freely around the  program.

 It bundles the data more closely to the functions that operate on it; it also protects data from the accidental modification from outside the  function.

 The object oriented programming approach divides the program into number of entities called objects and builds the data and functions that operates on data around the  objects.

 The data of an object can only access by the functions associated with that object.However the functions of one object can access the functions of other  objects.

![](Images/image01312.jpeg)

## ![](Images/image01313.jpeg)![](Images/image01314.jpeg)Fig. Organisation of data and functions in OOP

Characteristics of Object-oriented Programming (C++)

*   Emphasis is on data rather than  procedure.
*   Programs are divided into what known as  OBJECTS
*   Data structures are designed such that they characterize the  objects
*   Functions that operate on the data of an object are tied together in the data structure.
*   Data is hidden and cannot be accessed by external  functions.
*   Objects may communicate with each other through  functions
*   New data and functions can be easily added whenever  necessary
*   Follows BOTTOM-UP approach in program  design.

###  Comparison of Programming  Paradigms

 Difference between C &  C++

C is an procedure oriented programming language, whereas C++ is an object oriented programming language .The need for an object oriented environment is because procedure oriented programming language such as C fails to show the desired results for larger programs inters of bug free, complexity & reusable programs. C++ eliminates the pitfalls faced by C language.

There are many differences which makes C++ as an apt alternative to C. There are many concepts in C++ which C language doesn’t support. They are data hiding, data encapsulation, inheritance, polymorphism, classes, objects, operator overloading & message passing.These concepts can eliminate the complexity of C for larger programs.

The main difference between C & C++ is where we use the class (user defined data type), Through class we derive the other concepts. Class is similar to structure in C. In structure only mixed data type can be declared, whereas C++ allows us to declare & define functions in addition to the data's. This makes the main function more simple & grouping all functions into a single class.

Operator overloading concept in C++ makes us to create a new language of or own. Through this we can perform arithmetic operations on variables of class i.e. objects which makes the program easier to understand. In C we can’t perform arithmetic operation on structure variable as we do in C++.

In c for larger programs the presence of redundant codes is unavoidable. This can be eliminated in C++ by following inheritance.

In C there may be accidental invading of codes of one program by another program. This can be eliminated in C++ which supports data hiding which helps the programmer to build secure programs that cannot be invaded by code in other parts of the program.

In C, if we want to add additional features to the program without modifying the function is very difficult. This can be eliminated in C++ which supports inheritance where we can add additional features to an existing class without modifying it. This concept provides the idea of reusability of the programs.

| S.No | Procedure oriented Programming (C) | Object Oriented Programming (C++) |
| 1.2.3.4.5. | Programs are divided into smaller sub-programs known as functionsHere global data is shared by most of the  functionsFollows Top-Down ApproachData cannot be secured and available to all the  functions.Here, the reusability is not possible, hence redundant code cannot be avoided. | Programs are divides into objects & classesObjects are easily communicated with each other through  functions.Follows Bottom-Up  ApproachData can be secured and can be available in the class in which it is declared.Here, we can reuse the existing one using the Inheritance concept |

###  Object oriented Languages:

Object oriented programming languages are divided into two.They are 1.Object based programming languages

2.Object oriented programming languages Object based programming:

Languages that supports programming with objects are said to be Object based programming languages.They do not inheritance and Dynamic binding.

Object based programming is the style of programming that supports encapsulation and identity.

Major features that are required for this are:

1. Data  Encapsulation

2. Data hiding and access mechanism 3.Automatic initialization and clear up of objects 4.Operator overloading

Object oriented programming

![](Images/image01315.jpeg)Object oriented programming includes all features of Object based programming with two additional features like inheritance and Dynamic binding.

### The oops concepts are

*   Objects
*   Classes
*   Data abstraction and  encapsulation
*   Inheritance
*   Polymorphism
*   Dynamic binding
*   Message  passing

###  Objects

*   Objects are the basic run time entities in an object-oriented  system.
*   Each entity can be treated as object. Object contains data and code to manipulate these  data’s.
*   They may represent a person, a place, a bank account, a table of data or any item with which the computer must deal or  handle.
*   Someobjectsmaycorrespondtoreal-worldentitiessuchas students,employees,bank  accounts,etc.
*   Every object will have a state called attributes(data) and the behavior called operations(function).

When a program is executed, the objects interact by sending messages to one another .For example, if ‘customer’ and ‘account’ are the two objects in a program, then the customer object may send a message to the account object. Each object contains data and code to manipulate the data. objects can interact without having to know details of each others data or code. It is sufficient to know the type of message accepted, and the type of response returned by the  objects.

![](Images/image01316.jpeg)![](Images/image01317.jpeg)

Fig.Two ways of representing an object

Desktop lamp may have only two possible states (on and off) and two possible behaviors (turn on, turn off), but your desktop radio might have additional states (on, off, current volume, current station) and behavior (turn on, turn off, increase volume, decrease volume, seek, scan, and  tune).

### ![](Images/image01318.jpeg)Eg:

| Account |
| Ac_ number Account type Name Balance |
| Deposit() Withdraw() Enquire() |

*   Each object will have its own identity though its attributes and operations are same, the objects will never be equal.
*   For example in case of a person object, two persons will have same attributes like name,age,sex;but they are not  equal.

###  Classes

*   We know that objects contain data and function or code to manipulate that data. The entire set of data and code of an object can be made a user-defined data type with the help of a  class.
*   Objects are variables of type  class.
*   Classes are user defined data types and behaves like the built-in types of a programming  language.
*   Once a class has been defined, we can create any number of objects associated with that  class.
*   Thus, a class is collection of objects of similar type i.e., the objects with the same state (attributes) and behavior(operations) are grouped into a class.
*   For example, mango, apple and orange are members of class  fruit.
*   The syntax used to create an object is no different from the syntax used to create an integer object in  C.
*   If fruit has been defined as a class, then the  statement

### Eg:

fruit mango;

will create an object mango belonging to the class fruit.

### Examples:

1. Class: person Object: girl,boy Attributes :  Name,Age

Operations : speak( ),listen( ),walk( )

2. Class: vehicle Object:  car,bus

Attributes : Name,model,color Operations : start( ),stop( ),accelerate( )

### In C++ class can be represented as:

Class account

{

Private:

char name[20]; int act_type; float balance;

Public:

};

deposit( ); withdraw( );

*   It is similar to structure declaration in  C.
*   It enables the creation of class variables called  objects.

### Example:

account saving; account current;

### Example programs:

1. /*To find whether given number is even or odd using  Class*/

#include<iostream.h> #include<conio.h>

class even

{

private:

int a; public:

void getdata()

{

cout<<”\nenter the number to check: ”; cin>>a;

}

void check()

{ if(a%2==0)

cout<<”\ngiven number is even”; else

cout<<”\ngiven number is odd”;

}

};

void  main()

{

clrscr();

even e; e.getdata();

e.check();

getch();

}

### Output:

Enter the number to check: 9 Given number is odd

2. /*To calculate velocity by using the formula v=u+(a*t) */ #include<iostream.h>

#include<conio.h> class velocity

{

int v,u,a,t; public:

void getdata(  )

{

cout<<"Enter the values for initial velocity, acceleration and time\n"; cin>>u>>a>>t;

}

void calculate( )

{

v=u+(a*t);

cout<<"FINAL VELOCITY= "<<v<<endl;

}

};

void main( )

{

clrscr( );

velocity ob; ob.getdata( ); ob.calculate( );

getch( );

}

###  Data Encapsulation

*   Encapsulation is the most basic concept of  OOP.
*   The wrapping up of data and functions into a single unit(called class) is known as encapsulation.
*   Data encapsulation is the most striking feature of a  class.
*   It is a mechanism that associates the code and the data it manipulates and keeps them safe from any external interface and  misuse.
*   The data is not accessible to the outside world (entire program), and only those functions which are wrapped in the class can access  it.
*   These functions provide the interface between the object’s data and the program.
*   This is also known as “data hiding “ or “information  hiding”.

###  Data  Abstraction

*   Abstraction refers to the act of representing essential features without including the background details or  explanations.

To understand this concept more clearly, take an example of 'switch board'. You only press particular switches as per your requirement. You need

know the internal working of these switches. What is happening inside is hidden from you. This is abstraction, where you only know the essential things  to operate on switch board without knowing the background details of switch  board.

*   Classes use the concept of  abstraction.
*   Since the classes use the concept of abstraction, they are also known as Abstract Data Types  (ADT).

###  Inheritance

*   It is the process by which objects of one class acquire the properties of objects of another  class.
*   It provides reusability i.e., we can add additional features to an existing class without modifying it.
*   It is the capability to define a new class in terms of an existing  class.
*   This is possible by deriving a new class from the existing  one.
*   An existing class is known as a base class and the new class is known  as

derived class. Consider an example,

*   When the class child inherits the class parent - the class child is referred to as derived class (sub-class), class parent is referred to as base class (super  class).

![](Images/image01319.jpeg)Parent Class or Super Class or Base Class

Child Class or Derived Class or Sub Class

*   Child has two  parts:
    *   a derived part  and
    *   Incremental part (new code written specifically for child  class).
*   Child has its own properties, in addition to those acquired from its  parent.

![](Images/image01320.jpeg)

### Example:

![](Images/image01321.jpeg) 

C++ supports such hierarchical classification of classes:

*   Single  inheritance
*   Multiple  inheritance
*   Multi-level  inheritance
*   Hierarchical  inheritance

###  Polymorphism

*   Polymorphism is a key to the power of  OOPs.
*   It is a Greek word, means the ability to take more than one form(many forms).
*   It is the concept that supports the capability of data to be processed in more than one form i.e., It allows a single name to be used for more than one related purpose, which are technically  different.
*   For example, an operation may exhibit different behavior in different instances.
*   The behavior depends upon the types of data used in the  operation.

The following are the different ways of achieving polymorphism in a C++ program:

### Example:

*   Function  overloading
*   Operator  overloading
*   Dynamic binding

![](Images/image01322.jpeg)

![](Images/image01323.jpeg)![](Images/image01324.jpeg)![](Images/image01325.jpeg)Fig. Polymorphism

Fig. illustrates that a single function name can be used to handle different number and different types of arguments. This is similar to a particular word having several different meanings depending on the context. Using a single function name to perform different types of tasks is known as function overloading.

*   Let us consider the operation of  addition.
    *   For two numbers, the operation (+) will generate a  sum.
    *   If the operands are strings then the operation (+) would produce a third string by concatenation. This is known as operator  overloading.

###  Dynamic  binding

*   Binding refers to the linking of a procedure call to the code to be executed in response to the  call.
*   Dynamic binding (also known as late binding) means that the code associated with a given procedure is not known until the time of the call at  run-time.
*   It is associated with polymorphism and inheritance.

### Example:

*   Consider the procedure “draw” in the above fig. By inheritance every object will have this procedure.
*   Its algorithm is however, unique to each object and so the draw procedure will be redefined in each class that defines the  object.
*   At run-time, the code matching the object under current reference will be called.

###  Message passing

*   An OO program consists of a set of objects that communicate with each other.
*   The process of programming in an OO language, therefore involves the following  steps:
    *   Creating classes that define objects and their  behavior.
    *   Creating objects from class definitions  and
    *   Establishing communication among  objects.
*   A message for an object is a request for execution of a procedure and therefore will invoke a function (procedure) in the receiving object that generates the desired  result.
*   Objects communicate with one another by sending and receiving information much the same way as people pass messages to one another.
*   Message passing involves specifying the name of the objects, the name of the function (message) and the information to be  sent.

### Example:

Object

employee . salary (name);

![](Images/image01326.jpeg)

![](Images/image01327.jpeg)Information

Objects have a life cycle. They can be created and destroyed.

Communication with the object is feasible as long as it is alive.

###  Benefits or Advantages of  OOP’s

*   The complexity of software can be managed  easily.
*   Data hiding concept help the programmer to build secure  programs
*   Through the class concept we can define the user defined data  type
*   The inheritance concept can be used to eliminate redundant  code
*   The message-passing concept helps the programmer to communicate between different  objects.
*   New data and functions can be easily added whenever  necessary.
*   OOP’s ties data elements more closely to the functions that operates  on.

### Application of OOP

*   Real-time  system
*   Simulation and  modelling
*   Object-oriented  database
*   Hypertext,hypermedia and  expertext
*   Artificial intelligence and expert  system
*   Neural network and parallel  programming
*   Decision support and office automation  systems

*   CIM/CAM/CAD  system

###  COMPARISON of C with  C++

C Language

*   Top Down  approach
*   Procedure  oriented
*   Variables cannot be dynamically  initialised
*   Reference variables cocept is not  there
*   Memory  management

*   Allocation: malloc(), calloc()
*   Deallocation:  free()
    *   Type  casting:

Syntax: (typename) expression

*   Object Oriented concepts like Inheritanc, polymorphism,dynamic binding, encapsulation etc are not  supported
*   There is no inline function or friend  function
*   Input and  output:

oScanf() and printf() library functions are used for reading input and writing output  respectively.

*   There is no scope resolution operator to access the global variables in the interior blocks of the  functions
*   Constructors and destructors are not  used
*   Object oriented concepts like inheritance, polymorphism, encapsulation, dynamic binding etc are not  suppoted

### C++ Language

*   Bottom up  approach
*   Object  oriented
*   Allows dynamic initialisation of variables Eg:cin>>str;

int len=strlen(str);

*   Uses reference variables Eg:float  tot=100

float & sum=tot;

// Here the reference variable sum references the variable tot

*   Memory  management

*   Allocation: new operator is  used
*   Deallocation: delete operator is  used
    *   Type  casting:

Syntax: typename (expression)

*   Inline functions : an inline function is a function upon which the [compiler](http://en.wikipedia.org/wiki/Compiler) has been requested to perform [inline  expansion](http://en.wikipedia.org/wiki/Inline_expansion)

*   Eg: #include<iostream.h> class  inl

{

public:

![](Images/image01328.jpeg)inline int cube(int a) return a*a*a;

};

Int main()

{

inl o;

int c=o.cube(3); return 0;

}

*   Input and  output:
    *   >> Extraction operator for reading  input
    *   << Insertopm operator for printing the  output
        *   Eg:cin>>  a;

cout<<a;

*   Scope resolution  operator:

The scope resolution operator helps to identify and specify the context to which an identifier refers. Syntax:  ::member_name

*   Friend functions and virtual functions are  used
*   Constructors and destructors are not  used
*   Object oriented concepts like inheritance, polymorphism, encapsulation, dynamic binding etc are  suppoted.

###  Overview of C++  Programming

C++ was developed by BJARNE STROUSSTRUP at AT&T BELL Laboratories in Murry Hill, USA in early 1980’s.

Striysstryo combines the features of ‘C’ language and ‘SIMULA67’ to create more powerful language that support OOPS concepts, and that language was named as “C with CLASSES”. In late 1983, the name got changed to C++.

The idea of C++ comes from ‘C’ language increment operator (++) means more additions.

C++ is the superset of ‘C’ language, most of the ‘C’ language features can also applied to C++, but the object oriented features (Classes, Inheritance, Polymorphism, Overloading) makes the C++ truly as Object Oriented Programming language

### ![](Images/image01329.jpeg)![](Images/image01330.jpeg)Structure of C++ Program

| Include files |
| Class Definition |
| Member function Definitions |
| Main function Program |

Include files provides instructions to the compiler to link functions from the system library.

Eg:  #include <iostream.h>

#include–Preprocessor  Directive iostream.h–Header File

 A class is a way to bind and its associated functions together. It is a user defined datatype. It must be declared at class declaration  part.

 Member function definition describes how the class functions are implemented. This must be the next part of the C++  program.

 Finally main program part, which begins program  execution.

main( )

{

}

Program execution begins at the opening brace and ends at the closing brace.

The closing brace of the main function is the logical and of the program.

###  ![](Images/image01311.jpeg)Input / Output statements Input Stream

Syntax:

cin >> var1 >> var2 >>;

cin – Keyword, it is an object, predefined in C++ to correspond to the standard input stream.

>> - is the extraction or get from operator

Extraction operation (>>) takes the value from the stream object on its left and places it in the variable on its  right.

### Eg:

cin>>x; cin>>a>>b>>c;

### ![](Images/image01311.jpeg)Output Stream: Syntax:

cout<<var1<<var2;

cout - object of standard output stream

<< -is called the insertion or put to  operator

It directs the contents of the variable on its right to the object on its left.

Output stream can be used to display messages on output screen.

### Eg:

cout<<a<<b; cout<<”value of x is”<<x;

cout<<”Value of x is”<<x<<”less than”<<y;

###  Tokens

The smallest individual units in a program are known as tokens.

C++ has the following tokens:

 Keywords

 Identifiers

 Constants

 Strings

 Operators

*   In C++ program’s written using these tokens, white spaces and the syntax of the language.
*   Most of the C++ tokens are basically similar to the C tokens with the exception of some additions and minor  modifications.

### ![](Images/image01311.jpeg)Keywords

*   The keywords implementt specific C++ language  features.
*   Keywords has a predefined meaning and cannot be changed by the  user
*   Keywords cannot be used as names for the program  variables.
*   Additional keywords have been added to ANSI C keywords,in order to enhance its features amd make it an OO  language.

### The specific C++ Keywords

There are several keywords specific to C++

![](Images/image01311.jpeg)![](Images/image01331.jpeg)

Identifiers refer to the names of variables, functions, arrays, classes, etc. created by the programmer.They are the fundamental requirement of any language.

Rules for naming these identifiers are common to both C and C++:

1. Only alphabetic characters, digits and underscores are  permitted.

2. The name cannot start with a digit.

3. Uppercase and lowercase letters are  distinct.

4. A declared keyword cannot be used as a variable  name.

The major difference between C and C++ is the limit on the length of a name i.e., C recognizes only the first 32 characters in a name.Where as C++ has no limit on its length and therefore,all the characters in a name are significant.

### ![](Images/image01311.jpeg)Constants

It refers to fixed values that do not change during the execution of a program.C++ recognises all constants available in C.

### Types of constants:

*   Integer constants-Eg: 123,  25– without decimal point
*   Character  constants-Eg: ‘A’, ‘B’, ‘*’,  ‘1’
*   Real  constants-Eg: 12.3, 2.5 - with decimal  point

### ![](Images/image01311.jpeg)Strings

A  sequence  of  characters  is  called  string.String constants are enclosed in double quotes as  follows:

### Eg:

“Hello”

### ![](Images/image01311.jpeg)Operators

An operator is a symbol that tells the computer to perform certain mathematical or logical  manipulations.

### Types of Operators

1. Arithmetic  Operators

2. Relational  Operators

3. Logical  Operators

4. Assignment  Operators

5. Increment & decrement  Operators

6. Conditional  Operators

7. Bitwise  Operators

8. Special  Operators

9. Manipulators

10.  Memory allocate / delete  Operators

### • Manipulators

Manipulators are operators used to format the data display. The commonly used manipulators are endl, setw.

###  endl  manipulators

It is used in output statement causes a line feed to be inserted, it has the same effect as using the newline character “\n” in ‘C’ language.

### Eg:

#include <iostream.h> main()

{

}

### Output:

int a=10, b=20;

cout << “C++ language” << endl; cout << “A value: “ << a << endl; cout << “B value:” << b << endl;

C++ language A value:  10

B value:  20

###  Pointers

C++ adds the concept of constant pointers and pointer to a constant.

### Constant pointer

Char *  const  ptr1=”GOOD”;//constant pointer We cannot modify the address of  pointer1.

### Pointer to constant

int const *  ptr1=&m;//pointer to a constant Contents of what it points to cannot be  changed.

### Void

Uses of void:

(i) To specify the return type of a function when it is not returning a  value.

(ii) To indicate an empty argument list to a  function.

### Eg:

void func(void);

(iii)  It is used in pointer  declaration.

### Eg:

void  *p;//p becomes  pointer

Assigning any void pointer to a non-void poiter without using a cast to non-void pointer type is allowed in C.

### Eg:

void *ptr1; char *ptr2; ptr2=ptr1;

But this is not allowed in C++.A void pointer cannot be directly assigned to other type pointers in C++.we need to use a cast operator.

### For example:

void *ptr1; char *ptr2;

ptr2=(char*)ptr2;

### Reference Variables

C++ provides a new kind of variable known as reference variable. A reference variable provides an alias (alternative name) for a previously defined variable.

For example, if we make the variable sum a reference to the variable total, then

![](Images/image01332.jpeg)sum and total can be used interchangeably to represent that variable. A reference variable is created as follows:

### Eg:

float total = 100; float & sum = total;

cout << sum << total;

Both the variables refer to the same data object in the memory i.e.

total, sum

![](Images/image01333.jpeg)

A major application of reference variables is in passing arguments to functions.

### Example program:

void f(int  &  x)//uses reference

{

x=x+10;//x is incremented; so also  m

}

int main( )

{

int m=10;

f(m);//function  call

..................

..................

}

When the function call f(m) is executed, the following initialization occurs: int & x=m;

Thus x becomes an alias of m after executing the statement f(m);

When the function increments x, m is also incremented.

2 Such functions are also known as call by  reference.

3 The call by reference mechanism is useful in OO programming because it permits the manipulation of objects by reference and eliminates the copying of object parameters back and  forth.

4 References can be created not only for buit-in data types, but also for user-defined data types such as structures and  classes.

### Example program:

int main()

{

int  x;//declaration

float sum=0;

for(int  i=1;i<5;i++)//declaration

{

cout<<”enter a value”<<endl; cin>>x;

sum=sum+x;

}

float avg;//declaration avg=sum/(i-1);

cout<<avg;

return 0;

}

### POINTERS AND REFERENCES EXAMPLE

/* CALL BY REFERENCE USING POINTER CONCEPT*/

#include<iostream.h> #include<conio.h> class ptr

{

public:

void swap(int *a,int *b)

{

int t; t=*a;

*a=*b;

*b=t;

}

void show(int *x,int *y)

{

cout<<*x<<" .."<<*y;

}

};

void main()

{

ptr o; clrscr(); int x,y;

cin>>x>>y; o.swap(&x,&y);

o.show(&x,&y); getch();

}

### /*RETURN BY REFERENCE*/

#include<iostream.h> #include<conio.h> class abc

{

public:

int & max(int &x,int &y)

{

if(x>y) return x; else return y;

}

};

void main()

{

int a,b; clrscr(); abc o; a=10;

b=20;

int &ar=a; int  &br=b;

int & u=o.max(a,b); if(u==ar)

cout<<"a is big"; else if(u==br) cout<<"b is big"; getch();

}

### Structures

We have user defined data types such as struct and union in C. While these data types are legal in C++,some more features have been added to make them suitable for the object-oriented programming. C++also permits us to define another user defined data type known as class which can be used just like any other basic data type, to declare variables. The class variables are known as objects, which are the central focus of OOPs.

The only difference between a structure and a class is that, in a class, the member data or function are private by default whereas, in a structure, they are public by default.

### The following code segment:

Class demo

{

private:

int Num1; public:

void func(void);

};

can be written as:

class demo

{

int Num1; public:

void func(void);

};

The keyword private need not be mentioned because, in a class, the members are private by default.

The code segment can be modified using a structure in the following way:

class demo

{

int Num1; public:

void func(void);

};

### The keyword private need not be mentioned because, in a class, the members are private by default.

The code segment can be modified using a structure in the following way: struct demo

{

void func(void); int Num1;

};

### The keyword public need not be mentioned because the structure members are public by default.

Structure:

Structure is the collection of elements of different datatypes.

Structure Initialization:  #include<iostream.h> Struct date

{

int day; int month; int  year;

};

Void main()

{

date d1={12,3,2013}; date d2={14,3,2013};

cout<<”bday”;

cout<<d1.day<<”-”<<d1.month<<”-”<<d1.year; cout<<”today’s date”;

cout<<d2.day<<”-”<<d2.month<<”-”<<d2.year; getch();

}

Array of structure  #include<iostream.h> Struct  student

{

char name[10]; int  mark[12];

};

Void main()

{

Student s[10]; int n;

cout<<”enter no of students”; cin>>n;

for(i=0;i<n;i++)

{

Cout<<”enter the name”; Cin>>s[i].name; Cout<<”enter mark”; Cin>>s[i].mark;

}

for(i=0;i<n;i++)

{

Cout<<”name” <<s[i].name; Cout<<”mark”>> s[i].mark;

}

}

### ![](Images/image01311.jpeg)Enumerated data type

*   It provides a way for attaching names to  numbers.
*   The enum keyword autumatically enumerates a list of words by assigning them values 0,1,2, and so  on.
*   This facility provides an alternative means for creating symbolic constants ( using #define preprocessor  directive).
*   The syntax of enum is similar to that of the struct  statement.

### Syntax:

![](Images/image01334.jpeg)

• In this form, enum-type-name is optional. However, if you want to use enum  type in several places, it is better to use another way of enum  declaration:

### (Or)

![](Images/image01335.jpeg)

• In the second case enum-type-name cannot be  omitted.

### Eg:

enum shape{circle,triangle,circle}; enum color{yellow,blue,white,red}; enum position{off,on};

• The enumerated data types differ slightly in C++ when compared with those  in C.In C++,the tag names shape,color,position becomes new type  names.

• By using these tag names we can declare new variables. shape  ellipse;//ellipse is of type  shape

color  background;//background is of type  color

• C defines the types of enums to be  ints.

• In C++,each enumerated data type retains its own seperate type i.e., C++ does not permit an int value to be automatically converted to an enum  value.

### Eg:

color background  = blue;//allowed

color background  = 7;//error in C++ color background =  (color)  7;              //OK

Enumerated value can be used in the place of an int value. int c =  red;//valid,color type promoted to  int

• By default, the enumerators are assigned integer values starting with 0 and each successive enumerator is one larger than the value of the previous one, unless you explicitly specify a value for a particular enumerator i.e., We can over-ride the default by explicitly assigning integer values to the  enumerators.

• Enumerators needn't have unique values within an enumeration.

• The name of each enumerator is treated as a constant and must be unique within the scope where the enum is  defined.

• An enumerator can be promoted to an integer  value.

### Eg:

Enum color{red,blue=5,green=9}; Enum color{red=5,blue,green};

Note:-  The subsequent initialised enumerators are larger by one than their predecessors.

• C++ also permits the creation of anonymous enums (i.e., enums without tag names)

### Eg:

enum{off,on};

Here, off is 0 and on is 1.These constants may be referenced in the same manner as regular constants.

int switch_1=off; int switch_2=on;

### Characteristics:

• An enumeration set can contain duplicate constant values. For example,  you could associate the value 0 with two different identifiers in the same  set.

• The identifiers in the enumeration list must be distinct from other identifiers in the same scope with the same visibility, including ordinary variable names and identifiers in other enumeration  lists.

• Enumeration tags follow the normal scoping rules. They must be distinct from other enumeration, structure, and union tags with the same  visibility.

###  Functions

Functions are the building blocks of C++ programs. A function groups a number of program statements into a single unit. This unit can be invoked from other parts of the program.

*   It is difficult to implement a large program even if it is algorithm is available.
*   To implement such a program in an easy manner, it should be split into a number of independent tasks, which can be easily designed, implemented, and  managed.
*   This process of splitting a large program into small manageable tasks and designing them independently is called Modular  Programming.
*   A repeated group of instruction in a program can be organized as a function.
*   A function is a set of program statements that can be  processed independently.

*   Member  functions
*   Main  function
*   Function  prototyping
*   Call by  reference
*   Return by  reference
*   Inline  functions
*   Default  arguments
*   Constant  arguments
*   Function  overloading
*   Friend and virtual  functions

### //DEFAULT ARGUMENTS

#include<iostream.h> #include<conio.h> class abc

{

public:

void sum(int a,int b,int c=20);

};

void abc::sum(int a,int b,int c)

{

int d=a+b+c; cout<<d;

}

void main()

{

clrscr(); abc o; o.sum(3,4); getch();

}

# SCOPE:

## In C, global version of a variable cannot be accessed from within the inner block. C++ resolves this problem by introducing a new operator ::.

Syntax:

:: variable-name

This operatoe allows access to the global version of a variable.

Example program: #include<iostream.h>

## int  m=10;//global m; int  main()

{

int m=20;//m redecalred, local to  main

{

int k=m;

int m=30;//m declared again, local to inner  block

cout<<”we are in the inner block \n”; cout<<”k =” << k<< “\n”; cout<<”m=”<<m<<”\n”;

cout<<” ::m = ”<< ::m << “\n”;

}

cout<<”\n we are in outer block\n”; cout <<”m =”<< m<<”\n”;

cout<< “::m” << ::m << “\n”;

return 0;

}

Output:

We are in inner block k=20

m=30

::m=10

### Namespace:

We are in outer block m=20

::m =10

It is used to define the context in which names are defined. In essence, a namespace defines a scope

## Example:

#include <iostream> using namespace std;

// first name space namespace first_space{

void func(){

cout << "Inside first_space" << endl;

}

}

// second name space namespace second_space{

void func(){

cout << "Inside second_space" << endl;

}

}

int main ()

{

// Calls function from first name space. first_space::func();

// Calls function from second name space.

second_space::func();

return 0;

}

###  Source Files and  Programs

All the previous given example programs.

 Unit      2

 Working with classes – Classes and objects – Class specification-Class  objects

 Accessing class members-Defining class members- Accessing member functions within class- Data hiding-Class member  accessibility

 Inline  functions

 Empty  classes

 Constructors-Parameterized constructors-Constructor overloading-Copy  constructors

 new, delete  operators

 ”this”  pointer

 friend classes and friend  functions

 Function  overloading

 Operator  overloading.

Class  Specification:

The class can be described as a collection of data member along with member functions. This property of C++, which allows association of data and functions into a single unit is called encapsulation. Sometimes classes may not contain any data members or member function called empty  classes.

Syntax for class specification

![](Images/image01336.jpeg)Keyword

![](Images/image01337.jpeg)Class classname

{

Userdefined name of the class

//body of a class

}; end of class requires semicolon

More than one object can be created with a single statement as, Class student s1,s2,s3;

Or Student s1,s2,s3.

Object can also be created by placing these names immediately after the closing brace. Thus the definition

Class student

{

---------------

---------------

} s1,s2,s3;

Accessing class members:

Once an object of a class has been created, there must be a provision to access its members. This is achieved by using the member access operator, dot(.).

![](Images/image01338.jpeg)![](Images/image01339.jpeg)Syntax: For accessing datamember of a class Object name . datamember

![](Images/image01340.jpeg)

Name of the class defined

object

Member access specifier

1Datamember of a  class

Syntax for accessing member function of a class

![](Images/image01341.jpeg)![](Images/image01342.jpeg)![](Images/image01343.jpeg)![](Images/image01344.jpeg)Objectname.Functionname (Actual arugements)

Name of the class defined object

Member access specifier

Name of the member function

Arguments to the function

Eg:s1.setdata(10, “Ram”); s1.outdata(  );

The object s1 can be used to access the member functions setdata and outdata respectively.

Consider the following program

#include <iostream.h> #include <string.h> class student

{

private:

int roll_no; char  name[20];

public:

void setdata(int roll_no_in, char name_in)

{

roll_no = roll_no_in; strcpy(name, name_in);

}

void  outdata(  )//display data  members

{

cout<<”rollno = “<< roll_no <<endl; cout<<”name = “ << name << endl;

}

};

void main( )

{

student s1; s1.setdata(1, “Ram”);

s2.setdata(10,”Kumar”); cout<<”Student details . . .”<<endl; s1.outdata(  );

s2.outdata(  );

}

Output:

Student details Rollno = 1 Name = Ram Rollno = 10 Name = Kumar

Client-server Model:

A client seeks service whereas, a server provides services requested by a client In the above example the class student resembles a server whereas, objects of the class student resemble clients. They make call to the server by sending messages.

In the statement

s2.setdata(10, “kumar”);

The object s2 seeks the messages setdata to the server with the parameter 10 and kumar and server accept the messages and perform the operation and display the result whenver the client called the outdata( )  function.

Defining member  function:

The data members of a class must be declared within the body of the class, whereas the member functions of the class can be defined in any one of the following ways.

*   Inside the class  specification
*   Outside the class  specification

The syntax of a member function definition changes depending on whether it is defined inside or outside the class specification, but it performs the same operation.

(a) Member function inside the class  body:

All the member functions defined within the body of a class. Eg:

Class classname

{

private:

int age;

int  setage(int  agein);//member  function

{

age  =  agein;//body of the  function

}

……….. public:

int b;

void rect( )

{

. .  .  .// body of a  function

}

};

(b)  Member functions outside the  classbody

To declare function prototype within the body of a class and then define it outside the body of a class. This is done by using the ‘scope resolution operator’ (::). It acts as an identity-label to inform the compiler, the class to which the function belongs.

Syntax:

class classname

{

. . . .

Returntype  memberfunction  (arguments);//function  declaration

. . . .

};

returntype classname ::  memberfunction  (arguments)//function definition

{

//body of the function

}

Accessing member functions within the class

A member of a class is accessed by the objects of that class using the dot operator.

Ex:

#include <iostream.h> class number

{

int  num1, num2;//private by default public:

void read( )

{

cout<<”Enter first number: “); cin>>num1;

cout<<”Enter second number: “); cin>>num2;

}

int max( )

{

if(num1>num2)

return num1;

else

}

return num2;

//Nesting of member function void showmax( )

{

cout<<”maximum = “<<max( ) ;

}

};

void main( )

{

}

Output:

number n1; n1.read( );

n1.showmax( );

Enter first number : 5 Enter second number : 10 Maximum =  10

This a member function of a class can call any other member function of its own class is called ‘nesting of member function’.

Data Hiding:

Data is hidden inside a class, so the unauthorized access is not possible, which is the key feature of OOP.

All the data and functions defined in a class are private by default. Normally the data members are declared as private and member functions are declared as public.

Methods of Data hiding:

*   Private
*   Public
*   Protected

These keywords are called access-control specifiers.

Private members:

In this only the member functions of the same class can access these members.

The private members of a class are inaccessible outside the class.

Class person

{

private:

int age;//private data int  getage(  )://private  function

. . .  .

}

person p1;

a  =  p1.age;//cannot access private data //error p1.getage(  );//Error  access

ie., we can access the private members by using objects.

Protected member:

The access control of the protected members is similar to that of private members.

The access control of protected members is shown below:

Class person

{

protected:

. . .  .

int age;// protected data int  getage(  )://protected  function

. . .  .

};

![](Images/image01345.jpeg)person p1; a = p1.age;

p1.getage( );

Public Members

Cannot access protected members

All data members and function declared in the public section of the class can be accessed without any restriction from anywhere in the program.

Eg:

Class person{

public:

}

int age;//public  data

int  getage(  );//public  function

person p1;

a  =  p1.age;// can access public data p1.getage(  );// can access public  function

Nesting of member function

A member function of a class can be called only by an object of that class using a dot operator. In nesting of member function, the member function can be called by using

its name inside another member function of the same class is called nesting member function.

Consider the following example #include <iostream.h>

class set

{

int m,n; public:

void input(void); void display(void); void largest(void);

};

int set :: largest(void)

{

if(m>=n)

return(m);

else

}

return(n);

void set:: input (void)

{

cout<<”input values of m and n” << “\n“;

}

void set:: display(void)

{

cout<<”largest value” << largest( )<<“\n“;

}

void main( )

{

set A:

A input( );

A.set( );

}

Arrays within a class

The arrays can be used as member variables in a class. That is more than one related variable or data are grouped under the common name,

Eg:

Class abc

{

int a[size];//a is name of the array size – represents the size of the array public:

void setdata(void); void display(void);

};

 Inline  function

One of the objective of using functions in a program is to save some memory space

, which becomes appreciable when a function is likely to be called many times. However, every time a function is called, it takes a lot of extra time in executing a series of instructions for tasks such as jumping to the function, saving registers, pushing arguments into the stack and returning to the calling function. When a function is small a substantial percentage of execution time may be spent in such overheads.

C++ has a solution to this problem. To eliminate the cost of calls to small function C++ proposes a new feature called inline function. An inline function is a function that  is expanded in line when it is invoked.That is,the compiler replaces the function call with the corresponding function  code.

An inline function can be defined as below:

![](Images/image01346.jpeg)

Example:

inline int cube(int a)

{

return (a*a*a);

}

The above inline function can be invoked by the statement like;

c = cube(3);

d = cube(2+2);

The output of the above statements will be 27 and 64 for c and d respectively.

To make the function inline, just prefix the keyword inline to the function definition. All inline functions must be defined before they are called.

Remember that the inline keyword merely sends a request , not a command to the compiler. The compiler may ignore this request if the the function definition is too long or too complicated and compile the function as a normal function.

Some of the situations where the inline function may not work are:

*   For functions returning values, if a loop, a switch, or a goto  exists.
*   For functions not returning values, if a return statement  exists.
*   If a function contains static  variables.
*   If inline function are  recrusive.

Example program:

/* program to multiply and divide two different data type using inline function*/

#include<iostream.h> #include<conio.h> class inlinefunc

{

int a,b; float c,d; public:

void multiply(); void divide();

};inline void inlinefunc::  multiply()

{

cout<<"Enter 2 integers:"; cin>>a>>b;

int x=a*b; cout<<x;

}

inline void inlinefunc::divide()

{

}

void main()

{

cout<<endl<<"Enter 2 float values:"; cin>>c>>d;

float y=c/d; cout<<y;

inlinefunc f; clrscr();

f.multiply();

f.divide();

getch();

}

 Empty classes (or  Stubs)

Main reason for using a class is to encapsulate data and code, it is however, possible to have a class that has neither data nor code. In otherwords, it is possible to empty classes.

The declaration of empty classes is as follows: Class xyz

{

};

Class abc

{

};

Such a empty classes are also called as stubs. They are used for creating class templates.

Passing Objects arguments:

*   It is possible to have functions which accept objects of a class as arguments, just as there are functions which accept other variables as  arguments.
*   An object can be passed as an argument to a function by the following ways: 1.Passing object by value, a copy of the entire object is passed to the function

2. Passing object by reference, only the address of the object is passed implicitly to the  function.

3.  Passing object by pointer, the address of the object is passed explicitly to the  function

*   Passing Object by  value

In this case a copy of the object is passed to the function and any modifications made to the object inside the function are not reflected in the object used to call the function.

Example: #include<iostream.h> class test

{

int m1,m2; public:

void get()

{

cin>>m1>>m2;

}

void read(test t3)

{

m1=t3.m1; m2=t3.m2;

}

void display()

{

cout<<m1<<m2;

}

};

void main()

{

test t1;

cout<<”Enter Ist object data”; t1.get();

cout<<”display Ist object data”; t1.display();

test t2;

cout<<”copy of object1 to object2”; t2.  read(t1);

cout<<”display 2nd object data”; t2.display();

}

Run:

Enter Ist object data 34

56

display Ist object data 34

56

copy of object1 to object2 display 2nd object data 34

56

The members of t1 are copied to t2. Any modification made to the data members of the objects t1 and t2 are not visible to the caller’s actual parameter

*   Passing objects by  Reference:

Accessibility of the objects passed reference is similar to those passed by value. Modifications carried out on such objects in the called function will also be reflected in the calling  function.

Example: #include<iostream.h> class test

{

int m1,m2; public:

void get()

{

cin>>m1>>m2;

}

void read(test &t3)

{

m1=t3.m1; m2=t3.m2;

}

void display()

{

cout<<m1<<m2;

}

};

void main()

{

test t1;

cout<<”Enter Ist object data”; t1.get();

cout<<”display Ist object data”; t1.display();

test t2;

cout<<”copy of object1 to object2”; t2.  read(t1);

cout<<”display 2nd object data”; t2.display();

}

Run:

Enter Ist object data 34

56

display Ist object data 34

56

copy of object1 to object2 display 2nd object data 34

56

CONSTRUCTORS

*   Constructor is a special member function, it is used to initialize object data members and allocate the necessary resources to  them.
*   Rules to be followed to construct  constructor:

1. Constructor should be declared in the public  section

2. They are invoked automatically when the objects are  created.

3. They do not have return value specification, not even void is  allowed.

4. It has the same name as that of the class to which it  belongs

*   Syntax

class  classname

{

…………

………… public: classname()

{

//constructor body

}

};

*   Types of  constructors

1. Default  constructors

2. Parameters  constructors

3. Copy  constructors

*   Default  constructors:

The constructor which does not take argument explicitly is called default constructors.

Example:

#include<iostream.h> class test

{

int m1,m2; public: test()

{ m1=50; m2=25;

}

void display()

{

cout<<m1<<m2;

}

};

void main()

{

test t1; //default constructor called cout<<”Initialized data members”; t1.display();

}

Run:

Initialized data members

50 25

*   Parameter Constructors:

Constructors can be invoked with arguments. The argument list can be specified within braces similar to argument list in the function.

Constructor with arguments are called parameterized constructor.

Example: #include<iostream.h> class test

{

int m1,m2; public:

test(int,int);// constructor declaration void  display()

{

cout<<m1<<m2;

}

};

test::test(int  x,int  y)//constructor  defined

{

m1=x; m2=y;

}

void main()

{

test  t1(50,100);//parameter constructor called test  t2(80,90);

cout<<”Initialized object 1 data members”; t1.display();

cout<<”Initialized object 2 data members”; t2.display();

}

Run:

Initialized object 1 data members

50100

Initialized object 2 data members

8090

When constructor has been parameterized we must pass the initial values as Arguments to the constructor function when an object is declared.

Special characteristics of constructor:

*   Constructor should be declared in the public  section
*   They are invoked automatically when the object are  created.
*   They do not have return type, not even void and therefore they cannot return values.
*   It has the same name as that of the class to which it  belongs
*   It is normally used to initialize the data member of a  class
*   It is also used to allocate resources such as memory, to the dynamic data  members of a  class.

Two ways of calling parameterized constructor as:

1. By calling the constructor  explicitly.

2. By calling the constructor  implicitly.

For example object declaration statement is: Test obj1;

In the parameterized constructor declare the object by using the first method( ie. Calling constructor explicitly) is,

Test  obj1=Test(  50,100);//explicit  call

By calling the constructor implicitly then the object declaration is Test obj1(50, 100); //implicit call (or) shorthand method

Thus the constructor is parameterized; we must provide appropriate arguments for the constructor.

#include<iostream.h> class test

{

int m1,m2; public:

test(int,int);// constructor declaration void  display()

{

cout<<m1<<m2;

}

};

test::test(int  x,int  y)//constructor  defined

{

m1=x; m2=y;

}

void main()

{

test  t1(50,100);//Implicit call test t2=Test (80,90); //explicit  call

cout<<”Initialized object 1 data members”; t1.display();

cout<<”Initialized object 2 data members”; t2.display();

}

Run:

Initialized object 1 data members

51100

Initialized object 2 data members

8090

In this program the class test creates an object t1, t2 and passes the values 50,100 and 80,90respectively. Hence can be called automatically whenever the object is created, and we call the display function for display the output.

Multiple constructors in a class:

Multiple kinds of constructor can be used in the program such as,

*   No argument constructor ( eg: test()  )
*   With argument constructor ( eg: test ( int, int)  )

In the first case constructor itself supplies the data values, and no values are passed by

the calling program.

In the second case, the function call passes the appropriate values from main(). The c++ class can permit us to use both these constructor int the same constructor.

Example:

class test

{

int m,n; public:

test()// default  constructor

{ m=0; n=0;

}

test(int s, int b) // with argument constructor

{

m=a; n=b;

}

};

Constructor Overloading:

*   The class can have multiple constructors and all the constructors have the same name as the corresponding class, and they differ only interms of  their number of arguments, or data types of their argument or both, is called constructor overloading.
*   Consider the following example for using more than one constructor on  the same  class.
*   Example: #include<iostream.h> class  account

{

private:

int accno; float balance; public: account()

{

cout<<”enter the account number”; cin>>accno;

cout<<”enter the balance”; cin>>balance;

}

account( int an)

{

accno=an; balance=0.0;

}

account(int acvalue, float bal)

{

accno=acvalue; balance=bal;

}

void display()

{

cout<<” Account number is:”<<accno; cout<<”Balance is:”<<balance;

}

};

void main()

{

account acc1; account acc2(45);

account acc3(324,675.50); cout<<”the account information is”; acc1.  display();

acc2\. display(); acc3.  display();

}

Run:

Enter the account Number: 3 Enter the balance: 546

Account information is Account number is :3 Balance is:546 Account number is :45 Balance is:0

Account number is :324 Balance is:675.50

Thus the constructor is called during the creation of an object depending on the number and type of arguments passed.

the invocation of different constructors during the creation of an object of the class account is

class account

{

public:

account(); account(int an);

account(int acvalue,float bal);

………………

};

accout acc1; account acc2(45);

account acc3(324,675.50);

Copy constructor:

*   A copy constructor is used to declare and initialize an object from another object (ie, all the data’s should be copied from one object to another  object)
*   For example:integer  obj2(obj1);

The above statement defines the object obj2 and at the same time initializes or copies the values of ‘obj1’

*   Another form of this statement  is

Integer obj2=obj1;

*   The process of initializing through a copy constructor is known as copy initialization.
*   “A copy constructor takes a reference to an object of the same class as itself as an  argument.”

*   Example: #include<iostream.h> class code

{

int id; public:

code()

{

}

code( int a)

{

id=a;

}

code( code &x)

{

id=x.id;

}

};

void main( )

{

code A(100); code B(A); code C=A; code D; D=A;

cout<<” Id of A object is:”; A.display();

cout<<” Id of B object is:”; B.display();

cout<<” Id of C object is:”; C.display();

cout<<” Id of D object is:”; D.display();

}

Output:

Id of A object is:100 Id of B object is:100 Id of C object is:100 Id of D object is:100

Explanation:

*   In this program the main program pass the value 100 whenever the single parameterized constructor is  called.
*   Now the data’s contained in the object A can be copied into the object B by the statement of code  B(A).
*   This data can be received by the object X through the reference. Here A should be act as actual parameter and x should be act as a formal parameter, that is the change should be made on actual argument reflect in formal argument , because it will be a copy  constructor.

DESTRUCTOR

*   When an object is no longer needed it can be  destroyed.
*   A class can have another special member function called destructor, which is called when the object is  destroyed.
*   Destructor is a member function having the character ~(tilde) followed by the name of its class and brackets.
*   It should be declared as  follows,

~classname( );

*   The destructor can be called automatically when the object goes out of scope and is no longer needed.
*   General format class classname

{

…………

………….. // private members public:

~classname( ); // destructor prototype or declaration

};

class name :: ~ classname(  )

{

// destructor body  definition

}

Rules for defining the destructor

*   The destructor name is same as the class name but prefixed by a  tilde(~).
*   Unlike constructor destructor does not take any  arguments
*   The destructor has no return type like the constructor, since it is invoked automatically whenever the object goes out of  scope.
*   Destructor must be declared in the public section of a class, so that it is accessible to all its  users.
*   There can be only one destructor in each class. The overloading is not possible.

Example Program #include< iostream.h> int count =0;

class test

{

public: test( );

~test ( );

};

test::test(  )

{

count  ++;

cout<< “object “<< count<<”constructor of class test is called”:

}

test::~test( )

{

cout<< “object “<< count<<” Destructor of class test is called”: count--;

}

void main()

{

test x; // constructor called

{

test y; //constructor called

}

}

Output:

object 1 constructor of class test is called object 2 constructor of class test is called

object 2 destructor of class test is called object 1 destructor of class test is called

Explanation:

In this above program whenever the object is created the corresponding constructor can be invoked. After terminating the program that is the object is out of the range(scope) than automatically the destructor is called.

DYNAMIC OR RUN TIME MEMORY ALLOCATION/ NEW, DELETE  OPERATORS

*   Whenever an array is defined, a specified amount of memory is set aside  at compile time, which may not be utilized fully or may not be  sufficient.
*   If a situation arises in which the amount of memory required is unknown at compile time, the memory allocation can be performed during execution  time.
*   Such a technique of allocating memory during run time is known as Dynamic memory  allocation.
*   C++ provides following two special operators to perform memory  management:

*   ‘new’ operator for dynamic memory  allocation
*   ‘delete’ operator for dynamic  deallocation

new Operator:

The new operator offers dynamic memory allocation for variable and object.

General format:

Pointer variable = new datatype;

*   Here, pointer- variable is a pointer of type  datatype.
*   New operator allocates sufficient memory for the  variable.
*   The pointer variable holds address of the memory space  allocated.
*   Example:

p=new int; q= new float;

where p is a pointer of type int and q is a pointer of type float.

Here, p & q are pointer variable we must declare it as a pointer  variable. int *p; float  *q;

we can combine the declaration of pointer and their assignment as: int *p=new  int;

float *q = new float; subsequently we have use statements:

*p=32;

*q=5.5;

assign 32 to the newly created int object and 5.5 to the float object.

Allocating memory along with initialization is:

Pointer variable= new datatype(value); Example:

int *p=new int( 32); float *q = new  float(5.5);

Memory allocation for one dimensional array is:

Pointer variable= new datatype [ size ]; Example: int *p=new int[20];

It will creates a memory space for an array of 100 integers. P[0] refers to the first element, p[1], to the second, and so, on.

Example:

void main( )

{

int n;

cout<<”enter no of elements to be processed”; cin>>n;

int *pt= new int[  n  ];// run time allocates space for array variable pt cout<<”enter the  elements”;

for(int i=0;i<n;i++)

{

cin>>pt[i];

}

cout<<”display elements”; for(int i=0;i<n;i++)

{

Run:

cout<<pt[i];

}

}

enter no of elements to be processed 5

enter the elements 43 56 54 23  67

display elements 43 56 54 23 67

delete Operator:

When data object is no longer needed, it is destroyed to release the memory space fro reuse.

General format:

delete pointer variable;

The pointer variable is the pointer that points to a data object created with new operator. Example:

delete p; delete q;

If we want to free a dynamically allocated array . the general format:

delete [size] pointer variable;

where the size specifies the number of elements in the array to be freed. Example: for the above example program:

delete [n] pt;

 ‘This’  pointer:

The ‘this’ pointer is passed as a hidden argument to all nonstatic member function calls and is available as a local variable within the body of all nonstatic functions. ‘this’ pointer is a constant pointer that holds the memory address of the current object. ‘this’ pointer is not available in static member functions as static member functions can be called without any object (with class  name).

Example: #include<iostream.h> #include<conio.h>

class add

{

int a; public:

add(int x)

{

a=x;

}

void sum()

{

this->a=this->a+4;

}

void display()

{

cout<<"\na="<<this->a;

}

};

void main()

{

clrscr();

add ob(3);

ob.display();

ob.sum();

ob.display();

getch();

}

Output:

a=3 a=7

‘this’ pointer with return

#include<iostream.h> #include<conio.h>

class add

{

int a; public:

add(int x)

{

a=x;

}

add*  sum()

{

this->a=this->a+4; return(this)

}

void display()

{

cout<<"\na="<<this->a;

}

};

void main()

{

clrscr(); add obj(3);

add *ob=&obj; ob->display(); ob=ob->sum(); ob->display(); getch();

}

Output:

a=3 a=7

FRIEND FUNCTIONS AND FRIEND  CLASSES

Definition: The function that are declared with the keyword ‘friend’ are called friend function, that is the common function to be made friendly with both the classes, thereby allowing the function to have access to the private data of those classes.

Special characteristics of friend function:

 The scope of a friend function is not  limited

 A friend function cannot be called using the object of that  class

 The friend function can access both private and public data  members

 The friend function can be declared either in private or public section without affecting it  meaning.

To make an outside function friendly to a class, we have to simply declare this function as a friend of the class as shown below:

class ABC

{

……..

……… public:

……

…….

friend void display( ); //declaration;

};

Example:

#include <iostream.h> class sample

{

int x,y; public:

void getvalue()

{

x=50; y=40;

}

friend void display( sample a);

};

void display( sample a)

{

cout<<a. x<< b. y;

}

void main( )

{

ABC obj1;

obj1\. getvalue( ); display( obj1);

}

The output of program would be: 50  40

*   the function accesses the class variables x and y by using the dot operator and the object passed to  it.
*   The function call display(obj1) passes the object obj1 by value to the friend function.

Classes with friend function:

Consider a situation of operating on objects of two different classes, in such situation, friend function can be used to bridge the two classes.

Exmaple:

#include<iostream.h>

class result; //advance declaration class test

{

int n1,n2; public:

void getmark( )

{ n1=45; n2=78;

}

friend void display(  test,  result);// friend function  declaration

};

class result

{

int tot; public:

friend  void  display(test,result);// friend function  declaration

};

void display( test t, result r)

{

 ot=  t.n1+t.n2;// private member of test class accessed using t objecr cout<<r.  tot;

}

void main(  )

{

test t; result r;

t.getmark(  );

display( t,  r);

}

Explanation:

*   The program contains two classes test and  result.
*   The display function is friend function to access the private data members of both the  classes.
*   Declaration of the friend function can be placed either in the private or public section of the  class.
*   An object of each class has been passed as an argument to the function display (  ).
*   It can access the private members of both classes through these  arguments.
*   The advanced declaration of the class result; in the beginning of the program is necessary, since a class cannot be referred until it has been declared before the class test.

Uses of friend function:

1. Function operating on objects of two different classes.

2. Friend function can be used to increase the versatility of overloaded  operators.

FRIEND CLASSES

Definition:

All the functions of another class to manipulate or use the private members of the friend class.

Example: #include<iostream.h> class  two;

class one

{

private:

int x, y;

public:

void setdata(int a, int b)

{

x=a; y=b;

}

friend class two;

};

class two

{

int z; public:

void addone(one obj)

{

z= obj. x + obj . y;

}

void display(one obj )

{cout<<”X is: “<<obj.x<<”Y  is:”<<obj.y;

cout<< “sum of one class data members”<< z;

}

};

void main( )

{

one obj1; two obj2;

obj1\. setdata( 45,65); obj2. addone(obj1); obj2\. display( obj1);

}

Run

X is:  45

Y is:  65

sum of one class data members: 110

Explanation:

*   Class two is friend to class one, so all the private members of class one can be accessed in member function of class two using class one  object.
*   Here addone () and display () functions using the private data members of class one. So both the functions are having argument as object of class  one.

Function  overloading

*   It is possible to define several functions having the same name, but performing different  actions.
*   It helps in reducing the need for unusual function name, making the code easier to  read.
*   This can be done using the concept Function polymorphism or function overloading.
*   Function overloading allows multiple functions to share the same name  with different argument type.
*   Function Polymorphism implies that the function definition can have multiple forms. The definitions must only differ in number of arguments and types of arguments.
*   Example: //Multiple swap functions #include<iostream.h>

void swap(char x, char y)

{

char  t=x;

x=y; y=t;

cout<<”Swapped characters”<<x<<setw(5)<<y;

}

void swap(int x, int y)

{

int t=x;

x=y; y=t;

cout<<”Swapped integers”<<x<<setw(5)<<y;

}

void swap(float x, float y)

{

float  t=x;

x=y; y=t;

cout<<”Swapped real numbers”<<x<<setw(5)<<y;

}

void main()

{

char a1,b1;

cout<<”Enter two characters”; cin>>a1>>b1;

swap(a1,b1);

int a2,b2;

cout<<”Enter two integers”; cin>>a2>>b2; swap(a2,b2);

float a3,b3;

cout<<”Enter two real numbers”; cin>>a3>>b3;

swap(a3,b3);

}

Run:

Enter two characters ET

Swapped characters T E Enter two integers

20 30

Swapped integers 30 20 Enter two real numbers 30.5 20.5

Swapped real numbers 20. 5  30.5

*   In the above program, three functions named swap() are defind, which  only differ in their arguments data type: char , int, or float. In main() when the statement

Swap(a1,b1);

*   Is encountered, the compiler invokes the swap() function which takes character type arguments. This decision is based on the data type of the  arguments.

void swap(float &x, float &y); void swap(float &x, float &y); void swap(float &x, float &y); void swap(float &x, float &y); void main()

{

char a1, b1; int a2,b2 float a3,b3; swap(a1,b1);

swap(a2,b2);

swap(a3,b3);

}

*   C++ does not permit overloading of function differing only in their return  value.

 Operator  Overloading

*   Unlike C, in C++, such operators can also be overloaded explicitly to operate on operand of user-defined types (i.e., objects of  class).
*   For instance, the  statement,

c3= addcomplex (c1, c2);

*   Performs the addition of operands c1 and c2 belonging to the user defined data type and assigns the result to c3 (which is also operand of the user-defined data  type).

*   ![](Images/image01347.jpeg)In C++,by overloading the + operator, the above statement can be changed to an easily readable  form:

c3=c1+c2;

Operand 1

Operand 2

*   Operator overloading, thus allows to provide additional meaning to operators such as +, *, >=, +=, etc., when they are applied to user-defined data  types.
*   The operator overloading feature of C++ is one of the methods of  realizing

polymorphism.

*   The word polymorphism is derived from the Greek word poly and morphism (polymorphism=poly+morphism).
*   Poly refers to many or multiple and morphism refers to actions i.e.,  performing many actions with a single  operator.
*   The concept of operator overloading can also be applied to data  conversions.
*   C++ offers automatic conversion of primitive data  types.
*   For example, in the statement x=a+b, the compiler implicitly converts the integer result to floating-point representation and then assigns to the float variable  x.
*   But, the conversion of user-defined data types requires some effort on the part of the  programmer.
*   Thus, operator overloading concepts are applied to the following two principle areas:

*   Extending capability of operators to operate on user-defined  data.
*   Data  conversion.

*   Operator overloading extends the semantics of an operator without changing  its

syntax.

*   The rules defined by C++ that governs its use such as number of operands, precedence, and associativity of the operator remains the same for overloaded operators.
*   Therefore, it should be remembered that the overloaded operator should not change its original  meaning.
*   However, semantics (meaning) can be changed, but it is advisable to retain the predefined  logical-meaning.
*   Operator overloading is a concept of overloading of existing  operators.
*   Operator overloading allows us to assign multiple meanings to the  operators.
*   An overloaded operator is called an operator  function.
*   The C++ language uses the keyword “operator” for overloading of  operators.
*   You declare an operator function with the keyword “operator” preceding the operator.
*   The operator keyword is to overload built-in  operators.
*   Overloaded operators are distinct from overloaded  functions.
*   Operator overloading is the ability to tell the compiler how to perform a certain operation when its corresponding operator is used on one or more  variables.
*   We can overload (give additional meaning to) all the C++ operators, except the following:

| S.No. | Operators | Meaning |
| 1. | . | Class member access operator |

| 2. | .* | Pointer-to-member access operator |
| 3. | :: | scope resolution operator |
| 4. | size of | size of operator |
| 5. | ?: | conditional operator |
| 6. | # | Preprocessor convert to string |
| 7. | ## | Preprocessor concatenate |

Table: Operators that cannot be overloaded

*   The excluded operators are very few when compared to the large number of operators which qualify for the operator overloading  definition.

Note:-  Although the semantics of an operator can be extended, we cannot change its syntax, the rules that govern its use such as number of operands, precedence and associativity. (For ex. multiplication operator will have higher precedence than the addition operator)

*   Remember, when an operator is overloaded, its original meaning is not  lost.

 Over loadable  operators

*   C++ provides a wide variety of operators to perform operations on various operands.
*   The operators are classified into unary and binary operators based on the number of arguments on which they  operate.
*   C++ allows almost all operators to be overloaded in which case at least one operand must be an instance of a class  (object).

| S.No. | Operator category | operators |
| 1. | Arithmetic | + , -, *, /,  % |
| 2. | Bit-wise | &, &#124;, ~, ^ |
| 3. | Logical | &&, &#124;&#124;, ! |
| 4. | Relational | >, <, ++, !=, <=,  >= |
| 5. | Assignment | = |
| 6. | Arithmetic assignment | +=, -=, +=, /=, %=, &=, &#124;=,  ^= |
| 7. | Shift | <<, >>, <<=,  >>= |
| 8. | Unary increment and decrement | ++,  -- |
| 9. | Subscripting | [ ] |
| 10. | Function call | ( ) |
| 11. | Dereferencing | -> |
| 12. | Unary sign prefix | +,  - |
| 13. | Allocate and free | new, delete |

Table. C++ overloadable operators

Examples:

I. The compiler acts differently with regards to the subtraction operator “-“ depending on how the operator is being  used.

*   When it is placed on the left of a numeric value such as -48, the compiler considers the number a negative  value.
*   When used between two integral values, such as 80-712, the compiler applies the subtraction  operation.
*   When used between an integer and a double-precision number, such as 558-9.27, the compiler subtracts the left number from the right number; the operation produces a double-precision  number.
*   When the - symbol is doubled and placed on one side of a variable, such as --Variable or Variable--, the value of the variable needs to be decremented; in other words, the value 1 shall be subtracted from it.

II. “*” operator when applied to a pointer variable, gives the value pointed by the pointer. But is also commonly used for  multiplication.

*   So, the number and type of operands decide the nature of operation to  follow.

III. The input/output operations like “<<” and” >>” are good examples of operator overloading.

<<-Built-in definition is for shifting of  bits.

-But in C++,it is used for diplaying the  values.

*   Similarly, we can define additional meaning to all other C++  operators.

 Operator keyword

*   The keyword operator facilitates overloading of the C++  operators.
*   The keyword operator indicates that the operator symbol following it, is the C++ operator to be overloaded to operate on members of its  class.
*   To define an additional task to an operator, we must specify what it means in relationship to the class to which the operator is  applied.
*   This is done with the help of a special function, called operator function,  which

![](Images/image01348.jpeg)![](Images/image01349.jpeg)describes th

*   The  gener

operatorsymbol return_typeoperatorop(arglist)

{

body of  operator function//task defined

}

Fig. Syntax of operator overloading

Where,

*   return_type is the type of value returned by the specified  operation.
*   Op is the operator being overloaded i.e., operator  symbol.
*   Op is the preceded by the keyword  operator.
*   ‘Operator op’ is the function  name.

Example:

int operator+(int a, int b)

{

return a+b;

}

 Process of  overloading

*   Create a  class.
*   Declare the operator function operator op( ) in the public part of the class. It may be either a normal member function or friend  function.
*   Define the operator function to implement the required  operations.
*   These operators may be defined as member or non-member  functions.

 Types of operator  overloading

*   Unary operator  overloading
*   Binary operator  overloading

 Unary operator  overloading

*   A Unary operator acts on only one operand i.e., takes one  operand.
*   The syntax  for invoking the overloaded unary operator function  is:

operator object (or) object operator

Ex:

++x(or)x++

*   Overloading without explicit arguments to an operator function is known as unary operator  overloading.

*   The syntax of overloading the unary operator  is:

![](Images/image01350.jpeg)

*   ![](Images/image01351.jpeg)Some commonly used unary operators are unary minus (-), increment (++)  and

decrement (--) operators.

*   Some Example unary overloaded operator  functions:

i. int operator--( );

ii. void operator+(  );

iii. float operator –(  );

iv. void operator++( );

Example programs:

*   For  example, let us consider the unary minus  operator.
*   A minus operator when used as a unary, takes just one  operand.

*   We know that minus operator changes the sign of operand when applied to a basic data item.
*   In the same manner, the unary minus when applied to an object should change the sign of its data  items.

1. /*overloading unary  minus*/

#include<iostream.h> #include<conio.h>

class unary

{

int x,y,z;

public:

};

void getdata(  )

{

cout<<"Enter the x,y,z values: "; cin>>x>>y>>z;

}

void display( )

{

cout<<x<<"\t"<<y<<"\t"<<z;

}

void operator-( );

void unary::operator-( )

{

x=-x;

y=-y;

z=-z;

}

void main( )

{

clrscr( );

unary ob; ob.getdata( );

cout<<" “BEFORE ACTIVATING THE OPERATOR\n”;

cout<<”Values of x,y,z \n"; ob.display( );

-ob;

cout<< “AFTER ACTIVATING THE OPERATOR\n“;

cout<<"Values of x,y,z \n”; ob.display( );

getch( );

}

Output:

Enter the x,y,z values: 5 6 7

BEFORE ACTIVATING THE OPERATOR

Values of x,y,z 5-67

AFTER ACTIVATING THE OPERATOR

Values of x,y,z

-56-7

Note:

*   The function operator –( ) takes no  argument.
*   It only changes the sign of data members of the object  ob.
*   Since this function is a member function of the same class, it can directly access the members of the object which activated  it.

2. /*overloading increment and decrement operators*/ #include<iostream.h>

#include<conio.h>

class space

{

private:

int x,y,p,q;

public:

void getdata(int a,int b,int m,int n)

{

x=a; y=b;

p=m; q=n;

}

void display( )

{

cout<<"values of x,y for increment operator "<<endl; cout<<x<<"\t"<<y<<endl;

cout<<"values of p,q for decrement operator "<<endl; cout<<p<<"\t"<<q<<endl;

}

void operator++( )

{

x=++x; y=y++;

}

void operator--( );

};

void space::operator--( )

{

p=--p;

q=q--;

}

void main( )

{

clrscr();

space s; s.getdata(12,76,80,45);

cout<<" BEFORE OVERLOADING \n";

s.display();

++s;

--s;

cout<<"\ nAFTER OVERLOADING\n";

s.display();

getch();

}

Output:

BEFORE OVERLOADING

values of x,y for increment operator 1276

values of p,q for decrement operator 8045

AFTER OVERLOADING

values of x,y for increment operator 1376

values of p,q for decrement operator 7945

 Limitations of increment/ decrement  operators

Adding or subtracting 1 from a variable is a very common programming practice. Adding 1 to a variable is called incrementing and subtracting 1 from a variable is called decrementing.

1. The prefix notation causes a variable to be updated before its value is used in the expression.

*   Whereas the postfix notation causes it to be updated after its value  is used.

obj1=++obj2;

*   Has exactly same effect as the statement obj1=obj2++;

*   When ++ and – operators are overloaded, there is no distinction between the prefix and postfix overloaded operator  function.

2. Increment and decrement operators work only with integer variables , not on floating point variables and not on  literals.

3. The execution of the prefix and postfix is under Java control ,you cannot change the order of execution

For example:

num = (((x--)))* count; //still decrements x last. parentheses will not force an early execution

4. A limitation with using the increment or decrement operator is that the variable being operated upon can only be incremented or decremented by the value  ONE.

*   If you need to increment (or decrement) by a larger (or  smaller) value, you must use statements  like:

j  += 2;(or)j-=  5;

 Binary operator  overloading

*   [Binary](http://www.tech-faq.com/binary.html) operators can be overloaded in a similar manner as unary  operators.
*   Binary operator acts on two operands i.e., takes two  operands.
*   Overloading with a single explicit argument is known as binary operator overloading.
*   The syntax of overloading the binary operator  is:

![](Images/image01352.jpeg)Argument to operator function return_type              operator              op(  arg)

{

body of  operator function//task defined

}

![](Images/image01353.jpeg)We should  note  thator:

1. It receives only one class type argument explicitly, in case of a member function.

2. i.e., the binary overloaded operator function takes the first object as an implicit operand and the second operand must be passed as an argument  explicitly.

3. The data members of the first object are accessed without using the dot operator.

4. Whereas, the second argument members can be accessed using the dot operator if the argument is object, otherwise it can be accessed directly.

Note  that, the overloaded binary operator function is a member function defined in the first object’s  class.

For example:

*   Consider the following  expression:

C = A  +  B;//arithmetic  notation

o The above expression contains three objects namely A, B and C of which A and B are the operands while C is the one to which the sum of A and B is assigned to  C.

o In the above expression, the operator function is supposed to add two user defined data types and return a user defined data  type.

*   For executing the above expression, the binary operator function will be written as,

![](Images/image01354.jpeg)

user_defined operator+(user_defined rhs)

{

user_defined temp; temp.x = x + rhs.x; temp.y = y + rhs.y;

return temp;

}

*   Now consider the  statement:

temp.x = x + rhs.x;

o In the above expression x is the data member of the object A that is invoking the operator member  function.

o while rhs.x refers to the data member of the object B, which is passed as an argument to the function. Since the function operator +( ) needs to return the  result.

o We need to have a temp variable (of the same class type) that stores the value to be  returned.

Note:-  It should be noted here that in overloading binary operators the object to the left of the operator is used to invoke the operator function while the operand to the right of the operator is always passed as an argument to the function.

Example program

/* Program that illustrates overloading of a binary operator*/ #include <iostream.h>

#include<conio.h>

class complex

{

float x;//real part

float y;//imaginary part public:

complex()//constructor  1

{

}

complex(float  real,float  imag)//constructor  2

{

x=real; y=imag;

}

complex operator+(complex c); void display();

};

/* Operator overloaded using a member function*/ complex complex::operator+(complex c)

{

complex  temp;//temporary temp.x=x+c.x;//these are temp.y=y+c.y;              //float additions return(temp);

}

void complex::display()

{

cout<<x<<"+j+"<<y<<"\n";

}

int main()

{

clrscr();

complex  c1,c2,c3;//invokes constructor 1 c1=complex(2.5,3.5);                            //invokes constrcutor 2 c2=complex(1.6,2.7);                            //invokes constrcutor 2 c3=c1+c2;                            //invokes operator+()  function

cout<<"c1= "; c1.display();

cout<<"c2= "; c2.display();

cout<<"c3= "; c3.display();

getch(); return 0;

}

Output:

c1= 2.5+j+3.5 c2= 1.6+j+2.7 c3= 4.1+j+6.2

 Explanation about the  program

*   Let us have look at the function operator +( ) and see how the operator overloading is  implemented.

complex complex::operator+(complex c)

{

complex  temp;//temporary temp.x=x+c.x;//these are temp.y=y+c.y;              //float additions return(temp);

}

*   We should note the following features of this  function:

*   It receives only one complex type argument  explicitly.
*   It returns a complex type  value.
*   It is a member function of  complex.

*   The function is expected to add two complex values and return a complex value as the result but receives only one value as  argument.
*   Then where does the other value comes from  ?

*   Now look at the statement that invokes the above  function:

c3=c1+c2;//invokes operator +( )  function

We know that a member function can be invoked only by an object of the same class.Here,the object c1 takes the responsibility of invoking the function and c2 plays the role of an argument that is passed to the function.

*   The above invocation statement is equivalent  to:

c3=c1.operator+(c2);//usual function call  syntax

Therefore,in the operator+( ) function,the data members of c1 are accessed directly and the data members of c2 (that is passed as an argument) are accessed using the dot operator.Thus,both the objects are available for the function.

*   For example in the  statement,

temp.x = a + c.x;

*   c.x refers to the object  c1.
*   temp.x is the real part of temp that has been created specially to hold the results of addition of c1 and  c2.

*   The function returns the complex temp to be assigned to  c3.

*   As a rule, in overloading of binary operators,left-hand operand is used to invoke operator function and the right-hand operand is passed as an  argument.

*   The figure below shows how this is  implemented:

![](Images/image01355.jpeg)

Fig. Implementation of operator +(complex c) function

 Arithmetic  operators

*   As binary operators, these involve two arguments which do not have to be the same  type.
*   The arithmetic operators  are:

o+ (addition)

*   -  (subtraction)
*   * (multiplication)
*   /  (division)
*   %  (modulus)

 Rules for overloading  operators

Although it looks like simple to redefine the operators, there are certain restrictions and limitations in overloading them.

*   Only existing operators can be overloaded. New operators cannot be  created.
*   The overloaded operator must have at least one operand that is of user-defined type.
*   We cannot change the basic meaning of an operator i.e., we cannot  redefine plus(+) operator to subtract one value from the  other.
*   Overloaded operators follow the syntax rules of the original operators. They cannot be  overridden.
*   There are some operators that cannot be overloaded.
*   We cannot use friend function to overload certain operators. However, member functions can be used to overload  them.
*   A Unary operator, overloaded by means of a member function, takes no  explicit arguments and returns no explicit  values.
*   Binary operators overloaded through a member function takes one  explicit argument.
*   When using binary operators overloaded through a member function, the left hand operand must be an object of the relevant  class.
*   Binary arithmetic operators such as +, =, *, and / must explicitly return a  value. They must not attempt to change their own  arguments.

UNIT-III

 Base class and derived class  relationship

 Derived class  declaration

 Forms of inheritance-Inheritance and member  accessibility

 Multiple  inheritance

 Multi level  inheritance

 Hybrid  inheritance

 Constructors in derived class-Destructors in derived  class

 Virtual base  classes

 Member function  overriding

 Virtual  functions.

 Inheritance

*   C++ strongly supports the concept of REUSABILTY i.e., one class that has been written and tested already can be used to create a new  class.
*   It is like child inheriting the features of its parents(such as beauty of the mother and intelligence of the father)The reusable property will reduce the debugging  time
*   The time overhead and cost overhead will be  reduced.
*   Thus, the reusability mechanism is applied to the  inheritance

 Base class and derived class  relationship

*   The mechanism of deriving the new class from an old one or the technique of building new classes from the existing classes is called  inheritance.
*   The old class is called as base class and the new class is called as derived class.
*   The derived class inherits some or all the traits from the base  class.
*   ![](Images/image01356.jpeg)![](Images/image01357.jpeg)The base class remains  unchanged.

![](Images/image01358.jpeg)

Base class

![](Images/image01359.jpeg)

![](Images/image01360.jpeg)

Derived class

1

Defined in derived class

![](Images/image01361.jpeg)![](Images/image01362.jpeg)![](Images/image01363.jpeg)Defined in base class also accessible from derived class

Fig. Base class and derived class relationship

*   A class can also inherit properties from more than one  level.
*   The base class is often called the ancestor, parent or super  class.
*   And the derived class is called the descendent, child or  subclass.
*   In the fig. above derived class inherits the features of the base class (A,B,C) and adds its own features  (D).

 Derived class  declaration

*   A derived class extends its features by inheriting the properties of  another class,called base class and adding features of its own.

*   ![](Images/image01364.jpeg)The general form  of declaring a derived class  is

![](Images/image01365.jpeg)

Fig. Syntax of derived class declaration

*   The derivation of he Derivedclass from the Baseclass is indicated by the colon (  :

).

*   The visibility mode is optional and , if present , it may be either private or  public.
*   The default visibility mode is private.
*   Visibility mode specifies whether the features of the base class are publicly  or

privately inherited.

Note:-

*   No memory is allocated to the derived class when it is  declared.
*   But memory is allocated when it is instantiated to create  objects.

4 Inheritance and member accessiblity

The following are the three possible styles of derivation:

1. Class abc :  private  xyz// private  derivation

{

.......// members of  abc

.......

};

the above class is derived from a base class xyz

2. Class abc :  public  xyz// public  derivation

{

......//members of  abc

......

};

3. Class abc  :  xyz// private derivation by  default

{

......//members of  abc

......

};

![](Images/image01366.jpeg)When a base class is inherited by a derived class with visibility mode “private” i.e., when base class is privately inherited:

*   All “‘public members” of the base class become “private members” of  the

derived class.

*   And therefore all the public members of the base class can only be accessed by the member functions of the derived  class.
*   They are inaccessible to the objects of the derived  class.
*   Note:-
    *   All “public members” of a class can be accesseb by its own objects  using

dot operator.

*   i.e., no member of the base class is accessible to the objects of  the

derived class.

![](Images/image01366.jpeg)When a base class is inherited by a derived class with visibility mode “public” i.e., when base class is “publicly” inherited:

*   All “‘public members” of the base class become “public members” of  the

derived class.

*   And therefore all the public members of the base class can be accessed by the member functions of the derived  class.
*   Also accessible to the objects of the derived class.

Note:-

*   In both the cases,the “private members” of the base class cannot be inherited to  the

derived class.

*   i.e.,the “private members” of the base class will never become the members of  its

derived class.

 Making a private member  inheritable

*   We can make the private members inherited by the derived  class.
*   This can be accomplished by modifying the visibility limit of the  private

member,by making it public.

*   This would make it accessible to all the other functions of the  program,thus taking away the advantage of “data  hiding”.

*   C++ provides a third visibility modifier, protected,which serve a limited  purpose in  inheritance.
*   The data members declared as protected will be accessible by the member functions of its own  class.
*   And any class which is immediately derived from  it.
*   These data protected data members cannot be accessed by no other functions outside these two  classes.
*   A class can now use all the three visibility modes as shown  below: class  abc

{

private://optional

.............

..............//visible to member functions within its  class

protected:

...............//visible to member functions

................// of its own class and its immediate derived  class

public:

................//visible to all functions

................//in the  program

};

*   When a protected member is inherited in public mode derivation,it  becomes

protected in the derived class too.

*   And therefore is accessible by the member functions of the derived  class.
*   It is also ready for funther  inheritance.

*   When a protected member is inherited in the private mode derivation,it becomes private in the derived  class.
*   Although it is avaible to the member functions of the derived  class.
*   It is not available for further inheritance (since private members cannot be inherited).
*   The keywords private,protected and public may appear in any order and  any number of times in the declaration of the  class.

For example:

class abc

{

protected:

...............

................

public:

................

................

private:

.............

..............

public:

.............

.  ............

};

is a valid class definition.

Note:-

*   It is possible to inherit a base class in protected mode (known as protected  derivation).
*   In protected derivation,both the public and protected members of the base  class become protected members of the derived  class.

![](Images/image01366.jpeg)Table below summarizes how the base class members undergoes modifications in all the three types of derivation:

| Base class visibility | Derived class visibility |
| Public derivation | Private derivation | Protected derivation |
| Private | Not inherited | Not inherited | Not inherited |
| Protected | Protected | Private | Protected |
| Public | Public | Private | Protected |
|  |  |  |  |

Table.Visibility of inherited members

![](Images/image01367.jpeg)Forms of  Inheritance

1. Single  inheritance

2. Multiple  inheritance

3. Multilevel inheritance

4. Hierarchical  inheritance

5. Hybrid  inheritance

 Single  inheritance

*   The derived class with with one base class is called Single  inheritance.

![](Images/image01368.jpeg)

Fig.Single inheritance

*   The syntax of single  inheritance:

![](Images/image01369.jpeg)

Example program:

#include <iostream.h> #include<conio.h>

class  base//base class

{

int  a,b;//private; not  inheritable

public://public; ready for  inheritance

int sum;

void getdata()

{

cout<<”enter sales values for a and b”<<endl; cin>>a>>b;

}

void calculate()

{

sum=a+b;;

}

};

class  derived:  public  base//derived class

{//base class is publicly  inherited

public:

void putdata()

{

cout<<”the sum value is:”<<sum;

}

};

void main()

{

clrscr();

derived  d;//object of derived class d.getdata();

d.calculate(); d.putdata();

getch();

}

Output:

enter sales values for a and b 58

the sum value is:13

 Explanation about program:

*   Here in the above example we have defined a “base” as the base class and “derived” as the derived class of in which the visibility mode is  “public”.
*   So that the public data’s can be inherited by the derived class as the public data’s of it’s own  class.

*   Here,  in  the  inheritance  it  is  not  necessary  to  create  an  object  of  the  both  base  and

derived classes.

*   Instead of that we can create an object of the derived  class.
*   And we can call all the member functions of the both the derived and the base class by using the derived class object.

 Multiple  inheritance

*   ![](Images/image01370.jpeg)The derived class with with more than one base class is called multiple  inheritance

Superclass (Parent 2)

Subclass (Child)

Fig.Multiple

inheritance

*   The general syntax for derived class with multiple inheritance (multiple base class) is as  follows:

![](Images/image01371.jpeg)

Fig. Syntax of multiple inheritance

*   A derived class with multiple inheritance is declared as  follows:

![](Images/image01372.jpeg)

*   Multiple inheritance allows us to combine the features of several existing classes as  a starting point for defining new  classes.
*   It is like child inheriting physical features of one parent and intelligence of  another.

![](Images/image01367.jpeg)

Example program1:

#include<iostream.h> #include<conio.h>

class abc

{

public:

int a;

void getdata()

{

cout<<"enter a value:"<<endl; cin>>a;

}

};

class def

{

public:

int b; void  get()

{

cout<<"\nenter b value: "<<endl; cin>>b;

}

};

class xyz : public abc, public def

{

public:

void show()

{

cout<<"a and b values are: "<<a<<"\t"<<b;

}

};

void main()

{

clrscr();

xyz w; w.getdata();

w.get();

w.show();

getch();

}

Output:

enter a value: 6 enter b value: 9

a and b values are: 6  9

Example program 2:

#include<iostream.h> #include<conio.h>

class M

{

protected:

int m;

public:

void getdata_m()

{

cout<<"enter the value of m:  "<<endl;

cin>>m;

}

};

class N

{

public: public:

};

int n;

void getdata_n()

{

cout<<"\nenter the value of n: "<<endl; cin>>n;

}

class mul: public M,public N

{

public:

int product;

void calculate()

{

product=m*n;

}

void show()

{

cout<<"product of m and n is: "<<product;

}

};

void main()

{

clrscr(); mul m1;

m1.getdata_n(); m1.getdata_m(); m1.calculate(); m1.show();

getch();

}

•

 Multilevel  inheritance

• The mechanism of deriving a class from derived class is known as multilevel  inheritance.

• A derived class with multilevel inheritance is declared as  follows:

![](Images/image01373.gif)

Fig. Multilevel inheritance

• A derived class with multlevel inheritance is declared as  follows:

![](Images/image01374.jpeg)

• It is not uncommon to drive a class from another derived class as shown in fig.  above.

• The class A serves as a base class for the derived class  B.

• Which inturn serves as a base class for the derived class  C.

• The class B is known as intermediate base class, since it provides a link for the inheritance between A and  C.

• The chain ABC is known as inheritance  path.

Example program:

//program for multilevel inheritance//

#include<iostream.h> #include<conio.h>

class student

{

protected:

int rollno; public:

void getno(); void  putno(void);

};

void student : : getno( )

{

cin>>rollno;

}

void student : : putno()

{

cout<<rollno;

}

class test :  public  student//1st level  derivation//

{

protected:

float mark1,mark2; public:

void getmark(); void putmark();

};

void test : : getmark()

{

cin>>mark1>>mark2;

}

void test : : putmark()

{

cout<<mark1<<mark2;

}

class result :  public test//2nd level  derivation

{

float  total;//private by default public:

void display()

};

void result : : display()

{

total = mark1 + mark2; putno();

putmark(); cout<<total;

}

void main()

{

result  r1;//object for derived class  result

r1.getno() r1.getmark();

r1.display();

}

 Explanation about the program

• In the above example we have a base class student and two derived classes test and  result.

• test is derived from the base class student and result is derived from the former derived class i.e. is from  test.

• So that test has all the traits of the base class and the derived  class.

• So that the object of the derived class is created i.e.  result.

• And all the member functions and the member data’s of the student and test class are accessed through the object of  result.

 Ambiguity resolution in  inheritance

• Occasionally, we may face a problem in using the multiple inheritance, when a function with the same name appears in more than one base  class.

• Consider the following two  classes:

class M

{

public:

void display()

{

cout<<"class M: "<<endl;

}

};

class N

{

public:

void display()

{

cout<<"class N: "<<endl;

}

};

• In the above example, both the classes are having the function  display().

• When we inherit these two classes, then which display() function is used by the derived class  ?

• We can solve this problem by defining a named instance within the derived class, using the class resolution operator with function as shown below:

class P:public M, public N

{

public:

void  display()//overrides display() of M and  N

{

M :: display();

}

};

• We can now use the derived class as  follows:

void main()

{

P p1;

p1.display();

}

• Ambiguity may also arise in single inheritance  applications.

• For example  , consider the following situation:

class A

{

public:

void display()

{

cout<<"class A: "<<endl;

}

};

class B : public B

{

public:

void display()

{

cout<<"class B: "<<endl;

}

};

• In this case, the function in the derived class overrides the inherited  function.

• And ,therefore, a simple call to display() by B class object will invoke function defined  in

B only.

• However, we may invoke the function defined in A by using the scope resolution operator to specify the class as shown  below:

void main()

{

B  b1;//derived class  object

b1.display();//invokes display() in B b1.A::display();//invokes display() in A b1.B::dipsplay();              //invokes display() in  B

}

 Hierarchical inheritance

• Hierarchical inheritance is the process of deriving two or more classes from only  one base  class.

• The representation of the hierarchical inheritance is shown in the following  Fig.

![](Images/image01375.jpeg)

Fig. Hierarchical inheritance

• The base class will include all the features that are common to the  subclasses.

• A subclass can be constructed by inheriting the properties of the base  class.

• A subclass can serve as a base class for the lower level classes and so  on.

The hierarchical inheritance is declared as follows:

Example program:

![](Images/image01376.jpeg) 

16

![](Images/image01377.jpeg)

/*Program for Hierarchical inheritance for the above shown fig.*/

#include<iostream.h> #include<conio.h>

class student

{

private:

int rollno; public:

void getdata_s()

{

cout<<"options the student have are: "<<endl;

}

};

class arts : public student

{

public:

void display_a()

{

cout<<"arts:  "<<endl;

}

};

class medical : public student

{

public:

void display_md()

{

cout<<"medical: "<<endl;

}

};

class engineering : public student

{

public:

void display_e()

{

cout<<"engineering: \n"<<endl;

cout<<"in engineering student can opt for any of the departments: "<<endl;

}

};

class mechanical: public engineering

{

public:

void display_m()

{

cout<<"engineering in mechanical: "<<endl;

}

};

class civil: public engineering

{

public:

void display_c()

{

cout<<"engineering in civil: "<<endl;

}

};

class electronics: public engineering

{

public:

void display_el()

{

cout<<"engineering in electronics: "<<endl;

}

};

void main()

{

clrscr();

arts a; medical md; civil c; mechanical m; electronics  el;

c.getdata_s(); a.display_a(); md.display_md(); c.display_e(); c.display_c(); m.display_m(); el.display_el();

getch();

}

Output:

options the student have are:

arts:

medical:

engineering:

in engineering student can opt for any of the departments: engineering in civil:

engineering in mechanical:

engineering in electronics:

 Hybrid  inheritance

• [Hybrid Inheritance](http://guides.wikinut.com/Inheritance-and-Its-types/6dfqqlfm/) is a method where one or more types of inheritance are  combined together.

![](Images/image01378.jpeg)

Fig. Hybrid (Multilevel, multiple) inheritance

 Virtual base class

• Consider a situation, when three kind’s of inheritance ,namely multilevel, multiple  and hierarchical inheritance are  involved.

• Then, the “child” will have two direct base classes “parent1” and “parent2” which  they themselves have a common base class grand  parent.

• The “child” inherits the traits of “grandparent” via two separate  paths.

• It can also inherit directly as shown by the ‘broken  line’.

• The “grandparent” is sometimes referred to as indirect base  class.

![](Images/image01379.jpeg)

Fig. Multipath inheritance

• Such inheritance by the “child” class may create some  problems.

• All the public and protected members of the “grandparent” class are inherited into  the “child” class twice; first via “parent1” class and then again via “parent2”  class.

• This means that the “child” class would have duplicate set of members inherited  from “grandparent”, which introduces ambiguity and should be  avoided.

• The duplication of inherited members due to these multiple paths can be avoided  by making the common base class as virtual base class, while declaring the direct or intermediate base classes  as shown  below:

class grandparent

{

….

….

};

class parent1 : virtual public grandparent

{

…….

…..

….

};

class parent2 : public virtual grandparent

{

…….

…..

….

};

class child : public parent1, public parent2

{

…….

.  ……// only one copy of grand parent will be  inherited

…….

};

• When a class is made a virtual base  class.

• C++ takes necessary care to see that only one copy of that class is inherited,  regardless of how many inheritance paths exist between the virtual base class and the derived class.

Note:-  The keywords virtual and public may be used in either order.

Example program

![](Images/image01380.jpeg)As virtual  base  classAs virtual base  class

Fig.Virtual base class

#include<iostream.h> #include<conio.h>

class employee

{

public:

char ename[ ];

void getname()

{

cout<<"Enter the emp name"; cin>>ename;

}

};

class grosssalary : virtual public employee

{

public:

float bp,hra,da,gross;

void getdetails()

{

cout<<"Enter the basicpay, hra, da"; cin>>bp>>hra>>da; gross=bp+hra+da; cout<<"gross"<<gross<<endl;

}

};

class taxdeduct : public virtual employee

{

public:

float tax;

void deduct()

{

cout<<"Enter the tax amount to be deducted: "; cin>>tax;

}

};

class netsalary : public salary,public taxcal

{

float net;

public:

void netpay()

{

net=gross-tax;

cout<<"Netsalary of the employee:  "<<ename<<"\t"<<net;

}

};

void main()

{

netsalary ob; clrscr();

ob.getname(); ob.getdetails(); ob.deduct();

ob.netpay();

getch();

}

Output:

Enter the emp name:  geetha

Enter the  basicpay,   hra,  da  : 1200040005000

Gross: 21000

Enter the tax amount to be deducted: 2000 Netsalary of the employee geetha: 19000

 Abstract  classes

*   An abstract class is one that is not used to create  objects.
*   An abstract class is designed only to act as a base class (to be inherited by  other classes).
*   In the previous example, the employee class is an abstract class, since it was  not used to create any  object.

 Virtual  Functions

• When we use the same function name in base and derived classes, the function in the base class is declared as virtual using keyword ‘virtual’ preceding its normal declaration.

• The member function that can be changed at runtime is called virtual  function.

• When is function is made virtual,C++ determines which function to use at run-time based on the type of object pointed to by the base pointer,rathre than the type of the pointer.

• Thus, making the base pointer to point to different objects,we can execute different versions of the virtual  functions.

• Syntax  for defining virtual function  is: class  classname

{

public:

. . . . .

virtual returntype functionname (arguments)

{

. . . .  .

. . . .  .

}

};

• The virtual function should be defined in the public section of a  class.

• When one function is made virtual and another one is normal, and compiler determines which function to create at runtime.

• In this we have to create a  ‘basepointer’.

• If the basepointer points to a base class object means it will execute the baseclass function.

• If the basepointer points to a derived class object means it will execute the derived class  function.

Example Program:

#include <iostream.h> #include<conio.h>

class Base

{

public:

void display()

{

cout<<"\ndisplay base";

}

virtual void show()

{

cout<<"\nshow base";

}

};

class Derived:public Base

{

public:

void display()

{

cout<<"\ndisplay Derived";

}

void show()

{

cout<<"\nshow Derived";

}

};

void main()

{

clrscr(); Base b;

Derived d; Base *bptr;

cout<<”\nbptr points to Base”; bptr=&b;

bptr->display();//Calls base class  display()

bptr->show();//Calls base class show()

cout<<”\nbptr points to Derived”; bptr=&d;

bptr->display();////Calls base class display() bptr->show();                            //Calls derived class  show()

getch();

}

Output:

bptr points to Base display base

show base

bptr points to Derived display base

show Derived

 Explanation about the program

*   The base pointer first holds the address of the base class object means it will run the base class member function display and show will be  executed.
*   Next the base pointer points to the derived class object, in this before executing the derived class function it will check whether the corresponding base class function is ‘virtual’ or not.
*   If it is not virtual then execute the base class function otherwise it will execute the derived class  function.

Rules for virtual function:

1. Virtual function must be a member of some  class.

2. They cannot be static  members.

3. They are accessed by using base  pointer.

4. A virtual function in a base class must be defined eventhough it may not be  used.

5. A  prototype  (or  declaration)  of  a  base  class  virtual  function  andthe derived class version must be  identical.

6. We cannot use the pointer of the derived class to access an object of the base  class.

 Member function  overridding

Base class and derived class have member functions with same name and arguments. If you create an object of derived class and write code to access that member function then, the member function in derived class is only invoked, i.e., the member function of derived class overrides the member function of base class. This feature in C++ programming is known as function  overriding.

Example program: Class base

{

Public:

Void print()

{

Cout<<”Print from base”;

}

};

Class derived:public base

{

Public:

Void print()

{

Cout<<”Print from derived”;

}

};

Void main()

{

Derived d;

d.print(); //invokes print() from derived d.print(); //invokes print() from derived

}

Output:

Print from derived Print from derived

 Using Constructors and destructors in  Inheritance Constructors in derived class

• Constructors can be used to initiative an object data members and allocating required resources such as  memory.

• In case of single inheritance, when both the derived and base class contain constructors,the base constructor is executed first and then the constructor in the derived class is  executed.

• In case of multiple inheritance,the base class constructors are executed in the order in which they appear in the declaration of the derived  class.

• In case of multilevel inheritance,the constructors will be executed in the order of inheritance.

• The constructors of virtual base classes are invoked before any non-virtual base classes.

• If there are multiple virtual base classes, they are invoked in the order in which they are  declared.

| Method of inheritance | Order of execution |
| Class A : public B | A(); base constructor |
| { | B(); derived constructor |
| }; |  |
| Class A : public B,public C | B(); base(first) |
| { | C(); base(second) |
| }; | A();derived |
| Class A : public B,virtual public C | C(); virtual base |
| { | B(); ordinary base |
| }; | A();derived |

Table.Order of execution of base class constructors

![](Images/image01366.jpeg)    Null constructors in derived class

 Single  inheritance Case  1:

No Constructor in the base class and derived class

*   When there are no constructors either in the base or derived classes, the compiler automatically creates objects of classes without any  error.

Example program:

Class A

{

public: void dis( )

{

cout<<”Hai Friends”;

}

};

Class B: public A

{

public:

void display( )

{

cout<<”Have a nice day”;

}

};

void main( )

{

}

Case 2:

B s;/*object for the derived  class*/ s.dis( );

s. display( );

Constructor only in the base class

#include <iostream.h> class A

{

public:

A (  )/*null constructor in base  class*/

{

cout<<” Have a nice day”;

}

};

class B: public A

{

public:

};

void main( )

{

B s;/*object for the derived  class*/

}

*   If the derived class object is created it will check the base class first and execute the corresponding default  constructor.

Case 3:

Constructor only in the derived class

#include <iostream.h> Class A

{

public:

};

Class B: public A

{

public:

A (  )/*null constructor in derived  class*/

{

cout<<”Have a nice day”;

}

};

void main( )

{

B  s;/*object for the derived  class*/

}

*   When the derived class object is created, it will check the base class first if there is no constructor in the base class, it will skip the base class & run the constructor in the derived  class.

Case 4:

Constructor in both base and derived class

#include <iostream.h> class A

{

public:

A (  )/*null constructor in base  class*/

{

cout<<”Have a nice day”;

}

};

class B: public A

{

public:

B (  )/*null constructor in derived class*/

{

cout<<”Welcome”;

}

};

void main( )

{

B  s;/*object for the derived  class*/

}

*   When the derived class object is created it will check the base class & execute the corresponding constructor and then it will execute the corresponding derived class constructor.

 Multiple  inheritance

Constructor in multiple inherited class

#include <iostream.h>

class  A/*base class1*/

{

public:

A  (  )/*null constructor in base  class1*/

{

cout<<”Have a nice day”;

}

};

class  B/*base class2*/

{

public:

B( )/*null constructor in derived base class2*/

{

cout<<”Welcome”;

}

};

class C: public A,  public B/*derived  class*/

{

public:

C  (  )/*null constructor in derived  class*/

{

cout<<”Good Morning”;

}

};

void main( )

{

C  s;/*object for the derived  class*/

}

Output:

Have a nice day Welcome

Good Morning

*   The constructor can be executed depending upon the order in which the classes inherited to desire a new class i.e., public A, public B, it will execute the corresponding class A constructor first and then class B constructor, derived  constructor.

 Multilevel inheritance Constructor in multilevel  inheritance

#include <iostream.h>

class A

{

public:

A (  )/*null constructor in base  class*/

{

cout<<”Have a nice day”;

}

};

class B: public A

{

public:

B( )/*null constructor in 1st derived class  */

{

cout<<”Welcome”;

}

};

class C:  public  B/*null constructor in 2nd derived class  */

{

public:

C ( )

{

}

};

cout<<”Good Morning”;

void main( )

{

![](Images/image01381.jpeg)C  s(  );/*object for the derived  class*/

}

Output:

Have a nice day Welcome

Good Morning

![](Images/image01366.jpeg)    Parameterised constructors in derived class

*   As long as no base class constructor takes any arguments,the derived class need not have a constructor  function.
*   However, if the base class contains a constructor with one or more parameters, then it is mandatory for the derived clas to have a constructor and pass the arguments to the base class  constructors.
*   Since the derived class takes the responsibility of supplying initial values to its base classes,we supply the initial values that are required by all the classes together,when a derived class object is declared.
*   C++ supports a special argument mechanism for such  situations:

*   The constructor of the derived class receives the entire list of values as its arguments and passes then on to the base constructors in the order in which they are declared in the derived  class.
*   The base constructors are called and executed before executing the statements in the body of the derived  constructor.

*   The general form  of defining a derived constructor  is:

*   The  header  line  of  derived-constructor  function  contains  two  parts  separated  by  a  colon

( : ).

*   The first part provides the declaration of the arguments that are passed to the derived constrcutor and the second part lists the function calls to the base  constructors.
*   base1(arglist1),base2(arglist2)             are function calls to the base  constructors

base1(),base2(),.....

*   And therefore  the  arglist1,arglist2,                          etc, represents the actual parameters that  are

passed to the base constructors.

*   Arglist1 through ArglistN are the argument declarations for base constructors  base1

through baseN.

*   ArglistD provides the parameters that are necessary to initialise the members of  the derived  class.

Example program

#include <iostream.h>

class alpha

{

int x; public:

alpha(  int  i)/* parameterised constructor in  base

class*/

};

{

x=i;

cout<<”alpha initialised”;

}

void  show_x()

{

cout<<”x”<<x;

}

class  beta

{

float y; public:

beta(  float  j)/* parameterised constructor in  base

class*/

{

y=j;

cout<<”beta initialised”;

}

void  show_y()

{

cout<<”y”<<y;

}

};

class gamma: public beta,public aplha

{

int m,n; public:

gamma(int a,float b,int c,int d): alpha(a),beta(b)

{

m=c; n=d;

cout<<”gamma initialised”;

}

void show_mn()

{

cout<<”m”<<m<<”\n”<<”n”<<n;

}

};

void main( )

{

gamma g(5,3.4,8,9); g.show_x();

g.show_y();

g.show_mn();

}

Output:

beta initialised alpha initialised gamma initialised

x=5 y=3.4

m=8 n=9

Note:-

*   Beta will be initialise dfirst,although it appears second in the derived  constructor.
*   This is because it has been declared first in the derived class header  line.
*   Also,note that alpha(a) and beta(b) are function  calls.
*   Therefore,parameters should not include  types.

 I/O  Stream

 File  I/O

 Exception  Handling

 Templates

UNIT-IV

 STL – Library Organization and Containers – Standard Containers Overview of Standard Algorithms-Iterators and  Allocators.

 I/O  STREAM

C/C++ IO are based on  streams, which are sequence of bytes flowing in and out of the  programs  (just  like  water  and  oil  flowing  through  a  pipe).  In  input  operations,  data bytes  flow  from  an  input  source  (such  as  keyboard,  file,  network  or  another  program) into the program. In output  operations,  data  bytes  flow from  the  program  to an  output sink  (such as console, file, network or another program). Streams acts  as an intermediaries between the programs and the actual IO devices, in such the way that  frees  the  programmers  from  handling  the  actual  devices,  so  as  to  archive  device independent IO  operations.

![](Images/image01382.jpeg)

C++  provides  both  the  formatted  and  unformatted  IO  functions.  In  formatted  or  high- level  IO,  bytes  are  grouped  and  converted  to  types  such  as  int,  double,  string  or  user- defined types. In unformatted or low-level IO, bytes are treated as raw bytes and unconverted.  Formatted  IO  operations  are  supported  via  overloading  the  stream

insertion (<<) and stream extraction (>>) operators, which presents a consistent public IO interface.

To perform input and output, a C++ program:

1. Construct a stream  object.

2. Connect (Associate) the stream object to an actual IO device (e.g., keyboard, console, file, network, another  program).

3. Perform  input/output  operations  on  the  stream,  via  the  functions  defined  in  the stream's pubic interface in a device independent manner. Some functions convert the data between the external format and internal format (formatted IO);  while  other  does  not  (unformatted  or  binary  IO).

4. Disconnect  (Dissociate)  the  stream  to  the  actual  IO  device  (e.g.,  close  the  file).

5. Free the stream  object.

iostream library contains

<iostream.h>: Contains cin, cout, cerr, and clog objects

<iomanip.h>: Contains  parameterized stream manipulators

<fstream.h>: Contains information important to user-controlled file processing operations

ios base class

istream and ostream inherit from ios iostream  inherits  from  istream  and  ostream.

<< (left-shift operator)

– Overloaded as  stream insertion  operator

>> (right-shift operator)

– Overloaded as  stream extraction  operator

– Both operators used with cin, cout, cerr, clog, and with user-defined stream  objects

istream: input streams

cin >> someVariable;

• cin knows what type of data is to be assigned to someVariable (based on the type of  someVariable).

ostream: output streams

– cout <<  someVariable;

• cout  knows  the  type  of  data  to  output

– cerr <<  someString;

• Unbuffered - prints someString  immediately.

– clog <<  someString;

• Buffered - prints someString as soon as output buffer is full or flushed

ostream: performs formatted and unformatted  output

– Uses  put  for  characters  and  write  for  unformatted  characters

– Output  of  numbers  in  decimal,  octal  and  hexadecimal

– Varying precision for floating  points

– Formatted text  outputs

![](Images/image01383.jpeg)cin.get():  inputs  a  character  from  stream  (even  white  spaces)  and  returns  it  cin.get( c ):  inputs a character from stream and stores it in  c Unformatted Input/Output  Functions

put(),  get()  and  getline()

The  ostream's member function  put()  can be used to put out a  char.  put()  returns the invoking  ostream  reference, and thus, can be cascaded. For example,

// ostream class

ostream & put (char c); // put char c to ostream

// Examples cout.put('A');

cout.put('A').put('p').put('p').put('\n'); cout.put(65);

// istream class

// Single character input int get ();

// Get a char

store in c and return the invoking istream reference

// C-string input

istream & get (char and return as int. It returns EOF at end-of-file istream & get (char & c);

// Get a char * cstr, streamsize n, char delim = '\n');

// Get n-1 chars or until delimiter and store in C-string array cstr.

// Append null char to terminate C-string

// Keep the delim char in the input stream.

istream & getline (char * cstr, streamsize n, char delim = '\n');

// Same as get(), but extract and discard delim char from the

// input stream.

Example:

int inChar;

while ((inChar = cin.get()) != EOF) { // Read till End-of-file cout.put(inchar);

}

read(), write() and gcount()

// istream class

istream & read (char * buf, streamsize n);

// Read n characters from istream and keep in char array buf.

// Unlike get()/getline(), it does not append null char at the end of input.

// It is used for binary input, instead of C-string. streamsize gcount() const;

// Return the number of character extracted by the last unformatted input operation

// get(), getline(), ignore() or read().

// ostream class

ostream & write (const char * buf, streamsize n)

// Write n character from char array.

Formatted console IO functions

C++  provides  various  formatted  console  I/O  functions  for  formatting  the  output.  They are of three  types.

(1)  ios class function and  flags

(2)  Manipulators

(3)  User-defined output  functions

Member functions and flags

Output  streams  (class  ostream  and  related  classes)  have  some  useful  member functions  for  controlling  output  formatting.  Note  that  these  can  be  used  not  only

with  cout,  but  with  other  types  of  output  streams.  (We'll  learn  about  file  output streams  soon).

setf()  --  the  "set  flags"  function.  Takes  as  a  parameter  the  flag  to  be  turned  "on". Some  of  the  flags  that  can  be  turned  on  or  off  are:

ios::fixed  --  to  specify  that  floating-point  numbers  will  be  printed  in  fixed notation.

ios::scientific  -- to specify that floating-point numbers will be printed in scientific (exponential) notation.

ios::showpoint  -- specifies that the decimal point will always be printed for floating point types (even if the value is a whole number, like 4.0

ios::right  --  right-justifies  an  output  item  in  a  field,  if  a  field  width  is specified

ios::left  -- left-justifies an output item in a field, if a field width is specified

unsetf()  -- the "unset flags" function. Call this to turn  off  one of the flags

precision()  --  sets  the  precision  for  floating-point  values  to  a  specific  number  of significant  digits  after  the  decimal  point.  Takes  that  number  as  a  parameter

width()  -- used to specify the "field width" for the  next  item that is output. Number  of  character  positions  is  specified  as  a  parameter.  Left  and  right  justify flags  will  apply  when  this  function  is  used  to  specify  field  widths.  Extra  "space"  in the  field  will  be  filled  with  a  fill  character,  which  is  set  to  a  space  by  default:

int x = 1234; cout.setf(ios::right); cout.width(10); cout << "Hello"; cout.width(15); cout <<  x;

// output of the above  is:

//Hello1234

fill()  --  used  to  specify  the  fill  character  to  be  used  to  pad  out  extra  space  in  a field  (when  using  width()).  Takes  the  character  as  a  parameter.

int x = 1234; cout.setf(ios::right);

cout.fill('.'); // change the fill character cout.width(10);// set field width to 10 cout  <<  x;              // print  x

// output of the above  is:

// ......1234

Stream Manipulators

A  Stream  manipulator  is  a  symbol  or  function  that  is  used  by  placing  it  on  the  right side  of  the  insertion  operator  <<  .

A plain manipulator is just a symbol, like a variable:

cout  <<  endl;// endl is a stream  manipulator

A  parameterized stream manipulator  looks like a function call -- it has one or more parameters:

cout  <<  setw(10);// setw() is a parameterized  manipulator

To  use  parameterized  stream  manipulators,  you  need  to  include the <iomanip>  library

#include  <iomanip>

Many  of  the  stream  manipulators  are  just  alternate  ways  of  doing  tasks  performed by member functions. A nice benefit is that cascading can be used, intermixing manipulators  and  other  output  statements  that  use  the  insertion  operator

cout << setw(10) << "Hello" << endl;

setprecision()  is a parameterized stream manipulator that performs the same task as the member function  precision()

cout.precision(2);// sets decimal precision to 2 significant digits cout << setprecision(2); // does the same  thing!

setw()  is  a  parameterized  stream  manipulator  that  performs  the  same  task  as  the member function  width()

cout.width(10);// sets field width to 10 for next output cout  <<  setw(10);                            // does the same  thing!

setfill()  is a parameterized stream manipulator that performs the same task as the member function fill()

cout.fill('*');// sets fill character to  '*'

cout  <<  setfill('*');// does the same  thing!

setiosflags()  is a parameterized stream manipulator that performs the same task as the member function setf()

cout.setf(ios::left);// sets left justification flag cout  <<  setiosflags(ios::left);              // does the same  thing!

There  are  also  some  newer  stream  manipulators  that  correspond  to  some  of  the formatting flags. For  example:

cout.setf(ios::left);// sets left justification for  cout

cout  <<  left;//  also  sets  left  justification  for  cout

 FILE  I/O

![](Images/image01384.jpeg)

To perform file processing in C++, the header files  <iostream.h>  and  <fstream.h> must be included.

<fstream.> includes <ifstream> and <ofstream>

File Open Modes

Where filename is a string representing the name of the file to be opened, and  mode  is  an  optional  parameter  with  a  combination  of  the  following  flags:

| ios::in | Open for input operations. |
| ios::out | Open for output operations. |
| ios::bin ary | Open in binary mode. |
| ios::ate | Set the initial position at the end of the file.If this flag is not set, the initial position is the beginning of the file. |
| ios::app | All  output  operations  are  performed  at  the  end  of  the  file,  appending  the content  to  the  current  content  of  the  file. |
| ios::trun c | If  the  file  is  opened  for  output  operations  and  it  already  existed,  its  previous content  is  deleted  and  replaced  by  the  new  one. |

ios:nocreate  -  if  the  file  does  NOT  exists,  the  open  operation  fails ios:noreplace  -  if  the  file  exists,  the  open  operation  fails

Each  of  the  open  member  functions  of  classes  ofstream,  ifstream  and  fstream  has  a default  mode  that  is  used  if  the  file  is  opened  without  a  second  argument:

| class | default mode parameter |
| ofstream | ios::out |
| ifstream | ios::in |
| fstream | ios::in &#124; ios::out |

File  Close                                                                                                

When  we  are  finished  with  our  input  and  output  operations  on  a  file  we  shall  close  it so  that  the  operating  system  is  notified  and  its  resources  become  available  again.  For that,  we  call  the  stream's  member  function  close.  This  member  function  takes  flushes the  associated  buffers  and  closes  the  file:

![](Images/image01385.jpeg)

Once this member function is called, the stream object can be re-used to open another file, and the file is available again to be opened by other processes.

![](Images/image01386.gif)

Example

A file can be opened either by using the constructor or by creating object for the corresponding  ifstream  or  ofstream  classes.  The  following  example  is  opening  the  file using  constructor:

Example for Writing to a file:

// writing on a text file #include <iostream.h> #include <fstream.h>

int main () {

ofstream myfile ("example.txt"); myfile << "This is a line.\n"; myfile  <<  "This  is  another  line.\n"; myfile.close();

else  cout  <<  "Unable  to  open  file"; return 0;  }

Output:

[file example.txt] This is a line.

This is another line.

Following is the C++ program which opens a file in reading and writing mode by creating objects. After writing information inputted by the user to a file named afile.dat,  the  program  reads  information  from  the  file  and  outputs  it  onto  the  screen:

![](Images/image01387.jpeg)#include <fstream.h> #include <iostream.h>

void main ()

{

char line[100];

// open a file in write mode. ofstream fout; fout.open("afile.txt", ios:: out);

cout << "Writing to the file" << endl; cout << "Enter your name: "; cin.getline(line, 100);

// write inputted data into the file. fout << line << endl;

cout << "Enter your age: "; cin >> line;

// again write inputted data into the file. fout << line << endl;

// close the opened file. fout.close();

// open a file in read mode. ifstream infile; infile.open("afile.txt", ios:: in);

cout << "Reading from the file" << endl; infile >> line;

// write the data at the screen. cout << line << endl;

// again read the data from the file and display it. infile >>line;

cout << line << endl;

infile.close();// close the opened file. return 0;

}

When the above code is compiled and executed, it produces the following sample input and output:

![](Images/image01388.jpeg)

In the above program the object “fout” is created for the ofstream class. It opens a

text file named “afile.txt”. It gets input like name and age from the user using getline()  function  and  cin  object  with  extraction(>>)  operator.  Then  it  writes  them  on the  “afile.txt”  using  the  fout  object.  Then  the  file  is  closed.

Again the same file “afile.txt” is opened for reading purpose. This the object “infile” is created for the ifstream class. It opens the “afile.txt” file for reading. Then its content are extracted using the infile object and (>>) extraction operator. They are then displayed on the screen using cout.

The above program clearly explains how a file can be opened for writing as well as reading.

File position pointer

<istream> and <ostream> classes provide member functions for repositioning the

file  pointer  (the  byte  number  of  the  next  byte  in  the  file  to  be  read  or  to  be  written.) These member functions  are:

seekg  (seek get) for istream  class

seekp  (seek put) for ostream  class

Member functions  tellg  and  tellp  are provided to return the current locations of the get and put pointers, respectively.

 ERROR (Exception)  HANDLING

The exception refers to unexpected condition in a program. The unexpected conditions  could  be  faults,  causing  an  error  which  in  turn  causes  the  program  to  fail. The  error  handling  mechanism  of  C++  is  generally  referred  to  as  exception  handling.  Types of  Exceptions

1. Synchronous  Exception

2. Asynchronous  Exception

*   Synchronous Exception

The  exception  which  occurs  during  the  program  execution,  due  to  some fault in the input data or technique that is not suitable to handle the current class of data, with in the program are known as synchronous exception.

Example:  out of range, divide by zero, overflow, underflow

*   Asynchronous  Exception

The  errors  that  are  caused  by  events  beyond  the  control  of  the  program are called asynchronous  exceptions.

Example: disk failure

Exception handling Mechanism:

The  purpose  of  the  exception  handling  mechanism  is  to  provide  means  to  detect and report an “exceptional circumstance” so that appropriate action a\can be taken.

The exception handling mechanism consists of the following task or operations:

1. Find  the  problem  (  hit  the  exception)

2. Inform  that  an  error  has  occurred  (throw  the  exception)

3. Receive  the  error  information  (  catch  the  exceptions)

4. Take corrective actions( handle the  exceptions)

Error handling basically consists of two segments;

*   One  to  detect  and  to  thro  exceptions
*   Other  to  catch  the  exceptions  and  to  take  appropriate  actions.

Exception Handling Model:

The  exception  handling  mechanism  uses  three  blocks  try,  throw,  catch.  The relationship  of  those  three  exception  handling  model  shown  below

*   The keyword try is used to preface a block of statements (surrounded by braces)  which  may  generate  exceptions.  This  block  of  statements  known  as  try bock.
*   When  an  exception  is  detected,  it  is  thrown  using  a  throw  statement  in  the  try block.
*   A  catch  block  defined  by  the  keyword  catch  catches  the  exception  thrown  by the  throw  statement  in  the  try  block,  and  handle  it  appropriately.
*   General  format:

…………

…………

try

{

……….// block of statements which detects  and

throw exception// throws an  exception

……….

……….

}

catch ( type arg)

{

}

……..

……..

………// block of statements that handles the  exception

………

………

*   When  the  try  block  throws  an  exception,  the  program  control  leaves  the  try block  and  enters  the  catch  statement  of  the  catch  block.
*   Exceptions  are  objects  or  variables  used  to  transmit  information  about  a problem.
*   If  the  type  of  object  thrown  matches  the  arg  type  in  the  catch  statement,  then catch  block  is  executed  for  handling  the  exception.
*   If  they  do  not  match,  the  program  is  aborted  with  the  help  of  the  abort()

function which is invoked automatically.

*   The  catch  block  may  have  more  than  one  catch  statements,  each corresponding  to  a  particular  type  of  exception.
*   For  example  if  the  throw  block  is  likely  to  throw  two  exception,  the  catch  block will have two catch statements one for each type of exception. Each catch statement is called is exception  handler.
*   When  no  exception  is  detected  and  thrown,  the  control  goes  to  the  statement immediately  after  the  catch  block.  That  is  catch  block  is  skipped.

Example: divide by zero #include<iostream.h>

void main( )

{

int x, y, z;

cout<<”enter  the  values  of  x,  y,  z”; cin>>x>>y>>z;

try

{

if(x= =y)

throw y;

else

}

int d= z / ( x- y);

cout<<”the result of z/ (x-y )is:”<< d;

catch( int y)

{

cout<<”exception caught x-y is “<< x-y ;

}

}

RUN 1:

enter  the  values  of  x  ,  y,  z 50 30  20

the result of z/ (x-y ) is: 1

RUN 2:

Enter  the  values  of  x,  y,  z 30 30  20

exception caught x-y is :  0

Using  function  that  generate  exceptions: #include<iostream.h>

void divide ( int x, int y, int z)

{

if(x= =y)

}

cout<<”we are inside the function”;

throw (x-y);

else

int d= z / ( x- y);

cout<<”the result of z/ (x-y )is:”<< d;

void main( )

{

try

{

}

cout<<” we are inside the try block”; divide( 10,  20,  30);//  invoke  divide  ()

divide( 10,  10,  20);// invoke divide  ()

catch(  int  i)// catches the  exception

{

cout<<”exception caught x-y is : “<<i;

}

}

RUN:

we  are  inside  the  try  block we  are  inside  the  function the  result  of  z/  (x-y  )is:  -3 we  are  inside  the  function exception  caught  x-y  is:  0

Multiple catches with object:

*   To  throw  an  exception  with  an  object  it  needs  to  define  an  abstract  class.
*   Abstract  class  is  nothing  but  a  class  with  empty  data  members.
*   Class  name  is  called  as  nameless  object  which  is  used  to  throw  the  exceptions

Example:

#include<iostream.h> class positive { }; class negative { }; class zero {  };

void greater ( int num)

{

if( num >0)

else

throw positive( );

if (num < 0)

throw negative( );

else

}

throw zero( );

void main( )

{

int num;

cout<<”enter any  number”; cin>>num;

try

{

greater ( num);

}

catch( positive)

{

cout<<”+ve exception”;

}

catch(negative)

{

cout<<”-ve exception”;

}

catch (zero)

{

cout<<”0 exception”;

}

}

 Templates

A  significant  feature  of  OOP  is  re-usability  of  code,  which  eliminates  redundant coding.  Templates  support  generic  programming,  which  allows  to  develop reusable  software  components  such  as  functions,  classes,  etc.,  supporting different  data  types  in  a  single  framework.

Types of templates

There are two kinds of  templates:

*   Function  templates
*   Class  templates.

FUNCTION TEMPLATES

A function template defines how a group of functions can be generated.

Function template instantiation

A  function  template  by  itself  is  not  a  type,  or  a  function,  or  any  other  entity.  No  code is generated from a source file that contains only template definitions. In order for any code to appear, a template must be instantiated: the template arguments must be  determined  so  that  the  compiler  can  generate  an  actual  function  (or  class,  from  a class  template).

Explicit instantiation

An explicit instantiation definition forces instantiation of the function or member function they refer to. It may appear in the program anywhere after the template definition, and for a given argument-list, is only allowed to appear once in the program.

Implicit instantiation

When  code  refers  to  a  function  in  context  that  requires  the  function  definition  to  exist, and this particular function has not been explicitly instantiated, implicit instantiation occurs.

Syntax of function template

*   A  function  template  is  prefixed  with  the  keyword  template  and  a  list  of template type  arguments.
*   These template type arguments are called  generic data types, since their exact  representation  (memory  representation  and  data  representation)  is  not known  in  the  declaration  of  function  template.
*   It  is  known  only  at  the  point  of  a  call  to  a  function  template.

![](Images/image01389.jpeg)

Fig. syntax of function template

Example

#include<iostream.h> #include<conio.h> template <class T> void swap(T &x, T &y)

{

T z; z=x; x=y; y=z;

}

void main()

{

clrscr();

int a,b;float c,d; cout<<"\nenter 2 integers:"; cin>>a>>b;

cout<<"\nBefore swapping the values are "<<a<<"\t"<<b; swap(a,b);

cout<<"\nafter swapping the values are "<<a<<"\t"<<b; cout<<"\nenter 2 float value:";

cin>>c>>d;

cout<<"\nBefore swapping the values are "<<c<<"\t"<<d; swap(c,d);

cout<<"\nafter swapping the values are "<<c<<"\t"<<d; getch();

}

CLASS TEMPLATES

The relationship between a class template and an individual class is like the relationship  between  a  class  and  an  individual  object.  An  individual  class  defines  how a  group  of  objects  can  be  constructed,  while  a  class  template  defines  how  a  group  of classes can be  generated.

Note the distinction between the terms class template and template class:

Class template

is  a  template  used  to  generate  template  classes.  You  cannot  declare  an  object of a class  template.

Template class

is an instance of a class template.

A  template  definition  is  identical  to  any  valid  class  definition  that  the  template  might generate, except for the  following:

The class template definition is preceded by

 template< template-parameter-list  >

Objects  and  function  members  of  individual  template  classes  can  be  accessed  by  any of  the  techniques  used  to  access  ordinary  class  member  objects  and  functions.

![](Images/image01390.jpeg)Syntax of class template

![](Images/image01391.jpeg)

Example:

![](Images/image01392.jpeg)#include<iostream.h>

#include<conio.h> template <class  T> class  pair{

T a,b; public:

pair(T, T);

T getmax();

};

template <class T> pair<T>:: pair(T x, T y)

{

a=x; b=y;

}

template <class T> T pair<T>::  getmax()

{

T z; z=(a>b)?a:b; return z;

}

void main()

{

clrscr();

int p,q; float r,s; cout<<"\nEnter 2 integers:"; cin>>p>>q;

pair<int> ob1(p,q);

cout<<"\nThe  biggest  number  is  "<<ob1.getmax(); cout<<"\nEnter 2 float  values:";

cin>>r>>s; pair<float> ob2(r,s);

cout<<"\nThe biggest number is "<<ob2.getmax(); getch();

}

Advantages  to the use of templates

*   Templates  support  generic  programming,  which  allows  developing  reusable software components such as functions, classes, etc., supporting different data types in a single  framework.
*   Templates perform appropriate operations depending on the data type of the parameters passed to  them.
*   Templates are very useful when implementing generic constructs like vectors,  stacks,  lists,  queues  which  can  be  used  with  any  arbitrary  type.
*   Templates require type-checking at compile-time. Hence, the compiler  can determine at compile-time whether or not the type associated with a template definition can perform all of the functions required by that template  definition.
*   By  design,  templates  can  be  utilized  in  very  complex  problem  spaces.

Fundamental drawbacks to the use of templates:

*   Historically, some compilers exhibited poor support for templates. So, the use  of  templates  could  decrease  code  portability.
*   Many compilers lack clear instructions when they detect a template definition error. This can increase the effort of developing templates, and has prompted the development of Concepts for possible inclusion in a future C++  standard.
*   Since the compiler generates additional code for each template type, indiscriminate use of templates can lead to code bloat, resulting in larger executables.
*   Because a template by its nature exposes its implementation, injudicious use  in  large  systems  can  lead  to  longer  build  times.
*   It can be difficult to debug code that is developed using templates. Since the compiler replaces the templates, it becomes difficult for the debugger to locate the code at  runtime.
*   Templates of Templates (nesting) are not supported by all compilers, or might have a max nesting  level.
*   Templates are in the headers, which require a complete rebuild of all project pieces when changes are  made.
*   No  information  hiding.  All  code  is  exposed  in  the  header  file.  No  one  library can solely contain the  code.

 STANDARD TEMPLATE  LIBRARY:

The standard template library (STL) contains

*   Containers
*   Algorithms
*   Iterators

![](Images/image01393.jpeg)

A  container  is a way that stored data is organized in memory, for example an array of elements.

Algorithms  in the STL are procedures that are applied to containers to process their data, for example search for an element in an array, or sort an array.

Iterators  are a generalization of the concept of pointers, they point to  elements in a container, for example you can increment an iterator to point to the next element in an  array.

*   Iterators  are  pointer-like  entities  that  are  used  toaccess individual elements in a  container.
*   Often they are used to move sequentially from element to element, a process called  iterating  through a  container.
*   The member functions begin() and end() return an iterator to the first  and past  the  last  element  of  a  container

Container:

A container is a way to store data, either built-in data types like int and float, or class objects

The STL provides several basic kinds of containers

<vector> : one-dimensional array

<list> : double linked list

<deque> : double-ended queue

<queue> : queue

<stack> : stack

<set> : set

<map> : associative array

i) Sequence  Containers

A sequence container stores a set of elements in sequence, in other words  each  element  (except)  for  the  first  and  last  one)  is  preceded  by  one specific element and followed by another, <vector>, <list> and <deque> are sequential  containers

ii) Associative  Containers

An associative container is non-sequential but uses a  key  to access elements. The keys, typically a number or a string, are used by the container  to  arrange  the  stored  elements  in  a  specific  order,  for  example  in a  dictionary  the  entries  are  ordered  alphabetically.

*   A  <set>  stores  a  number  of  items  which  contain  keys

The keys are the attributes used to order the items, for example a set might store objects of the class Person which are ordered alphabetically using their name

*   A <map> stores pairs of objects: a key object  and

An associated value object. A <map> is somehow similar to an array except instead of accessing its elements with index numbers, you access them with indices of an arbitrary type.

iii) Adaptor  Containers

Container adapters are just special containers that use the general framework  of  the  containers,  iterators,  and  algorithms  provided  by  the  STL.

![](Images/image01394.jpeg)

Algorithms:

A range is any sequence of objects that can be accessed through iterators or pointers, such as an array or an instance of some of the [STL containers](http://www.cplusplus.com/stl). Notice though, that algorithms operate through iterators directly on the values, not affecting in any way the structure of any possible container (it never affects the size or storage allocation of the container). The types of algorithms  are

I.  Non-mutating  Algorithm Some of the methods are 1.count()

2.  equal()

3.  find() 4.find_end() 5.find_if() 6.search()

II. Mutating Algorithm Some of the methods  are 1.copy()

2.fill() 3.generate() 4.remove() 5.replace() 6.reverse() 7.unique()

III. Sorting  algorithm

Some of the methods are 1.binary_search() 2.equal_range() 3.merge()

4.sort() 5.partial_sort() 6.Partition()

IV.  Set algorithms 1.include() 2.set_difference() 3.set_intersection() 4.set_union()

V.  Relational alogorithm Some of the methods  are 1.equal()

2.max() 3.max_element() 4.min() 5.min_element() 6.mismatch()

Let us the example of using vector template for showing the working of Containers, Iterators and Algorithms.

![](Images/image01395.jpeg)

#include <vector> #include <iostream>

vector<int>  v(3);  //  create  a  vector  of  ints  of  size  3 v[0]=23;

v[1]=12;

v[2]=9;// vector  full

v.push_back(17);// put a new value at the end of  array

for (int i=0;  i<v.size();  i++)// member function size() of vector cout << v[i] <<  ”  ”;              // random access to i-th  element

![](Images/image01396.gif)cout << endl;

#include <vector> #include <algorithm> #include <iostream> int key;

int  arr[]  =  {  12,  3,  17,  8,  34,  56,  9  };  //  standard  C  array vector<int>  v(arr,  arr+7);  //  initialize  vector  with  C  array vector<int>::iterator  iter;

cout << ”enter value :”; cin >> key;

iter=find(v.begin(),v.end(),key); // finds integer key in v if (iter != v.end()) // found the element

cout  <<  ”Element  ”  <<  key  <<  ”  found”  <<  endl; else

cout << ”Element ” << key << ” not in vector v” << endl;

this Algorithm find() is for finding whether a number is present or not inside a given vector.

Allocators

Allocators are classes that define memory models to be used by some parts of the Standard Library, and most specifically, by [STL containers](http://www.cplusplus.com/stl).

It provides an interface for the STL containers.

UNIT-V

 Development Process ,Management

 Object  Identification

 Object Oriented Design  Fundamentals

 Components

 Case  Studies.

 DEVELOPMENT  PROCESSES

Waterfall model is the earliest SDLC approach that was used for software development .

The waterfall Model illustrates the software development process in a linear sequential flow; hence it is also referred to as a linear-sequential life cycle model. This means that any phase in the development process begins only if the previous phase is complete. In waterfall model phases do not overlap.

WATERFALL MODEL DESIGN

Waterfall approach was the first SDLC Model to be used widely in Software Engineering to ensure success of the project. In "The Waterfall" approach, the whole process of software development is divided into separate phases. In Waterfall model, typically, the outcome of one phase acts as the input for the next phase  sequentially.

Following is a diagrammatic representation of different phases of waterfall model.

![](Images/image01397.jpeg)

The sequential phases in Waterfall model are:

*   Requirement Gathering and analysis: All possible requirements of the system to be developed are captured in this phase and documented in a requirement specification  doc.
*   System Design: The requirement specifications from first phase are studied in this phase and system design is prepared. System Design helps in specifying hardware and system requirements and also helps in defining overall system  architecture.
*   Implementation: With inputs from system design, the system is first developed in small programs called units, which are integrated in the next phase. Each unit is developed and tested for its functionality which is referred to as Unit  Testing.
*   Integration and Testing: All the units developed in the implementation phase are integrated into a system after testing of each unit. Post integration the entire system is tested for any faults and  failures.
*   Deployment of system: Once the functional and non functional testing is done, the product is deployed in the customer environment or released into the market.
*   Maintenance: There are some issues which come up in the client environment. To fix those issues patches are released. Also to enhance the product some better versions are released. Maintenance is done to deliver these changes in the customer  environment.

All these phases are cascaded to each other in which progress is seen as flowing steadily downwards (like a waterfall) through the phases. The next phase is started only after the defined set of goals are achieved for previous phase and it is signed off, so the name "Waterfall Model". In this model phases do not overlap.

WATERFALL MODEL APPLICATION

Every software developed is different and requires a suitable SDLC approach to be followed based on the internal and external factors. Some situations where the use of Waterfall model is most appropriate are:

*   Requirements are very well documented, clear and  fixed.

*   Product definition is  stable.

*   Technology is understood and is not  dynamic.

*   There are no ambiguous  requirements.

*   Ample resources with required expertise are available to support the  product.

*   The project is  short.

WATERFALL MODEL PROS & CONS

ADVANTAGE

The advantage of waterfall development is that it allows for departmentalization and control. A schedule can be set with deadlines for each stage of development and a product can proceed through the development process model phases one by one.

Development moves from concept, through design, implementation, testing, installation, troubleshooting, and ends up at operation and maintenance. Each phase of development proceeds in strict  order.

DISADVANTAGE

The disadvantage of waterfall development is that it does not allow for much reflection or revision. Once an application is in the testing stage, it is very difficult to go back and change something that was not well- documented or thought upon in the concept stage.

The following table lists out the pros and cons of Waterfall model:

| Pros | Cons |
|  
*   Simple and easy to understand and use

*   Easy to manage due to the rigidity of the model . each phase has specific deliverables and a review  process.

*   Phases are processed and completed one at a time.

*   Works well for smaller projects where requirements are very well  understood.

*   Clearly defined stages.

*   Well understood milestones.

*   Easy to arrange tasks.

*   Process and results are well documented.

 |  
*   No working software is produced until late during the life cycle.

*   High amounts of risk and  uncertainty.

*   Not a good model for complex and object-oriented projects.

*   Poor model for long and ongoing  projects.

*   Not suitable for the projects where requirements are at a moderate to high risk of changing. So risk and uncertainty is high with this process  model.

*   It is difficult to measure progress within  stages.

*   Cannot accommodate changing  requirements.

*   No working software is produced until late in the life cycle.

*   Adjusting scope during the life cycle can end a  project.

*   Integration is done as a "big-bang. at the very end, which doesn't allow identifying any technological or business bottleneck or challenges  early.

 |

FOUNTAIN FLOW MODEL

Anthony Aleong, Glen Mitchell, Kareem Shaw

The waterfall model is well understood, but it's not as useful as it once was. In a 1991Information Center Quarterly article, Larry Runge says that SDLC "works very well when we are automating the activities of clerks and accountants. It doesn't work nearly as well, if at all, when building systems for knowledge workers -- people at help desks, experts trying to solve problems, or executives trying to lead their company into the Fortune 100."

Another problem is that the waterfall model assumes that the only role for users is in specifying requirements, and that all requirements can be specified in advance. Unfortunately, requirements grow and change throughout the process and beyond, calling for considerable feedback and iterative consultation. Thus many other SDLC models have been  developed.

The fountain model recognizes that although some activities can't start before others --such as you need a design before you can start coding -- here's a considerable overlap of activities throughout the development cycle.

FOUNTAIN MODEL

*   Support Incremental  Development
*   Recognizes that some activities can’t stand before others, yet there’s  a considerable overlap of activities throughout the development  cycle

*   Implies that you do some analysis, then some design, then some  implementation
*   Parallelism among various phases and iteration within  phases
*   Development of an object-oriented system that more likely to lead us to focus  on sections of the whole known as clusters or subsystems

*   Subsystems are collections of classes, which work closely  together
*   Supports human learning and is recommended for most  projects

Object-Oriented Life Cycle Notation (Fountain Model)

Any graphical representation of the object-oriented version of the overall software development life cycle must take into account the high degree of overlap and iteration implicit. In a pure object-oriented approach to software development, the “waterfall” model is too restrictive an approach and may be replaced by the highly-iterative “fountain” model of Figure 1\. This model incorporates reuse and domain analysis/design.

![](Images/image01398.gif)

Figure 1\. Fountain model for the object-oriented software life cycle.

Merging and overlap of activities are represented by the degree of overlap of the circle symbols. The decreased need for maintenance in an object-oriented system is symbolized by the smaller activity circle.

In a fountain, water rises up the middle and falls back, either to the ‘pool’ below or is re-entrained at an intermediate level. Just so in an object-oriented software development where the general flow from analysis through design to implementation is overlain with iterative cycles across two (or all three) of these broad “phases” of analysis, design and implementation, the ‘pool’ representing the ‘software pool’ or ‘repository’ of classes.

The picture, Figure 1, outlines the general characteristics of the systems level perception of an object-oriented development. There is a high degree of merging in the analysis, design, implementation and unit testing phases.

Characteristics

First, the fountain model provides a diagrammatic version of the stages present in an object-oriented software life cycle and a clearer representation of the iteration and overlap made possible by object-oriented technology. Second, since the foundation of a successful software project is its requirements analysis and specification, this stage has been placed at the base of the diagram. The life cycle thus grows upward to a pinnacle of software use, falling only in terms of necessary maintenance. This effectively reverts the stage of the cycle to a lower level. Application of this model to specific environments may lead to software life cycles such as prototyping: a development environment for which object-oriented programming languages are well  suited.

The system can be viewed not only in terms of the systems life cycle, as presented in Figure 1, but also in terms of synergistic amalgamation of a (usually large) number of autonomous classes. Modifications can more easily be made interactively between class development and systems specification so there is no longer a need to freeze the overall systems requirement specification at an early stage of the system life cycle-an attribute of the object-oriented methodology viewed very positively by many authors. Consequently, since an object-oriented program will be developed essentially as an interacting system of classes (usually developed independently), the stages of the life cycle model can be applied more accurately to the development cycle of each individual class rather that the system as a whole.

Fountain Model - Advantage

*   Iterative Waterfall Development  Fashion
*   Classic Linear
*   Analyze, Design, Code, Test &  Release

Fountain Model - Draw Back

*   Doesn’t Reflect Object Orientation
*   Unable To Commit  Deliverables

 DIFFERENT MODELS FOR OBJECT  ANALYSIS

Unlike the traditional systems analysis where user requirements are gathered and then specifications are put on the requirements and users are then asked to sign off on the specifications, the object methodologies use a more iterative process where the requirements and specifications are reviewed repeatedly and the users are heavily involved.

Object technology has many different methodologies to help analyze and design computer systems. We will review four of the more popular systems: Rumbaugh,

Booch, Coad-Yourdon, and Shlaer-Mellor. In most cases these methodologies are very similar, but each has its own way to graphically represent the entities. To understand and use these four methodologies would become difficult, if not impossible, for all projects.  If need be, it is possible to use concepts from one method with concepts from another technique,   basically  creating   your   own  object development technique.              The most important point is to remember is that the final outcome is what really matters, not the choice of one analysis technique over another technique. Remember, it is more important to do proper analysis and design to meet user requirements than it is to just follow a blind, meaningless  procedure.

The traditional systems development approach is sometimes referred to as the waterfall method. By waterfall, object analyst's follow a logical progression through analysis, design, coding, testing, and maintenance. Unfortunately system development seldom fits this kind of structured approach. End-users are notorious for changing their minds or identifying some feature that they forgot to identify. These changes in requirements can happen at any phase of system development and the analyst must struggle to accommodate these changes into the system.

The object-oriented methodologies require a more iterative process with the same five steps. The iterative process either adds new or more clearly defines existing properties, unlike the traditional approach that would re-hash specifications that are already done. The iterative process helps to reduce confusion around what the system is really suppose to do and what the users really want. The object-oriented software development methods make the assumption that user requirements will change. However it doesn't matter which programming language you use, be it FORTRAN or C++. Furthermore, it doesn't matter which system development technique you use, you will follow the same five steps in system development. It is just, how these five steps are applied that will make the difference in your system development project.

The Rumbaugh method

The Rumbaugh method is listed first because it is these authors favorite, and we find it a very friendly and easy methodology. For traditional system analyst's, the Rumbaugh's methodology is the closest to the traditional approach to system analysis and design, and beginners will recognize familiar symbols and techniques. The Rumbaugh methodology has its primary strength in object analysis but it also does an excellent job with object design. Rumbaugh has three deliverables to the object analysis phase; the Object model, the Dynamic model, and the functional model. These three models are similar to traditional system analysis, with the additions for the object model, including definitions of classes along with the classes variables and behaviors. The Rumbaugh object model is very much like an entity relationship diagram except that there are now behaviors in the diagram and class hierarchies. The dynamic model is a "state transition" diagram that shows how an entity changes from one state to another state. The functional model is the equivalent of the familiar data flow diagrams from a traditional systems analysis.

The Booch method

Booch's methodology has its primary strength in the object system design. Grady Booch has included in his methodology a requirements analysis that is similar to a traditional requirements analysis, as well as a domain analysis phase. Booch's object system design method has four parts, the logical structure design where the class hierarchies are defined, the physical structure diagram where the object methods are described. In addition, Booch defines the dynamics of classes in a fashion very similar to the Rumbaugh method, as well as an analysis of the dynamics of object instances, where he describes how an object may change state.

The Coad-Yourdon method

Coad-Yourdon methodology has its primary strength in system analysis. Their methodology is based on a technique called "SOSAS", which stands for the five steps  that help make up the analysis part of their methodology. The first step in system analysis is called "Subjects", which are basically data flow diagrams for objects. The second step is called "Objects", where they identify the object classes and the class hierarchies. The third step is called "Structures", where they decompose structures into two types, classification structures and composition structures. Classification structures handle the inheritance connection between related classes, while composition structures handle all of the other connections among classes. The next step in analysis is called "Attributes", and the final step is called "Services", where all of the behaviors or methods for each class are identified.

Following analysis, Coad and Yourdon define four parts that make up the design part of their methodology. The steps of system design are:

• The problem domain component - This will define the classes that should be in the problem  domain.

• The human interaction component - These steps defines the interface classes between objects.

• The task management component - This is where system-wide management classes are identified.

• The data management component - This design step identifies the classes needed for database access  methods.

The Shlaer-Mellor method

Shlaer-Mellor methodology has its primary strength in system design and is considered somewhat weak on analysis. The Shlaer-Mellor methodology includes three models; the information model, the state model, and the process model. The information model contains objects, variables, and all the relationships between the objects, and is basically a data model for the system. The state model records the different states of objects and changes that can occur between the objects. The process model is really not much more than a traditional data flow  diagram.

Now that we have covered the basics of the object approach, let's take a look at how a real-world object is created by using these techniques.

 The Object-Oriented Design  Model

One object-oriented methodology is based around the re-use of development modules and components. As such, a new development model is required that takes this re-use into account. The object-oriented model as shown in Figure 1.15, “The Object-Oriented Design Model” builds integration of existing software modules into the system development. A database of reusable components supplies the components for re-use. The object-oriented model starts with the formulation and analysis of the problem. The design phase is followed by a survey of the component library to see if any of the components can be re-used in the system development. If the component is not available in the library then a new component must be developed, involving formulation, analysis, coding and testing of the module. The new component is added to the library and used to construct the new  application.

This model aims to reduce costs by integrating existing modules into development. These modules are usually of a higher quality as they have been tested in the field by other clients and should have been debugged. The development time using this model should be lower as there is less code to  write.

Figure 1.15\. The Object-Oriented Design Model

![](Images/image01399.jpeg)

The object-oriented model should provide advantages over the other models as the libary of components grows over time.

An Example Design  Problem                                                         

Task: If we were given the problem; “Write a program to implement a simple savings account”… The account should allow deposits, withdrawals, interest and  fees.

Solution: The problem produces many concepts, such as bank account, deposit, withdrawal, balance etc.. that are important to understand. An OO language allows the  programmer to  bring  these concepts  right  through  to  the coding  step. The

savings account may be built with the properties of an account number and balance and with the methods of deposit and withdrawal, in keeping with the concept of the bank account. This allows an almost direct mapping between the design and the coding stages, allowing code that is easy to read and understand (reducing maintenance and development costs).

OOP also allows software re-use! … The concept of this savings account should be understood, independent of the rest of the problem. This general savings account  will certainly find re-use in some other financial  problem.

So after discussion with the client, the following formulation could be achieved - Design a banking system that contains both teller and ATM interaction with the  rules:

• The cashiers and ATMs dispense  cash.

• The network is shared by numerous  banks.

• Each transaction will involve an account and  documentation.

• There are different types of bank  accounts.

• There are different kinds of  transactions.

• All banks use the same  currency.

• Foreign currency transactions are permitted.

• ATMs and tellers require a cash  card.

Step 1\. Identify Possible Classes

• ATM, cashier, cashier station, software, customer,  cash.

• banking network,  bank.

• transaction, transaction  record.

• account, deposit account, long term savings account, current  account.

• withdrawal, lodgement,  cheque.

• currency.

• foreign currency, euro  cheque.

• cash card, computer  system.

Step 2\. Remove Vague Classes

• software, computer system,  cash.

Step 3\. Add New classes that arise!

• currency  converter

Step 4\. Create  Associations

• Banking Network (includes cashiers and  ATMs)

• Banks (holds  accounts)

• Account ( has a balance, a currency, a log of  transactions)

• Transaction (requires a cash  card)

• Lodgement (has an account number, an amount)

• Withdrawal (has an account number, an  amount)

• Cheque ( is a withdrawal, has a payee, an  amount)

• Eurocheque (is a cheque, has a currency)

• ATMs (accept cashcards, dispenses  cash)

Step 5\. Refine the Classes

Bank:

• has a  name

• has accounts

• has a base  currency

• has a sort  code

Account:

• has an  owner

• has a  balance

• has an account  number

• has a log of  transactions

Deposit Account:

• is an  account

• has a shared interest  rate

Current Account:

• is an  account

• has an overdraft  limit

Transaction:

• has an  account

• has a  date

• has a  value

• has a  bank

• has an account  Number

• has a  number

Withdrawal:

• is a  transaction

Lodgement:

• is a  transaction

Cheque:

• is a  withdrawal

• has a  payee

EuroCheque:

• is a  cheque

• has a  currency

CurrencyConverter:

Step 6\. Visual Representation of the Classes

![](Images/image01400.jpeg)Figure  1.16.  TheBank  class.

![](Images/image01401.jpeg)

![](Images/image01400.jpeg)Figure  1.17.  TheAccount  class.

![](Images/image01402.jpeg)

![](Images/image01400.jpeg)Figure  1.18.  TheTransaction  class.

![](Images/image01403.jpeg)

 COMPONENT  SOFTWARE:

(How to represent ‘components’ in object-oriented  design?  Explain.)

The breakdown of a project into its logical components is the essence of object-oriented analysis and design. That's also the basis for component software, which is composed of reusable pieces of software in binary form (as opposed to source code) that can be plugged into components from other vendors with relatively little effort. It is important to realize that a component-based approach to software development does not dictate the structure of an application. Rather, it is a model that makes possible the programming, use, and independent evolution of binary software components. Components are independent of the applications that use them as well as the programming languages used to create  them.

Software components can be divided into a variety of categories, including visual components, such as buttons or list boxes, and functional components, such as ones that add printing or spell checking capability. For example, a component-based architecture might enable spell checker components from multiple vendors to be plugged into a single word processing program from another vendor. This would hold many advantages for the end user. A user might love the word processor produced by company A but hate the spell checker it comes with. If the word processor was designed so that the spell checker component can be replaced, the user can purchase a spell checker from company B, which specializes in creating spell checkers. Component software enables software developers to specialize in what they do best.

A good analogy for component software can be found in the automobile industry, in which car manufacturers often buy individual car parts, such as engines and transmissions, from various manufacturers and then assemble cars from these components. With component software, the pieces can be used as they are—they don't need to be recompiled, you don't need the source code, and you aren't restricted to one programming language. The term for this process is binary reuse, because it is based on interfaces rather than on reuse at the source code level. While the software components must adhere to the agreed upon interface, their internal implementation is completely autonomous. For this reason, you can build the components using procedural languages as well as object-oriented  languages.

One  of  the  main  goals  of  a  component-based   programming   model   is   to   promote interoperability. Interoperability is one of those buzzwords in the computer field that means different things to different people. In the context of component software, interoperability simply means the ability of components to work together. When you examine a project and notice areas in which software seems to be forced together unnaturally, the application should be divided into  components.

Let's use the example of controls. In the good old days of Windows programming, if your program needed a toolbar, you simply wrote the toolbar code directly into the main part of the application. This approach had two inherent problems. First, your goal was probably not to create a cool toolbar but to create a great application with a toolbar. Second, after you consumed many precious hours developing a toolbar, if other developers in your company wanted to use that toolbar in their projects, they couldn't easily reuse it if the code was sprinkled throughout the program, responding to WM_CREATE, WM_PAINT, and WM_LBUTTONDOWN  messages.

A component-based approach to this problem would make the toolbar into a separate component. The problem then becomes how the toolbar component and the application should interact—the whole issue of interoperability. The component software paradigm mandates that all components define an interface that exposes the functionality available in that component. As long as the component implements the interface and the client applications abide by it, interoperability results. In the toolbar example, the application developers could simply purchase the toolbar component from some other developer who specializes in toolbars, thus saving development, debugging, and maintenance time.

One important principle of object-oriented programming, mentioned earlier, is encapsulation. Encapsulation hides the implementation of an object from users of the object. The users of an object have access only to the object's interface. Developers who use prebuilt objects in their projects are interested only in the "contract"—the promised behavior that the object supports. Component software formalizes the notion of a contract between an object and a client. Each object declares what it is capable of by implementing certain interfaces. The only way to access the services of an object is through the interfaces that it supports. Such a contract is the basis for interoperability.

PROTOTYPES:

Although the object-oriented analysis and design describe the system features, it is important to construct a prototype of some of the key system components shortly after the products are selected. A prototype enables you to fully understand how easy or difficult it will be to implement some of the features of the system. It also can give users a chance to comment on the usability and usefulness of the user interface design and lets you assess the fit between the software tools selected, the functional specification, and the user needs. Additionally, prototyping can further define the use cases, and it actually makes use-case modeling much easier.

Prototypes have been categorized in various ways. The following categories are some of the commonly accepted prototypes and represent very distinct ways of viewing a prototype, each having its own strengths:

• Horizontal  Prototype

• Vertical  Prototype

• Analysis  Prototype

A Horizontal prototype is a simulation of the interface (that is, it has the entire user interface that will be in the full-featured system) but contains no functionality. This has the advantages of being very quick to implement, providing a good overall feel of the system, and allowing users to evaluate the interface on the basis of their normal, expected perception of the system.

A Vertical prototype is a subset of the system features with complete functionality. The principal advantage of this method is that the few implemented functions can be tested in great depth. In practice, prototypes are a hybrid between horizontal and vertical: The major portions of the interface are established so the user can get the feel of the system, and features having a high degree of risk are prototyped with much more functionality.

An Analysis prototype is an aid for exploring the problem domain. This class of prototype is used to inform the user and demonstrate the proof of a concept. It is not used as the basis of development, however, and is discarded when it has served its purpose. The final product will use the concepts exposed by the prototype, not its code. A domain prototype is an aid for the incremental development of the ultimate software solution. It often is used as a tool for the staged delivery of subsystems to the users or other members of the development team. It demonstrates the feasibility of the implementation and eventually will evolve into a deliverable product.

The typical time required to produce a prototype is anywhere from a few days to several weeks, depending on the type and function of prototype. Prototyping should involve representation from all user groups that will be affected by the project, especially the end users and management members to ascertain that the general structure of the prototype meets the requirements established for the overall design.

ORDER OF ACTIVITIES FOR OBJECT IDENTIFICATION

1. Formulate a few scenarios with help from an end user or application domain  expert

2. Extract the use cases  from the scenarios, with the help of an application domain  expert

3. Then proceed in parallel with the  following:

*   Analyse the flow of events in each use case using Abbot's textual analysis technique
*   Generate the UML class  diagram.

 CASE  STUDY

Develop a system for railway reservation using object oriented design. Draw the necessary diagrams.

Let us show the process of OOAD through software tools.

Problem Statement for Railway Reservation System

Software has to be developed for automating the manual railway reservation system. The system should be distributed in nature. It should be designed to provide functionalities as explained below:

1.  Reserve Seat: A passenger should be able to reserve seats in the train. A reservation form is filled by the passenger and given to the clerk, who then checks for the availability of seats for the specified date of journey. If seats are available then the entries are made in the system regarding the train name, train number, date of journey, boarding station, destination, person name, sex and total fare. Passenger is asked to pay the required fare and the tickets are printed. If the seats are not available then the passenger is  informed.
2.  Cancel Reservation: A passenger wishing to cancel a reservation is required to fill a form. The passenger then submits the form and the ticket to the clerk. The clerk then deletes the entries in the system and changes the reservation status of that train. The clerk crosses the ticket by hand to mark as  cancelled.
3.  Update Train Information: Only the administrator enters any changes related to the train information like change in the train name, train number, train route etc. in the system.
4.  Report Generation: Provision for generation of different reports should be given in the system. The system should be able to generate reservation chart, monthly train report etc.
5.  Login: For security reasons all the users of the system are given a user id and a password. Only if the id and password are correct is the user allowed entry to the system and select from the options available in the  system.
6.  View Reservation Status: All the users should be able to see the reservation status of the train online. The user needs to enter the train number and the pin number printed on his ticket so that the system can display his current reservation status like confirmed, RAC or  Wait-listed.

7.  View Train Schedule: Provision should be given to see information related to the train schedules for the entire train network. The user should be able to see the train name, train number, boarding and destination stations, duration of journey etc.

Analysis and Design Methodology

The sequences of steps for the process are as follows:

Step 1: Choose a pre-designed model if it exists.

Choose the framework according to the development platform.

Step 2: Make Use of Case Diagram.

The general flow of any analysis and design process is to begin with the identification of the functionalities of the system and the actors associated with the system. We depict the overview of the system to be developed by a Use Case diagram.

After analysing the above problem we have identified the following Use Case and Actors of the system.

Actors associated with the system are:

1.  Admin

2.  Reservation Clerk

3.  Passenger

4.  Printer

Use Cases for the system are:

1.  Reserve Seat

2.  Cancel Reservation

3.  Update Train  Information

4.  Report Generation

5.  Login

6.  View Reservation Status

7.  View Train Schedule

![](Images/image01404.jpeg)

Figure 2: Use case diagram for railway reservation system

Step 3: Define Classes and associate them with each Use Case.

We will consider the Login Use Case and describe its complete flow.

For realization of this Use Case we need a user interface for entering the user id and password. This needs to be validated with the database so we need an entity class and for coordinating the working between the front-end and back-end we need a controller class. We need to assign a name for each of these classes.

Type of Class Name of Class Boundary Class : Login Form

Entity Class : Login_Information (Name of table in the database) Control Class : Login_Ctrl

Step 4: Depict the interaction between the classes with a Sequence and Collaboration Diagram

![](Images/image01405.jpeg)

Step 5: Draw Activity Diagram and State Chart Diagram if required. These diagrams should be names and linked to other related diagrams.

Step 6: Draw Class Diagram for all the Entity classes depicting relationships between the classes. Attributes are defined for each class. You must give proper names

to these diagrams. Mark each class as persistent. They are the database tables where data is to be stored.

![](Images/image01406.jpeg)

![](Images/image01407.jpeg)

Step 7: Define the components of the system, for example, exes, dlls, activeX controls etc.

Suppose, you wish to develop the software as an executable, so all the boundary and control classes are assigned to the exe. Create an executable software component and give it a name. This component must be assigned to  class.

Then, draw a component diagram to show the relations between the components of the system. You must give a name to the diagram.

![](Images/image01408.jpeg)![](Images/image01409.jpeg)

Step 8: Now, draw a deployment diagram for depicting the network layout of the system.

![](Images/image01410.jpeg)

Create the Deployment diagram and give it a name.

Step 9: Now, perform the task of forward engineering to generate pseudo code