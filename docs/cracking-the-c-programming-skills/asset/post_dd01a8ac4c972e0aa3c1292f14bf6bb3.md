
- (a) Prints nothing
- (b) Segmentation fault
- (c) Error
- (d) None of the above

Answer: (a) Even void pointers work as normal pointers.

### 11. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
void fun()
{ static int count;
    cout<<count; };
int main()
{ fun();}
```

- (a) 0
- (b) Unpredictable
- (c) Error
- (d) None of the above

Answer: (a) 'static' storage class means that the variable will be stored in memory even after the block completes its execution. The variable will be freed only after the execution of the whole program. If next time the variable is called, it retains the old value.

### 12. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
void fun()
{ static int count;
    cout<<count; };
int main()
{ fun();
    cout<<count; }
```

- (a) 0
- (b) 1
- (c) Error
- (d) None of the above

Answer: (c) Even though 'count' is in memory, it will be accessible only within its scope.

### 13. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
void fun()
{ static int count;
    cout<<count++<<" "; };
int main()
{ fun();
    fun();
    fun(); }
```

- (a) 0 1 2
- (b) 0 0 0
- (c) Error
- (d) None of the above

Answer: (a) As said previously, as 'count' is static it will retain the old value.

### 14. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
void fun()
{ static int count = 0;
    cout<<count++<<" "; };
int main()
{ fun();
    fun();
    fun(); }
```

- (a) 0 1 2
- (b) 0 0 0
- (c) Error
- (d) None of the above

Answer: (a) Repeated declaration of 'static' variable is skipped, so the assignment is also skipped. It works normally.

### 15. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
void fun()
{ static int count;
    count = 0;
    cout<<count++<<" "; };
int main()
{ fun();
    fun();
    fun(); }
```

- (a) 0 1 2
- (b) 0 0 0
- (c) Error
- (d) None of the above

Answer: (b) Here the variable will be reinitialised on every call.

### 22. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
int main()
{ static int c = 9;
  cout<<sizeof(c); }
```

- (a) 4
- (b) 6
- (c) Error
- (d) None of the above

**Answer: (a)** `static` storage class doesn’t affect the size of the variable. It just changes the storage properties of the variable.

### 23. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};
int main()
{ S.c = 8;
  cout<<S.c; }
```

- (a) 8
- (b) 0
- (c) Error
- (d) None of the above

**Answer: (c)** `static` member means, irrespective of the number of objects the member will be only one. It retains common value in a common memory. As it is not associated with any object it cannot be initiated with an object. It should be initiated only by using the class name with `::` operator.

### 24. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c = 8;
};
int main()
{ cout<<sto::c; }
```

- (a) 8
- (b) 0
- (c) Error
- (d) None of the above

**Answer: (c)** Even though the static variable is common to the class, it cannot be initiated within the class.

### 25. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};
int sto::c = 3;
int main()
{ cout<<sto::c; }
```

- (a) 3
- (b) 0
- (c) Error
- (d) None of the above

**Answer: (a)** This is the way of initialising static variable.

### 26. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};
int sto::c = 6;
int main()
{ cout<<S.c; }
```

- (a) 6
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer: (a)** Static variable can be read with separate objects also.

### 27. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
};S;
sto::c = 6;
int main()
{ cout<<S.c; }
```

- (a) 6
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (c) While initializing also type is required. It throws “ ‘c’ in ‘class sto’ and does not name a type”.

### 28. What will be the error thrown by the code? (L4)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    sto()
    { static int c = 4;
    cout<<c; }
};
int main()
{ sto S; }
```

- (a) ISO C++ forbids in-class initialization of member ‘sto::c’
- (b) Undefined reference to ‘sto::c’
- (c) ‘sto’ has no member named ‘c’
- (d) No error

**Answer:** (d) Here the static variable goes into the function. So it is not a class member. So it has no error.

### 29. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
void fun()
{ cout<<m; }
};S;
int student::m;
int main()
{ S.m=9;
  S.fun();}
```

- (a) 9
- (b) 0
- (c) Unpredictable
- (d) Error

**Answer:** (d) This doesn't make the member ‘m’ as static. Instead it throws the error “int student::m” is not a static member of ‘class student’. Static members cannot be added like this. They should be declared inside the class only.

### 30. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int c;
    static int b;
};S;
int sto::b = 6;
int sto::c = &(sto::b);
int main()
{ cout<<*(sto::c); }
```

- (a) 6
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer:** (c) This type of usage is not possible. The ‘&’ and ‘*’ do not go well with static variables. So pointers cannot be static members.

### 31. What will be the error thrown by the code? (L4)

```cpp
#include<iostream>
using namespace std;
class sto
{ public:
    static int *c;
};S;
int sto::*c = NULL;
int main()
{ cout<<sizeof(sto::c); }
```

- (a) ‘c’ was not declared in this scope
- (b) Expected variable before ‘*’ in ‘int sto::*c = NULL’
- (c) Both ‘a’ and ‘b’
- (d) None of the above

**Answer:** (d) It throws no error. It is actually the right way of using static pointers. The output will be ‘8’ as usual.

### 32. What will be the error thrown by the code? (L4)

```cpp
#include<iostream>
using namespace std;
class sto
{
 public:
   static int *c;
};
int sto::*c = NULL;
int main()
{
 cout<<sizeof(sto::*c);
}
```

- (a) ISO C++ forbids pointer of static `sto::c`
- (b) Expected variable before `*` in `sto::*c`
- (c) Expected unqualified id before `*` token
- (d) No error

**Answer:** (c) This usage inside main causes problem.

### 33. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class sto
{
 public:
   static int *c;
   int b;
};
S.b = 6;
int sto::c = &(S.b);
int main()
{
 cout<<sizeof(sto::*c);
}
```

- (a) 6
- (b) 8
- (c) Error
- (d) Unpredictable

**Answer:** (c) Global object member cannot be defined globally. It can be initialised only inside a particular scope.

### 34. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class sto
{
 public:
   static int *c;
   static int b;
};
int sto::b = 6;
int* sto::c = &(sto::b);
int main()
{ cout<<*(sto::c); }
```

- (a) 6
- (b) 0
- (c) Error
- (d) Unpredictable

**Answer:** (a) This works properly.

### 35. What will be the error thrown by the code? (L5)

```cpp
#include<iostream>
using namespace std;
class sto
{
 public:
   static int *c;
   static int b;
};
int main()
{
 S.b = 9;
 int* sto::c = &(S.b);
 cout<<*(sto::c); }
```

- (a) Invalid use of unqualified-name `sto::c`
- (b) Undefined call `sto::c` inside main
- (c) Invalid use of qualified-name `sto::c`
- (d) No error, gives output 9

**Answer:** (c) Usage of `class::member` is not possible inside main.

### 36. What is the output of the code? (L5)

```cpp
#include<iostream>
using namespace std;
class sto
{
 public:
```
