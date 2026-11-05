
## Chapter 61: Using Directive

### Section 61.1: Associate an Alias to Resolve Conflicts

If you are using multiple namespaces that may have same-name classes (such as System.Random and UnityEngine.Random), you can use an alias to specify that Random comes from one or the other without having to use the entire namespace in the call.

For instance:

```
using UnityEngine;
using System;

Random rnd = new Random();
```

This will cause the compiler to be unsure which Random to evaluate the new variable as. Instead, you can do:

```
using UnityEngine;
using System;
using Random = System.Random;

Random rnd = new Random();
```

This doesn't preclude you from calling the other by its fully qualified namespace, like this:

```
using UnityEngine;
using System;
using Random = System.Random;

Random rnd = new Random();
int unityRandom = UnityEngine.Random.Range(0,100);
```

rnd will be a System.Random variable and unityRandom will be a UnityEngine.Random variable.

### Section 61.2: Using alias directives

You can use using in order to set an alias for a namespace or type. More detail can be found in here.

Syntax:

```
using <identifier> = <namespace-or-type-name>;
```

Example:

```
using NewType = Dictionary<string, Dictionary<string,int>>;
NewType multiDictionary = new NewType();
//Use instances as you are using the original one
multiDictionary.Add("test", new Dictionary<string,int>());
```

### Section 61.3: Access Static Members of a Class

Version >= 6.0

Allows you to import a specific type and use the type's static members without qualifying them with the type name. This shows an example using static methods:

```csharp
using static System.Console;

// ...
string GetName()
{
    WriteLine("Enter your name.");
    return ReadLine();
}
```

And this shows an example using static properties and methods:

```csharp
using static System.Math;

namespace Geometry
{
    public class Circle
    {
        public double Radius { get; set; };
        public double Area => PI * Pow(Radius, 2);
    }
}
```

### Section 61.4: Basic Usage

```csharp
using System;
using BasicStuff = System;
using Sayer = System.Console;
using static System.Console; //From C# 6

class Program
{
    public static void Main()
    {
        System.Console.WriteLine("Ignoring usings and specifying full type name");
        Console.WriteLine("Thanks to the 'using System' directive");
        BasicStuff.Console.WriteLine("Namespace aliasing");
        Sayer.WriteLine("Type aliasing");
        WriteLine("Thanks to the 'using static' directive (from C# 6)");
    }
}
```

### Section 61.5: Reference a Namespace

```csharp
using System.Text;
//allows you to access classes within this namespace such as StringBuilder
//without prefixing them with the namespace. i.e:

//...
var sb = new StringBuilder();
//instead of
var sb = new System.Text.StringBuilder();
```

### Section 61.6: Associate an Alias with a Namespace

```csharp
using st = System.Text;
//allows you to access classes within this namespace such as StringBuilder
```

```csharp
//prefixing them with only the defined alias and not the full namespace. i.e:

//...
var sb = new st.StringBuilder();
//instead of
var sb = new System.Text.StringBuilder();
```

## Chapter 62: IDisposable interface

### Section 62.1: In a class that contains only managed resources

Managed resources are resources that the runtime's garbage collector is aware and under control of. There are many classes available in the BCL, for example, such as a SqlConnection that is a wrapper class for an unmanaged resource. These classes already implement the IDisposable interface -- it's up to your code to clean them up when you are done.

It's not necessary to implement a finalizer if your class only contains managed resources.

```
public class ObjectWithManagedResourcesOnly : IDisposable
{
    private SqlConnection sqlConnection = new SqlConnection();

    public void Dispose()
    {
        sqlConnection.Dispose();
    }
}
```

### Section 62.2: In a class with managed and unmanaged resources

It's important to let finalization ignore managed resources. The finalizer runs on another thread -- it's possible that the managed objects don't exist anymore by the time the finalizer runs. Implementing a protected Dispose(bool) method is a common practice to ensure managed resources do not have their Dispose method called from a finalizer.

```
public class ManagedAndUnmanagedObject : IDisposable
{
    private SqlConnection sqlConnection = new SqlConnection();
    private UnmanagedHandle unmanagedHandle = Win32.SomeUnmanagedResource();
    private bool disposed;

    public void Dispose()
    {
        Dispose(true); // client called dispose
        GC.SuppressFinalize(this); // tell the GC to not execute the Finalizer
    }

    protected virtual void Dispose(bool disposeManaged)
    {
        if (!disposed)
        {
            if (disposeManaged)
            {
                if (sqlConnection != null)
                {
                    sqlConnection.Dispose();
                }
            }

            unmanagedHandle.Release();

            disposed = true;
        }
    }
}
```

```
{
    // do foo stuff
}
finally
{
    if (foo != null)
        ((IDisposable)foo).Dispose();
}
}
```

### Section 62.5: In an inherited class with managed resources

It's fairly common that you may create a class that implements IDisposable, and then derive classes that also contain managed resources. It is recommended to mark the Dispose method with the virtual keyword so that clients have the ability to cleanup any resources they may own.

```csharp
public class Parent : IDisposable
{
    private ManagedResource parentManagedResource = new ManagedResource();

    public virtual void Dispose()
    {
        if (parentManagedResource != null)
        {
            parentManagedResource.Dispose();
        }
    }
}

public class Child : Parent
{
    private ManagedResource childManagedResource = new ManagedResource();

    public override void Dispose()
    {
        if (childManagedResource != null)
        {
            childManagedResource.Dispose();
        }
        //clean up the parent's resources
        base.Dispose();
    }
}
```

## Chapter 63: Reflection

Reflection is a C# language mechanism for accessing dynamic object properties on runtime. Typically, reflection is used to fetch the information about dynamic object type and object attribute values. In REST application, for example, reflection could be used to iterate through serialized response object.

Remark: According to MS guidelines performance critical code should avoid reflection. See https://msdn.microsoft.com/en-us/library/ff647790.aspx

### Section 63.1: Get the members of a type

```
using System;
using System.Reflection;
using System.Linq;

public class Program
{
    public static void Main()
    {
        var members = typeof(object)
            .GetMembers(BindingFlags.Public |
                        BindingFlags.Static |
                        BindingFlags.Instance);

        foreach (var member in members)
        {
            bool inherited = member.DeclaringType.Equals(typeof(object).Name );
            Console.WriteLine($"{member.Name} is a {member.MemberType}, " +
                $"it has {(inherited ? "":"not")} been inherited.");
        }
    }
}
```

Output (see note about output order further down):

GetType is a Method, it has not been inherited. GetHashCode is a Method, it has not been inherited. ToString is a Method, it has not been inherited. Equals is a Method, it has not been inherited. Equals is a Method, it has not been inherited. ReferenceEquals is a Method, it has not been inherited. .ctor is a Constructor, it has not been inherited.

We can also use the GetMembers() without passing any BindingFlags. This will return all public members of that specific type.

One thing to note that GetMembers does not return the members in any particular order, so never rely on the order that GetMembers returns you.

View Demo

### Section 63.2: Get a method and invoke it

#### Get Instance method and invoke it

```
using System;

public class Program
{
    public static void Main()
    {
