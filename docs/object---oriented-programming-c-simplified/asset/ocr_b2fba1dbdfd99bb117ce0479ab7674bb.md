![](bbox=[0.32, 0.14, 0.67, 0.32])

Figure 3.42. Output screen of program.

EXPLANATION : Initially numbers of elements are taken is n. The first number is taken outside the loop and assumed to be maximum; this number is stored in max. Then remaining numbers are taken inside the loop. On each iteration the number is compared with the max, if the max is less than number taken then number will be the maximum one. This is checked through if statement. In the end when control comes out from while loop max is displayed.

# Break Statement

Break statement is used to come out early from loop without waiting for the condition to become false. We have seen one such usage of break in the switch-case statements. When the break statement is encountered in the while loop or any of the loops which will see later, the control immediately transfers to first statement out of the loop i.e., loop is exited prematurely. If there is nesting of loops the break will exit only from the current loop containing it.

Let’s write some programs which make use of break statement.

```
/*PROG 3.42 DEMO OF BREAK STATEMENT*/

#include <iostream.h>
void main()
{
    int x =1;
    while(x <= 5)
    {
    if(x == 3)
    break;
    cout << "Inside the loop x=" << x << endl;
    x ++;
    }
    cout << "Outside the loopx=" << x << endl;
}
```