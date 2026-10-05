# 20 • Inheritance 683

```
B::B(const B b) : A(b) /* It is called with the B b2(b1) statement. The copy
constructor of the base class is called. */
{
  s = new char[strlen(b.s)+1];
  strcpy(s, b.s);
}
```

```
void B::show() const
{
  std::cout << s << '\n';
  A::show();
}
```

Comments: Since we see that both classes contain a pointer for which memory will be remembered we understand that each should contain a constructor, an overloaded copy function, and a destructor. The copy constructor, the overloaded copy function, and the destructor of the derived class must call their base counterparts to handle the base sub-object. This requirement is accomplished with the following actions.

The constructor of the derived class calls the constructor of the base class in the initialization list (another example is C.20.6). The copy function of the derived class uses the scope operator and explicitly calls the respective operator function of the base class to copy the members of the base sub-object (another example is C.20.7). Finally, when an object is destroyed, the destructor of the derived class automatically calls the destructor of the base class.

C.20.9 Define the Company with private members, the name of the public access, the tax number, and the total number of employees. From derive with public access the Software_Cmp and Finance_Cmp classes should contain private members the name of the main product and the number of the programmers. The Finance_Cmp class should contain as private members the name of the main service and the number of the accountants. All classes should contain a constructor to initialize the respective members and the constructors of the derived classes should not explicitly call the constructor of the base class. Also, each class should have its own version of show(), which displays the registered name and the number of employees. Create three objects (one for each class), the pointers to these objects in the vector, and then call show() of each element to make sure that the name contained in each class and the respective number of employees are displayed correctly.

```
int main()
{
  vector<Company*> v;
  ...
  return 0;
}
```

# Answer:

```
#include <iostream>
#include <string>
#include <vector>
using std::cout;
using std::string;
using std::vector;
```