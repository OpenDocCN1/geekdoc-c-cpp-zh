```
public Bar (string s) { ... }
}
class Factory<T>
    where T : new()
{
    public T Create()
    {
        return new T();
    }
}
```

```
Foo f = new Factory<Foo>().Create(); // Valid.
Bar b = new Factory<Bar>().Create(); // Invalid, Bar does not define a default/empty constructor.
```

The second call to to Create() will give compile time error with following message:

> > 'Bar' must be a non-abstract type with a public parameterless constructor in order to use it as parameter 'T' in the generic type or method 'Factory'

There is no constraint for a constructor with parameters, only parameterless constructors are supported.

# Section 59.5: Type constraints (classes and interfaces)

Type constraints are able to force a type parameter to implement a certain interface or class.

```
interface IType;
interface IAnotherType;

// T must be a subtype of IType
interface IGeneric<T>
    where T : IType
{
}

// T must be a subtype of IType
class Generic<T>
    where T : IType
{
}

class NonGeneric
{
    // T must be a subtype of IType
    public void DoSomething<T>(T arg)
        where T : IType
    {
    }
}

// Valid definitions and expressions:
class Type : IType { }
class Sub : IGeneric<Type> { }
class Sub : Generic<Type> { }
new NonGeneric().DoSomething(new Type());

// Invalid definitions and expressions:
class AnotherType : IAnotherType { }
```