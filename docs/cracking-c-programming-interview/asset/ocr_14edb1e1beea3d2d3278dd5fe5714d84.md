(b) 21
(c) 19
(d) 15

# 4. What is the output of the following program?

```
#include<stdio.h>
void demo() 
{
    printf("xx");
}
int main() 
{
    void demo();
    void (*fun)();
    fun = demo();
    (*fun)(); // line 4
    fun(); // line 5
    return 0;
}
```

(a) xxxx
(b) yyyy
(c) xx
(d) error- compile time

# 5. What is the significance of prefixing extern before the function declaration?

e.g.
extern int sum(int x, int y, int z)
{
    return x+y+z;
}

# 6. What is the significance of prefixing static before the function declaration?

```
#include<stdio.h>
```