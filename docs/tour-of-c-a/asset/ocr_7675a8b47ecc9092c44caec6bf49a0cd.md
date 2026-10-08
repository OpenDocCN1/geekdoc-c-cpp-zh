Unfortunately, the standard-library uses unsigned integers for sizes and subscripts, so we need to use the ugly static_cast to explicitly convert the size of the list to an int. This is pedantic because the number of elements in a handwritten list larger than the largest integer (32,767 for 16-bit integers and 2,147,483,647 for 32-bit integers) is rather low. However, the type system has no common sense. It knows about the possible values of variables, rather than actual values, so it might complain when there is no actual violation. Such warnings can occasionally save the programmer from a bad error.

A `_cast` does not check the value it is converting; the programmer is trusted to use it correctly. This is not always a good assumption, so if you doubt, check. Explicit conversions (often called casts to remind you that you are up to popping something broken) are avoided. Try to use unchecked casts for the lowest level of a system. They are error-prone.

Other cases are reinterpret_cast and bit_cast (§16.7) for treating an object as a simple sequence of bytes, const_cast for "casting away `const`.". Judicious use of the type system and well-designed libraries allow us to eliminate unchecked casts in higher-level software.

# 5.3 Abstract Types

Types such as complex and Vector are called *concrete* types because their representation is part of their definition. In that, they resemble built-in types. In contrast, an *abstract type* is a type that completely isolates a user from implementation details. To do that, we decouple the interface from the representation and give up local variables. Since we don't know anything about the representation of an abstract (even its size), (§5.2.2) and access them through references or pointers (§1.7, §15.2.1), we must allocate objects on the store of our version of Vector:.

First, we define a class `Container`, which we will design as a more abstract interface.

Click here to view code image

```
class Container {
public:
    virtual double&operator[](int) = 0; // pure virtual function
    virtual int size() const = 0;      // const member function (§5.2.1)
    virtual ~Container()               // destructor (§5.2.2)
};
```

This class is a pure interface to specify certain data. The word `virtual` means "may be redefined in a `virtual` class.\ A class derived from `Container` provides an implementation for the `Container` interface. The curious `=0` syntax says the function is *pure virtual*; that is, some class derived from `Container` must define the function. Then, it is not possible to define an object that is just a `Container`. For example:

Click here to view code image

```
Container c;
Container* p = new Vector_container(10); // error: there are no objects of an abstract class
// OK: Container is an interface for Vector_container
```

A `Container` can only serve as the interface to a class that implements `operator[]()` and `size()` functions. A class with a pure virtual function is called an *abstract* class.