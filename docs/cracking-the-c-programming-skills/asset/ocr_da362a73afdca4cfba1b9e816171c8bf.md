(a) Compilation fault
(b) No error. No output
(c) This is a demo for pure virtual function
(d) None of the above
**Answer: (c)** This is demo for pure virtual function as the base class virtual function equated to zero and has been overridden in the derived class.

**61. What is the output of the following piece of code? (L4)**

```
#include <iostream>
using namespace std;
class Base_class
{
public:
virtual void show() = 0;
};
class Derived_class:public Base_class
{
public:
virtual void show()
{
cout << "\n" << " This is a demo for pure virtual function";
}
};
int main()
{
Base_class *p;
Derived_class obj2;
p = &obj2;
p->show();
return 0;
}
```

+   (a) Compilation fault
+   (b) No error. No output
+   (c) This is a demo for pure virtual function
+   (d) None of the above

**Answer: (c)** This is demo for pure virtual function as the base class virtual function is equated to zero and has been overridden in the derived class.

**62. What is the output of the following piece of code? (L4)**

```
#include <iostream>
using namespace std;
class Base_class
{
public:
virtual void show() = NULL;
};
class Derived_class:public Base_class
{
public:
virtual void show()
{
cout << "\n" << " This is a demo for pure virtual function";
}
};
int main()
{
Base_class *p;
Derived_class obj2;
p = &obj2;
p->show();
return 0;
}
```

+   (a) Compilation fault
+   (b) No error. No output
+   (c) This is a demo for pure virtual function
+   (d) None of the above

**Answer: (a)** Compilation error as NULL is invalid pure specifier. Only 0 is preferred as pure specifier.

**63. What is the output of the following piece of code? (L4)**

```
#include <iostream>
using namespace std;
class Base_class
{
public:
virtual void show() = "ZERO";
```