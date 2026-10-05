# 17. POLYMORPHISM

You may argue that the compiler could be made to be able to determine in all situations virtual method to call. In the code below:

```
Text t1("ABC\nFancyText t2("XYZ", "", "]", ":");
cout << t1.get() << " " << t2.get() << endl;
Text +p1, +p2;
p1 = &t1;
p2 = &t2;
cout << p1->get() << " " << p2->get() << endl;
```

the compiler cannot deduce p2's type since p2 is assigned to point to t2, and it knows t2's type is FancyText?


Such extended analysis capabilities would further complicate the compiler, and C++ compilers are already readily complicated pieces of software. Attempting to add this method would prove futile anyway because the compiler cannot determine in general which method to invoke. To see why, consider the following code:

```
Text +p;
if (std::rand() % 2 == 0)
    p = new Text("ABC")
else
    p = new FancyText("XYZ", "", "]", ":");
cout << p->get() << endl;
```

This code generates a pseudorandom number at run time. If it generates an even number, it directs p to point to a Text object; otherwise, it directs p to a FancyText object. Which method will this code call, Text::get or FancyText::get? Since the code generates the pseudorandom number at run time, the compiler is powerless to determine the exact object to which p points; the compiler cannot determine which get method to call. The compiler can, however, generate code that jumps to the method at the address stored in p's associated virtual table at the index corresponding to the get method.

Listing 17.3 (vtables.cpp) demonstrates that the vtable pointer occupies space within an object that contains a virtual method.

Listing 17.3: vtables.cpp

```
#include <iostream>
using namespace std;
// A class with no virtual methods
class NoTable {
    int data;
public:
    void set(int d) { data = d; }
    int get() { return data; }
};

// A class with virtual methods
class HasVTable {
    int data;
public:
```