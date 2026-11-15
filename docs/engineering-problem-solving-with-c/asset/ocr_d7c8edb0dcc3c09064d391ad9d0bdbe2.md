The following memory snapshot shows the contents of the two memory locations at the time the cout statements are executed. This memory snapshot also shows the memory address of each of the variables.

```
int a [0xbfff8d8] [1]
int b [0xbfff8d4] [2]
```

We do not usually indicate the memory addresses in these diagrams because the addresses used are system dependent and change with every run of the program.

In the next example, which is a modification to the previous program, there are no initial values given to objects a and b:

```
/**
 * Program chapter9_2
 *
 * This program demonstrates the relationship
 * between objects and addresses.
 */
#include <iostream>//Required for cout
using namespace std;
int main()
{
   // Declare and initialize objects.
   // int a, b;

   // Print the contents and addresses of a and b.
   cout << "a= " << a << " address of a = " << &a << endl;
   cout << "b= " << b << " address of b = " << &b << endl;

   return 0;
}
```

A sample output from this program is the following:

```
a = -1073743608; address of a = 0xbffff8e8
b = 1073784016; address of b = 0xbffff8e4
```

A memory snapshot at the time the cout statements are executed shows a question mark for the contents of the memory locations because the variables have not been initialized. However, memory has been allocated for the variables, thus the memory addresses for each of the variables has been established.

```
int a [0xbfff8e8] [?]
int b [0xbfff8e4] [?]
```

While we see that there are values in the variables, even though we have not assigned any in the program, we should not assume anything about these values. This example illustrates the importance of being sure that a program initializes an object before using its value in other statements in a program.