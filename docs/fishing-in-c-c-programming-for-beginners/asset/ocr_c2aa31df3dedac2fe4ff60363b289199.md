Register – Register is a type of variable which give request the compiler to store the variable in a CPU register, if possible else it is declared auto. A Register gives faster read and write access to the variables.

To declare a variable in C++ as register, just add register keyword before the declaration.

E.g.

```
register int a=5
```

+   - Default initial value . Garbage value.

+   - Life . Till the control remains within the block in which the variable is defined.

+   - Scope . Local to the block in which the variable is defined.

+   - Storage . CPU registers.

Extern – This variable is defined outside of the main() and all other functions. Its value can be modified by any of the function.

Consider the following program

```
#include<iostream>
using namespace std;
int a=5;
int display1();
int main()
{
    cout<<a;
    display1();
    cout<<a;
}
int display1()
{
    a=6;
}
```

Its output will be 56 as initially it was assigned 5 then display1() function is called which modifies its value and assign 6 to it. Now, just after function calling, the handle is returned to the main function. Now, when value is displayed there, it shows 6. Here, a is called global variable and accessible to all the functions inside the program.

Consider the following program:

```
#include<iostream>
```