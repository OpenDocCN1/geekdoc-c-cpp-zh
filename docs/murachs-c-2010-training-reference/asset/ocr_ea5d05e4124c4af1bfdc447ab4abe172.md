# The class declaration for a sealed Book class

public sealed class Book : Product

# How sealed methods work

```
A base class named A that declares a virtual method
public class A
{
    public void ShowMessage()
{
        MessageBox.Show("Hello from class A");
    }
}
```

```
A class named B that inherits class A and overrides and seals its method
public class B : A
{
    public sealed override void ShowMessage()
{
        MessageBox.Show("Hello from class B");
    }
}
```

```
A class named C that inherits class B and tries to override its sealed method
public class C : B
{
    public override void ShowMessage() // Not allowed
{
        MessageBox.Show("Hello from class C");
    }
}
```

# Description

+   - A sealed class is a class that can't be inherited. To create a sealed class, you code the sealed keyword in the class declaration.

+   - Sealing a class can result in a minor performance improvement for your application because the C# compiler doesn't have to allow inheritance and polymorphism. As a result, it can generate more efficient code.

+   - You can also seal individual properties and methods. To create a sealed property or a sealed method, code the sealed keyword in the property or method declaration.

+   - You can only seal a property or method if the property or method overrides a member of the base class. This allows you to create a virtual member in a base class, and seal it in a derived class so that subclasses derived from that class can't override the member. This feature is rarely used in business applications.

![](bbox=[0.066, 0.946, 0.468, 0.961])