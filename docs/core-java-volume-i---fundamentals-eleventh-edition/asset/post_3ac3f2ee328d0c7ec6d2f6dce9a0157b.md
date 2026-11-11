
information in a file therefore will need to notify the compiler that it can throw some sort of `IOException`.

The place in which you advertise that your method can throw an exception is the header of the method; the header changes to reflect the checked exceptions the method can throw. For example, here is the declaration of one of the constructors of the `FileInputStream` class from the standard library. (See Chapter 1 of Volume II for more on input and output.)

```java
public FileInputStream(String name) throws FileNotFoundException
```

The declaration says that this constructor produces a `FileInputStream` object from a `String` parameter but that it also can go wrong in a special way—by throwing a `FileNotFoundException`. If this sad state should come to pass, the constructor call will not initialize a new `FileInputStream` object but instead will throw an object of the `FileNotFoundException` class. If it does, the runtime system will begin to search for a `FileNotFoundException` handler that knows how to deal with `FileNotFoundException` objects.

When you write your own methods, you don’t have to advertise every possible throwable object that your method might actually throw. To understand when (and what) you have to advertise in the throws clause of the methods you write, keep in mind that an exception is thrown in any of the following four situations:

- You call a method that throws a checked exception—for example, the `FileInputStream` constructor.
- You detect an error and throw a checked exception with the `throw` statement (we cover the `throw` statement in the next section).
- You make a programming error, such as `a[-1] = 0` that gives rise to an unchecked exception (in this case, an `ArrayIndexOutOfBoundsException`).
- An internal error occurs in the virtual machine or runtime library.

If either of the first two scenarios occurs, you must tell the programmers who will use your method about the possibility of an exception. Why? Any method that throws an exception is a potential death trap. If no handler catches the exception, the current thread of execution terminates.

As with Java methods that are part of the supplied classes, you declare that your method may throw an exception with an *exception specification* in the method header.

```java
class MyAnimation
{
    . . .
    public Image loadImage(String s) throws IOException
    {
        . . .
    }
}
```

If a method might throw more than one checked exception type, you must list all exception classes in the header. Separate them by commas, as in the following example:

```java
class MyAnimation
{
    . . .
    public Image loadImage(String s) throws FileNotFoundException, EOFException
    {
        . . .
    }
}
```

However, you do not need to advertise internal Java errors—that is, exceptions inheriting from *Error*. Any code could potentially throw those exceptions, and they are entirely beyond your control.

Similarly, you should not advertise unchecked exceptions inheriting from *RuntimeException*.

```java
class MyAnimation
{
    . . .
    void drawImage(int i) throws ArrayIndexOutOfBoundsException // bad style
    {
        . . .
    }
}
```

These runtime errors are completely under your control. If you are so concerned about array index errors, you should spend your time fixing them instead of advertising the possibility that they can happen.

In summary, a method must declare all the *checked* exceptions that it might throw. Unchecked exceptions are either beyond your control (*Error*) or result from conditions that you should not have allowed in the first place (*RuntimeException*). If your method fails to faithfully declare all checked exceptions, the compiler will issue an error message.

Of course, as you have already seen in quite a few examples, instead of declaring the exception, you can also catch it. Then the exception won’t be thrown out of the method, and no throws specification is necessary. You will see later in this chapter how to decide whether to catch an exception or to enable someone else to catch it.

> **CAUTION:** If you override a method from a superclass, the checked exceptions that the subclass method declares cannot be more general than those of the superclass method. (It is OK to throw more specific exceptions, or not to throw any exceptions in the subclass method.) In particular, if the superclass method throws no checked exception at all, neither can the subclass. For example, if you override `JComponent.paintComponent`, your `paintComponent` method must not throw any checked exceptions, because the superclass method doesn’t throw any.

When a method in a class declares that it throws an exception that is an instance of a particular class, it may throw an exception of that class or of any of its subclasses. For example, the `FileInputStream` constructor could have declared that it throws an `IOException`. In that case, you would not have known what kind of `IOException` it is; it could be a plain `IOException` or an object of one of the various subclasses, such as `FileNotFoundException`.

> **C++ NOTE:** The throws specifier is the same as the throw specifier in C++, with one important difference. In C++, throw specifiers are enforced at runtime, not at compile time. That is, the C++ compiler pays no attention to exception specifications. But if an exception is thrown in a function that is not part of the throw list, the unexpected function is called, and, by default, the program terminates.
>
> Also, in C++, a function may throw any exception if no throw specification is given. In Java, a method without a throws specifier may not throw any checked exceptions at all.

## 7.1.3 How to Throw an Exception

Now, suppose something terrible has happened in your code. You have a method, `readData`, that is reading in a file whose header promised

```
Content-Length: 1024
```

but you got an end of file after 733 characters. You may decide this situation is so abnormal that you want to throw an exception.

You need to decide what exception type to throw. Some kind of `IOException` would be a good choice. Perusing the Java API documentation, you find an `EOFException` with the description “Signals that an EOF has been reached unexpectedly during input.” Perfect. Here is how you throw it:

```java
throw new EOFException();
```

or, if you prefer,

```java
var e = new EOFException();
throw e;
```

Here is how it all fits together:

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

The EOFException has a second constructor that takes a string argument. You can put this to good use by describing the exceptional condition more carefully.

```java
String gripe = "Content-length: " + len + ", Received: " + n;
throw new EOFException(gripe);
```

As you can see, throwing an exception is easy if one of the existing exception classes works for you. In this case:

1. Find an appropriate exception class.
2. Make an object of that class.
3. Throw it.

Once a method throws an exception, it does not return to its caller. This means you do not have to worry about cooking up a default return value or an error code.

> **C++ NOTE:** Throwing an exception is the same in C++ and in Java, with one small difference. In Java, you can throw only objects of subclasses of Throwable. In C++, you can throw values of any type.

## 7.1.4 Creating Exception Classes

Your code may run into a problem which is not adequately described by any of the standard exception classes. In this case, it is easy enough to create your own exception class. Just derive it from Exception, or from a child class of Exception such as IOException. It is customary to give both a default constructor and a constructor that contains a detailed message. (The toString method of the Throwable superclass returns a string containing that detailed message, which is handy for debugging.)

```java
class FileFormatException extends IOException
{
   public FileFormatException() {}
   public FileFormatException(String gripe)
   {
      super(gripe);
   }
}
```

Now you are ready to throw your very own exception type.

```java
String readData(Scanner in) throws FileFormatException
{
   . . .
   while (. . .)
   {
      if (ch == -1) // EOF encountered
      {
         if (n < len)
            throw new FileFormatException();
      }
      . . .
   }
   return s;
}
```

- **java.lang.Throwable 1.0**
  - `Throwable()`
    constructs a new Throwable object with no detailed message.
  - `Throwable(String message)`
    constructs a new Throwable object with the specified detailed message. By convention, all derived exception classes support both a default constructor and a constructor with a detailed message.
  - `String getMessage()`
    gets the detailed message of the Throwable object.
