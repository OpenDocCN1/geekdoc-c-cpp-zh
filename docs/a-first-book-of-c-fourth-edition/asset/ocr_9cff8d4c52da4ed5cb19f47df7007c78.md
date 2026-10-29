both the array’s starting address and the amount of storage each element uses. Calling the fourth element `grade[3]` forces the compiler to make this address computation:

`&grade[3] = &grade[0] + (3 * sizeof(int))`

Remembering that the address operator (`&`) means “the address of,” this statement is read as “the address of `grade[3]` equals the address of `grade[0]` plus 3 times the size of an integer (which is 12 bytes).” Figure 8.12 shows the address computation used to locate `grade[3]`.

![](bbox=[0.222, 0.265, 0.847, 0.436])

**Figure 8.12**  Using a subscript to obtain an address

Because a pointer is a variable used to store an address, you can create a pointer to store the address of the first element of an array. Doing so allows you to mimic the computer’s operation in accessing array elements. Before you do this, take a look at Program 8.5.

# Program 8.5

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    const int ARRAYSIZE = 5;

    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    for (i = 0; i < ARRAYSIZE; i++)
        cout << "\\nElement " << i << " is " << grade[i];

    cout << endl;

    return 0;
}
```
```