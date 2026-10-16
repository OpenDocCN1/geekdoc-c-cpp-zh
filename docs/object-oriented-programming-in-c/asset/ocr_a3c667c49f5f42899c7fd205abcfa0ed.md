# Object-Oriented Programming with C++

The output of Program 6.4 is shown below

```
id of A: 100
id of B: 100
id of C: 100
id of D: 100
```

> A reference variable has been used as an argument to the copy constructor. We cannot pass the argument by value to a copy constructor.

When no copy constructor is defined, the compiler supplies its own copy constructor.



The constructors can also be used to allocate memory while creating objects. This will enable the system to allocate the right amount of memory for each object when the objects are not of the same size, thus resulting in the saving of memory. Allocation of memory to objects at the time of their construction is known as dynamic construction of objects. The memory is allocated with the help of the new operator. Program 6.5 shows the use of new, in constructors that are used to construct strings in objects.



```
#include <iostream>
#include <string>
using namespace std;

class String
{
  char *name;
  int length;
public:
  String()  // constructor-1
  {
    length = 0;
    name = new char[length + 1];
  }
  String(char *s)  // constructor-2
  {
    length = strlen(s);
  }

(Contd)
```