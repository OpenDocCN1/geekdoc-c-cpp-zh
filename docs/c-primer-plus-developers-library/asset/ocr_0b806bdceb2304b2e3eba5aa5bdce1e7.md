Third, the temporary object is used and then discarded. For instance, in Statement 2, the program computes the sum of `force1` and `force2`, copies the answer into the temporary return object, overwrites the contents with the contents of `net`, and then discards the temporary object. The original vectors are all left unchanged. In Statement 3, the magnitude of the temporary object is displayed before the object is deleted.

If you are concerned about the potential for misuse and abuse created by this behavior, you have a simple recourse: Declare the return type as a `const` object. For instance, if `Vector::operator+()` is declared to have return type `const Vector`, then Statement 1 is still allowed but Statements 2 and 3 become invalid.

In summary, if a method or function returns a local object, it should return an object, not a reference. In this example, the program uses the copy constructor to generate the returned object. If a method or function returns an object of a class for which there is no public copy constructor, such as the ostream class, it must return a reference to an object. Finally, some methods and functions, such as the overloaded assignment operator, can return either an object or a reference to an object. In this example, the reference is preferred for reasons of efficiency.

# Using Pointers to Objects

C++ programs often use pointers to objects, so let’s get in a bit of practice. Listing 12.6 uses array indexes to keep track of the shortest string and of the first string alphabetically. Another approach is to use pointers to point to the current leaders in these categories. Listing 12.7 implements this approach, using two pointers to String. Initially, the shortest pointer points to the first object in the array. Each time the program finds an object with a shorter string, it resets shortest to point to that object. Similarly, a first pointer tracks the alphabetically earliest string. Note that these two pointers do not create new objects; they merely point to existing objects. Hence they don’t require using new to allocate additional memory.

For variety, the program in Listing 12.7 uses a pointer that does keep track of a new object:

`String * favorite = new String(sayings[choice]);`

Here the pointer `favorite` provides the only access to the nameless object created by `new`. This particular syntax means to initialize the new String object by using the object `sayings[choice]`. That invokes the copy constructor because the argument type for the copy constructor (`const String &`) matches the initialization value (`sayings[choice]`). The program uses `srand()`, `rand()`, and `time()` to select a value for choice at random.

Listing 12.7   `sayings2.cpp`

```
```cpp
// sayings2.cpp -- using pointers to objects
// compile with string1.cpp
#include <iostream>
#include <cstdlib>        // (or stdlib.h) for rand(), srand()
#include <ctime>          // (or time.h) for time()
```
```