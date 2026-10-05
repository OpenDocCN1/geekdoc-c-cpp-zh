# Introduction to C++

Especially, you must remember that the expression on the left of the assignment operator must be capable of being evaluated at a valid address at which data can be written.
Now, let us study reference variables. A reference variable is nothing but a reference for an existing variable. It shares the memory location with an existing variable. The syntax for declaring a reference variable is as follows:

```
<data-type> & <ref-var-name>=<existing-var-name>;
```

For example, if 'x' is an integer-type variable and we want to declare iRef as a reference to it the statement is as follows:

```
int &iRef=x;
```

iRef is a 'x'. This means that iRef and 'x' have separate entries in the OS, their addresses are actually the same!
Thus, a change in the value of 'x' will naturally reflect in iRef and vice versa.
Listing 1.16 illustrates this.

Listing 1.16 Reference variables

```
/*Beginning of reference01.cpp*/
#include<iostream.h>
void main() {
    int x;
    x=10;
    cout<<x<<endl;
    int &iRef=x;
    iRef=20;
    cout<<x<<endl;
    x++;
    cout<<iRef<<endl;
}//iRef is a reference to x
//same as x=10;
//same as iRef++;
/*End of reference01.cpp*/
```

Output
10
20
21

Reference variables must be initialized at the time of declaration (otherwise the compiler will not know what address it has to record for the reference variable).
Reference variables are variables in their own right. They just happen to have the address of another variable. After their creation, they function like any other variable.
We have just seen what happens when a value is written into a reference variable. The value of a reference variable can be read in the same way as the value of an ordinary variable is. Listing 1.17 illustrates this.

Listing 1.17 Reading the value of a reference variable

```
/*Beginning of reference02.cpp*/
#include<iostream.h>
void main() {

```