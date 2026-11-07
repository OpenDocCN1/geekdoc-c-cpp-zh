```
```cpp
// use string version of operator>>()
istream & operator>>(istream & is, Student & stu)
{
    is >> stu.name;
    return is;
}

// use string friend getline(istream &, const string &)
istream & getline(istream & is, Student & stu)
{
    getline(is, stu.name);
    return is;
}

// use string version of operator<<()
ostream & operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << stu.name << ":\n";
    stu.arr_out(os);  // use private method for scores
    return os;
}
```
```

Aside from the private helper method, Listing 14.2 doesn’t require much new code. Using containment allows you to take advantage of the code you or someone else has already written.

# Using the New Student Class

Let’s put together a small program to test the new Student class. To keep things simple, it should use an array of just three Student objects, each holding five quiz scores. And it should use an unsophisticated input cycle that doesn’t verify input and that doesn’t let you cut the input process short. Listing 14.3 presents the test program. Be sure to compile it along with studentc.cpp.

Listing 14.3  use_stuc.cpp

```
```cpp
// use_stuc.cpp -- using a composite class
// compile with studentc.cpp
#include <iostream>
#include "studentc.h"
using std::cin;
using std::cout;
using std::endl;

void set(Student & sa, int n);
```
```