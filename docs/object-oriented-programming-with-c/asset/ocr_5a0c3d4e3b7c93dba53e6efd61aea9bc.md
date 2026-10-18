```
```cpp
integer(void); // constructor declared
....
....
};
integer :: integer(void) // constructor defined
{
m = 0; n = 0;
}
```
```

When a class contains a constructor like the one defined above, it is guaranteed that an object created by the class will be initialized automatically. For example, the declaration

```
```cpp
integer int1; // object int1 created
```
```

not only creates the object int1 of type integer but also initializes its data members m and n to zero. There is no need to write any statement to invoke the constructor function (as we do with the normal member functions). If a ‘normal’ member function is defined for zero initialization, we would need to invoke this function for each of the objects separately. This would be very inconvenient, if there are a large number of objects.

A constructor that accepts no parameters is called the *default constructor*. The default constructor for **class A** is **A::A( )**. If no such constructor is defined, then the compiler supplies a default constructor. Therefore a statement such as

```
```cpp
A a;
```
```

invokes the default constructor of the compiler to create the object a.

The constructor functions have some special characteristics. These are:

+   - They should be declared in the public section.
+   - They are invoked automatically when the objects are created.