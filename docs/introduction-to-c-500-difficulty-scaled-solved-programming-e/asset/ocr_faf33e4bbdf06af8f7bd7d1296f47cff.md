# Introduction to C++

```
T* f()
{
    T t;
    return new T;
}
int main()
{
    delete f();
    return 0;
}
```

A class is allowed to contain only the destructor, f() reserves memory for a T object and returns it, and main() first calls f() and then releases the returned memory. I do not see any error. The destructor is called once, to destroy the t object in f() and when calling delete to destroy the object created dynamically in f(). So, the program interprets it twice.

> In general, because using pointers is not the easiest thing to do, when a class needs dynamic memory, it is safer to use classes that contain dynamic memory management instead, such as the string and vector classes.

Also, the default functions work normally for classes that contain string or vector members. For example, when we copy an object that has a vector member, the copy function of the vector class undertakes the copying of the elements it. When the object is destroyed, the destructor of the vector class undertakes the destruction of its elements. Exercise C.17.5 is such an example.

# THE this POINTER

Each member function, with the exception of the static functions as we will see below, has access to a hidden pointer called this. The important thing to remember is that when a member function is called, this points to the object that class calls. For example, suppose that the T class contains the f() and g() functions, an integer member named mem and t is an object of that class. If we

t.f();
The compiler passes the address of the t object to f() and the this pointer in the f() is initialized with that address. As is is, the compiler interprets it as:

```
f(at) and the declaration as f(T *const this);
```

The this parameter is defined for us implicitly. Inside function any direct access to a member is assumed to be an implicit reference through this. For example:

```
T::f()
{
    mem = 10; // It is as we've written this->mem = 10;
    g(); // It is as we've written this->g();
}
```