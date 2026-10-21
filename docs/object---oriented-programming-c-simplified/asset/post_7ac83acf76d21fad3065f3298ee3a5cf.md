
# /*PROG 10.21 DEMO OF PURE VIRTUAL FUNCTION VER 4*/

```
#include <iostream.h>
#include <conio.h>
class first
{
public :
    void virtual show( ) =0;
};
class second :public first
{
public :
    void show( )
    {
        cout<<"Show of second"<<endl;
    }
};
class third :public first
{
public :
    void show( )
    {
        cout<<"Show of third"<<endl;
    }
};
void main( )
{
    clrscr( );
    second s;
    third t;
    int i;
    first &ref1 =s;
    first &ref2 =t;
    ref1.show( );
    ref2.show( );
    getch( );
}
```

# OUTPUT :

Show of second

Show of third

EXPLANATION : The program is similar to previous one with the difference that instead of pointer we have created two reference variables of class first type and in them assigned the reference object of class second and class third as shown below :
first & ref1 = s;
first & ref2 = t;
So when ref1.show () ; executes show of class second is called and when ref2.show () ; executes show of class third is called.

```
/*PROG 10.22 DEMO OF PURE VIRTUAL FUNCTION VER 5 */
#include <iostream.h>
#include <conio.h>

class first
{
public :
void virtual show() =0;
void disp()
{
cout << "Display of first" << endl;
}
virtual void silly ()
{
cout << "Silly of first" << endl;
}
};

class second :public first
{
public :
void show ()
{
cout << "Show of second" << endl;
}
void disp ()
{
cout << "Display of second" << endl;
}
};

class third :public first
{
public :
void show ()
{
cout << "Show of third" << endl;
}
void disp ()
{
cout << "Display of third" << endl;
}
};
```

```
public :
    void show( )
    {
        cout<<"Show of third"<<endl;
    }
    void silly( )
    {
        cout<<"silly of third"<<endl;
    }
};

void main( )
{
    clrscr( );
    second s;
    third t;
    int i;
    first *ptr[ ] ={&s,&t};
    for(i=0;i<2;i++)
    {
        ptr[i]->show( );
        ptr[i]->silly( );
        ptr[i]->disp( );
    }
    getch( );
}
```

# OUTPUT :

Show of second
Silly of first
Display of first
Show of third
silly of third
Display of first

EXPLANATION : The program demonstrates the fact that apart from creating a pure virtual function to make a class as an abstract, we may write simply ordinary function also in an abstract class. In the class first there are three functions :

+   (a) show( ) which is pure virtual function,
+   (b) disp ( ) which is an ordinary function
+   (c) silly ( ) which is a virtual function.

## Object-Oriented Programming C++ Simplified

The class second provides implementation of function show and overriding function disp. The class third also provide implementation of function show and overrides silly function which was in class first.

In the main we assign addresses of object of class second and class third to an array of pointer of first class as :

```
first *ptr [] = (&s, &t);
```

In the for loop for i=0; ptr[0] refers to an object of second class type now for the following function calls.

```
ptr[0]->show( );
ptr[0]->silly( );
ptr[0]->disp ( );
```

show of class second will be called as it is quite obvious from the code. Silly was virtual in class first and was not overridden in class second so silly of class first will be called. disp was not overridden in class second and disp was not virtual in class first, so disp of class first will be called.

Now for i = 1, ptr[1] refers to an object of third class type. For the following function calls

```
ptr[1]->show();
ptr[1]->silly();
ptr[1]->disp();
```

```
/*PROG 10.23 FINDING FLYING STATUS OF VARIOUS INSECTS */
#include <iostream.h>
#include <conio.h>

class Insect
{
public :
	virtual void flystatus()=0;
};
class Cockroach :public Insect
{
public :
	void flystatus()
	{
		cout << "Cockroach can fly" << endl;
	}
};
```

```
class Termite :public Insect
{
public :
    void flystatus( )
    {
        cout<< "Termite cannot fly"<<endl;
    }
};
class Grasshopper :public Insect
{
public :
    void flystatus( )
    {
        cout<< "Grasshopper can fly"<<endl;
    }
};
class Ant : public Insect
{
public :
    void flystatus( )
    {
        cout<< "Ant cannot fly"<<endl;
    }
};
void main( )
{
    clrscr( );
    Insect *ptr[4];
    ptr[0]=new Cockroach;
    ptr[1]=new Termite;
    ptr[2]=new Grasshopper;
    ptr[3]=new Ant;
    for(int i=0;i<4;i++)
        ptr[i]->flystatus( );
    getch( );
}

OUTPUT :
Cockroach can fly
Termite cannot fly
Grasshopper can fly
Ant cannot fly
```

**EXPLANATION** : The class **Insect** declares one **pure virtual function flystatus**. Any class which inherits this class has to redefine this function and tell his/her flying status *i.e.*, whether he/she can fly or not. This class **Insect** is inherited by **4 different classes** viz **Cockroach, Termite, Grasshopper** and **Ant**. Each class does provide implementation of function **flystatus**. In the **main** function we create an array of pointer **ptr** of class **Insect** type. In each location of this array we assign dynamically created objects of various derived classes as shown:

```
ptr[0] = new Cockroach;
ptr[1] = new Termite;
ptr[2] = new Grasshopper;
ptr[3] = new Ant;
```

In the **for** loop when we call **flystatus** function using this pointer array **ptr**, respective **flystatus** functions of each class is called.

```
/*PROG 10.24 TO FIND THE COLOR OF VEGETABLE AND WHERE THEY GROW*/

#include <iostream.h>
#include <conio.h>

class Vegetable
{
public :
    virtual void color( ) = 0;
    virtual void wh_grow( ) = 0;
};
class Spinach :public Vegetable
{
public :
    void color( )
    {
        cout << "Color of spinach is green" << endl;
    }
    void wh_grow( )
    {
        cout << "Spinach grows above ground" << endl;
    }
};
class Potato :public Vegetable
{
public :
    void color( )
    {
        cout << "Color of Potato is white" << endl;
    }
```

```
void wh_grow()
{
    cout<<"Potato grows underground"<<endl;
}
};
class Onion :public Vegetable
{
public :
    void color()
    {
        cout<<"Color of Onion is red "<<endl;
    }
    void wh_grow()
    {
        cout<<"Onion grows underground"<<endl;
    }
};
class Tomato :public Vegetable
{
public :
    void color()
    {
        cout<<"Color of Tomato is red"<<endl;
    }
    void wh_grow()
    {
        cout<<"Tomato grows above ground"<<endl;
    }
};
void main()
{
    clrscr();
    Vegetable *ptr[4];
    ptr[0]=new Spinach;
    ptr[1]=new Potato;
    ptr[2]=new Onion;
    ptr[3]=new Tomato;
    for(int i=0;i<4;i++)
    {
        ptr[i]->color();
        ptr[i]->wh_grow();
```

## Object-Oriented Programming C++ Simplified

```
}

getch( );

}
```

+   OUTPUT :
+   Color of spinach is green
+   Spinach grows above ground
+   Color of Potato is white
+   Potato grows under ground
+   Color of Onion is red
+   Onion grows under ground
+   Color of Tomato is red
+   Tomato grows above ground

The class vegetable declares two pure virtual functions. The function color is for finding the color of the vegetable and wh_grow for finding where the vegetable grows underground or above ground. Any class which inherits the Vegetable class has to redefined these functions and tell what the color of vegetable is and where it grows. This class Vegetable is inherited by 4 different classes viz Spinach, Potato, Onion and Tomato. Each class does provide implementation of both the functions. In the main we create an array of pointer of class Vegetable type. In each location of this array we assign dynamically created objects of various derived classes as shown :

ptr[0]=new Spinach;
ptr[1]=new Potato;
ptr[2]=new Onion;
ptr[3]=new Tomato;

/*PROG 10.25 CHECKING WHETHER SWEET CONTAINS MAWA AS ITS MAIN INGREDIENT */
#include <iostream.h>
#include <conio.h>

class Sweet 
{
public :
virtual void mawastatus( ) = 0;
};

class Burfi :public Sweet 
{
public :
void mawastatus( )
{
}
}
```

```
cout<<"Burfi has mawa as one of its main ingredient"<<endl;
}
};
class Kajukatli :public Sweet
{
public :
    void mawastatus( )
    {
        cout<<"Kajukatli does not have mawa as one of its main ingredient"<<endl;
    }
};
class Jalebee :public Sweet
{
public :
    void mawastatus( )
    {
        cout<<"Jalebee does not have mawa as one of its main ingredient"<<endl;
    }
};
class Rasgulla :public Sweet
{
public :
    void mawastatus ( )
    {
        cout<<"Rasgulla does not have mawa as one of its main ingredient "<<endl;
    }
};
void main( )
{
    clrscr( );
    Burfi B;
    Kajukatli k;
    Jalebee J;
    Rasgulla R;
    Sweet *ptr[4]={&B,&k,&J,&R};
    for(int i=0;i<4;i++)
    {
        ptr[i]->mawastatus( );
    }
    getch( );
}
```
