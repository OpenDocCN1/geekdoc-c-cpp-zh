# 7.3 IMPLICIT AND EXPLICIT CALL TO CONSTRUCTOR

Constructor can be called implicitly or explicitly. For example for the above program just explained. All three calls to 3 different constructors were implicit.

```
demo d1;
demo d2 (10, 20);
demo d3 (30);
```

+   > In implicit call we simply write the class name and then object name (in case of default constructor) or pass parameters but does not use the constructor name is any manner.
+   > In explicit call to constructor we explicitly call the constructor by writing its name and passing argument if any. For the above implicit call to constructors explicit calls would be :

```
demo d1 = demo();
demo d2 = demo (10,20);
demo d3 = demo (30);
```

Note on the left side of assignment operator object is created and on the right hand side constructor is called explicitly.

Even when you called a constructor for an object implicitly you can call it explicitly in case you want to provide values to data members or want to modify the values like :
	demo d1(10);

Both a and b gets the value 10. Later you can write if you want d1 = demo (100, 200); which makes a =100 and b =200.

```
/*PROG 7.3 DEMO OF PARAMETERIZED CONSTRUCTOR WITH STRING DATA */

#include <iostream.h>
#include <string.h>
#include <conio.h>

class string
{
char str[20];
public :
string();
string (char s[]);
void show();
};
string ::string()
{
```