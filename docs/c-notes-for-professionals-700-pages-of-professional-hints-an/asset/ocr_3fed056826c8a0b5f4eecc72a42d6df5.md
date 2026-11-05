> > A partial method has its signature defined in one part of a partial type, and its implementation defined in another part of the type. Partial methods enable class designers to provide method hooks, similar to event handlers, that developers may decide to implement or not. If the developer does not supply an implementation, the compiler removes the signature at compile time. The following conditions apply to partial methods:
> >
> > * Signatures in both parts of the partial type must match.
> > * The method must return void.
> > * No access modifiers are allowed. Partial methods are implicitly private.
> >
> > -- MSDN

**File1.cs**

```
```csharp
namespace A
{
    public partial class Test
    {
        public string Var1 {get;set;}
        public partial Method1(string str);
    }
}
```
```

**File2.cs**

```
```csharp
namespace A
{
    public partial class Test
    {
        public string Var2 {get;set;}
        public partial Method1(string str)
        {
            Console.WriteLine(str);
        }
    }
}
```
```

**Note:** The type containing the partial method must also be declared partial.

# ## Section 52.63: event

An event allows the developer to implement a notification pattern.

**Simple example**

```
```csharp
public class Server
{
    // defines the event
    public event EventHandler DataChangeEvent;

    void RaiseEvent()
    {
        var ev = DataChangeEvent;
        if(ev != null)
        {
            ev(this, EventArgs.Empty);
        }
    }
}
```
```