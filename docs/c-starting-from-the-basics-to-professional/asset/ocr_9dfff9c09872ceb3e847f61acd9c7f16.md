The destructor for a class is always called automatically when an object is destroyed. The circumstances where you need to call a destructor explicitly are so rare you can ignore this possibility. Calling a destructor when it is not necessary can cause problems.

You only need to define a class destructor when something needs to be done when an object is destroyed. A class that deals with physical resources such as a file or a network connection that needs to be closed is one example, and of course, if memory is allocated by a constructor using `new`, the destructor is the place to release the memory. In Chapter 18 we'll argue that defining a destructor should in fact be reserved for only a small minority of your classes—those specifically designated to manage a given resource. This notwithstanding, the Box class in Ex12_14 would surely definitely benefit from a destructor implementation as well, namely, one that decrements `s_object_count`:

```
```cpp
class Box
{
public:
    // Same constructors as before...

    ~Box();                         // Destructor

    // Rest of the class as before...

    static size_t getObjectCount() { return s_object_count; }

private:
    // ...

    static inline size_t s_object_count;   // Count of objects in existence
};
```
```

The destructor has been added to decrement `s_object_count`, and `getObjectCount()` is now a static member function (without a const qualifier). The implementation of the Box destructor can be added to the Box.cpp file from Ex12_14 as follows. It outputs a message when it is called so you can see when this occurs:

```
```cpp
Box::~Box()                              // Destructor
{
    std::cout << "Box destructor called." << std::endl;
    --s_object_count;
}
```
```

The following code will check the destructor operation out:

```
```cpp
// Ex12_16.cpp
// Implementing a destructor
import <iostream>;
import <memory>;
import box;

int main()
{
    std::cout << "There are now " << Box::getObjectCount() << " Box objects." << std::endl;

    const Box box1 {2.0, 3.0, 4.0};       // An arbitrary box
```
```