```
```cpp
void fun()
{ cout<< b<< " "; }
};
    class dev1 : virtual public base
{ }S;
class dev2 : virtual public base
{ }D;
class dev3 : public dev1, public dev2
{ }E;
    int main()
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```
```

(a) 3 2 5          (b) Unpredictable
(c) Error          (d) None of the above

**Answer: (c)** This is possible. But inheritance will be in private mode. So 'D.base::b' is inaccessible.

101. What is the output of the code? (L4)

```
```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
    void fun()
    { cout<< b<< " "; }
};
    class dev1 : virtual public base
{ public:
    int b; }S;
class dev2 : virtual public base
{ }D;
class dev3 : public dev1, public dev2
{ }E;
    int main()
```
```

```
```cpp
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```
```

(a) 0 2 5
(b) Unpredictable, depends on the compiling environment
(c) Error
(d) None of the above

**Answer: (d)** It prints '0 3 0 '. When calling to variable, the compiler points to the variable that is closest in hierarchy. So in 'E.b' the value initialized is 'dev1::b' and not 'base::b'. So while 'base::fun()' is called 0 is printed and not 5.

102. What is the output of the code? (L4)

```
```cpp
#include<iostream>
using namespace std;
class base
{ public:
    int b;
    void fun()
    { cout<< b<< " "; }
};
    class dev1 : public base
{ public:
    int b; }S;
class dev2 : public base
{ }D;
class dev3 : public dev1, public dev2
{ }E;
    int main()
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```
```