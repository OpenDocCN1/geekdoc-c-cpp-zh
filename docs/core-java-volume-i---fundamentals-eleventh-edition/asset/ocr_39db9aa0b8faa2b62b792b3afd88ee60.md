```
```java
throw new EOFException();
```
```

or, if you prefer,

```
```java
var e = new EOFException();
throw e;
```
```

Here is how it all fits together:

```
```java
String readData(Scanner in) throws EOFException
{
    while (. . .)
    {
        if (!in.hasNext()) // EOF encountered
        {
            if (n < len)
                throw new EOFException();
        }
        . . .
        return s;
    }
}
```
```

The EOFException has a second constructor that takes a string argument. You can put this to good use by describing the exceptional condition more carefully.

```
```java
String gripe = "Content-length: " + len + ", Received: " + n;
throw new EOFException(gripe);
```
```

As you can see, throwing an exception is easy if one of the existing exception classes works for you. In this case:

+   1. Find an appropriate exception class.
+   2. Make an object of that class.
+   3. Throw it.

Once a method throws an exception, it does not return to its caller. This means you do not have to worry about cooking up a default return value or an error code.

> > **C++ NOTE:** Throwing an exception is the same in C++ and in Java, with one small difference. In Java, you can throw only objects of subclasses of Throwable. In C++, you can throw values of any type.