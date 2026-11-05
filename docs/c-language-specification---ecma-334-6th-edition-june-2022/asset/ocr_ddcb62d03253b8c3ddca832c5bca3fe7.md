```
| expression
;
```

A resource is a class or struct that implements the System.IDisposable interface, which includes a single parameterless method named Dispose. Code that is using a resource can call Dispose to indicate that the resource is no longer needed.

If the form of resource_acquisition is local_variable_declaration then the type of the local_variable_declaration shall be either dynamic or a type that can be implicitly converted to System.IDisposable. If the form of resource_acquisition is expression then this expression shall be implicitly convertible to System.IDisposable.

Local variables declared in a resource_acquisition are read-only, and shall include an initializer. A compile-time error occurs if the embedded statement attempts to modify these local variables (via assignment or the ++ and -- operators), take the address of them, or pass them as ref or out parameters.

A using statement is translated into three parts: acquisition, usage, and disposal. Usage of the resource is implicitly enclosed in a try statement that includes a finally clause. This finally clause disposes of the resource. If a null resource is acquired, then no call to Dispose is made, and no exception is thrown. If the resource is of type dynamic it is dynamically converted through an implicit dynamic conversion (§10.2.10) to IDisposable during acquisition in order to ensure that the conversion is successful before the usage and disposal.

A using statement of the form

```
using (ResourceType resource = «expression» ) «statement»
```

corresponds to one of three possible expansions. When ResourceType is a non-nullable value type or a type parameter with the value type constraint (§14.2.5), the expansion is semantically equivalent to

```
{
  ResourceType resource = «expression»;
  try
  {
    «statement»;
  }
  finally
  {
    ((IDisposable)resource).Dispose();
  }
}
```

except that the cast of resource to System.IDisposable shall not cause boxing to occur.

Otherwise, when ResourceType is dynamic, the expansion is