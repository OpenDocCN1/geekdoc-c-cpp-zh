```
```cpp
d1.display();
break;

case 6:
    d1.sort();
    d1.display();
    break;

default:
    cout<<"\n Wrong choice";
}
cout<<"\n Do you want to continue:(Y/N)";
cin>>ans;
} while(toupper(ans)!='N');

getch();
}
```
```

Q50: Use the concept of inheritance to declare two classes to perform data manipulation. Write a program to develop a class for a single dimensional array manipulation. Incorporate functions for reading two single dimensional arrays, sorting them, inserting an element in them, deleting an element from them, merging the values of the two arrays into another single dimensional array and finally to display the array. Incorporate overloaded functions wherever possible. Also include constructors. In the inherited class, include functions for finding the mean, mode, median and standard deviation of every element in the array. Using the project option, make a different project in which these function declarations and definitions are added, and then compile the project to get the results.

Ans: /*First File: Firstdmanip.cpp*/

```
```cpp
# include <iostream.h>
# include <iomanip.h>
# include <conio.h>
# include <ctype.h>
# include <math.h>

class dmanip  //defining a class by the name dmanip
{

    public: //All the functions following this declaration are public.
    int n ;
    int a[100];

    dmanip();
```
```