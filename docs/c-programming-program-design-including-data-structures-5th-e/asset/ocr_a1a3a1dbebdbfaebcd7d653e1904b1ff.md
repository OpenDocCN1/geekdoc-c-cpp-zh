```
```cpp
void testClass::print() const
{
    cout << "x = " << x << ", y = " << y << endl;
}

testClass::testClass()
{
    x = 0;
    y = 0;
}

testClass::testClass(int a, int b)
{
    x = a;
    y = b;
}
```
```

+   b. One possible solution. (We assume that the name of the header file containing the definition of the class `testClass` is `Exercise5Ch11.h`.)

```
```cpp
#include <iostream>
#include "Exercise5Ch11.h"

int main()
{
    testClass one;
    testClass two(4, 5);

    one.print();
    two.print();

    return 0;
}
```
```

+   7. a. `personType student("Buddy", "Arora");`
+      b. `student.print();`
+      c. `student.setName("Susan", "Gilbert");`

9. A constructor is a member of a class, and it executes automatically when a class object is instantiated and a call to the constructor is specified in the object declaration. A constructor is included in a class so that the objects are properly initialized when they are declared.

11. A destructor is a member of a class, and if it is included in a class, it executes automatically when a class object goes out of scope. Its main purpose is to deallocate the dynamic memory created by an object.

+   13. a. `myClass::count = 0;`
+       b. `myClass.incrementCount();`
+       c. `myClass.printCount();`
+       d. `int myClass::count = 0;`