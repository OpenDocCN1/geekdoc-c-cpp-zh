![](bbox=[0.164, 0.193, 0.226, 0.259])

+   4. **When you are finished with the pointer, call `delete`.**
+   
+      This step frees the object from the heap. Remember that this does not delete the pointer itself, but frees the object memory.
+   
+   5. **Clear the pointer by setting it to `0`.**
+   
+      If your `delete` statement is at the end of the application, you don’t need to clear the pointer to `0` because the pointer is going out of scope. The pointer won’t exist any longer, so setting it to `0` isn’t essential, but it’s good practice because you get into the habit of doing it in places where clearing the pointer to `0` would be important.

# Using classes and smart pointers

If you’re working with C++ 17 or above, you probably want to use smart pointers with your objects, rather than the labor-intensive and error-prone raw pointers. The `SmartPtr` example, shown in Listing 1-7, shows the same process as Listing 1-6 but uses smart pointers instead. You still need to add `Pen.cpp` and `Pen.h` from PenClass2.

# LISTING 1-7: Managing an Object’s Life Using Smart Pointers

```
```cpp
#include <iostream>
#include <memory>
#include "../PenClass2/Pen.h"

using namespace std;

int main() {
    unique_ptr<Pen> MyPen;
    MyPen.reset(new Pen());
    MyPen->InkColor = red;
    cout << MyPen->InkColor << endl;
    MyPen.reset();
    return 0;
}
```
```

![](bbox=[0.164, 0.796, 0.226, 0.863])

You wouldn’t ordinarily assign an object to a `unique_ptr` as a separate step, but this example shows you how by using `reset()`. In this case, you actually reset MyPen to point to a new object, `new Pen()`, which must include the opening and closing parentheses. If you were to do this in an application, `reset()` would take care of freeing any old object before pointing MyPen to any new object. The “Creating smart pointers using std::unique_ptr and std::shared_ptr” section of Book 1, Chapter 8 shows the standard approach to creating smart pointers.