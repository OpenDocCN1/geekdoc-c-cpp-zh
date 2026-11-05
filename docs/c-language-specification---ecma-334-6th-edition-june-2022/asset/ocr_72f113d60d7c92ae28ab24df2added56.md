# 17.6.4 Implementation of generic methods

When a generic method implicitly implements an interface method, the constraints given for each method type parameter shall be equivalent in both declarations (after any interface type parameters are replaced with the appropriate type arguments), where method type parameters are identified by ordinal positions, left to right.

*Example:* In the following code:

```
```csharp
interface I<X, Y, Z>
{
    void F<T>(T t) where T : X;
    void G<T>(T t) where T : Y;
    void H<T>(T t) where T : Z;
}

class C : I<object, C, string>
{
    public void F<T>(T t) {...}             // Ok
    public void G<T>(T t) where T : C {...} // Ok
    public void H<T>(T t) where T : string {...} // Error
}
```
```

the method C.F<T> implicitly implements I<object,C,string>.F<T>. In this case, C.F<T> is not required (nor permitted) to specify the constraint T: object since object is an implicit constraint on all type parameters. The method C.G<T> implicitly implements I<object,C,string>.G<T> because the constraints match those in the interface, after the interface type parameters are replaced with the corresponding type arguments. The constraint for method C.H<T> is an error because sealed types (string in this case) cannot be used as constraints. Omitting the constraint would also be an error since constraints of implicit interface method implementations are required to match. Thus, it is impossible to implicitly implement I<object,C,string>.H<T>. This interface member can only be implemented using an explicit interface member implementation:

```
```csharp
class C : I<object, C, string>
{
    ...
    public void H<U>(U u) where U : class {...}

    void I<object, C, string>.H<T>(T t)
    {
        string s = t; // Ok
        H<T>(t);
    }
}
```
```

In this case, the explicit interface member implementation invokes a public method having strictly weaker constraints. The assignment from t to s is valid since T inherits a constraint of T: string, even though this constraint is not expressed in source code. *end example*

*Note:* When a generic method explicitly implements an interface method no constraints are allowed on the implementing method (§14.7.1, §17.6.2). *end note*