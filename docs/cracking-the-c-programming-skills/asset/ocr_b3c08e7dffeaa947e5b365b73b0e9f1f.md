+   (a) Compilation fault
+   (b) Run time error
+   (c) address some address
+   (d) None of the above

**Answer: (c)** It is not illegal to use new twice for the same instance. But, it is not a good practice. This code would return the address.

13. What is the output of the following code? (L4)
(Assume address allocation starts from 1000)

```
# include <iostream>
using namespace std;
int main ()
{
    int n=10;
    int *pointer;
    pointer = new (nothrow) int;
    cout<<pointer<< " ,";
    *pointer =n;
    cout<<* pointer<<endl;
    getchar ();
    return 0;
}
```

+   (a) 1000, 10
+   (b) Syntax error as nothing called nothrow is usable.
+   (c) 10, 1000
+   (d) Compilation fault

**Answer: (a)** is the correct answer. Here, nothrow is used by the program to avoid throwing exception. Instead of throwing exception it would give the address allotted as return value or zero if address allocation fails.

14. What is the output of the following code? (L4)
(Assume address allocation starts from 1000)

```
# include <iostream>
```

```
using namespace std;
int main ()
{
    int n=10;
    int *pointer;
    pointer = new (no throw) int;
    cout<<pointer<< " ,";
    *pointer =n;
    cout<<*pointer<<endl;
    getchar ();
    return 0;
}
```

+   (a) 1000, 10
+   (b) Syntax error as nothing called nothrow is usable.
+   (c) 10, 1000
+   (d) Compilation fault

**Answer: (d)** is the answer as it is a compilation fault. Nothrow is a single word and can be written like nothrow.

15. What is the output of the following piece of code? (L4)

```
# include <iostream>
using namespace std;
int main ()
{
    int n=10;
    int *pointer;
    pointer = new (nothrow) float;
    cout<<pointer<< " ,";
    *pointer =n;
    cout<<*pointer<< endl;
    getchar ();

    return 0;
}
```

+   (a) Compilation fault
+   (b) No error will display the address and 10
+   (c) Runtime error
+   (d) None of the above