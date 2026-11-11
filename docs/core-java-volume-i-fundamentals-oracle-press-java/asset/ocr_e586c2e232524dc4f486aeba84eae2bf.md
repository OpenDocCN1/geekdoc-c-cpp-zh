```
java.lang.reflect.Constructor 1.1

• Object newInstance(Object... params)

constructs a new instance of the constructor's declaring class, passing params to the constructor. See Section 5.9.7, "Invoking Arbitrary Methods and Constructors," on p. 304 for more information on how to supply parameters.
```

```
java.lang.Throwable 1.0

• void printStackTrace()

prints the Throwable object and the stack trace to the standard error stream.
```

# 5.9.2 A Primer on Declaring Exceptions

I cover exception handling fully in Chapter 7, but in the meantime you will occasionally encounter methods that threaten to throw exceptions.

When an error occurs at runtime, a program can "throw an exception." Throwing an exception is more flexible than terminating the program because you can provide a *handler* that "catches" the exception and deals with it.

If you don't provide a handler, the program terminates and prints a message to the console, giving the type of the exception. You may have already seen exception reports when you accidentally used a `null` reference or overstepped the bounds of an array.

There are two kinds of exceptions: *unchecked* exceptions and *checked* exceptions. With checked exceptions, the compiler checks that you, the programmer, are aware of the exception and are prepared to deal with the consequences. However, many common exceptions, such as bounds errors,