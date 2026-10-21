```
```cpp
~second()
{
    cout << "Bye Bye from des of second" << endl;
};

void main()
{
    clrscr();
    second s;
    getch();
}

OUTPUT :
Hello from con
Hello from con of second
Bye Bye from des of second
Bye Bye from des of first
```
```

![](bbox=[0.164, 0.487, 0.837, 0.589])

**Figure 9.13.** *Output screen of program after pressing (Ctrl + F9) and after pressing (Alt + F9)*

**EXPLANATION:** Destructors are called in the reverse order of constructor. So, destructor of second class will be called first then destructor of first class will be called.

```
```cpp
/*PROG 9.33 CONSTRUCTOR IN TWO LEVEL INHERITANCE VER 1*/

#include <iostream.h>
#include <conio.h>

class first
{
    public:
        first()
        {
            cout << "Hello from con of first" << endl;
        }
};
```
```