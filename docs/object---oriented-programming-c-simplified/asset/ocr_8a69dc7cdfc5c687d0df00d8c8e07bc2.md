```
{
    sup_input(x*2);
    sub_a=x;
}
void sub_show()
{
    sup_show();
    cout<<"sub_a="<<sub_a<<endl;
}
};
void main()
{
    int i;
    clrscr();
    sub o1;
    cout<<"Enter the data member :=";
    cin>>i;
    o1.sub_input(i);
    o1.sub_show();
    getch();
}

OUTPUT :
Enter the data member : =145
sup_a=290
sub_a=145
```

# EXPLANATION :

In the main we have called only the functions of sub class. The function sup_input is called from sub_input with a value x*2 as argument. Similarly sup_show is called from class sub. So, when sub_input is called from main with value of `i` of int type, it is collected in variable x and the function of base class sup_input is called with value 2*145 (290), where it is assigned to sup_a of super class. When control returns sup_input function the value x is assigned to sub_a. When sup_show is called, it calls sup_show first in its body. When the function sup_show returns after displaying the value of sup_a, the function sup_show displays the value of sub_a.

# /* PROG 9.6 DEMO OF SINGLE LEVEL INHERITANCE VER 6 */

```
#include <iostream.h>
#include <conio.h>

class super
{
```