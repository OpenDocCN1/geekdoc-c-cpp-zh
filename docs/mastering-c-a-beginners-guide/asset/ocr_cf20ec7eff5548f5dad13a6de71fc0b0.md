if the data member of enum member has not been initialized, then its value is set according to rules stated below:

+   - If it is the first member, then its value is set to 0 otherwise.
+   - It set out the value which is obtained by adding 1 to the previous value of enum data member.

To demonstrate with an example:

```
enum random {
A,
B,
C = 6;
D
}
```

Here, A is set to 0 by default, B will be incremented to 1. However, as C is initialized with 6 so the value of D will be 7.

To demonstrate the initialization of enum data member with user define values and some particular case of initialization:

```
// C# program to illustrate the enum
// data member Initialisation
using System;
namespace ConsoleApplication3 {
// enum declaration
enum days {
    // enum data members
```