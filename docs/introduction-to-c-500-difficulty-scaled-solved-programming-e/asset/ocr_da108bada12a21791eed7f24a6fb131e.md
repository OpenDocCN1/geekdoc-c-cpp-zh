# 21 • More about Inheritance 709

```
public:
  C() : v(10) {}
  void show() const { std::cout << v << '\n'; }
  };
```

```
int main()
{
  C c;
  c.p = 10;
  c.show("test");
  return 0;
}
```

Answer: The first error is when c is created. The error is that since no default constructor is defined in A, the A sub-object cannot be constructed. If we had the existing constructor there would be no problem. For example, C(): A(5), v(10){}. The second error is when p is accessed. Both the A and B classes contain a variable with the same name p, the compiler does not know which of the two to access. For example, if we wrote c.p = 10; the third error is when calling the show(). The show() of the C class hides the show() of the B class. So, if we want to call the show() of the C class we have to call c.show(), while for the show() of the B class we have to write B::show("test");

C.21.2 Define the A and B classes and the C class which is derived with public access from A and B. Define the D and E classes derived with public access from C. Finally, define the F class derived with public access from D and E. Suppose that an F object is created (e.g., f). F contains only one sub-object of A and B. In what order do you think the sub-objects of the classes will be created and destroyed? Write a program that implements the above inheritance scheme. Each class should contain a constructor and a destructor that display messages so you can verify your answer about the order in which the objects are created and destroyed.

```
#include <iostream>
using std::cout;
```

```
class A
{
public:
  A() { cout << "A()"; }
  virtual ~A() { cout << "~A()"; }
}
```

```
class B
{
public:
  B() { cout << "B()"; }
  virtual ~B() { cout << "~B()"; }
}
```

```
class C : virtual A, virtual public B
{
public:
  C() { cout << "C()"; }
  ~C() { cout << "~C()"; }
}
```