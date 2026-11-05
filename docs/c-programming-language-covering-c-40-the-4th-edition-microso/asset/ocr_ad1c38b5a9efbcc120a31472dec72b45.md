produces the output

```
B's destructor
A's destructor
```

since destructors in an inheritance chain are called in order, from most derived to least derived.

> ERIC LIPPERT Traditionally, the term “destructor” refers to a deterministic cleanup method and a “finalizer” refers to a nondeterministic cleanup method called by a garbage collector. “Destructor” is a bit of an unfortunate misnomer in C#; ideally these methods would be called “finalizers” and the Dispose method of IDisposable would be called a “destructor.”

Destructors are implemented by overriding the virtual method Finalize on System.Object. C# programs are not permitted to override this method or call it (or overrides of it) directly. For instance, the program

```
class A
{
    override protected void Finalize() { }    // Error
    public void F()
    {
        this.Finalize();    // Error
    }
}
```

contains two errors.

The compiler behaves as if this method, and overrides of it, do not exist at all. Thus the program

```
class A
{
    void Finalize() { }    // Permitted
}
```

is valid, and the method shown hides System.Object's Finalize method.

For a discussion of the behavior when an exception is thrown from a destructor, see §16.3.