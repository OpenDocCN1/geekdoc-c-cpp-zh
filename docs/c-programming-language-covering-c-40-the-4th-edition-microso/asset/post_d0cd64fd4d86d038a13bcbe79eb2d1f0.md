
The **try** block of a **try** statement is reachable if the **try** statement is reachable.

A **catch** block of a **try** statement is reachable if the **try** statement is reachable.

The **finally** block of a **try** statement is reachable if the **try** statement is reachable.

The end point of a **try** statement is reachable if both of the following are true:

- The end point of the **try** block is reachable or the end point of at least one **catch** block is reachable.
- If a **finally** block is present, the end point of the **finally** block is reachable.

## 8.11 The checked and unchecked Statements

The **checked** and **unchecked** statements are used to control the *overflow* checking context for integral-type arithmetic operations and conversions.

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

The **checked** statement causes all expressions in the *block* to be evaluated in a **checked** context. The **unchecked** statement causes all expressions in the *block* to be evaluated in an **unchecked** context.

The **checked** and **unchecked** statements are precisely equivalent to the **checked** and **unchecked** operators (§7.6.12), except that they operate on blocks instead of expressions.

## 8.12 The lock Statement

The **lock** statement obtains the mutual-exclusion lock for a given object, executes a statement, and then releases the lock.

```
lock-statement:
    lock ( expression ) embedded-statement
```

The expression of a **lock** statement must denote a value of a type known to be a *reference-type*. No implicit boxing conversion (§6.1.7) is ever performed for the expression of a **lock** statement, and thus it is a compile-time error for the expression to denote a value of a value-type.

A lock statement of the form

```
lock (x) ...
```

where x is an expression of a reference-type, is precisely equivalent to

```
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, __lockWasTaken);
    ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```

except that x is evaluated only once.

> **BILL WAGNER** The lock() statement provides additional compiler checks against trying to lock a value type.

While a mutual-exclusion lock is held, code executing in the same execution thread can also obtain and release the lock. However, code executing in other threads is blocked from obtaining the lock until the lock is released.

Locking System.Type objects so as to synchronize access to static data is not recommended. Other code might lock on the same type, which can result in deadlock. A better approach is to synchronize access to static data by locking a private static object. For example:

```
class Cache
{
    private static readonly object synchronizationObject = new object();
    public static void Add(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }

    public static void Remove(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }
}
```

> **JOSEPH ALBAHARI** A good policy, when writing libraries for public consumption, is to make static functions thread-safe from the outset (typically, by implementing locking *within* your functions, as in this example). It’s much more difficult (or even impossible) for consumers to lock around calling your static methods or properties, because they won’t know from which other locations your functions are called.

## 8.13 The using Statement

The using statement obtains one or more resources, executes a statement, and then disposes of the resource.

> **ERIC LIPPERT** The specification explicitly calls out here, the point of a using statement is to ensure the acquisition of and timely disposal of a *resource*. Typically, this will consist of some unmanaged resource from the operating system, such as a file handle. It is polite to stop using resources as soon as possible; some other program might want to read that file when you’re done with it. I recommend against the use of using statements to enforce program invariants. For example, one sometimes sees code like this:
>
> ```csharp
> using(new TemporarilyStopReportingErrors()) AttemptSomething();
> ```
>
> Here TemporarilyStopReportingErrors is a type whose constructor turns off error reporting as a side effect and whose disposal method turns it back on. I consider this (unfortunately widespread) practice to be an abuse of the using statement; a program side effect is not a resource, and causing global side effects in constructors and disposers seems like a bad idea. I would write this code using a try-finally construct instead.

```
using-statement:
    using ( resource-acquisition ) embedded-statement

resource-acquisition:
    local-variable-declaration
    expression
```

A *resource* is a class or struct that implements System.IDisposable, which includes a single parameterless method named Dispose. Code that is using a resource can call Dispose to indicate that the resource is no longer needed. If Dispose is not called, then automatic disposal eventually occurs as a consequence of garbage collection.

> **JOSEPH ALBAHARI** Calling Dispose doesn’t influence garbage collection in any way: An object becomes eligible for automatic garbage collection when (and only when) no other object refers to it. Likewise, garbage collection doesn’t influence disposal: The garbage collector will not call Dispose unless you write a finalizer (destructor) that explicitly makes this call.
>
> The two activities most commonly performed within a Dispose method are releasing unmanaged resources and calling Dispose on other referenced or “owned” objects. It is also possible to release unmanaged resources from within a finalizer, although such an operation means waiting an indeterminate amount of time for the garbage collector to fire. This is why IDisposable exists.

If the form of *resource-acquisition* is *local-variable-declaration*, then the type of the *local-variable-declaration* must be either dynamic or a type that can be implicitly converted to `System.IDisposable`. If the form of *resource-acquisition* is *expression*, then this expression must be implicitly convertible to `System.IDisposable`.

Local variables declared in a *resource-acquisition* are read-only, and must include an initializer. A compile-time error occurs if the embedded statement attempts to modify these local variables (via assignment or the ++ and -- operators), take the address of them, or pass them as ref or out parameters.

A using statement is translated into three parts: acquisition, usage, and disposal. Usage of the resource is implicitly enclosed in a try statement that includes a finally clause. This finally clause disposes of the resource. If a null resource is acquired, then no call to Dispose is made, and no exception is thrown. If the resource is of type dynamic, it is dynamically converted through an implicit dynamic conversion (§6.1.8) to IDisposable during acquisition to ensure that the conversion is successful before the usage and disposal take place.

A using statement of the form

```
using (ResourceType resource = expression) statement
```

corresponds to one of three possible expansions. When ResourceType is a non-nullable value type, the expansion is

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        ((IDisposable)resource).Dispose();
    }
}
```

Otherwise, when ResourceType is a nullable value type or a reference type other than dynamic, the expansion is

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        if (resource != null) ((IDisposable)resource).Dispose();
    }
}
```

Otherwise, when ResourceType is dynamic, the expansion is

```
{
    ResourceType resource = expression;
    IDisposable d = (IDisposable)resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

In either expansion, the resource variable is read-only in the embedded statement, and the d variable is inaccessible in, and invisible to, the embedded statement.

> **PETER SESTOFT** Thanks to the above rule, the using statement could also be (ab)used to declare read-only local variables, in this style:
>
> ```csharp
> using (MyClass v = ...)
> using (MyStruct s = ...) {
>     ...
> }
> ```
>
> In fact, this is the only way to declare an immutable local variable in C#, but it is ugly and strange. Moreover, it works only for types MyClass and MyStruct that implement interface IDisposable, and not for int and string, for example. What is perhaps puzzling from a language design point of view is that unlike a read-only field (§10.5.2 and §7.6.4) of struct type, an immutable resource variable s of struct type MyStruct is treated like a variable, not a value. Thus a method call s.SetX() acts on the struct stored in s, not on a copy of it. All in all, this behavior shows that the machinery for declaring immutable local variables and parameters in C# exists, but alas not in a usable form.
