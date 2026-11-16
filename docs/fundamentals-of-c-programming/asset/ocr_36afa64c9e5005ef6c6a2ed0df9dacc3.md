Accessibility rules, also called visibility rules or permissions, determine what parts of a class and/or object are accessible to the outside world. C++ provides a great deal of flexibility in assigning access permissions, but some general principles exist that, if followed, foster programs that are easier to build and extend.

+   • In general, fields should be `private`. Clients should not be able to arbitrarily change the state of an object. Allowing such might allow client code to put an object into an undefined state (for example, changing the denominator of a fraction to zero). An object's state should only change as a result of calling the object's methods.

The built-in primitive types like `int` and `double` offer no protection from client access. One exception to the private fields rule applies to simple objects that programmers naturally would treat as primitive types. Recall the geometric `Point` class found in Listing 14.1 (Mathpoints.cpp). The `x` and `y` fields of a point object may assume any legitimate floating-point value, and it may be reasonable in some applications for clients to treat a `Point` object as a primitive type. In this case it is appropriate to make the `x` and `y` fields public.

+   • Methods that provide a service to client code should be part of the `public` section of the class. The author of the class must ensure that the `public` methods cannot place the object into an illegal state. For example, consider the following method:

```
void set_denominator(int d) {
    denominator = d;
}
```

If this method were part of the `SimpleRational` class, it would permit client code to sabotage a valid fraction with a simple statement:

```
fract.set_denominator(0);
```

+   • Methods that assist the service methods but that are not meant to be used by the outside world should be in the `private` section of the class. This allows a `public` method to be decomposed into simpler, perhaps more coherent activities without the threat of client code accessing these more primitive methods. These private methods are sometimes called helper methods or auxiliary methods.

Why would a programmer intentionally choose to limit access to parts of an object? Restricting access obviously limits the client's control over the objects it creates. While this may appear to be a disadvantage at first glance, this access restriction actually provides a number of advantages:

+   • Flexibility in implementation. A class conceptually consists of two parts:

+   – The class interface—the visible part. Clients see and can use the public parts of an object. The public methods and public variables of a class constitute the interface of the class. A class's interface specifies what it does.

+   – The class implementation—the hidden part. Clients cannot see any private methods or private variables. Since this private information is invisible to clients, class developers are free to do whatever they want with the private parts of the class. A class's implementation specifies how it accomplishes what it needs to do.

We would like our objects to be black boxes: clients shouldn't need to know how the objects work but merely rely on what objects can do.