**EXPLANATION :** In the program we are swapping the data members of two classes **first** and **second** using friend function. The function is a Friend of both the classes and accepts **first** argument of class type first and **second** argument of class type second, both by reference. If we do not pass argument by reference then swapping will be done on local variables of type class first and class second. So changes won't be reflected back to object **F** and **S** in **main.**

```
/* PROG 6.41 FUNCTION OF ONE CLASS FRIEND OF ANOTHER CLASS */

#include <iostream.h>
#include <conio.h>

class second;
class first
{
    int num;
public :
    void input_first()
    {
        num = 20;
    }
    void show(second);
};

class second
{
    int num;
public :
    void input_second(int x)
    {
        num = x;
    }
    friend void first ::show(second);
};
void first ::show(second s)
{
    cout << "NUM OF CLASS FIRST := " << num << endl;
    s.input_second(num*num);

```