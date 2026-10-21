
## OUTPUT

Burfi has mawa as one of its main ingredient
Kajukati does not have mawa as one of its main ingredient
Jalebee does not have mawa as one of its main ingredient
Rasgulla does not have mawa as one of its main ingredient

## EXPLANATION

The class Sweet declares one pure virtual function mawastatus. Any classes which inherits this class has to redefine this function and tell whether they contain mawa as one of its main ingredients. This class Sweet is inherited by 4 different class viz Burfi, Kajukati, Jalebee and Rasgulla. Each class does provide implementation of function mawastatus. In the main we create an array of pointer ptr of class Sweet type. We also create an object of the 4 derived classes. In the pointer array ptr, we assign the addresses of theses objects.

```
Burfi B;
Kajukati k;
Jalebee J;
Rasgulla R;
Sweet *ptr[4] = {&B,&k,&J,&R};
```

In the for loop when we call the function mawastatus using the pointer array ptr, respective mawastatus function of each class is called.

## 10.8 OBJECT SLICING

Object slicing is a process of removing off the derived portion of the object when an object of derived class is assigned to a base class object. Only the base class data are copied to derived class object. Consider the following two classes :

```
class A
{
public :
int Ax, Ay;
};
class B :public A
{
public :
int Bx;
};
```

Through inheritance public data members Ax and Ay of class A are copied to class B. When in the main we write as :

```
B b1; A a1;
a1 = b1;
```

Only the data members of object **b1** which were inherited from **class A** are assigned to **object a1**. The data member **Bx** of object **b1** is not copied. That is we say that **object b1** was sliced off.

```
/*PROG 10.26 DEMO OF OBJECT SLICING VER 1*/

#include <iostream.h>
#include <conio.h>

class demo
{
public :
    void show_demo()
    {
        cout<<"Hello from show of demo"<<endl;
    }
};
class der_demo :public demo
{
public :
    void show_der()
    {
        cout<<"Hello from show of der_demo"<<endl;
    }
};
void main()
{
    clrscr();
    demo d1;
    der_demo d2;
    d1=d2;
    d1.show_der();
    getch();
}

OUTPUT :
ERROR MESSAGE
‘show_der’ is not a member of ‘demo’
```

**EXPLANATION :** In the **main** function when an **object d2** of derived class **der_demo** is assigned to an object **d1** of **base class demo**. Only the inherited portion of **base class** is assigned to **d1**. Through function are usually not part of the object but a function of one class can be called from object of that class or from objects of derived class. Here from **d1**, we cannot call the function **show_der** of derived class.

## /*PROG 10.27 DEMO OF OBJECT SLICING VER 2*/

```
#include <iostream.h>
#include <conio.h>

class demo
{
public :
    int bx,by;
    demo(int x,int y)
    {
        bx=y;
        by=y;
    }
    demo() {}
};
class der_demo :public demo
{
public :
    int dx;
    der_demo(int x,int y,int z) :demo(x,y),dx(z)
    {
    }
};
void main()
{
    clrscr();
    der_demo d2(10,20,30);
    demo d1;
    d1=d2;
    cout << d1.bx << "\t" << d1.by << "\t" << d1.dx;
    getch();
}
```

# OUTPUT :

ERROR MESSAGE
‘dx’;is not a member of demo

# EXPLANATION :

The class demo consists of two data members bx and by and der_demo has just one data member dx. When in the main we write d1=d2, only the inherited data members bx and by are assigned to object d1. The data member dx from d2 is not assigned to d1. In the effect object d2 gets sliced. So you cannot call dx from an object of demo class.

## 10.9 SOME FACTS ABOUT VIRTUAL FUNCTION

```
/*PROG 10.28 CALLING VIRTUAL FUNCTION EXPLICITLY */

#include <iostream.h>
#include <conio.h>

class first
{
public :
    virtual void show()
    {
        cout<<"In show of first"<<endl;
    }
};
class second :public first
{
public :
    void show()
    {
        cout<<"In show of second"<<endl;
    }
};
void main()
{
    clrscr();
    first f;
    f.show();
    second s;
    s.show();
    getch();
}

OUTPUT :
In show of first
In show of second
```

EXPLANATION : The basic aim of the program is to simply show that virtual functions can be called explicitly using objects of class. virtual mechanism works only in case of pointers to object.

## /*PROG 10.29 PURE VIRTUAL FUNCTION CAN HAVE BODY */

```
#include <iostream.h>
#include <conio.h>
class first
{
public :
    virtual void show( ) =0
    {
        cout<<"In show of first"<<endl;
    }
};
class second :public first
{
public :
    void show( )
    {
        cout<<"In show of second"<<endl;
    }
};
void main( )
{
    clrscr( );
    first *ptr=new second;
    ptr->show( );
    getch( );
}
```

# OUTPUT :

In show of second

# EXPLANATION :

The sole aim of this program is to show that a pure virtual function can have body but in no way we can use this body.

## /*PROG 10.30 CALLING VIRTUAL FUNCTION FROM CONSTRUCTION VER 1*/

```
#include <iostream.h>
#include <conio.h>
class first
{
public :
virtual void silly()
{
    cout<<"Hello from silly of first"<<endl;
}
first ()
{
    silly ();
}
};

class second :public first
{
public :
    void silly()
    {
        cout<<"Hello from silly of second"<<endl;
    }
};
void main()
{
    clrscr();
    (new second);
    getch();
}

OUTPUT :
Hello from silly of first
```

EXPLANATION : In the above program when object of second class is created. First constructor of first class gets called then constructor of second class. In the first class we are calling the function silly which has been overridden in derived class second. As derived class second will be constructed when its constructor would be called. Compiler has at this time no idea of silly function present in second class. So the base class first version of silly is called.

```
/*PROG 10.31 CALLING VIRTUAL FUNCTION FROM CONSTRUCTOR VER 2*/

#include <iostream.h>
#include <conio.h>

class first
{
public :
```

```
virtual void silly( )
{
    cout << “Hello from of first” << endl;
}
first( )
{
    silly( );
}
};
class second :public first
{
public :
    second( )
    {
        silly( );
    }
    void silly( )
    {
        cout << “Hello from silly of second” << endl;
    }
};
void main( )
{
    clrscr( );
    second s;
    getch( );
}

OUTPUT :
Hello from of first
Hello from silly of second
```

**EXPLANATION** : Here it is clear from the program that we are calling silly function from constructor of both the classes. The silly of first class is called from constructor of class first. As silly was defined in the class second and is called from its constructor, silly of second class will be called too. We have simply followed the normal calling of constructor in inheritance.

## 10.10 VIRTUAL DESTRUCTOR

There is no concept of virtual constructor in C++ but a virtual destructor can be in C++. In the normal call sequence of constructor and destructor, they follows the basic rules which have been discussed earlier i.e., constructor of base class is called first and destructor of derived class calls first even the destructor in the base class is virtual. See the program given below for better understanding point of view.

```
/*PROG 10.32 DEMO OF VIRTUAL DESTRUCTOR VER 1*/

#include <iostream.h>
#include <conio.h>

class first
{
public :
    first()
    {
        cout<<"First con called"<<endl;
    }
    virtual ~first()
    {
        cout<<"First des called"<<endl;
    }
};
class second :public first
{
    char *ptr;
public :
    second()
    {
        ptr=new char[10];
        cout<<"Second con called"<<endl;
    }
    ~second()
    {
        cout<<"Second des called"<<endl;
        delete ptr;
    }
};
void main()
{
    clrscr();
    second s;
    getch();
}
```

```
clrscr();
first *f=new second;
delete f;
getch();
}

OUTPUT :
first des called
```

EXPLANATION : As pointer f is of class first type, only the destructor of first class is called. But ideally destructor of second class should get called first, after that destructor would be called, so that memory for string pointer ptr would be de-allocated. The solution is to make destructor of class first as virtual. See the next program.

# /*PROG 10.34 DEMO OF VIRTUAL DESTRUCTOR VER 3*/

```
#include <iostream.h>
#include <conio.h>

class first
{
public :
    virtual ~first( )
    {
        cout<<"First des called"<<endl;
    }
};
class second :public first
{
    char *ptr;
public :
    second( )
    {
        ptr=new char [10];
    }
    ~second ( )
    {
        cout<<"Second des called"<<endl;
        delete ptr;
    }
};
void main( )
```
