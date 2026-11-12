```
```cpp
};S;
sto::c = 6;
int main()
{ cout<<S.c; }
```
```

(a) 6 (b) Unpredictable
(c) Error (d) None of the above

**Answer:** (c) While initializing also type is required. It throws “ ‘c’ in ‘class sto’ and does not name a type”.

28. What will be the error thrown by the code? (L4)

```
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
```

(a) ISO C++ forbids in-class initialization of member ‘sto::c’
(b) Undefined reference to ‘sto::c’
(c) ‘sto’ has no member named ‘c’
(d) No error

**Answer:** (d) Here the static variable goes into the function. So it is not a class member. So it has no error.

29. What is the output of the code? (L3)

```
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
```

(a) 9 (b) 0
(c) Unpredictable (d) Error

**Answer:** (d) This doesn't make the member ‘m’ as static. Instead it throws the error “int student::m” is not a static member of ‘class student’. Static members cannot be added like this. They should be declared inside the class only.

30. What is the output of the code? (L2)

```
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
```

(a) 6 (b) Unpredictable
(c) Error (d) None of the above

**Answer:** (c) This type of usage is not possible. The ‘&’ and ‘*’ do not go well with static variables. So pointers cannot be static members.

31. What will be the error thrown by the code? (L4)

```
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
```

(a) ‘c’ was not declared in this scope
(b) Expected variable before ‘*’ in ‘int sto::*c = NULL’