
This depends, case by case. In most instances, I treat the occurrence of this type of exception as a bug in my code.

Notice that the list of documented exceptions shows up in IntelliSense as soon as you type the member name. Figure 23.20 shows this for the File.OpenRead method.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1235_0.png)

FIGURE 23.20 Documented exceptions for File.OpenRead.

The most commonly used constructor overload for ArgumentException looks as follows:

```csharp
public ArgumentException(string message, string paramName);
```

For the second parameter, specify the name of the parameter that received an invalid value. This data can be retrieved again through the ParamName property.

## ArgumentNullException

ArgumentNullException is the little, more specialized brother of ArgumentException and is used to signal an unexpected null reference supplied for a parameter. Again, it pinpoints a missing null check in your code and should be treated seriously. Ask yourself how the null reference got to that very place in the code to begin with.

Extinguish the evil null reference as close to its root as possible (for example, an entry point to the component you're developing). And the way to do it is by throwing exactly this exception. Constructors typically used for this purpose include the following:

```csharp
public ArgumentNullException(string paramName);
public ArgumentNullException(string paramName, string message);
```

The first constructor often suffices because the meaning of a null argument doesn't need much more explanation other than its parameter.

### THE API HALL OF SHAME AND FXCOP

If you choose to use the second overload, notice the little mess-up made by the framework designers back in the early .NET days: The paramName and message parameters are opposite compared to the ones on ArgumentException. As a band-aid, the FxCop rule "Microsoft.Usage CA2208" was introduced, which detects swapped arguments on the constructors of those exception types. It does so by inspecting the string passed to the paramName parameter against all the method's parameter names that are present.

### EXTENSION METHODS

A question that comes up sometimes is what exception type to use when an extension method's this parameter receives a null reference. At the call site, it looks like an instance method call, so a NullReferenceException may be the most natural thing to expect:

```csharp
var res = source.Where(n => n > 0); // LINQ's Where operator
```

However, NullReferenceException should really be reserved for real attempts to dereference a null reference, as detected by the runtime. This becomes especially apparent when the extension method is written as a regular static method call:

```csharp
var res = Enumerable.Where(source, n => n > 0);
```

Here you don't expect a NullReferenceException at all.

## ArgumentOutOfRangeException

Similar in spirit to the IndexOutOfRangeException for arrays, this exception type is used to signal a supplied argument is outside some range. Once more, it typically indicates sloppy input validation on the side of the caller, which should be avoidable in general.

Examples of the use of this exception type include the various collection data types in System.Collections and its sub-namespaces:

```csharp
var lst = new List<int> { 1, 2, 3 };
int thereIsNoThirdElement = lst[3];
```

Use of the exception type for your own APIs is straightforward using constructors similar to the ones seen for ArgumentException (with the paramName coming first). As a little reminder, keep in mind that argument and index are distinct concepts. Use of this type of exception doesn't imply any particular member type (like an indexer) or a specific data type (like a numeric value) is to be used. It's equally valid for a method to throw an exception of this type to signal its string argument was outside a range of acceptable values.

## InvalidOperationException

When an operation is carried out on an object that's not in a valid state to do so, this exception type is raised. Sometimes this is due to not following a certain "protocol" that may be documented informally in the documentation for the type. For example, an object might need some kind of Initialize call before any other members can be called. As a concrete example, consider the SqlConnection class from System.Data.SqlClient:

```csharp
using (SqlConnection conn = new SqlConnection(connString)) {
    Console.WriteLine(conn.ServerVersion);
}
```

Here the ServerVersion property getter will throw the discussed exception because the connection hasn't been opened yet by calling conn.Open().

This exception is also commonly thrown when enumerating over a collection while it's being modified. This invalidates enumerator objects that are in use because all sorts of things could have happened to the collection underneath. Although you might think all collection change operations could be accounted for inside the enumerator, there are quite a few interesting situations that can arise. For example, MoveNext may already have said there's still an element to follow, but a change happening immediately thereafter might get rid of the element. This would break the contract that a MoveNext call returning true ensures that the subsequent call to the Current method will succeed. For reasons such as these, any further use of the enumerator after a collection modification is simply disallowed:

```csharp
var lst = new List<int> { 1, 2, 3 };
foreach (var n in lst)
    lst.Add(n);
```

## NotImplementedException

As the name pretty much implies, this exception results whenever a method or member is not implemented. This can indicate you're dealing with a stub for functionality that's not yet implemented. Visual Studio's code editor Implement Interface feature uses this exception type for the method stubs it generates, as shown in Figure 23.21.

```csharp
class MyCollection<T> : IEnumerable<T>
{
    public IEnumerator<T> GetEnumerator()
    {
        throw new NotImplementedException();
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        throw new NotImplementedException();
    }
}
```

FIGURE 23.21  Code generated by Visual Studio's Implement Interface feature.

From a code-generation point of view, this is very beneficial because throwing an exception makes the compiler's flow analysis happy as well: If a method has to return an object, throwing an exception instead is the simplest way to make the generated code compile.

The use of NotImplementedException should be reserved to indicate missing functionality as opposed to signaling an operation is not supported. The former exception type is more often used for stubs, whereas the use of NotSupportedException indicates that a certain interface member implementation doesn't make sense in the context of the type that implements it. We come back to this in a second.

## NotSupportedException

NotSupportedException doesn't indicate an implementation of an operation is not present; instead, it means the operation doesn't make sense to implement. You might wonder why the operation isn't just omitted in such a case, but often you don't have a choice but to provide it when an interface is implemented or a base class has to be used.

Examples of the use of this exception type can be found in the System.IO namespace when dealing with Stream objects that do not support certain operations, such as Seek. It's not uncommon for custom derived stream objects to support only a fraction of the base class's functionality, hence warranting the use of NotSupportedException to indicate the missing functionality.

Another place where NotSupportedException occurs is in the code that gets emitted by the C# compiler for the implementation of an iterator. As you remember from our discussion about LINQ, iterators implement the IEnumerator<T> interface, which has a Reset method on it. However, this method gets a stock implementation that throws this exception:

```csharp
static IEnumerator<int> GetNumbers() {
    int i = 0;
    while (true)
        yield return i++;
}

static void Main() {
    var nums = GetNumbers();
    if (nums.MoveNext())
        Console.WriteLine(nums.Current);

    // Oops, we advanced the enumerator too far. Let's try to reset it...
    nums.Reset();            // Throws a NotSupportedException.

    if (nums.MoveNext())
        Console.WriteLine(nums.Current);
}
```

The Reset method was a bit of overengineering back in the .NET 1.0 days, mainly present for COM interop purposes (compare the IEnumVARIANT COM interface). Because the interface specifies this method may throw the NotSupportedException, it's not worth much as an abstraction we can rely on in general. In addition, it never gets called by the code emitted for foreach loops.

Because of all those reasons, Reset is mostly unused, and the C# iterator feature doesn't bother to support it either. Iterators are one of the most complex language features in terms of code generation, so avoiding further complication for an additional marginally useful Reset method was a welcome simplification. And if you really want to reset an iterator, just request a new one (which is a cheap operation anyway):
