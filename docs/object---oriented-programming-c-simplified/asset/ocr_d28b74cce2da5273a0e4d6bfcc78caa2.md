# OUTPUT :

num = 15
num = 20
num = 45
num = 30

# EXPLANATION : Note how we have initialized array of objects.

```
demo d[] = {
    demo(15),
    demo(20),
    demo(45),
    demo(30),
};
```

Each demo(x); (x may have any int value) creates an object in array by calling default constructor. The sizeof(d) gives total size of array and sizeof(demo) gives size of an object. Dividing first by second gives number of objects in the array. Later we display value of num for all objects using show( ) function.

```
/* PROG 7.12 INITIALIZING ARRAY OF OBJECTS VER 2 */

#include <iostream.h>
#include <conio.h>
#include <string.h>

class demo
{
    char name[20];

public :
    demo(char s[20])
    {
        strcpy(name, s);
    }

    void show()
    {
        cout << name << endl;
    }
};
```