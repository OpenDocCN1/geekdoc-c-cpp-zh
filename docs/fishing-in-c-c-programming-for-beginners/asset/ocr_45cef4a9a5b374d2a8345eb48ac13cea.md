```
}
return 0;
}
```

Output

12

The continue statement place the cursor at the increment statement in for loop i.e. third statement of for loop. So, i is never displayed, always the value stored in i is displayed.

Consider the following program

```
#include<iostream>
using namespace std;
int main()
{
    int i=1;
    do
    {
    cout<<i;
    continue;
    i++;
    }while(i<5);
}
```

Output of the above code will be: