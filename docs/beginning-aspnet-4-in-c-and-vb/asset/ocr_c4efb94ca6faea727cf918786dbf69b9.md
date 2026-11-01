Within the finally block, you can release any resources you have used. The only trouble with this method is that you have to ensure that you close the connection — it is all too easy to forget to add the finally clause, so something less prone to vagaries of coding style might be worthwhile.

In addition, you might find that you open a number of resources (say two database connections and a file) within a given method, so the cascade of try...catch...finally blocks can sometimes become less easy to read. There is, however, another way to guarantee resource cleanup — the using statement.

# Option Two: The using Block Statement

During development of C#, the debate on how .NET uses nondeterministic destruction became very heated.

In C++, as soon as an object went out of scope, its destructor would be automatically called. This was great news for designers of resource-based classes because the destructor was the ideal place to close the resource if the user had forgotten to do so. A C++ destructor is called whenever an object goes out of scope — so, for instance, if an exception were raised and not caught, all destructors would be called.

With C# and the other managed languages, there is no concept of automatic, deterministic destruction. Instead, there is the garbage collector, which disposes of resources at some point in the future. What makes this nondeterministic is that you have little say over when this process actually happens. Forgetting to close a database connection could cause all sorts of problems for a .NET executable. Luckily, help is at hand.

The following code demonstrates how to use the using clause to ensure that objects that implement the IDisposable interface (see Chapter 13, “Memory Management and Pointers”) are cleared up immediately after the block exits:

```
```csharp
string source = "server=(local);" +
                "integrated security=SSPI;" +
                "database=Northwind";

using ( SqlConnection conn = new SqlConnection ( source ) )
{
    // Open the connection
    conn.Open ( );
    // Do something useful
}
```
```

In this instance, the using clause ensures that the database connection is closed, regardless of how the block is exited.

Looking at the IL code for the Dispose() method of the connection classes, you can see that all of them check the current state of the connection object and, if it is open, will call the Close() method. A great tool for browsing .NET assemblies is Reflector (available at www.red-gate.com/products/reflector/). This tool permits you to view the IL code for any .NET method and will also reverse-engineer the IL into C# source code, so you can easily see what a given method is doing.

When programming, you should use at least one of these methods, and probably both. Wherever you acquire resources, it is good practice to use the using statement; even though we all mean to write the Close() statement, sometimes we forget, and in the face of exceptions the using clause does the right thing. There is no substitute for good exception handling either, so in most instances, it is best to use both methods together, as in the following example:

```
```csharp
try
{
    using (SqlConnection conn = new SqlConnection ( source ))
    {
        // Open the connection
        conn.Open ( );
        // Do something useful
```
```