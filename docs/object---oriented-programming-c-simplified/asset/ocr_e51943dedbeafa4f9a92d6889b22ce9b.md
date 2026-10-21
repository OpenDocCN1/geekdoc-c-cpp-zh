```
public :
    void input(int x)
    {
        num = x;
    }
    int getnum()
    {
        return num;
    }
};
class sub :super
{
public :
    void show()
    {
        input(50);
        cout << "The square of num is"
            << getnum()*getnum() << endl;
    }
};

void main()
{
    clrscr();
    sub obj;
    obj.show();
    getch();
}

OUTPUT :
The square of num is 2500
```

EXPLANATION : The variable num is private in class super. The class sub inherits class super in private mode so num won't be accessible in class sub. Then how can we use num in class sub ? The solution is simple which we have seen earlier. We make a function in public mode which returns in the value of num. We have made function getnum which returns the value of num. Through this getnum we can easily compute the square of the num.

```
/* PROG 9.17 ACCESSING PRIVATE MEMBERS IN PRIVATE INHERITANCE AND MODIFYING THEM */

#include <iostream.h>
#include <conio.h>
```