```
// workdata.cpp

#include <iostream>
#include <string.h>
#include "Workdata.h"

using namespace std;

Workdata::Workdata(char *nm, char *ad, char *oc, int ag, int dp,
                   int jc) : Employee(nm, ad, ag, dp, jc) {
    occupation = new char[strlen(oc)+1];
    strcpy(occupation, oc);
}

void Workdata::display() {
    Employee::display();
    cout << occupation << endl;
}
```

Class Workdata is a derived class that inherits from the public base class Employee. The base class for this derived class can either be private, protected, or public. More on this later.

A derived class will inherit all the data members and member functions of its base class and can declare some of its own. The member functions of the derived class can see the public and protected data members of the base class, but not the private data members.

The base class member functions cannot see the data members of any of its derived classes. How could it? The base class has no idea what classes may be derived from it. The derived class can only indirectly access the private data members of the base class by using the protected or public member functions of the base class.

Note that the derived class has a constructor with 6 arguments, although the class has only declared one data member of its own:

```
char *occupation;
```

One argument is used to give occupation a value, while the remaining five arguments are used to initialize the memory inherited from the base class. More on this later when we discuss base class initializations. So the constructor for