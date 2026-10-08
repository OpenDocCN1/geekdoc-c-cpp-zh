then having the back trace from an unhandled exception can be very useful.

# Using the Unified Exception Model

```
try {
    @throw @"An exception!";
} catch (int a) {
    NSLog(\@"Caught: %d", a);
} catch (id exception) {
    NSLog(\@"Caught: %@", exception);
}
```

*From: tryCatch.mm*

With early Objective-C++ implementations, the Objective-C and C++ exception models were completely different and incompatible. You could throw C++ exceptions with throw and catch them with catch. You could throw Objective-C++ exceptions with @throw and catch them with @throw. You could mix these two within a program, but not within the same function and not for the same exception.

With more recent implementations, Objective-C++ uses a unified exception model. A catch statement with an Objective-C type can catch objects thrown with @throw. Similarly, a throw statement with an Objective-C type produces an exception that can be caught with @catch.

The snippet at the start of this section shows