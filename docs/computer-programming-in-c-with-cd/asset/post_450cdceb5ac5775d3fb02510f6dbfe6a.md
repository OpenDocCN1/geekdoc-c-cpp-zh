
```cpp
void ConstFunction::setVal()
{

x=10;
y=x*x;
}
void ConstFunction::display() const
{
cout<<"x = "<<x<<endl;
cout<<"y = "<<y<<endl;
}

void main()
{
ConstFunction cf;
cf.setVal();
cf.display();
}
```

### Output:
```text
x = 10
y = 100
```

In Listing 3, x and y are variables of int type that are assigned with values in the setVal() function. The display() is a const function, which is used to display the values of x and y variables. If you try to assign values to the variables in the display() function, you get compilation error as a const function cannot modify the values of data members of a class.

## Nesting of Member Functions

In C++, it is not necessary that a function can be invoked only by an object of a class. The functions that can be invoked by other functions are called nested functions.

Listing 4 shows how to call a function through another function call (you can find this example in the NumberAddition.cpp file on the CD in the code\chapter6 folder):

### Listing 4: Calling a Function through another Function

```cpp
#include<iostream.h>

class NumberAddition
{
    int a, b;
    int add();
    public:
    void numAccept();
    void display();
};

void NumberAddition::numAccept()
{
    cout<<"Enter any two numbers:";
    cin>>a>>b;
}
int NumberAddition::add()
{
    return a+b;
}
void NumberAddition::display()
{
    cout<<"The Addition of two numbers is ="<<add();
}

void main()
{
    NumberAddition na;
    na.numAccept();
    na.display();
}
```

### Output:
```text
Enter any two numbers:34
89
The Addition of two numbers is =123
```

In Listing 4, two random numbers are given as input values and then the program displays their sum. This program has a class, NumberAddition, which has a and b as its private data members; and numAccept(), add(), and display() are defined as its member functions.

The numAccept() function accepts the input values for the variables a and b. The add() function returns the sum of the values stored in the a and b variables. The return type of the add() function is of the int type; and its scope is private in the class NumberAddition. The display() function is used to display the value returned by the add() function as well as a user-defined message. Note that an object cannot invoke a private function of a class; however, the same private member function can be invoked indirectly, through a public member function of the same class.

## TEST YOUR KNOWLEDGE

- **Q1.** Create a program to display the area and perimeter of a circle.

```cpp
#include<iostream.h>

class circle
{
    private:
        float radius,area,perimeter;
    public:
        inline void get_details()
        {
            cout<<"enter the radius of the circle";
            cin>>radius;
        }
        inline void cal()
        {
            area=radius*radius*3.14;
            perimeter=2*3.14*radius;
        }
        inline void display()
        {
            cout<<"area is "<<area;
            cout<<endl;
            cout<<"perimeter is"<<perimeter;
        }
};

void main()
{
    circle cir;
    cir.get_details();
    cir.cal();
    cir.display();
}
```

### Output:
```text
enter the radius of the circle100
area is 31400
perimeter is 628
```

- **Q2.** Create a distance class and calculate the sum and difference of between the objects of the class.

Ans.

```cpp
#include<iostream.h>

class distance
{
    private:
    float meter;
    public:
    void init()
    {
        cout<<"Enter The Distance";
        cin>>meter;
    }
    void add(distance d1,distance d2)
    {
        meter =d1.meter+d2.meter;
    }
    void subtract(distance d1,distance d2)
    {
        meter=d1.meter-d2.meter;
    }
    void display()
    {
        cout<<"distance ="<<meter;
    }
};
void main()
{
    distance d1,d2,d3;
    cout<<"distance1"<<endl;
    d1.init();
    cout<<"distance2"<<endl;
    d2.init();
    d3.add(d1,d2);
    cout<<"addition of distance=";
    d3.display();
    d3.subtract(d1,d2);
    cout<<endl<<"subtraction of distance=";
    d3.display();
}
```

### Output:
```text
distance1
Enter The Distance100
distance2
Enter The Distance82
addition of distance=distance =182
subtraction of distance=distance =18
```

Next, you learn the difference between the concept of structures in the C language and the concept of classes in the C++ language.

## 6.3 Explaining the Difference between C Structures and C++ Classes

In the C language, structure (or struct) is a user-defined type, with a limitation that you cannot use a struct data type as a built-in data type for the mathematical operations, such as addition or subtraction. For instance the following code snippet shows the definition of a struct data type, MyNum:

```cpp
struct MyNum
{
    int num1;
    int num2;
};
struct MyNum obj1,obj2,obj3;
```

In the preceding code snippet, MyNum is a struct data type, and obj1, obj2, and obj3 are its variables. The obj1, obj2, and obj3 variables can be assigned with the values by using the dot (.) operator. However, you cannot use these variables in an operation, for instance addition, as shown in the following code snippet:

```cpp
obj3=obj1+obj2;
```

Another limitation of structures in the C language is that they do not support data hiding. The members of a structure can be accessed by the variables of the structure in any function. This is because the members of a structure in the C language are public, by default.

The C++ language also supports structures and implements all the features of structures in the C language. In C++, however, you can declare the variables of a structure without using the struct keyword, as shown in the following code snippet:

```cpp
struct CppMyNum
{
    int num1;
    int num2;
    void mynumFunc()
    {
        //body of a structure function
    }
};
CppMyNum obj1,obj2,obj3;
```

C++ also allows you to define the functions in a structure; whereas, in C language, you can only declare variables in a structure. This means that a C++ structure can have both variables as well as functions as its structure members. In addition, you can declare some of the members of a C++ structure as private, so that external functions cannot access these members directly outside the body of the structure.

Besides structures, C++ supports another type of a user-defined data type, which is known as class. In C++, a class is similar to a struct with the exception that, by default, all the members of a class are private; while the members of a struct are public. Moreover, one user-defined data type can inherit the features and functioning from another user-defined data type. This means that a class or structure can be inherited from another structure or class.

Let’s now explore how to create data access methods in a class.

## 6.4 Creating Data Access Methods

At times, you need to access the private data members of a class. For this purpose, you can use the data access methods, which allows you to access the private data members outside the class. Usually the data access methods are implemented in a pair of getX() and setX() methods, where X can be any user-defined name. The getX() method gets the value of a data item, and the setX() method sets the value of a data item. Listing 5 shows an example of the getX() and setX() pair defined in a class (you can find this example in the DataAccessMethods.cpp file on the CD in the code\chapter6 folder):

### Listing 5: Creating Data Access Methods in a Class

```cpp
#include<iostream.h>

class GreatestNumber
{
    private:
    int x,y;
    public:
    void setNum(int a,int b);
    int getNum();
};

void GreatestNumber::setNum(int a,int b)
{
    x=a;
    y=b;
}

int GreatestNumber::getNum()
{
    if(x>=y)
    return x;
    else
    return y;
}

int main()
{
```

(you can find this example in the InlineInClass.cpp file on the CD in the code\chapter6 folder):

### Listing 6: Creating Inline Functions in a Class

```cpp
#include<iostream.h>

class MyClass
{
    int x,y,z;
public:
    void getdata()
    {
        cout<<"Enter any two numbers";
        cin>>x>>y;
        z=x+y;
    }
    void displayData()
    {
        cout<<"The sum of two numbers is="<<z<<endl;
    }
};

int main()
{
    MyClass o;
    o.getdata();
    o.displayData();
    return 0;
}
```

### Output:
```text
Enter any two numbers78
43
The sum of two numbers is=121
```

In Listing 6, getData() and displayData() are two inline member functions of the MyClass class. These functions are defined inside the boundary of the MyClass class without using the inline keyword.

The functions defined outside a class are non-inline or outline functions. Member functions defined outside the class declaration can also be made inline functions by prefixing the `inline` keyword to its definition. Listing 7 shows the creation of inline functions outside a class (you can find this example in the InlineOutClass.cpp file on the CD in the code\chapter6 folder):
