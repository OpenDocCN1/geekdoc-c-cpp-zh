```
```cpp
show (one, two, three);
return 0;
}
void show (char x[])
{
cout << x << endl;
}

void show (char x[], char y[])
{ cout << x << endl << y << endl; }
void show (char x[], char y[], char z[])
{
cout << x << endl << y << endl << z << endl;
}
```
```

+   (a) No output.
+   (b) I LOVE INDIA
+       I LOVE INDIA
+       INDIA IS MY COUNTRY
+       I LOVE INDIA
+       INDIA IS MY COUNTRY
+       JAIHIND
+   (c) JAIHIND
+       I LOVE INDIA
+       INDIA IS MY COUNTRY
+   (d) Compilation fault

Answer: (b) This is an example for how number of arguments would be used for identifying appropriate function.

9. Which of the following are inappropriate with respect to function overloading in C++? (L2)

+   (a) Overloading functions is not possible.
+   (b) Overloading operators is not possible.
+   (c) Overloading constructors is not possible.
+   (d) Overloading destructors is not possible.

Answer: a, b and c are possible and are claimed to be not possible in the question. Only destructors cannot be overloaded.

10. What is the output of the following code snippet? (L3)

```
```cpp
#include <iostream>
using namespace std;
void add(int);
void add(int, int);
void add(int, int, int);
int main()
{
    int x = 1;
    int y = 2;
    int z = 3;
    add(x);
    add(x, y);
    add (x, y, z);
    return 0;
}
void add (int a)
{
    cout << a << endl;
}
void add (int a, int b)
{
    cout << a + b << endl;
}
void add (int a, int b, int c)
{
    cout << a + b + c << endl;
}
```
```

+   (a) Syntax error
+   (b) 1, 3, 6
+   (c) Compilation fault
+   (d) None of the above

Answer: (b) is the answer. The number of arguments are different for all the three functions hence, the call will be precise. The output will be 1, 1 + 2 and 1 + 2 + 3 getting 1, 3 and 6.