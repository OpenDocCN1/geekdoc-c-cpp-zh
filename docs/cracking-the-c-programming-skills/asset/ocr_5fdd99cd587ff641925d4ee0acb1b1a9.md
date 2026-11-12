(c) Compilation fault
(d) None of the above

**Answer: (a)** Since p is a pointer it would hold an address. But, as far as the programmer is concerned it is a garbage value only.

21. What is the output of the following code snippet? (L3)

```
# include <iostream>
using namespace std;
int main ()
{
    int *p;
    cout << "\n" << *p;
    p = 0;
    cout << "\n" << p;
    getchar ();
    return 0;
}
```

+   (a) Garbage and 0
+   (b) 0 and 0
+   (c) Compilation fault
+   (d) None of the above

**Answer: (a)** Before assigning anything to the pointer, it may hold garbage. Here, it would print an address as garbage value.

22. What is the output of the following code snippet?

```
# include <iostream>
using namespace std;
int main ()
{
    int *p;
    p = 0;
    p = NULL;
    cout << "\n" << p;
    getchar ();
    return 0;
}
```

(a) It is illegal to load the pointer twice with NULL. Compilation error
(b) 0
(c) Garbage value
(d) None of the above

**Answer: (b)** Nothing wrong in loading a variable or pointer twice with the same value. Hence, would not return any error.

23. Using new is preferred over Malloc. – True or False. (L3)

**Answer:** True.

24. What is the output of the following code? (L4)

```
# include <iostream>
using namespace std;
int main ()
{
    int a = 10;
    float b = 10.235;
    void *p;
    p= &a;
    cout <<"\n" << *(int *)p;
    p= &b;
    cout <<"\n" << *(float *)p;
    getchar ();
    return 0;
}
```

+   (a) Compilation error
+   (b) 10 and 10.235
+   (c) No output
+   (d) Syntax error

**Answer: (b)** This is referred as void pointer and is a general purpose pointer. It can hold the address of any data type.