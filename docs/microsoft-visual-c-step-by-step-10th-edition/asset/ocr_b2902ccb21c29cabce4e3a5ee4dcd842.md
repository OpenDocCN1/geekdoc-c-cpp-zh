| To | Do this |
|---|---|
| Call a finalizer | You can't call a finalizer. Only the garbage collector can call a finalizer. |
| Force garbage collection (not recommended) | Call GC.Collect. |
| Release a resource at a known point in time (but the risk of resource leaks if an exception interrupts the execution) | Write a disposal method (a method that disposes of a resource) and call it explicitly from the program. For example:\ [Click here to view code image]
```java
class TextReader
{
    public virtual void Close() {
        ...
    }
}
class Example
{
    void Use() {
        TextReader reader = ...;
        // use reader
        reader.Close();
    }
}
``` |
| Support exception-safe disposal in a class | Implement the IDisposable interface. For example: [Click here to view code image]
```java
class SafeResource : IDisposable
{
    ...
    public void Dispose() {
        // Dispose resources here
    }
}
``` |