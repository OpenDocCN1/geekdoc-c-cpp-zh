
Note: Since Dispose is guaranteed to be called irrespective of the code flow, it's a good idea to make sure that Dispose never throws an exception when you implement IDisposable. Otherwise an actual exception would get overridden by the new exception resulting in a debugging nightmare.

## Returning from using block

```
using ( var disposable = new DisposableItem() )
{
    return disposable.SomeProperty;
}
```

Because of the semantics of try ...finally to which the using block translates, the return statement works as expected - the return value is evaluated before finally block is executed and the value disposed. The order of evaluation is as follows:

- 1. Evaluate the try body
- 2. Evaluate and cache the returned value
- 3. Execute finally block
- 4. Return the cached return value

However, you may not return the variable disposable itself, as it would contain invalid, disposed reference - see related example.

## Section 60.2: Gotcha: returning the resource which you are disposing

The following is a bad idea because it would dispose the db variable before returning it.

```
public IDBContext GetDBContext()
{
    using (var db = new DBContext())
    {
        return db;
    }
}
```

This can also create more subtle mistakes:

```
public IEnumerable<Person> GetPeople(int age)
{
    using (var db = new DBContext())
    {
        return db.Persons.Where(p => p.Age == age);
    }
}
```

This looks ok, but the catch is that the LINQ expression evaluation is lazy, and will possibly only be executed later when the underlying DBContext has already been disposed.

So in short the expression isn't evaluated before leaving the using. One possible solution to this problem, which still makes use of using, is to cause the expression to evaluate immediately by calling a method that will enumerate the result. For example ToList(), ToArray(), etc. If you are using the newest version of Entity Framework you could use the async counterparts like ToListAsync() or ToArrayAsync().

Below you find the example in action:

```csharp
public IEnumerable<Person> GetPeople(int age)
{
    using (var db = new DBContext())
    {
        return db.Persons.Where(p => p.Age == age).ToList();
    }
}
```

It is important to note, though, that by calling ToList() or ToArray(), the expression will be eagerly evaluated, meaning that all the persons with the specified age will be loaded to memory even if you do not iterate on them.

## Section 60.3: Multiple using statements with one block

It is possible to use multiple nested using statements without added multiple levels of nested braces. For example:

```csharp
using (var input = File.OpenRead("input.txt"))
{
    using (var output = File.OpenWrite("output.txt"))
    {
        input.CopyTo(output);
    } // output is disposed here
} // input is disposed here
```

An alternative is to write:

```csharp
using (var input = File.OpenRead("input.txt"))
using (var output = File.OpenWrite("output.txt"))
{
    input.CopyTo(output);
} // output and then input are disposed here
```

Which is exactly equivalent to the first example.

Note: Nested using statements might trigger Microsoft Code Analysis rule CS2002 (see this answer for clarification) and generate a warning. As explained in the linked answer, it is generally safe to nest using statements.

When the types within the using statement are of the same type you can comma-delimit them and specify the type only once (though this is uncommon):

```csharp
using (FileStream file = File.Open("MyFile.txt"), file2 = File.Open("MyFile2.txt"))
{
}
```

This can also be used when the types have a shared hierarchy:

```csharp
using (Stream file = File.Open("MyFile.txt"), data = new MemoryStream())
{
}
```

The var keyword cannot be used in the above example. A compilation error would occur. Even the comma separated declaration won't work when the declared variables have types from different hierarchies.

## Section 60.4: Gotcha: Exception in Dispose method masking other errors in Using blocks

Consider the following block of code.

```
try
{
    using (var disposable = new MyDisposable())
    {
        throw new Exception("Couldn't perform operation.");
    }
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}

class MyDisposable : IDisposable
{
    public void Dispose()
    {
        throw new Exception("Couldn't dispose successfully.");
    }
}
```

You may expect to see "Couldn't perform operation" printed to the Console but you would actually see "Couldn't dispose successfully." as the Dispose method is still called even after the first exception is thrown.

It is worth being aware of this subtlety as it may be masking the real error that prevented the object from being disposed and make it harder to debug.

## Section 60.5: Using statements are null-safe

You don't have to check the IDisposable object for null. using will not throw an exception and Dispose() will not be called:

```
DisposableObject TryOpenFile()
{
    return null;
}

// disposable is null here, but this does not throw an exception
using (var disposable = TryOpenFile())
{
    // this will throw a NullReferenceException because disposable is null
    disposable.DoSomething();

    if(disposable != null)
    {
        // here we are safe because disposable has been checked for null
        disposable.DoSomething();
    }
}
```

## Section 60.6: Using Dispose Syntax to define custom scope

For some use cases, you can use the using syntax to help define a custom scope. For example, you can define the following class to execute code in a specific culture.

```
public class CultureContext : IDisposable
{
    private readonly CultureInfo originalCulture;

    public CultureContext(string culture)
    {
        originalCulture = CultureInfo.CurrentCulture;
        Thread.CurrentThread.CurrentCulture = new CultureInfo(culture);
    }

    public void Dispose()
    {
        Thread.CurrentThread.CurrentCulture = originalCulture;
    }
}
```

You can then use this class to define blocks of code that execute in a specific culture.

```
Thread.CurrentThread.CurrentCulture = new CultureInfo("en-US");

using (new CultureContext("nl-NL"))
{
    // Code in this block uses the "nl-NL" culture
    Console.WriteLine(new DateTime(2016, 12, 25)); // Output: 25-12-2016 00:00:00
}

using (new CultureContext("es-ES"))
{
    // Code in this block uses the "es-ES" culture
    Console.WriteLine(new DateTime(2016, 12, 25)); // Output: 25/12/2016 0:00:00
}

// Reverted back to the original culture
Console.WriteLine(new DateTime(2016, 12, 25)); // Output: 12/25/2016 12:00:00 AM
```

Note: as we don't use the CultureContext instance we create, we don't assign a variable for it.

This technique is used by the BeginForm helper in ASP.NET MVC.

## Section 60.7: Using Statements and Database Connections

The using keyword ensures that the resource defined within the statement only exists within the scope of the statement itself. Any resources defined within the statement must implement the IDisposable interface.

These are incredibly important when dealing with any connections that implement the IDisposable interface as it can ensure the connections are not only properly closed but that their resources are freed after the using statement is out of scope.

## Common IDisposable Data Classes

Many of the following are data-related classes that implement the IDisposable interface and are perfect candidates for a using statement:

- SqlConnection, SqlCommand, SqlDataReader, etc.
- OleDbConnection, OleDbCommand, OleDbDataReader, etc.
- MySqlConnection, MySqlCommand, MySqlDataReader, etc.
- DbContext

## Section 60.8: Executing code in constraint context

If you have code (a routine) you want to execute under a specific (constraint) context, you can use dependency injection.

The following example shows the constraint of executing under an open SSL connection. This first part would be in your library or framework, which you won't expose to the client code.

```
public static class SSLContext
{
    // define the delegate to inject
    public delegate void TunnelRoutine(BinaryReader sslReader, BinaryWriter sslWriter);

    // this allows the routine to be executed under SSL
    public static void ClientTunnel(TcpClient tcpClient, TunnelRoutine routine)
    {
        using (SslStream sslStream = new SslStream(tcpClient.GetStream(), true, _validate))
        {
            sslStream.AuthenticateAsClient(HOSTNAME, null, SslProtocols.Tls, false);

            if (!sslStream.IsAuthenticated)
            {
                throw new SecurityException("SSL tunnel not authenticated");
            }

            if (!sslStream.IsEncrypted)
            {
                throw new SecurityException("SSL tunnel not encrypted");
            }

            using (BinaryReader sslReader = new BinaryReader(sslStream))
            using (BinaryWriter sslWriter = new BinaryWriter(sslStream))
            {
                routine(sslReader, sslWriter);
            }
        }
    }
}
```

Now the client code which wants to do something under SSL but does not want to handle all the SSL details. You can now do whatever you want inside the SSL tunnel, for example exchange a symmetric key:

```
public void ExchangeSymmetricKey(BinaryReader sslReader, BinaryWriter sslWriter)
{
    byte[] bytes = new byte[8];
    (new RNGCryptoServiceProvider()).GetNonZeroBytes(bytes);
    sslWriter.Write(BitConverter.ToInt64(bytes, 0));
}
```

You execute this routine as follows:

```
SSLContext.ClientTunnel(tcpClient, this.ExchangeSymmetricKey);
```

To do this, you need the using() clause because it is the only way (apart from a try...finally block) you can guarantee the client code (ExchangeSymmetricKey) never exits without properly disposing of the disposable resources. Without using() clause, you would never know if a routine could break the context's constraint to dispose of those resources.
