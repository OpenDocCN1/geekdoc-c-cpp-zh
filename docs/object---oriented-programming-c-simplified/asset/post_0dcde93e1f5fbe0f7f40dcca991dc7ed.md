
## CHAPTER 6
## CLASS AND OBJECTS IN C++
### 6.1 WORKING WITH CLASS

The most remarkable feature of C ++ is a class. The class binds together data and methods which work on data. The class is an abstract data type (ADT) so creation of class simply creates a template. The general syntax of creating a class in C++ is given below:

```
class class_name
{

    public :
        data & function;
    private :
        data & function;
    protected :
        data & function;
};
```

The class is a keyword. Following this keyword class, class_name represents name of the class. The class name must obey rules of writing identifier as class_name is nothing but an identifier. The class is opened by opening brace { and closed by closing brace }. The class definition/declaration must end with semicolon. Inside the class we define the data members and member functions. They may be defined either public, private or in protected mode. There are three different types of mode :

- 1. public
- 2. private
- 3. protected.

The mode is also known as visibility modifier or access specifier. Data members and functions declared under the public mode can be used inside and outside the class. Private data members and functions can be used only inside the class. Protected data member and function also can only be used inside the class. Protected data member and function also can only used inside the class only but serve a different purpose which you will study in inheritance.

The data member of class are used inside the member functions of the class. Data members are declared inside the class but used in the member functions of the class. Usually the data members are private and member functions are public. So data members can only be used inside the functions of the class. This is to safeguard private data from external access.

If no visibility mode is written the default visibility mode private is assumed for the class.

The declaration of a class alone does not serve any purpose. To make use of the class we need to create variable of type class. A variable of class type is known as an object. The class is loaded into memory when first object of the class is created. Creation of object creates memory space for the object which depends upon size of the data members of the class. For each object separate copy of the data members is created. But only one copy of the member function is created which is shared by the entire object.

The objects call member functions of the class using operator dot (.) operator. Which is known as period or membership operator?

Before a member function can work on to the data member of the class, they must be initialized by calling a function which provides initial values to the data member of the class.

Let’s take a practical example of class now.

# /*PROG 6.1 DEMO OF CLASS AND OBJECT VER 1*/

```
#include <iostream.h>
#include <conio.h>
class demo
{
private :
    int cx,cy;
public :
    void input_data(int x,int y)
    {
        cx=x;
        cy=y;
    }
    void show_data()
    {
        cout<<"cx="<<cx<<"\t"<<"cy="<<cy<<endl;
    }
};
void main()
{
```

```
demo d1;
clrscr();
d1.input_data(10,20);
d1.show_data();
getch();
}

OUTPUT :
 cx=10 cy=20
```

EXPLANATION : A class is created using keyword class followed by class name. The class name follows the rules of writing identifiers. Inside the class demo we have two variables cx and cy of type integer. The private and public are known as visibility modifier or access specifier. Each visibility modifier must end with : (colon). All the variables, function etc. declared under private a visibility modifier bear that prototype of visibility modifier. Here cx and cy written under private so they become private. If we do not write private, they are also considered as private is the default access level in a class. The function input_data takes two parameters of type int and returns nothing as void is the return type. The function show_data display the two data members' cx and cy. Note the two functions are defined within the class. We can also declare them inside the class and defined outside the class. The class declaration has to end with semicolon.

In the main the statement demo d1; creates a variable of class demo type. Not we do not have to write class demo.d1;. The variable d1 of class demo type is known as an instance of class demo or an object. The creation of an object allocates memory depending upon the size of the class which is the sum of size of data members. Functions do not add to the size of the class or object. Here a memory of 8 bytes will be allocated for the object d1. Functions are given memory when a class is loaded into the memory.

All public members (data + functions) can be accessed in the main with the help of object using dot (.) operator which is also known as membership operator or period. Through statement d1.input_data (10, 20) we are calling the function input_data and passing two int constant 10 and 20. They are collected in the formal parameters x and y and then assigned to cx and cy. Now cx and cy can be used in all the functions of demo. Whenever you are working with the class & object, the first thing you need to perform is to assign values to data members of class through function. You cannot initialize them directly in the class. As cx and cy are private they can only be accessed inside the member function of the class and not anywhere. Usually we make data members as private and functions as public while designing a class. All the functions defined inside the class are treated as inline.

```
/*PROG 6.2 DEMO OF CLASS AND OBJECT VER 2*/

#include <iostream.h>
#include <conio.h>
class demo
{
private :
```

```
int cx, cy;
public :
    void input_data(int,int);
    void show_data();
};
void demo ::input_data(int x,int y)
{
    cx = x;
    cy = y;
}
void demo ::show_data()
{
    cout << "cx=" << cx << "\t" << "cy=" << cy << endl;
}
void main()
{
    demo d1;
    clrscr();
    d1.input_data(10,40);
    d1.show_data();
    getch();
}
```

# OUTPUT :

cx=10 cy=40

# EXPLANATION :

In the program we have declared the function inside the class and defined outside the class. When we define a function outside a class, scope resolution operator(::) has to be used with the function to tell the compiler to which class the function belongs. The declaration of function was void show_data(); to define this function outside the class we first present the general syntax:

```
return_type class_name :: function_name(arguments/parameters)
{
    function code;
}
```

Here return_type is void, class name is demo and function name is show_data and it takes no arguments so we define:

```
return_type
↓
class_name
↓
function_name
↓
void demo :: show_data ()
{
cout << "cx = " << cx << "\t" << "cy = " << cy << endl;
}
```

This notation of associating a class name with function using : : is a must. It allows us to have two functions with the same name in two different classes. Then to resolve them we have to use : : operator.

### 6.2 PROGRAMMING EXAMPLES (PART-1)

```
/*PROG 6.3 DEMO OF CLASS AND OBJECT VER 3 */
#include <iostream.h>
#include <conio.h>

class demo
{
private :
int cx,cy;
public :
void input_data();
void show_data();
};

void demo :: input_data()
{
cout << "Enter the value of cx and cy \n";
cin >> cx >> cy;
}

void demo :: show_data()
{
cout << "cx = " << cx << "\t" << "cy = " << cy << endl;
}
```

```
void main()
{
    demo d1;
    d1.input_data();
    d1.show_data();
    getch();
}

OUTPUT :
Enter the value of cx and cy
12
56
cx=12 cy=56
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_217_0.png)

# FIGURE 6.1. Output Screen of Program.

EXPLANATION : In the earlier two programs, we assigned the values to cx and cy through formal parameters x and y. Here, we have changed the function input_data completely. Inside the function we take two values from keyboard and store them directly into cx and cy. Thus the function does not take any argument.

# /* PROG 6.4 STUDENT CLASS & OBJECT DEMO */

```
#include <iostream.h>
#include <string.h>
#include <conio.h>
class student
{
    char sname[10];
    int sage;
    char sclass[10];
public :
    void getdata (char[], int, char[]);
    void showdata();
};
```
