# **VLADIMIR RESHETNIKOV**

One exception to the uniqueness requirement for indexer signatures: If an indexer is an explicit implementation of an interface, its signature is checked for uniqueness only within those interface's explicitly implemented indexers:

```
```csharp
class A : IIndexable
{
    int IIndexable.this[int x]
    {
        get { /* ... */ }
    }

    public int this[int x] // Okay
    {
        get { /* ... */ }
    }
}
```
```

+   - Overloading of operators permits a *class or struct* to declare multiple operators with the same name, provided their signatures are unique within that *class or struct*.

Although *out* and *ref* parameter modifiers are considered part of a signature, members declared in a single type cannot differ in signature solely by *ref* and *out*. A compile-time error occurs if two members are declared in the same type with signatures that would be the same if all parameters in both methods with *out* modifiers were changed to *ref* modifiers. For other purposes of signature matching (*e.g., hiding or overriding*), *ref* and *out* are considered part of the signature and do not match each other. (This restriction is to allow C# programs to be easily translated to run on the Common Language Infrastructure [CLI], which does not provide a way to define methods that differ solely in *ref* and *out*.)

For the purposes of signatures, the types *object* and *dynamic* are considered the same. Members declared in a single type cannot, therefore, differ in signature solely by *object* and *dynamic*.

The following example shows a set of overloaded method declarations along with their signatures.

```
```csharp
interface ITest
{
    void F();                // F()
    void F(int x);           // F(int)
    void F(ref int x);       // F(ref int)
    void F(out int x);       // F(out int)   error
}
```
```