```
cout<<"NUM OF CLASS SECOND :="<<s.num<<endl;
}

void main()
{
    first f;
    clrscr();
    f.input_first();
    second s;
    f.show(s);
    getch();
}

OUTPUT :
NUM OF CLASS FIRST :=20
NUM OF CLASS SECOND :=400
```

EXPLANATION : In the program we want to create a function in class first which will be friend of class second. As function will be friend of class we can have object of class second in the function of the first class. In the class first we want function show to be friend of class second. As function show takes a parameter of class second, we have to make forward declaration of class second prior to defining class first.

The line
class second; does the same
Note the declaration of this function show in class second.

```
friend void first :: show (second);
```

The line tells the compiler that a function show of class first (due to first ::show) which returns nothing (void) and which takes an argument of class type second by value is a friend second class.

As function show is friend of class second, private members functions of second class can be used in show function only through objects using dot operator. But as the function show is of class first, private data members of class first can be used directly. In the main the function is called using an object of class first and passes an object of class second. In the function num* num (num is of class first) is assigned to num of class second object using a call to function input_second.

```
/*PROG 6.42 WHOLE CLASS AS A FRIEND OF ANOTHER CLASS VER 1*/

#include <iostream.h>
#include <conio.h>
```