> > **ERIC LIPPERT**
> >
> > Although it is not legal to create classes such that two interfaces can become identical under construction, it is possible in C# 4.0 to create classes that are ambiguous in various, more subtle ways thanks to generic covariance and contra-variance. Imagine, for example, a base class that implements IEnumerable<object> and a derived class that implements IEnumerable<string>. These were incompatible types in C# 3.0, but that is no longer the case. Because IEnumerable<string> is now convertible to IEnumerable<object>, it's not entirely clear which implementation will be called when a method of IEnumerable<object> is invoked on the derived class. These sorts of bizarre scenarios tend to expose implementation-defined behavior of the runtime and should be avoided whenever possible.

# ### 13.4.3 Implementation of Generic Methods

When a generic method implicitly implements an interface method, the constraints given for each method type parameter must be equivalent in both declarations (after any interface type parameters are replaced with the appropriate type arguments), where method type parameters are identified by ordinal positions, left to right.

When a generic method explicitly implements an interface method, however, no constraints are allowed on the implementing method. Instead, the constraints are inherited from the interface method:

```
```csharp
interface I<A, B, C>
{
    void F<T>(T t) where T : A;
    void G<T>(T t) where T : B;
    void H<T>(T t) where T : C;
}

class C : I<object, C, string>
{
    public void F<T>(T t) {...}                    // Okay
    public void G<T>(T t) where T : C {...}        // Okay
    public void H<T>(T t) where T : string {...}   // Error
}
```
```

The method C.F<T> implicitly implements I<object,C,string>.F<T>. In this case, C.F<T> is not required (nor permitted) to specify the constraint T : object since object is an implicit constraint on all type parameters. The method C.G<T> implicitly implements I<object,C,string>.G<T> because the constraints match those in the interface, after the interface type parameters are replaced with the corresponding type arguments. The constraint for method C.H<T> is an error because sealed types (string in this case) cannot be used as constraints. Omitting the constraint would also be an error since constraints of