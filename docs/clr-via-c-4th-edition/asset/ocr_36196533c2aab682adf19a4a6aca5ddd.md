# # Raising an Event in a Thread-Safe Way

When the .NET Framework first shipped, the recommended way for developers to raise an event was by using code similar to the following.

```
```csharp
// Version 1
protected virtual void OnNewMail(NewMailEventArgs e) {
    if (NewMail != null) NewMail(this, e);
}
```
```

The problem with the OnNewMail method is that the thread could see that NewMail is not null, and then, just before invoking NewMail, another thread could remove a delegate from the chain making NewMail null, resulting in a NullReferenceException being thrown. To fix this race condition, many developers write the OnNewMail method as follows.

```
```csharp
// Version 2
protected virtual void OnNewMail(NewMailEventArgs e) {
    EventHandler<NewMailEventArgs> temp = NewMail;
    if (temp != null) temp(this, e);
}
```
```

The thinking here is that a reference to NewMail is copied into a temporary variable, temp, which refers to the chain of delegates at the moment the assignment is performed. Now, this method compares temp and null and invokes temp, so it doesn't matter if another thread changes NewMail after the assignment to temp. Remember that delegates are immutable and this is why this technique works in theory. However, what a lot of developers don't realize is that this code could be optimized by the compiler to remove the local temp variable entirely. If this happens, this version of the code is identical to the first version, so a NullReferenceException is still possible.

To really fix this code, you should rewrite OnNewMail like the following.

```
```csharp
// Version 3
protected virtual void OnNewMail(NewMailEventArgs e) {
    EventHandler<NewMailEventArgs> temp = Volatile.Read(ref NewMail);
    if (temp != null) temp(this, e);
}
```
```

The call to Volatile.Read forces NewMail to be read at the point of the call and the reference really has to be copied to the temp variable now. Then, temp will be invoked only if it is not null. See Chapter 29, "Primitive Thread Synchronization Constructs," for more information about the Volatile.Read method.