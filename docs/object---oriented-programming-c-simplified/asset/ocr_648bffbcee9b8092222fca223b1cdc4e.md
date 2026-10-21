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
class Spanich :public Vegetable
{
public :
    void color( )
    {
        cout << “Color of spinach is green” << endl;
    }
    void wh_grow( )
    {
        cout << “Spinach grows above ground” << endl;
    }
};
class Potato :public Vegetable
{
public :
    void color( )
    {
        cout << “Color of Potato is white” << endl;
    }
```