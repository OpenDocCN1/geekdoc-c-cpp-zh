Answer: (a) Compilation fault. Pointer is of type integer and compiler cannot convert float to integer in assignment and vice versa.

16. Null pointer is same as the void pointer. – True or False.

Answer: False – Both are significantly different.

17. What is the output of the following piece of code? (L3)

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    int *p;
    p = NULL;
    cout << "\n" << p;
    getchar ();
    return 0;
}
```
```

+   - (a) invalid use of pointer error
+   - (b) Runtime error
+   - (c) 0
+   - (d) None of the above

Answer: (c) This is a proper code and the NULL assigned to a pointer makes the pointer NULL pointer. It is very much legal to do this way of assignment and will prevent garbage from entering the pointer.

18. What is the output of the following piece of code? (L3)

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    int *p;
    p = null;
    cout << "\n" << p;
    getchar ();
    return 0;
}
```
```

+   - (a) Compilation error
+   - (b) Runtime error
+   - (c) 0
+   - (d) None of the above

Answer: (a) is the answer as it can be only NULL and not null.

19. What is the output of the following code snippet? (L2)

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    int *p;
    p = 0;
    cout << "\n" << p;
    getchar ();
    return 0;
}
```
```

+   - (a) Compilation error
+   - (b) Runtime error
+   - (c) 0
+   - (d) None of the above

Answer: (c), This is another way of keeping the pointer safe from garbage. This is also a form of NULL pointer.

20. What is the output of the following code snippet? (L3)

```
```cpp
# include <iostream>
using namespace std;
int main ()
{
    int *p;
    cout << "\n" << p;
    p = 0;
    cout << "\n" << p;
    getchar ();
    return 0;
}
```
```

+   - (a) Garbage and 0
+   - (b) 0 and 0