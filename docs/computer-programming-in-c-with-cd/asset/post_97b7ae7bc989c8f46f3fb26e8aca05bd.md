
```cpp
{
    char fName[15];
    char lName[15];
};

int main ()
{
    name p1 = {"First_Name ", "Surname"};

    cout<<p1.fName<<p1.lName;

    return 0;
}
```

Ans. Output of the preceding program is as follows:

```text
First_Name Surname
```

### Q6. What will be the output of the following program?

```cpp
#include <iostream.h>

struct date
{
    int day;
    int month;
    int year;
};

int main()
{
    date d1, d2;

    cout<<"Enter Day of the date: ";
    cin>>d1.day;
    cout<<"\nEnter Month of the date: ";
    cin>>d1.month;
    cout<<"\nEnter Year of the date: ";
    cin>>d1.year;

    d2 = d1;
    cout<<"\nThe date you have Entered is: "<<d2.day<<"/"<<d2.month<<"/"<<d2.year;

    getch();
    return 0;
}
```

Ans. Output of the preceding program is as follows:

```text
Enter Day of the date: 30

Enter Month of the date: 12

Enter Year of the date: 1985

The date you have Entered is: 30/12/1985
```

### Q7. What will be the output of the following program?

```cpp
#include <iostream.h>

union Test_Defvalue
{
    int num1;
    double num2;
};

int main()
{
    Test_Defvalue tdv;

    tdv.num1 = 12;
    cout<<"Default Value of an Integer Variable: "<<tdv.num1<<endl;
    tdv.num2 = 12.12456;
    cout<<"Default Value of a Double Variable: "<<tdv.num2;

    return 0;
}
```

Ans. Output of the preceding program is as follows:

```text
Default Value of an Integer Variable: 12
Default Value of a Double Variable: 12.1246
```

### Q8. What will be the output of the following program?

```cpp
#include <iostream.h>

union Test
{
    int var1;
    char var2[20];
    double var3;
};
struct Test2
{
    int var1;
    char var2[20];
    double var3;
};

int main()
{
    Test t1;
    Test2 t2;

    cout<<"Memory occupied by the variable of a Union: "<<sizeof(t1)<<endl;
    cout<<"Memory occupied by the variable of a Structure: "<<sizeof(t2)<<endl;
    return 0;
}
```

Ans. Output of the preceding program is as follows:

```text
Memory occupied by the variable of a Union: 20
Memory occupied by the variable of a Structure: 30
```

### Q9. What will be the output of the following program?

```cpp
#include <iostream.h>

int main ()
{
    struct myStruct
    {
        int var1;
        float var2;
    }ms;

    ms.var1 = 123;
    ms.var2 = 123.123;

    cout<<"value of var1: "<<ms.var1<<endl;
    cout<<"value of var2: "<<ms.var2<<endl;

    return 0;
}
```

Ans. The output of the preceding program is as follows:

```text
value of var1: 123
value of var2: 123.123
```

### Q10. What will be the output of the following program?

```cpp
#include <iostream.h>

union MyUnion
{
    int var1;
    double var2;
};

int main()
{

    MyUnion u1;
    u1.var1 = 2;
    cout <<"Value of var1: "<<u1.var1<< endl;

    u1.var2 = 4.5658;
    cout <<"Value of Var2: "<< u1.var2 << endl;

    u1.var2 = 456.000;
    cout<<"New value of Var2 is: "<<u1.var2<<endl;

    return 0;
}
```

Ans. The output of the preceding program is as follows:

```text
Value of var1: 2
Value of Var2: 4.5658
New value of Var2 is: 456
```

### Q11. What will be the output of the following program?

```cpp
#include <iostream.h>
#include <stdio.h>

struct student
{
    char student_ID[15];
    char student_name[30];
    int student_marks;
};

student input()
{
    student new_student;
    cout<<"Enter student ID :"<<endl;
    gets(new_student.student_ID);
    cout<<"Enter student name :"<<endl;
    gets(new_student.student_name);
    cout<<"Enter student marks :"<<endl;
    cin>>new_student.student_marks;

    return new_student;
}

void display(student p)
{
    cout<<"The descriptions of student are -->"<<endl;
    cout<<"-----------------------------------"<<endl;
    cout<<"student ID :"<<p.student_ID<<endl;
    cout<<"student name :"<<p.student_name<<endl;
    cout<<"student marks :"<<p.student_marks<<endl;

    cout<<"-----------------------------------"<<endl;
    cout<<"Percentage of marks out of 400 = "
    <<(((p.student_marks)*100)/400);
}

int main()
{
    student input();
    student p;
    p = input();
    display(p);
    return 0;
}
```

Ans. The output of the preceding program is as follows:

```text
Enter student ID :
ABC123
Enter student name :
XYZ
Enter student marks :
315
The descriptions of student are -->
-----------------------------------
student ID :ABC123
student name :XYZ
student marks :315
-----------------------------------
Percentage of marks out of 400 = 78
```

### Q12. What will be the output of the following program?

```cpp
#include <iostream.h>

union Detail
{
    char *Monitor;
    int Memory;
};

struct My_Computer
{
    char *os;
    char *processor;
    int price;
    union Detail computer_Detail;
};
int main ()
{
    struct My_Computer c1;
    c1.computer_Detail.Monitor = "LG Flatron";
    cout<<"The computer has Monitor of: "
        <<c1.computer_Detail.Monitor<<"\n";

    c1.computer_Detail.Memory = 1024;
    cout<<"This computer has: "<<c1.computer_Detail.Memory<<" MB of Memory\n";

    c1.os = "Windows Vista";
    c1.processor = "Intel Dual Core";
    c1.price = 24500;

    cout<<"Operating System of the computer is: "<<c1.os<<"\n";
    cout<<"processor of the computer is: "<<c1.processor<<"\n";
    cout<<"Price of the computer is: "<<c1.price;

    return 0;
}
```

Ans. The output of the preceding program is as follows:

```text
The computer has Monitor of: LG Flatron
This computer has: 1024 MB of Memory
Operating System of the computer is: Windows Vista
processor of the computer is: Intel Dual Core
Price of the computer is: 24500
```

## 06 | Object-Oriented Programming with C++

### OBJECTIVES

- 6.1 Exploring Basic Concepts of Object-Oriented Programming
- 6.2 Working with Classes and Objects
- 6.3 Explaining the Difference between C Structures and C++ Classes
- 6.4 Creating Data Access Methods
- 6.5 Creating Inline Functions
- 6.6 Working with Constructors and Destructors
- 6.7 Exploring Local and Nested Classes
- 6.8 Passing Objects as Function Parameters
- 6.9 Returning Objects from Functions
- 6.10 Working with Arrays in C++
- 6.11 Creating a const Object
- 6.12 Using the this Pointer
- 6.13 Working with Friend Functions and Friend Classes
- 6.14 Declaring and Using Static Variables and Functions
- 6.15 Overloading

Object-oriented programming (OOP) is a programming model that uses objects and their interactions to design applications and computer programs. In OOP, objects represent real world entities, such as students, doctors, and bank accounts. These objects can interact with each other by sending or receiving messages. This OOP model is based on four basic pillars, namely abstraction, encapsulation, inheritance, and polymorphism. Earlier programming languages, such as C, FORTRAN, and BASIC are based on procedural language. In procedural language, program often uses branching statements and procedures to execute one or other set of instructions depending upon the result that you want. Procedure is also known as routine or subroutine, or a function. When you write large programs in procedural language, it becomes complex to understand and hard to program. This problem is overcome by a new programming technique, which is known as OOP.

OOP is a modular approach to comprehend the design and functioning of a computer program (software). Each module (or object) is a combination of the data and procedures (sequences of instructions) that act on the data. On the other hand, in procedural programming the data is separated from instructions for processing. In OOP, a group of objects that have common properties, operations, and behaviors is called a class. The classes that are developed for previous applications can be reused so that new applications can be developed faster with improved reliability and consistency of design. An OOP language designs programs around built-in data types and user-defined data types. You can even represent real world entities, such as dogs, kingdoms, students in your application using the user-defined data types.

In this chapter, you learn about the basic concepts of OOP, such as class, object, abstraction, and inheritance. Next, you learn how to create a class, data members, member functions, and objects. You also learn about data access methods, inline functions, constructors, and destructors that are created as part of a class. Next, you learn how to create a local class and a nested class in C++, functions that take objects as function parameters and can return objects, const objects, and an array of objects. Next, you learn how to use this pointer to represent the reference of the current class. You also learn how to create friend functions, friend classes of a class, static variables and functions of a class. Finally, you learn the concept of overloading in C++ and creating overloaded functions, constructors, and operators. Let's start by exploring the basic concepts of OOP.

### 6.1 Exploring Basic Concepts of Object-Oriented Programming

C++ introduces OOP that allows programmers to divide long programs into more autonomous units and helps to solve many other problems as well. The following basic concepts are included in OOP:

- Object
- Class
- Method
- Message Passing
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

Let's explain these concepts in detail.

### Object

An object is a pattern (instance) of a class. For example, Maruti Zen and Tata Indica are objects of the car class. An object represents a real world entity, such as a person, place, or a programming entity, such as constants, variables, and memory location. An object has the following three main characteristics:

- It has a state
- It may or may not display a behavior
- It has a unique identity
