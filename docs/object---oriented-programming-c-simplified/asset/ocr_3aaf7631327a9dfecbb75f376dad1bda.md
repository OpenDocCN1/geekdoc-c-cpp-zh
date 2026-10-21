![](bbox=[0.225, 0.139, 0.777, 0.249])

**Figure 7.14.** *After applying `strcat()` for concatenating space.*

![](bbox=[0.225, 0.258, 0.777, 0.317])

`s3 = strcat(s1, s2)`  
`strcat(temp.sname, B.sname);`

**Figure 7.15.** *After concatenating string1 with string2.*

```
/*PROG 7.22 CONSTRUCTING OBJECTS DYNAMICALLY */

#include <iostream.h>
#include <conio.h>

class demo
{
    public :
        demo( )
        {
            cout << “Constructor called” << endl;
        }
};
void main( )
{
    clrscr( );
    demo *ptr = new demo( );
    getch( );
}

OUTPUT :
Constructor called
```

**EXPLANATION :** The new operator can be used for creating objects dynamically. Creation of pointer does not create objects. For the statement `new demo ( )`, object is constructed by allocating memory from heap and calling the default constructor of the class.