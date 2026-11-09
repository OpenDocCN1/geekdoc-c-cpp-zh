When a catch block accepts the exception, the CLR records where the exception was caught. If, inside a catch block, you now access the thrown exception object’s StackTrace property, the code that implements the property calls into the CLR, which builds a string identifying all of the methods between the place where the exception was thrown and the filter that caught the exception.

**Important** When you throw an exception, the CLR resets the starting point for the exception; that is, the CLR remembers only the location where the most recent exception object was thrown.

The following code throws the same exception object that it caught and causes the CLR to reset its starting point for the exception:

```
private void SomeMethod() {
    try { ... }
    catch (Exception e) {
        throw e;  // CLR thinks this is where exception originated.
                   // FxCop reports this as an error
    }
}
```

In contrast, if you re-throw an exception object by using the throw keyword by itself, the CLR doesn't reset the stack's starting point. The following code re-throws the same exception object that it caught, causing the CLR to not reset its starting point for the exception:

```
private void SomeMethod() {
    try { ... }
    catch (Exception e) {
        ...
        throw;  // This has no effect on where the CLR thinks the exception
                // originated. FxCop does NOT report this as an error
    }
}
```

In fact, the only difference between these two code fragments is what the CLR thinks is the original location where the exception was thrown. Unfortunately, when you re-throw an exception, Windows does reset the stack’s starting point. So if the exception becomes unhandled, the stack location that gets reported to Windows Error Reporting is the location of the last throw or re-throw, even though the CLR knows the stack location where the original exception was thrown. This is unfortunate because it makes debugging applications that have failed in the field much more difficult. Some developers have found this so intolerable that they have chosen a different way to implement their code to ensure that the stack trace truly reflects the location where an exception was originally thrown:

```
private void SomeMethod() {
    Boolean trySucceeds = false;
    try {
        ...
        trySucceeds = true;
    }
}
```