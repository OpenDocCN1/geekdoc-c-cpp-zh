
![](img/ad5299318df8d4d7c6df5eaa86590ea3_440_0.png)

Figure 9.8. Output screen of program 9.19

EXPLANATION : In the earlier program length and width in the class. Area was protected and through public inheritance we could use them in class Volume. But here both the data members are private so we cannot make use of these data members in the derived class Volume as private members are never inherited. For that we have created two public member function get_l and get_w which returns length and width respectively. In the main we create an object v of class Volume and call the function input_V with three arguments 5, 10 and 15. These three values are collected in the formal parameters x, y and z respectively. The first two values x and y are passed to the input_A function of class Area where they are assigned to length and width. Later we find out the area and volume by making use of get_l and get_w function.

```cpp
/* PROG 9.20 DEMO OF TWO LEVEL INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>
class first
{
public :
    void show_f()
    {
        cout<<"Hello from first"<<endl;
    }
};
class second :public first
{
public :
    void show_s()
    {
        cout<<"Hello from second"<<endl;
    }
};
class third : public second
{
public :
void show_t()
{
    show_f();
    show_s();
    cout<<"Hello from third"<<endl;
}
};

void main()
{
    clrscr();
    third t;
    t.show_t();
    getch();
}
```

OUTPUT :
Hello from first
Hello from second
Hello from third

![](img/ad5299318df8d4d7c6df5eaa86590ea3_441_0.png)

Figure 9.9. Output screen of program 9.20

EXPLANATION : The above program demonstrate 2 level of inheritance. The class first is the base class (parent class) for class second (child class) and class second is the base class (parent class) for class third (child class). In turn class first is the grandfather of class third (grand child). In show_t function of class third show_s is inherited directly from class second but show_f is inherited indirectly from class first through class second.

```cpp
/*PROG 9.21 FINDING MAXIMUM OF THREE CLASS'S DATA */

#include <iostream.h>
#include <conio.h>
class first
{
    protected :
        int fa;
    public :
        void input_f( )
        {
            cout << "Enter the value for fa :="; 
            cin >> fa;
        }
};
class second :public first
{
    protected :
        int sa;
    public :
        void input_s( )
        {
            input_f( );
            cout << "Enter the value for sa :="; 
            cin >> sa;
        }
};
class third :public second
{
    protected :
        int ta;
    public :
        void input_t( )
        {
            input_s( );
            cout << "Enter the value for ta :="; 
            cin >> ta;
        }
        void show( )
        {
            cout << "Data of class first fa :    =" << fa << endl;
            cout << "Data of class second sa :=" << sa << endl;
            cout << "Data of class third ta :    =" << ta << endl;
        }
};
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_444_0.png)

The diagram in the figure shows a class, collectible String. It is like a Collectible (something that can be contained in a collection). It is like a String. Multiple inheritance is a good solution to this kind of problem (Where a derived class has attributes of more than one class) because it is easy to form a Collectible Customer, Collectible Windows, and so on. If the properties of either class are not required for a particular application, either class can be used alone or in combination with other classes. Therefore, given the hierarchy depicted in figure as a basic, you can form noncollection strings and collectibles that are not strings. This flexibility is not possible using single inheritance. We present few examples for better understanding point of view.

```cpp
/*PROG 9.22 FINDING POWER FROM BASE AND EXPONENT*/

#include <iostream.h>
#include <conio.h>
#include <stdlib.h>
class base
{
    protected :
        int ba;
    public :
        void input_base()
        {
            cout << "Enter the base :=";
            cin >> ba;
        }
        void show_base()
        {
            cout << "base :=" << ba << endl;
        }
};
class exponent
{
    protected :
        int exp;
    public :
        void input_exp()
        {
            cout << "Enter the exponent :=";
            cin >> exp;
        }
        void show_exp()
        {
            cout << "exponent=" << exp << endl;
        }
};
class power :public base, public exponent
{
    int po;
    public :
    void input()
    {
        input_base ();
        input_exp();
    };
    void show()
    {
        show_base();
        show_exp();
        int i;
        po = 1;
        for(i = 1; i <= exp; i++)
        po = po*ba;
        cout << "power :=" << po << endl;
    }
};
void main()
{
    clrscr();
    power o1;
    o1.input();
    o1.show();
    getch();
}
```

OUTPUT :
Enter the base : =5
Enter the exponent : =3
base :      =5
exponent =3
power :     =125

EXPLANATION : The program is simple. In the base class we have a data member ba which represent base and in the class exponent we have a data member exp which represent exponent. These two classes are inherited by class power which has two function input and show. In the input of this class the base and exponent is called. In the show function we find the power using for loop and display the result.

```cpp
/*PROG 9.23 FINDING TOTAL MARKS FROM INTERNAL AND EXTERNAL MARKS */

#include <iostream.h>
#include <conio.h>
#include <stdlib.h>
class Internal
{
protected :
    int i_marks;
public :
    void input_im()
    {
        cout << "Enter internal marks :=";
        cin >> i_marks;
        if(!(i_marks >= 0 && i_marks <= 60))
        {
            cout << "Invalid Marks";
            exit(0);
        }
    }
    void show_im()
    {
        cout << "Internal marks :=" << i_marks << endl;
    }
};
class External
{
protected :
    int e_marks;
public :
    void input_em()
    {
        cout << "Enter external marks :=";
        cin >> e_marks;
        if(!(e_marks >= 0 && e_marks <= 60))
        {
            cout << "Invalid Marks";
            exit(0);
        }
    }
    void show_em()
    {
        cout << "External marks := " << e_marks << endl;
    }
};
class Total :public Internal, public External
{
    int total_marks;
public :
    void input()
    {
        input_im();
        input_em();
    }
    void show()
    {
        show_im();
        show_em();
        total_marks = i_marks + e_marks;
        cout << "Total Marks := " << total_marks << endl;
    }
};
void main()
{
    clrscr();
    Total tm;
    tm.input();
    tm.show();
    getch();
}
```

OUTPUT :
Enter internal marks : =56
Enter external marks : =35
Internal marks : =56
External marks : =35
Total Marks :   =91

EXPLANATION : For student's internal marks we have a class Internal and for student's external marks we have a class External. The internal marks must be between 0 to 60 and external marks must be between 0 to 40. These two classes are inherited by class total which finds the total marks and display all three marks :

- (a) Internal
- (b) External and
- (c) Total

Note here that i_marks and e_marks are protected so that they can be used inside the total class. They can be modified by the class total. So ideally i_marks and e_marks. Try to make use of this and create a new program yourself.

## → Resolving Ambiguity

In multiple inheritance when two base classes having same name for their functions and data, ambiguity arises when they are used in the derived class. For example, consider the two classes A and B having same function signature for function named show like void show (). Both the classes are inherited in the third class C. Now how class C can use show of A class and show of B class individually. Simply accessing show function in class C creates confusion as to which show we want to refer; show of class A or show of class B. In these situations we can use the scope resolution operator with class names to functions for accessing the function of individual class. Thus inside the member functions of class C we can access show of class A as A :: show() and show of class B as B :: show. If function show is also defined in the class C and all show are public then they can access in the main using an object of C class as :

- C o1;
- o1.A ::show( );      //calls show of A class
- o1.B ::show( );      //calls show of B class
- o1.show( );          // calls show of C class

See the example given below :

```cpp
/*PROG 9.24 RESOLVING AMBIGUITY IN MULTIPLE INHERITANCE */

#include <iostream.h>
#include <conio.h>
class A
{
protected :
    int num;
public :
    void show()
    {
        cout<<"show of A\n";
        cout<<"num of A="<<num<<endl;
    }
};
```
