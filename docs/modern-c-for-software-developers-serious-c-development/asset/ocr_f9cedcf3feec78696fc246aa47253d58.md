An object's constructor is called when the object comes into existence, and an object's destructor is automatically called when the object is destroyed.

Global objects have their constructor functions execute before main begins execution. Global constructors are executed in the order of their declaration, within the same file. The order of execution of global constructors is unknown when they are spread among several files. Global destructors execute in reverse order after main has terminated.

A local object's constructor function is executed when the object's definition is encountered. The destructor functions for local objects are executed in the reverse order of the constructor functions.

# Private Destructors

Consider the following example:

```
#include <iostream>
class Foo {
private:
    ~Foo();
};
int main() {
    Foo foo;
}

// output
error: 'Foo::~Foo()' is private within this context
```

This program will not compile. The reason is that foo is created on the stack and once foo leaves its scope, the destructor cannot be called since it is private. Making a class destructor private ensures that only the class object can destroy itself. For example, a reference counting object can destroy itself when it's count reaches zero.