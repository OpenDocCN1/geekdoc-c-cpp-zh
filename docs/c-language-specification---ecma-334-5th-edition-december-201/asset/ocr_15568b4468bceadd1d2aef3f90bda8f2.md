# 13.13 The lock statement

The lock statement obtains the mutual-exclusion lock for a given object, executes a statement, and then releases the lock.

```
lock-statement:
    lock ( expression ) embedded-statement
```

The expression of a lock statement shall denote a value of a type known to be a reference. No implicit boxing conversion (§11.2.8) is ever performed for the expression of a lock statement, and thus it is a compile-time error for the expression to denote a value of a value-type.

A lock statement of the form

```
lock ( x ) ...
```

where x is an expression of a reference-type, is precisely equivalent to:

```
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, ref __lockwasTaken);  ...
}
finally {
    if (__lockwasTaken) System.Threading.Monitor.Exit(x);
}
```

except that x is only evaluated once.

While a mutual-exclusion lock is held, code executing in the same execution thread can also obtain and release the lock. However, code executing in other threads is blocked from obtaining the lock until the lock is released.

# 13.14 The using statement

The using statement obtains one or more resources, executes a statement, and then disposes of the resource.

```
using-statement:
    using ( resource-acquisition ) embedded-statement
resource-acquisition:
    local-variable-declaration
    expression
```

A resource is a class or struct that implements the System.IDisposable interface, which includes a single parameterless method named Dispose. Code that is using a resource can call dispose to indicate that the resource is no longer needed.