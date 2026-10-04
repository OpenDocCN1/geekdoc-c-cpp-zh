Using the correspondence between pointers and subscripts shown in Figure 12.13, the array elements accessed in Program 12.4 with subscripts can now be accessed with pointers, which is done in Program 12.5.

# Program 12.5

```
#include <iostream>
using namespace std;

int main()
{
    const int ARRAYSIZE = 5;

    int *gPtr; // declare a pointer to an int
    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    gPtr = &grade[0]; // store the starting array address
    for (i = 0; i < ARRAYSIZE; i++)
        cout << "\Element " << i << " is " << *(gPtr + i);

    cout << endl;

    return 0;
}
```

The following display is produced when Program 12.5 runs:

+   - Element 0 is 98
- Element 1 is 87
- Element 2 is 92
- Element 3 is 79
- Element 4 is 85

Notice that this display is the same as Program 12.4's display. The method used in Program 12.5 to access array elements simulates how the compiler references array elements internally. The compiler automatically converts any subscript by a programmer to an equivalent pointer expression. In this case, the declaration of gPtr includes the information that integers are pointed to, any offset added to the address in gPtr is scaled automatically by the size of an integer. Therefore, *(gPtr + 3), for example, refers to the address of grade[0] plus an offset of 12 bytes (3 * 4), assuming sizeof(int) = 4. This result is the address of grade[3] shown in Figure 12.13.