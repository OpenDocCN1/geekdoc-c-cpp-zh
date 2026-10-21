execution starts from this function. So, this can be put into the user defined function. Our whole discussion will be totally based on user defined functions.

# 5.2 FUNCTION DECLARATION/PROTOTYPING

In C++ each function used must be declared first. The declaration of the function is also termed as prototyping. A function prototype tells the compiler three things about a function :

+   1. **It's name.**
+   2. **Return type.**
+   3. **Number of arguments.**

For example : To write a function for sum which takes two argument of type int and return an int can be written as :

![](bbox=[0.25, 0.365, 0.8, 0.46])

The above statement tells the compiler that sum is a function which accepts two parameters of type int and return type of function is int. We give few example of function.

# /*PROG 5.1 DEMO OF FUNCTION VER 1*/

```
#include <iostream.h>
#include <conio.h>
void main()
{
    void show();
    clrscr();
    show();
}
void show()
{
    cout<<"Hello from show function\n";
}
```

**OUTPUT :**
Hello from show function

**EXPLANATION :** The line void show ( ) is called declaration or prototype of the function. The general syntax is given above :

```
void function_name ();
```