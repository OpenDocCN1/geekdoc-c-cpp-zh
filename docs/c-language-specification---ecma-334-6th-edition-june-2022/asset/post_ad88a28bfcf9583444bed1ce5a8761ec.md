
| expression
;

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

Otherwise, the expansion is

```csharp
    {
        ResourceType resource = «expression»;
        try
        {
            «statement»;
        }
        finally
        {
            IDisposable d = (IDisposable)resource;
            if (d != null)
            {
                d.Dispose();
            }
        }
    }
```

In any expansion, the `resource` variable is read-only in the embedded statement, and the `d` variable is inaccessible in, and invisible to, the embedded statement.

An implementation is permitted to implement a given `using_statement` differently, e.g., for performance reasons, as long as the behavior is consistent with the above expansion.

A using statement of the form:

```csharp
    using («expression») «statement»
```

has the same three possible expansions. In this case `ResourceType` is implicitly the compile-time type of the `expression`, if it has one. Otherwise the interface `IDisposable` itself is used as the `ResourceType`. The `resource` variable is inaccessible in, and invisible to, the embedded statement.

When a `resource_acquisition` takes the form of a `local_variable_declaration`, it is possible to acquire multiple resources of a given type. A using statement of the form

```csharp
    using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) «statement»
```

is precisely equivalent to a sequence of nested using statements:

```csharp
    using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
    ...
    using (ResourceType rN = eN)
    «statement»
```

Example: The example below creates a file named `log.txt` and writes two lines of text to the file. The example then opens that same file for reading and copies the contained lines of text to the console.

```csharp
using System;
using System.IO;

class Test
{
    static void Main()
    {
        using (TextWriter w = File.CreateText("log.txt"))
        {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }
        using (TextReader r = File.OpenText("log.txt"))
        {
            string s;
            while ((s = r.ReadLine()) != null)
            {
                Console.WriteLine(s);
            }
        }
    }
}
```

Since the TextWriter and TextReader classes implement the IDisposable interface, the example can use using statements to ensure that the underlying file is properly closed following the write or read operations.

*end example*

## 12.15 The yield statement

The yield statement is used in an iterator block (§12.3) to yield a value to the enumerator object (§14.14.5) or enumerator object (§14.14.6) of an iterator or to signal the end of the iteration.

```
yield_statement
  : 'yield' 'return' expression ';'
  | 'yield' 'break' ';'
```

yield is a contextual keyword (§6.4.4) and has special meaning only when used immediately before a return or break keyword.

There are several restrictions on where a yield statement can appear, as described in the following.

- It is a compile-time error for a yield statement (of either form) to appear outside a method_body, operator_body, or accessor_body.
- It is a compile-time error for a yield statement (of either form) to appear inside an anonymous function.
- It is a compile-time error for a yield statement (of either form) to appear in the finally clause of a try statement.
- It is a compile-time error for a yield return statement to appear anywhere in a try statement that contains any catch_clauses.

Example: The following example shows some valid and invalid uses of yield statements.

```
delegate IEnumerable<int> D();
IEnumerator<int> GetEnumerator()
{
    try
    {
        yield return 1; // Ok
        yield break;    // Ok
    }
    finally
    {
        yield return 2; // Error, yield in finally
        yield break;   // Error, yield in finally
    }
    try
    {
        yield return 3; // Error, yield return in try/catch
        yield break;   // Ok
    }
    catch
    {
        yield return 4; // Error, yield return in try/catch
        yield break;   // Ok
    }
    D d = delegate
    {
        yield return 5; // Error, yield in an anonymous function
    };

    int MyMethod()
    {
        yield return 1;   // Error, wrong return type for an iterator block
    }
}
```

*end example*

An implicit conversion (§10.2) shall exist from the type of the expression in the yield return statement to the yield type (§14.14.4) of the iterator.

A yield return statement is executed as follows:

- The expression given in the statement is evaluated, implicitly converted to the yield type, and assigned to the Current property of the enumerator object.
- Execution of the iterator block is suspended. If the yield return statement is within one or more try blocks, the associated finally blocks are not executed at this time.
- The MoveNext method of the enumerator object returns true to its caller, indicating that the enumerator object successfully advanced to the next item.

The next call to the enumerator object's MoveNext method resumes execution of the iterator block from where it was last suspended.

A yield break statement is executed as follows:

- If the yield break statement is enclosed by one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all enclosing try statements have been executed.
- Control is returned to the caller of the iterator block. This is either the MoveNext method or Dispose method of the enumerator object.

Because a `yield` break statement unconditionally transfers control elsewhere, the end point of a `yield` break statement is never reachable.

## 13. Namespaces

### 13.1 General

C# programs are organized using namespaces. Namespaces are used both as an “internal” organization system for a program, and as an “external” organization system—a way of presenting program elements that are exposed to other programs.

Using directives (§13.5) are provided to facilitate the use of namespaces.

### 13.2 Compilation units

A compilation_unit consists of zero or more extern_alias_directives followed by zero or more using_directives followed by zero or more global_attributes followed by zero or more namespace_member_declarations. The compilation_unit defines the overall structure of the input.

```
compilation_unit
  : extern_alias_directive* using_directive* global_attributes?
    namespace_member_declaration*
  ;
```

A C# program consists of one or more compilation units. When a C# program is compiled, all of the compilation units are processed together. Thus, compilation units can depend on each other, possibly in a circular fashion.

The extern_alias_directives of a compilation unit affect the using_directives, global_attributes and namespace_member_declarations of that compilation unit, but have no effect on other compilation units.

The using_directives of a compilation unit affect the global_attributes and namespace_member_declarations of that compilation unit, but have no effect on other compilation units.

The global_attributes (§21.3) of a compilation unit permit the specification of attributes for the target assembly and module. Assemblies and modules act as physical containers for types. An assembly may consist of several physically separate modules.

The namespace_member_declarations of each compilation unit of a program contribute members to a single declaration space called the global namespace.

*Example:*

```
File A.cs:
  class A {}
File B.cs:
  class B {}
```

The two compilation units contribute to the single global namespace, in this case declaring two classes with the fully qualified names A and B. Because the two compilation units contribute to the same declaration space, it would have been an error if each contained a declaration of a member with the same name.

*end example*
