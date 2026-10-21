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