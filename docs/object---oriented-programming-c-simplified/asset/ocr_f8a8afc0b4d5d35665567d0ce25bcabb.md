```
cout << "After calling change \n";
cout << "x=" << x << endl;
}
void change(int & y)
{
    y ++;
}
```

# OUTPUT :

Before calling change
x=20
After calling change
x=21

EXPLANATION : The declaration void change (int &); tells the compiler that change is a function which accepts a parameter of type int by reference and returns nothing. In the main we call the function as change (x) and pass x by reference. Note in the function call we does not come to know that we are passing value x or reference of x. This is resolved only when function definition is encountered. In the function definition the statement appears as int & y= x i.e., reference of x is assigned to y. Now x and y become one name for the common location. So any changes made in either x or in y become one name for the common location. So any changes made in either x or y actually occurs to the data at location. In the function change we increment the value of y by 1. This change also occurs in x. So, in the main when we display the value of x, 21 will be displayed.

# /*PROG 5.8 REFERENCE VARIABLE AS FUNCTION ARGUMENT SWAPPING TWO VALUES VER 1*/

```
#include <iostream.h>
#include <conio.h>

void main()
{
    void swap(int &, int &);
    int x,y;

    cout << "Enter the two numbers\n";
    cin >> x >> y;

    cout << "Before calling swap\n";
    cout << "x=" << x << "\t" << "y=" << y << endl;
    swap(x,y);
    cout << "After calling swap\n";
```