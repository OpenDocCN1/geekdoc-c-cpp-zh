```
```cpp
void main( )
{
    demo *ptr = new demo [5];
    getch( );
}
```

**OUTPUT :**

DEFAULT CONSTRUCTOR  
DEFAULT CONSTRUCTOR  
DEFAULT CONSTRUCTOR  
DEFAULT CONSTRUCTOR  
DEFAULT CONSTRUCTOR
```

**EXPLANATION :** In the program we have created array objects dynamically. The first object is ptr [0], second is ptr [1] and so on. For each object creation default constructor is called.

# 7.7 DESTRUCTOR

A destructor is a member function of the class whose name is same as the name of the class but the preceded with tilde sign (~). The purpose of destructor is to destroy the object when it is no longer needed or goes out of scope. As a very small example of destructor see the program given below :

```
```cpp
/*PROG 7.25 DEMO OF DESTRUCTOR VER 1*/
#include <iostream.h>
#include <conio.h>

class demo
{
public :
    demo( )
    {
        cout << “Constructor called\n”;
    }
    ~demo( )
    {
        cout << “Destructor called” << endl;
    }
};
```
```