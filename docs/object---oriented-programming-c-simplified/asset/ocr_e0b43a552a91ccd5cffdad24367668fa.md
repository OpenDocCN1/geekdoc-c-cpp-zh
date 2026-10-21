```
friend char* toupper(demo d)
{
 static char temp[15];
 strcpy(temp,strupr(d.str));
 return temp;
};
void main()
{
 demo F;
 clrscr();
 F.input("hari mohan");
 cout << "String in upper case \n";
 cout << toupper(F);
 getch();
};

OUTPUT :
String in upper case

HARI MOHAN
```

This is another example of friend function with single class. Note the function is declared and defined in the class itself. This can be done as function toupper is friend of demo class only. In the friend we use a static char array temp of size 15. We convert the original string (data member) str to uppercase using built-in string function strupr and copy it to temp. As we cannot return address of the local variable (local variable die when control goes out of block) we have declared array temp as static.

The above two programs could have been written with the use of friend function by simply writing the function within the class as their part. The real use of friend is visible where we have more than one class and we want friend function to be friend of both the class(in case of two class) so data members of both the classes can be accessed and processing can be done in the friend function.

```
/*PROG 6.39 FINDING MAXIMUM OF TWO DATA OF TWO DIFFERENT CLASS WITH FRIEND FUNCTION */
#include <iostream.h>
#include <conio.h>
class second;
class first
{
 int fx;
```