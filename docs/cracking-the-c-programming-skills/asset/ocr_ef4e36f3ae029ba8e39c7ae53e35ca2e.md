**Answer: (d)** It throws `class base` is inaccessible. This is because static variables are not inherited.

+   (a) 9 8			(b) 9 0
+   (c) Unpredictable		(d) Error

**Answer: (a)** Even though two `public` blocks have been defined, both the blocks are inherited.

**43.** What will be the error thrown by the code? (L5)

```
```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b; };
class dev private base
{ public:
      void fun()
      { b = 2;
        cout<< b; }
};
int main()
{ D.fun(); }
```
```

+   (a) Expected unqualified-id before `private`
+   (b) Expected `:` or `{` before `private`
+   (c) Invalid start of access block `private`
+   (d) None of the above

**Answer: (a)** `:` is very important in inheritance.

**45.** What is the output of the code? (L4)

```
```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b;
  protected:
      int c; };
class dev : public, protected
base
{ public:
      void fun()
      { b = 9;
        c = 7;
        cout<<b<< " "<<c; }
}D;
int main()
{ D.fun(); }
```
```

+   (a) 9 7			(b) Unpredictable
+   (c) Error			(d) None of the above

**Answer: (c)** A class cannot be inherited with multiple access modes.

**44.** What is the output of the code? (L4)

```
```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b;
  private:
      int v;
  public:
      int c; };
class dev : public base
{ }D;
int main()
{ D.b = 9;
  D.c = 8;
  cout<<D.b<< " "<<D.c; }
```
```

**46.** What will be the error thrown by the code? (L5)

```
```cpp
#include<iostream>
using namespace std;
class base
{ public:
      int b;
  protected:
      int c; };
class dev : public, protected base
{ public:
      void fun()
      {
```
```