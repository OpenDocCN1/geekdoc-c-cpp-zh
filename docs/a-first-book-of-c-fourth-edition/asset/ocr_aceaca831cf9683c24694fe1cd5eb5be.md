After an object has been dynamically created, it can be accessed only by using the address the new operator returns. So like the this pointer, the newly created object's address must be stored in a pointer variable. The mechanism for doing this is rather simple. For example, the statement

```
Checkout *anotherTrans = new Checkout;
```

declares anotherTrans as a pointer to a Checkout object, reserves memory for the object, and places this newly created object's address in the anotherTrans pointer.

This dynamic creation of a checkout object can also be made in two steps. The first step is to declare a pointer variable with a declaration statement. Then, when an object is actually required, a request can be made to create the object. When the object is created, its address is assigned to the previously declared pointer. Following are the two required statements:

```
Checkout *anotherTrans;  // declares anotherTrans as a pointer
// that can store the address
// of a Checkout object
```

```
anotherTrans = new Checkout;  // creates a new Checkout object and
// stores this object's address in
// the pointer named anotherTrans
```

The expression new Checkout on the right of the equals sign creates a new Checkout object. The address returned by the new operator is then assigned to the pointer variable on the left of the equals sign. These two statements are the first two shaded statements in Program 12.4's main() function.

# Program 12.4

```
#include <iostream>
using namespace std;

// class declaration section
class Checkout
{
private:
    int numItems;
    double arrivalTime;

public:
    Checkout();  // the constructor
    // the following is an inline destructor
    ~Checkout()
    {cout << "!!!! This Customer object has been deleted !!!!\n";};
```