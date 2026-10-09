# ADVANCED TOPIC

# **Public Constants Should Be Permanent Values**

Publicly accessible constants should be permanent, because changing the value of a constant will not necessarily take effect in the assemblies that use it. If an assembly references a constant from a different assembly, the value of the constant is compiled directly into the referencing assembly. Therefore, if the value in the referenced assembly is changed but the referencing assembly is not recompiled, the referencing assembly will still use the original value, not the new value. Values that could potentially change in the future should be specified as `readonly` instead.

# readonly

Unlike `const`, the `readonly` modifier is available only for fields (not for local variables). It declares that the field value is modifiable only from inside the constructor or via an initializer during declaration. Listing 6.44 demonstrates how to declare a read-only field.

# **LISTING 6.44: Declaring a Field as readonly**

```
class Employee
{
    public Employee(int id)
    {
        _Id = id;
    }

    // ...

    public readonly int _Id;

    public int Id
    {
        get { return _Id; }
    }

    // Error: A readonly field cannot be assigned to (except
    // in a constructor or a variable initializer)
    // public void SetId(int id) =>
    //     _Id = id;

    // ...
}
```