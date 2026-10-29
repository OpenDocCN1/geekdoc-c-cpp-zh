```
}
ostream& operator <<(ostream& Parameter_3,
    const Class_Name& Parameter_4)
{
    ...
}
```

If you have enough accessor and mutator functions, you can overload >> and << as nonfriend functions. However, it is natural and more efficient to define them as friends.

# What Mode of Returned Value to Use

A function can return a value of type T in four different ways:

+   - By plain old value, as in the function declaration T f();
+   - By constant value, as in the function declaration const T f();
+   - By reference, as in the function declaration T& f();
+   - By const reference, as in the function declaration const T& f();

There is not unanimous agreement on which to use when. So, do not expect too much consistency in usage. Even when an author or programmer has a clear policy, they seldom manage to follow it without exception. Still, some points are clear.

If you are returning a simple type, like int or char, there is no point in using a const when returning by value or by reference. So programmers typically do not use a const on the return type when it is a simple type. If you want the simple value returned to be allowed as an l-value, that is to be allowed on the left-hand side of an assignment statement, then return by reference; otherwise return the simple type by plain old value. Class types are not so simple. The rest of this discussion applies to returning an object of a class type.

The decision on whether or not to return by reference has to do with whether or not you want to be able to use the returned object as an l-value. If you want to return something that can be used as an l-value, that is, that can be used on the left-hand side of an assignment operator, you must return by reference and so must use an ampersand sign & on the returned type.

Returning a local variable (or other short lived object) by reference, with or without a const, can produce problems and should be avoided.

For class types, the two returned type specifications const T and const T& are very similar. They both mean that you cannot change the returned object by invoking some mutator function directly on the returned object, as in

```
f().mutator();
```