
### 85. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
    class dev1 : public base
{ };
class base
{  public:
       static int fun; };
class dev2 : public dev1
    { };
int dev2::base::fun = 3;
    int main()
{ cout<<dev2::base::fun; }
```

- (a) 3
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (c)** Base class must be defined before the derived class. It throws the error “class-name before ‘{’ token”.

### 86. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class base
{  public:
       int b; };
    class dev1 : public base
{ }S;
class dev2 : public base
    { }D;
    int main()
{ S.b = 9;
       D.b = 3;
cout<<S.b<< " "<<D.b; }
```

- (a) 9 3
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (a)** This form of inheritance is called hierarchical inheritance.

### 87. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class base
{ };
    class dev1 : public base
{  public:
       int b; }S;
class dev2 : public base
{  public:
       int b; }D;
int main()
{ S.b = 9;
       D.b = 3;
cout<<S.b<< " "<<D.b; }
```

- (a) 9 3
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (a)** Empty classes can also be inherited.

### 88. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{  public:
       void fun()
       { cout<<b<<" "; }
};
    class dev1 : public base
{  public:
       int b; }S;
class dev2 : public base
{  public:
       int b; }D;
    int main()
{ S.b = 9;
       D.b = 3;
       D.fun();
       S.fun(); }
```

- (a) 3 9
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (c)** Undefined variables cannot be used in a function.

### 89. What will be the error thrown by the code? (L5)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    void fun()
    { cout<<b<< " "; }
};
class dev1 : public base
{ public:
    int b; }S;
class dev2 : public base
{ public:
    int b; }D;
int main()
{ S.b = 9;
  D.b = 3;
  D.fun();
  S.fun(); }
```

- (a) ‘b’ undeclared
- (b) ‘b’ was not declared in this scope
- (c) ‘b’ was not declared first use in this function
- (d) None of the above

**Answer: (b)** When ‘fun’ is compiled ‘b’ will not be known. So it throws errors.

### 90. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    void fun()
    { cout<< "fun"; }
};
class dev1 : public base
{ public:
    int b;
    void fun()
    { cout<<b<< " "; } }S;
class dev2 : public base
{ public:
    int b; }D;
int main()
{ S.b = 9;
  D.b = 3;
  D.fun();
  S.fun(); }
```

- (a) 3 9
- (b) fun 9
- (c) Error
- (d) None of the above

**Answer: (b)** In 'dev1', 'fun' is defined. So it accesses the local function. While in 'dev2' it is not defined, so calls the inherited function. But the definitions do not affect each other.

### 91. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
    void fun()
    { cout<< "fun"; }
};
class dev1 : public base
{ public:
    void fun()
    { fun(); } }S;
class dev2 : public base
{ }D;
int main()
{ D.fun();
  S.fun(); }
```

- (a) fun fun
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (d)** In `dev1` call `fun()` is a recursive call and doesn't call the inherited function. On continuous recursion, the stack overflows and segmentation fault occurs.

### 92. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class base
{
public:
    static int b;
    static void fun()
    { cout<< b; }
};

class dev1 : public base
{ }S;

class dev2 : public base
{ }D;

int main()
{ base::dev1::b = 9;
  base::dev2::b = 3;
  dev1::fun();
  dev2::fun(); }
```

- (a) 9 3
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (c)** The hierarchy given is wrong; should be `dev1::base::` and `dev2::base::`.

### 93. Which of the following will be one of the errors thrown by the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{
public:
    static int b;
    static void fun()
    { cout<< b; }
};

class dev1 : public base
{ }S;
class dev2 : public base
{ }D;
int main()
{ base::dev1::b = 9;
  base::dev2::b = 3;
  dev1::fun();
  dev2::fun(); }
```

- (a) Invalid class hierarchy `base::dev2`
- (b) `base::dev2` has not been declared
- (c) `dev2` was not inherited by `base`. Invalid class hierarchy `base::dev2`
- (d) None of the above

**Answer: (b)** The compiler searched for `base` which has inherited `dev2`. As it is not defined it throws not declared. Similarly, it also throws "`base::dev1` has not been declared".

### 94. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{
public:
    int b;
    void fun()
    { cout<< b<< " "; }
};

class dev1 : public base
{ public:
    int b;
}S;

class dev2 : public base
{ }D;

class dev3 : public base
{ }E;

int main()
{ S.b = 3;
  D.b = 2;
  E.b = 5;
  S.fun();
  D.fun();
  E.fun(); }
```

- (a) 3 2 5
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (d)** It prints '0 2 5'.Here '3' in 'dev1' goes to its original member. But 'fun' in 'base' points to its member 'b'. So the inherited member 'b' of 'dev1' doesn't get value. Thus, it gets 0.

### 95. What is the output of the code? (L4)

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
{ int b; }S;
class dev2 : public base
{ }D;
class dev3 : public base
{ }E;
    int main()
{ S.b = 3;
    D.b = 2;
    E.b = 5;
    S.fun();
    D.fun();
    E.fun(); }
```

- (a) 3 2 5
- (b) Prints nothing
- (c) Error
- (d) None of the above

**Answer: (c)** Here also 'S.b' points to the private member of 'dev1' and not the inherited variable. So it is not accessible and throws error.

### 96. What is the output of the code? (L4)

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
{ }S;
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

- (a) 3 2 5
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer: (c)** This type of inheritance is called hybrid or virtual inheritance. It is a combination of multilevel, hierarchical and multiple inheritance. Here, the public members of 'base' are copied twice to 'dev3' one copy from 'dev1' and another from 'dev2'. So it throws some errors.

### 97. Which of the following will be a part of the error thrown by the code? (L5)

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
{ }S;
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

- (a) Request for member ‘b’ is ambiguous.
- (b) Redeclaration of member ‘b’ in ‘dev1’
- (c) Duplicate variable ‘base::b’ in ‘dev1’
- (d) Both ‘a’ and ‘c’

**Answer: (a)** Also it gives a note: "candidates are: int base::b". The same happens for 'base::fun()' also.

### 98. What is the output of the code? (L4)

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

- (a) 3 2 5
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer: (a)** Adding 'virtual' to first level inheritance avoids this duplicating. Now in 'dev3' only one copy of 'base' members will be inherited.

### 99. What is the output of the code? (L4)

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

- (a) 3 2 5
- (b) Unpredictable
- (c) Error
- (d) None of the above

**Answer: (c)** To avoid duplication, virtual must be specified in all duplication possible classes. Gives the same set of errors.

### 100. What is the output of the code? (L4)

```cpp
#include<iostream>
using namespace std;
class base
{ public:
  int b;
```
