
## 9. What is the output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *ptr = NULL;
    delete ptr;
    return 0;
}
```

- (a) An address would be returned if space is available and delete will be executed perfectly.
- (b) Compilation error.
- (c) Syntax error.
- (d) No output. No error.

Answer: (a) Usage of [] is proper with delete and it is acceptable with the code. No error would be thrown.

## 10. What is output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int;
    cout <<"return value" <<pointer <<"\n";
    delete pointer;
    delete pointer;
    return 0;
}
```

- (a) Compilation fault.
- (b) No error and no harm with deleting pointer twice.
- (c) Run time error.
- (d) Warning will be issued.

Answer: (c) Run time error. This may even result in corruption of the code. So it is preferred not to do this.

## 11. What is the output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int;
    cout <<"return value" <<pointer <<"\n";
    delete [] pointer;
    return 0;
}
```

- (a) Compilation fault.
- (b) No error and would return the address allotted.
- (c) Run time error.
- (d) Warning will be issued.

Answer: (b) No error. It is fine with using delete pointer or delete [] pointer.

## 12. What is the output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int;
    pointer = new int;
    cout <<"address " << pointer <<"\n";
    delete pointer;
    return 0;
}
```

- (a) Compilation fault
- (b) Run time error
- (c) address some address
- (d) None of the above

**Answer: (c)** It is not illegal to use new twice for the same instance. But, it is not a good practice. This code would return the address.

## 13. What is the output of the following code? (L4)
(Assume address allocation starts from 1000)

```cpp
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

- (a) 1000, 10
- (b) Syntax error as nothing called nothrow is usable.
- (c) 10, 1000
- (d) Compilation fault

**Answer: (a)** is the correct answer. Here, nothrow is used by the program to avoid throwing exception. Instead of throwing exception it would give the address allotted as return value or zero if address allocation fails.

## 14. What is the output of the following code? (L4)
(Assume address allocation starts from 1000)

```cpp
# include <iostream>
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

- (a) 1000, 10
- (b) Syntax error as nothing called nothrow is usable.
- (c) 10, 1000
- (d) Compilation fault

**Answer: (d)** is the answer as it is a compilation fault. Nothrow is a single word and can be written like nothrow.

## 15. What is the output of the following piece of code? (L4)

```cpp
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

- (a) Compilation fault
- (b) No error will display the address and 10
- (c) Runtime error
- (d) None of the above

Answer: (a) Compilation fault. Pointer is of type integer and compiler cannot convert float to integer in assignment and vice versa.

## 16. Null pointer is same as the void pointer. – True or False.

Answer: False – Both are significantly different.

## 17. What is the output of the following piece of code? (L3)

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

- (a) invalid use of pointer error
- (b) Runtime error
- (c) 0
- (d) None of the above

Answer: (c) This is a proper code and the NULL assigned to a pointer makes the pointer NULL pointer. It is very much legal to do this way of assignment and will prevent garbage from entering the pointer.

## 18. What is the output of the following piece of code? (L3)

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

- (a) Compilation error
- (b) Runtime error
- (c) 0
- (d) None of the above

Answer: (a) is the answer as it can be only NULL and not null.

## 19. What is the output of the following code snippet? (L2)

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

- (a) Compilation error
- (b) Runtime error
- (c) 0
- (d) None of the above

Answer: (c), This is another way of keeping the pointer safe from garbage. This is also a form of NULL pointer.

## 20. What is the output of the following code snippet? (L3)

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

- (a) Garbage and 0
- (b) 0 and 0
- (c) Compilation fault
- (d) None of the above

**Answer: (a)** Since p is a pointer it would hold an address. But, as far as the programmer is concerned it is a garbage value only.

## 21. What is the output of the following code snippet? (L3)

```cpp
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

- (a) Garbage and 0
- (b) 0 and 0
- (c) Compilation fault
- (d) None of the above

**Answer: (a)** Before assigning anything to the pointer, it may hold garbage. Here, it would print an address as garbage value.

## 22. What is the output of the following code snippet?

```cpp
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

- (a) It is illegal to load the pointer twice with NULL. Compilation error
- (b) 0
- (c) Garbage value
- (d) None of the above

**Answer: (b)** Nothing wrong in loading a variable or pointer twice with the same value. Hence, would not return any error.

## 23. Using new is preferred over Malloc. – True or False. (L3)

**Answer:** True.

## 24. What is the output of the following code? (L4)

```cpp
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

- (a) Compilation error
- (b) 10 and 10.235
- (c) No output
- (d) Syntax error

**Answer: (b)** This is referred as void pointer and is a general purpose pointer. It can hold the address of any data type.

## 25. What is the output of the following code? (L4)

```cpp
# include <iostream>
using namespace std;
int main ()
{
    int a = 10;
    float b = 10.235;
    void p;
    p= &a;
    cout <<"\n" << * (int *)p;
    p= &b;
    cout <<"\n" << * (float *)p;
    getchar ();
    return 0;
}
```

- (a) Compilation error
- (b) 10 and 10.235
- (c) No output
- (d) Syntax error

**Answer:** (a) void p is wrong way of initializing pointer. It has to be void *p.

## 26. What is the output of the following code? (L4)

```cpp
# include <iostream>
using namespace std;
int main ()
{
    int a = 10;
    float b = 10.235;
    void *p;
    p = NULL;
    cout <<p;
    getchar ();
    return 0;
}
```

- (a) Compilation fault. Void pointer cannot be allotted with 0.
- (b) 0
- (c) No output, no error
- (d) Runtime error

**Answer:** (b) No harm in allotting void pointer with 0.

## 27. What is the output of the following code? (L4)

```cpp
# include <iostream>
using namespace std;
int main ()
{
    int a = 10;
    float b = 10.235;
    void *p;
    int *q;
    q = NULL;
    p = q;
    cout <<p;
    getchar ();
    return 0;
}
```

- (a) Compilation fault. Void pointer cannot be equaled to null pointer.
- (b) 0
- (c) No output, no error
- (d) Runtime error

**Answer:** (b) It is very similar to the previous question.

## 28. What is the output of the below given piece of code? (L3)

```cpp
# include <iostream>
using namespace std;
int main ()
{
    int a = 10;
    float b = 10.235;
    void *p;
    cout <<sizeof (p) <<"\n";
    getchar ();
    return 0;
}
```
