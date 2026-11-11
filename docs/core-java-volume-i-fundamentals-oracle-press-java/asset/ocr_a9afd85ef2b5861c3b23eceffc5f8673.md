matters is that you do not circumvent the intent of the original design
when you override methods in subclasses.

+   6. *Use polymorphism, not type information.*

Whenever you find code of the form

```
if (x is of type 1)
    $$$action1(x);
else if (x is of type 2)
    $$$action2(x);
```

think polymorphism.

Do *action1* and *action2* represent a common concept? If so, make the
concept a method of a common superclass or interface of both types.
Then, you can simply call

```
x.action();
```

and have the dynamic dispatch mechanism inherent in polymorphism
launch the correct action.

Code that uses polymorphic methods or interface implementations is
much easier to maintain and extend than code using multiple type tests.

+   7. *Don't overuse reflection.*

The reflection mechanism lets you write programs with amazing
generality, by detecting fields and methods at runtime. This capability
can be extremely useful for systems programming, but it is usually not
appropriate in applications. Reflection is fragile—with it, the compiler
cannot help you find programming errors. Any errors are found at
runtime and result in exceptions.

You have now seen how Java supports the fundamentals of object-oriented
programming: classes, inheritance, and polymorphism. In the next chapter, I
will tackle two advanced topics that are very important for using Java
effectively: interfaces and lambda expressions.