In contrast, if you re-throw an exception object by using the throw keyword by itself, the CLR doesn't reset the stack's starting point. The following code re-throws the same exception object that it caught, causing the CLR to not reset its starting point for the exception.

```
    private void SomeMethod() {
        try {
            ...
        }
        catch (Exception e) {
            ...
            throw;   // This has no effect on where the CLR thinks the exception
                     // originated. FxCop does NOT report this as an error
        }
    }
```

In fact, the only difference between these two code fragments is what the CLR thinks is the original location where the exception was thrown. Unfortunately, when you throw or re-throw an exception, Windows does reset the stack's starting point. So if the exception becomes unhandled, the stack location that gets reported to Windows Error Reporting is the location of the last throw or re-throw, even though the CLR knows the stack location where the original exception was thrown. This is unfortunate because it makes debugging applications that have failed in the field much more difficult. Some developers have found this so intolerable that they have chosen a different way to implement their code to ensure that the stack trace truly reflects the location where an exception was originally thrown.

```
    private void SomeMethod() {
        Boolean trySucceeds = false;
        try {
            ...
            trySucceeds = true;
        }
        finally {
            if (!trySucceeds) { /* catch code goes in here */ }
        }
    }
```

The string returned from the StackTrace property doesn't include any of the methods in the call stack that are above the point where the catch block accepted the exception object. If you want the complete stack trace from the start of the thread up to the exception handler, you can use the System.Diagnostics.StackTrace type. This type defines some properties and methods that allow a developer to programmatically manipulate a stack trace and the frames that make up the stack trace.

You can construct a StackTrace object by using several different constructors. Some constructors build the frames from the start of the thread to the point where the StackTrace object is constructed. Other constructors initialize the frames of the StackTrace object by using an Exception-derived object passed as an argument.

If the CLR can find debug symbols (located in the .pdb files) for your assemblies, the string returned by System.Exception's StackTrace property or System.Diagnostics.StackTrace's ToString method will include source code file paths and line numbers. This information is incredibly useful for debugging.