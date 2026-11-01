Constructors follow the same rules for overloading as other methods (that is, you can provide as many overloads to the constructor as you want, provided they are clearly different in signature):

```
public MyClass()  // zeroparameter constructor
{
    // construction code
}
public MyClass(int number)  // another overload
{
    // construction code
}
```

Note, however, that if you supply any constructors that take parameters, the compiler will not automatically supply a default one. This is done only if you have not defined any constructors at all. In the following example, because a one-parameter constructor is defined, the compiler assumes that this is the only constructor you want to be available, so it will not implicitly supply any others:

```
public class MyNumber
{
    private int number;
    public MyNumber(int number)
    {
        this.number = number;
    }
}
```

This code also illustrates typical use of the this keyword to distinguish member fields from parameters of the same name. If you now try instantiating a MyNumber object using a no-parameter constructor, you will get a compilation error:

```
MyNumber numb = new MyNumber();  // causes compilation error
```

We should mention that it is possible to define constructors as private or protected, so that they are invisible to code in unrelated classes too:

```
public class MyNumber
{
    private int number;
    private MyNumber(int number)  // another overload
    {
        this.number = number;
    }
}
```

This example hasn’t actually defined any public or even any protected constructors for MyNumber. This would actually make it impossible for MyNumber to be instantiated by outside code using the new operator (though you might write a public static property or method in MyNumber that can instantiate the class). This is useful in two situations:

+   - If your class serves only as a container for some static members or properties and therefore should never be instantiated
+   - If you want the class to only ever be instantiated by calling some static member function (this is the so-called class factory approach to object instantiation)

# Static Constructors

One novel feature of C# is that it is also possible to write a static no-parameter constructor for a class. Such a constructor will be executed only once, as opposed to the constructors written so far, which are instance constructors that are executed whenever an object of that class is created.

```
class MyClass
{
    static MyClass()
}
```