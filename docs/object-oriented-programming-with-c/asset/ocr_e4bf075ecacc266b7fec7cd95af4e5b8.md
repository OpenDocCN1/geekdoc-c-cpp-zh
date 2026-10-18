```
```cpp
int circleArea(int &r)
{
    return r = pi * r * r;
}
```
```

# ### 3.5 Identify the error in the following program.

```
```cpp
#include <iostream.h>
#include <malloc.h>

char* allocateMemory();

void main()
{
        char* str;
        str = allocateMemory();
        cout << str;
        delete str;
        str = "";
        cout << str;
}

char* allocateMemory()
{
        str = "Memory allocation test, ";
        return str;
}
```
```

# ### 3.6 Find errors, if any, in the following C++ statements.

+   (a) `long float x;`
+   
+   (b) `char *cp = vp;`    // vp is a void pointer
+   
+   (c) `int code = three;`    // three is an enumerator
+   
+   (d) `int *p = new;`    // allocate memory with new
+   
+   (e) `enum (green, yellow, red);`