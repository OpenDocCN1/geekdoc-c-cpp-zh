Solution of this program will clear your doubt that just after continue statement, whether handle reaches to while(i<5) or whether it reaches to i=10. This means continue; statement places the cursor at the condition not to the first statement inside the while loop.

Consider the following program

```
#include<iostream>
using namespace std;
int main()
{
    int num=5;
    switch (num)
    {
        case 1: cout<<"1";
        case 5: cout<<"5";
            continue;
        case 6: cout<<"6";
    }
}
```

In this program, you will see a compile error “continue without a loop”. This is because continue can be used only within a loop. While break can be used within loops and switch case only. Consider the following source code

```
#include<iostream>
using namespace std;
int main()
{
    int num=5;
    break;
    cout<<"Now I am executed";
}
```

This program will generate an error “Break statement not within loop or switch”