# Chapter A

```
```cpp
obj2.show ();

example obj3 (30);
obj3.show ();

return 0;
}
```
```

Output

```
```text
Static = 1 Non Static = 10
Static = 2 Non Static = 20
Static = 3 Non Static = 30
```
```

In the preceding program, we can very clearly see the behavior of the two different types of member variables. Here, the static variable is incremented in the class’s constructor, and it is decremented in the class’s destructor. On the other hand, “memberData” is a private variable on per object basis, which has different values set for different objects of the class example.

Similar to static member data, a class’s method can also be static. But the following restrictions are placed on a static method defined by a class:

+   1. It should only access static data
+   2. Static functions does not have a “this” pointer
+   3. Static functions does not support function overloading with any non-static function

Therefore, for static functions, it is also accessed globally, i.e., generally, the class name is used to access the static method by the scope resolution operator within the class. It is not accessed directly by the class’s object.
Let us illustrate this concept with the help of the following example:

```
```cpp
#include <iostream>
using namespace std;

class example {
    static int counter;
    int memberData;
public:
    example () {
        counter++;
    }
    example (int var) {
        counter++;
        memberData = var;
    }
    ~example () {
        counter--;
    }
    static void show () {
        cout<<"Static = "<<counter <<endl;
    }
};

int example::counter = 0;

int main () {
    example obj1 (10);
    example::show ();

    example obj2 (20);
```
```