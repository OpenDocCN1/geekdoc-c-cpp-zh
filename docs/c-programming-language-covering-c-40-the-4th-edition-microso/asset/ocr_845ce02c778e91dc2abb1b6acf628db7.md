constructors consists of all accessible instance constructors declared in the class itself. If this set is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs. If an instance constructor declaration includes a constructor initializer that invokes the constructor itself, a compile-time error occurs.

> **VLADIMIR RESHETNIKOV**  An argument in a *constructor-initializer* can be of type `dynamic` only if the argument has a `ref` or `out` modifier; otherwise, a compile-time error occurs (CS1975). Thus a *constructor-initializer* is never dynamically dispatched.

If an instance constructor has no constructor initializer, a constructor initializer of the form `base()` is implicitly provided. Thus an instance constructor declaration of the form

```
~~~
C(...) {...}
~~~
```

is exactly equivalent to

```
~~~
C(...): base() {...}
~~~
```

The scope of the parameters given by the *formal-parameter-list* of an instance constructor declaration includes the constructor initializer of that declaration. Thus a constructor initializer is permitted to access the parameters of the constructor. For example:

```
~~~csharp
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
~~~
```

An instance constructor initializer cannot access the instance being created. Therefore it is a compile-time error to reference `this` in an argument expression of the constructor initializer, as is it a compile-time error for an argument expression to reference any instance member through a *simple-name*.

# ## 10.11.2 Instance Variable Initializers

When an instance constructor has no constructor initializer, or it has a constructor initializer of the form `base(...)`, that constructor implicitly performs the initializations specified by the *variable-initializers* of the instance fields declared in its class. This corresponds to a sequence of assignments that are executed immediately upon entry to the constructor and before the implicit invocation of the direct base class constructor. The variable initializers are executed in the textual order in which they appear in the class declaration.