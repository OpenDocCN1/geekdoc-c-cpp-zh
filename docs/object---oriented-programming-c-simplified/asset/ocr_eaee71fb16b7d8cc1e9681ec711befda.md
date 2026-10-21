# Object-Oriented Programming C++ Simplified

OUTPUT :
Hello from constructor

EXPLANATION : The name of class is demo and the following declaration

```
demo()
{
    cout << " Hello from constructor \n";
}
```

demo is a constructor of the class as the name of the function is the name of the class. Note the following features of the constructor.

+   1. The constructors are always declared in the public section. If declared in the private section then objects are can only be created inside the member functions but serve no purpose.
+   2. They are invoked automatically when objects of the class are created. The declaration demo d; creates an object d which automatically calls the constructor of the class and prints Hello from constructor.
+   3. They do not have any return type not even void so they cannot return any value.
+   4. Constructors cannot be inherited, but they can be called from the constructors of derived class.
+   5. Constructors are used to construct the object of the class.
+   6. The constructor with no argument is known as default constructor of the class. The default constructor for the class demo will be demo : demo()
+   7. Constructors which take arguments like a function takes are known as parameterized constructor.
+   8. There is no limit of the number of constructors declared in a class but they all must conform to rules of function overloading.
+   9. Constructor can have default arguments.
+   10. Addresses of constructors cannot be taken.
+   11. Constructors cannot be virtual.
+   12. Constructor make implicit calls to operators new and delete in case memory allocation and de-allocation is to be performed.

The other way to write the above program would be :

```
#include <iostream.h>
Class demo
{
public :
demo(); // declaration
};
```