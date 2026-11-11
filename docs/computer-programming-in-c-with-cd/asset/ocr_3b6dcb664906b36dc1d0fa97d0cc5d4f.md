Q4. What will be the output of the following program?

```
#include <iostream.h>

int main()
{
    char name [] = "Kogent Solutions";
    char *getchar;
    getchar = name;
    for (int i=0; name[i] != '\0'; i++)
        {
            cout<< *getchar<<"  ";
            getchar++;
        }
    return 0;
}
```

Ans. Output of the preceding program is as follows:

```
K o g e n t   S o l u t i o n s
```

Q5. What will be the output of the following program?

```
#include <iostream>

void display_num(int val)
{
    cout << val << endl;
}
int main()
{
    int MyInt[2], *PtoMyInt;
    MyInt [0] = 40;
    MyInt [1] = 25;
    PtoMyInt = &MyInt [1];
    display_num(*PtoMyInt);
    PtoMyInt--;
    display_num(*PtoMyInt);
    return 0;
}
```

Ans. Output of the preceding program is as follows:

```
25
40
```

Q6. What will be the output of the following program?

```
#include <iostream.h>
#include <string.h>
```