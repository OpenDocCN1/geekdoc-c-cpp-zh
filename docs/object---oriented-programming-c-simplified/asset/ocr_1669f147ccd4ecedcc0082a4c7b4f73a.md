Age= 21
Class= Third

Student2

Name= Ravi
Age= 24
Class= forth

EXPLANATION : In the student class we have three data members : sname, sage, sclass and two member function. One for inputting the data and second for displaying the data. In the main we have created two objects s1 and s2. As size of class is 24 bytes so two memory blocks of 24 bytes each are allocated for s1 and s2 and both having their different copy of each data members. We input values for these data members in local variables and call functions getdata and showdata for both the object. Note string data has to be assigned through strcpy function. You cannot write sname = sn in function get

# /* PROG 6.5 FINDING FACTORIAL OF A NUMBER */

```
#include <iostream.h>
#include <conio.h>

class Fact
{
    int num;
public :
    void input(int x)
    {
        num = x;
    }
    void getfact();
};

void Fact ::getfact()
{
    long int f = 1;
    short i;
    for(i=1;i<=num;i++)
        f=f*i;
    cout<<"Factorial of"<<num<<" is "<<f<<endl;
}
```