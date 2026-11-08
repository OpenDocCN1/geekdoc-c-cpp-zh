```
~~~cpp
*p=25.3;
~~~
```

This now means that x equals 25.3 by making p a pointer, and by pointing p to x. Since p holds x, x is now valued at 25.3 (whatever value p is). If we were to write a complete program which uses a pointer and assigns it a value, we could write the following:

```
~~~cpp
//Full working program
#include <iostream>
#include <stdlib.h>

using namespace std;

int main()
{
double x;
double *p;
p=&x;
*p=25.3
    cout<<x<<endl;

system (“pause”);
return 0;
}
~~~
```

This program points p at x and tells the program that x is valued at 25.3. However, this does not really seem that pointers are very useful. We could simply just use variables and define them (and perhaps use some conditional loops) in order to make our program work. What they are useful for though, is that they give you the ability to manipulate the information and code simply by pointing a variable at another variable. This is where they do become useful.

Let’s say for example that you have written several thousand lines of code. Now, imagine if all of a sudden you need to change the value of 50 of those variables