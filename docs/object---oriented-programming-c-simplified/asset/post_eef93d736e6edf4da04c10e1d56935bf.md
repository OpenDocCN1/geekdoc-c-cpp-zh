
9. Destructor can be virtual.

In our all earlier program destructor can be written. For instance in all our dynamic constructor program destructor can be written for the allocation of memory like.

```
~string( )
{
    delete sname;
}

And

~matrix ( )
{
    delete ptr[];
}
```

As one more example of destructor which makes use of block as scope, see the next program given below :

```
/*PROG 7.26 DEMO OF CONSTRUCTOR VER 2 */

#include <iostream.h>
#include <conio.h>

class demo
{
    static int count;

    public :

    demo( )
    {
        cout<<"Object created "<<++count<<endl;
    }
    ~demo( )
    {
        cout<<"Object Destroyed"<<count--<<endl;
    }
};

int demo ::count;
```

```
```cpp
void main()
{
    clrscr();
    cout << "I am in main \n";
    demo d1;
    {
        cout << "In block 1\n";
        demo d2;
        {
            cout << "In block 2 inside block 1\n";
            demo d3;
        }
    }
    {
        cout << "In block 3\n";
        demo d4;
    }
    cout << "Exiting main\n";
    getch();
}
```
```

**OUTPUT:**

I am in main

Object created 1

In block 1

Object created 2
In block 2 inside block 1

Object created 3
Object Destroyed3
Object Destroyed2

In block 3

Object created 2
Object Destroyed2
Exiting main

+   3. A constructor that accepts no argument is known as do-nothing constructor.
+   4. A class constructor demo cannot take demo as an argument.
+   5. Constructors can be overloaded.
+   6. A destructor must not have argument.
+   7. Constructor may be private.
+   8. The destructor and constructor are the only member functions that can be called for a const object.
+   9. Each class can have exactly one constructor.
+   10. Declaration of constructor and destructor within a class is mandatory.

## B. Answer the Following Questions :

+   1. What is the difference between constructor overloading and function overloading?
+   2. What is copy constructor? Why we pass an object by reference to the copy constructor?
+   3. Under what condition a copy constructor is called?
+   4. Can we have default argument in the constructors?
+   5. What is dynamic initialization of objects?
+   6. What is dynamic destructor? Do you have dynamic destructor?
+   7. Why an object is passed by reference into the copy constructor?
+   8. What two different types of constructor C++ provides to a class by default?
+   9. What is default constructor or do-nothing constructor?
+   10. What do you understand by an implicit and explicit call to constructor?
+   11. What is destructor?

## C. Brain Drill :

+   1. Define a class called time that has separate int data members for hours, minutes and seconds. One constructor should initialize these data to 0 and another should initialize them to fixed values. Write a member function to display time in the format 12:28:34. Another member function should add two objects of type time passed as arguments.
+   
+   2. Write a program to declare global and local objects with the same name. Access member function using both the objects.
+   
+   3. Define a class named Queue for holding ints and providing function for inserting items at one end and removing items from other end of a queue data structure to be supported by this class. Include a default constructor, a destructor and the usual queue operations: insert( ), remove( ), isempty( ), and isfull( ). Use array implementation.
+   
+   4. Define a class of square matrix N × N of integers. Define the necessary constructor/destructor and other members. Write a program to find the trace (sum of diagonal elements) of a matrix.

## WORKING WITH OPERATOR OVERLOADING

### 8.1 INTRODUCTION

Operator overloading refers to overloading of one operator for many different purpose. For example, the binary + can be used to add two integer numbers, two float numbers, two structures variables, two union variables or two class objects. Use of operator overloading permits us to see no difference between built-in data types and user defined data types. It is one of the powerful and fascinating features of the C++ which give additional meaning to built-in standard operators like +, −, *, /, >, <, <=, >= etc. Let’s see first a small example to give you idea of operator overloading and more concepts will be build later on.

```
/*PROG 8.1 DEMO OF OPERATOR OVERLOADING, ADDING INTEGER TO OBJECT*/

#include<iostream.h>

class demo_op1
{
    private :

        int num;

    public :

        void input( )
        {
            cout << "Enter the number" << endl;
            cin >> num;
        }
        void operator + (int x)
```

```
{
    num = num + x;
}
void show()
{
    cout << "The num is " << num << endl;
}
};
void main()
{
    demo_op1 d1;
    d1.input();
    d1.show();
    int x;
    cout << "Enter the value you want to add\n";
    cin >> x;
    d1 + x;
    d1.show();
}
```

# OUTPUT :

Enter the number
123
The num is 123
Enter the value you want to add
14
The num is 137

EXPLANATION : The syntax of the overloading an operator and writing new overloaded operator function is as follows :

```
return_type operator operator (arguments)
{
    Statements;
    Statements;
    Statements;
}
```

The first word operator is a keyword and must be specified. The second word operator represents the operator which we want to overload i.e., to give a new meaning. It may be +, -, =, ==, >, < etc. Later I will tell you about operators which cannot be overloaded. In the program we have overloaded + operator as given below:

![](img/ad5299318df8d4d7c6df5eaa86590ea3_355_0.png)

Which accepts an argument of type int and returns nothing as return type is void. Inside the function we add value of x to the num of the object. Now see how this function is called from main.

The statement d1+x; initially interpreted as d1.operator +(x); whenever compiler sees operator like +, -, *, /, ++, --, etc with variable of user defined data types (here object) it checks whether the operator has been overloaded in the class or not. If not it flashes an error else it calls the appropriate overloaded operator function. As operator function is member function of the class we require some object to call the function so an object is always preceded with the operator which is overloaded and being used in the expression. The argument to be passed is specified as the right operand of the overloaded operator. Here the overall effect of the statement d1+x; is to call the operator function operator + and pass x as argument to it. See how convenient to write d1+x for adding an integer x to object d1 ?

### 8.2 OPERATOR OVERLOADING WITH BINARY OPERATOR

When overloading binary operator using operator function as class member function, the left side operand must be an object of the class and right side operand may be either a built-in type or user defined type. The other method using friend function will be discussed later on. We present numerous program of overloading binary operators.

```
/*PROG 8.2 OVERLOADING BINARY + WITH CLASS OBJECTS AS ARGUMENT VER 1*/

#include <iostream.h>
#include <conio.h>
class demo_sum
{
    private :
        int num;
        static int count;
    public :
        void input()
{
```

```
cout << "Enter the number for" << "Object" << ++count << "\n";
cin >> num;
}
void operator +(demo_sum temp)
{
int x;
x=num +temp.num;
cout << "Sum of two is " << x << endl;
}
void show()
{
cout << "The num is" << num << endl;
}
};
int demo_sum : :count;
void main()
{
clrscr();
demo_sum d1,d2;
d1.input();
d1.show();
d2.input();
d2.show();
d1 + d2;
getch();
}
```

OUTPUT :
Enter the number forObject1
23
The num is23
Enter the number forObject2
45
The num is45
Sum of two is 68

```
void main()
{
    clrscr();
    demo_sum d1, d2;
    d1.input();
    d2.input();
    d1.show();
    d2.show();
    int sum=d1+d2;
    cout<<"The sum of two object's num is "<<sum<<endl;
    getch();
}

OUTPUT :
Enter the number for object1
23
Enter the number for object2
56
The num is 23
The num is 56
The sum of two object's num is 79
```

EXPLANATION : The program is similar to previous program but instead of displaying the sum in the operator function itself we have returned the sum from function. The function

```
int operator + (demo_sum temp)
{
    return (num + temp.num);
}
```

Overloads the binary + and accepts an argument of type demo_sum. In the function it finds the sum of two objects num and returns it that's why the return type of the function is int.

```
/*PROG 8.4 OVERLOADING BINARY + WITH CLASS OBJECTS AS ARGUMENT & RETURNING OBJECTS */

#include <iostream.h>
#include <conio.h>
class demo_sum
{
    private :
        int num;
```
