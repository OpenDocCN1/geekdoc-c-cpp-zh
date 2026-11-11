
```java
out.println(in.next().toUpperCase());
}
```

No matter how the block exits, both `in` and `out` are closed. If you programmed this by hand, you would have needed two nested `try/finally` statements.

As of Java 9, you can provide previously declared effectively final variables in the `try` header:

```java
public static void printAll(String[] lines, PrintWriter out)
{
    try (out)
    { // effectively final variable
        for (String line : lines)
            out.println(line);
    } // out.close() called here
}
```

A difficulty arises when the `try` block throws an exception and the `close` method also throws an exception. The `try-with-resources` statement handles this situation quite elegantly. The original exception is rethrown, and any exceptions thrown by `close` methods are considered “suppressed.” They are automatically caught and added to the original exception with the `addSuppressed` method. If you are interested in them, call the `getSuppressed` method which yields an array of the suppressed exceptions from `close` methods.

You don’t want to program this by hand. Use the `try-with-resources` statement whenever you need to close a resource.

> **NOTE:**
>
> A `try-with-resources` statement can itself have `catch` clauses and even a `finally` clause. These are executed after closing the resources.

### 7.2.6 Analyzing Stack Trace Elements

A *stack trace* is a listing of all pending method calls at a particular point in the execution of a program. You have almost certainly seen stack trace listings—they are displayed whenever a Java program terminates with an uncaught exception.

You can access the text description of a stack trace by calling the `printStackTrace` method of the `Throwable` class.

```java
var t = new Throwable();
var out = new StringWriter();
t.printStackTrace(new PrintWriter(out));
String description = out.toString();
```

A more flexible approach is the `StackWalker` class that yields a stream of `StackWalker.StackFrame` instances, each describing one stack frame. You can iterate over the stack frames with this call:

```java
StackWalker walker = StackWalker.getInstance();
walker.forEach(frame -> analyze(frame));
```

If you want to process the `Stream<StackWalker.StackFrame>` lazily, call

```java
walker.walk(stream -> process(stream));
```

Stream processing is described in detail in [Chapter 1](#) of Volume II.

The `StackWalker.StackFrame` class has methods to obtain the file name and line number, as well as the class object and method name, of the executing line of code. The `toString` method yields a formatted string containing all of this information.

### java.lang.Throwable 1.0

- `Throwable(String message, Throwable cause)` 1.4 constructs a Throwable with a given cause.
- `Throwable initCause(Throwable cause)` 1.4 sets the cause for this object or throws an exception if this object already has a cause. Returns `this`.
- `Throwable getCause()` 1.4 gets the exception object that was set as the cause for this object, or null if no cause was set.
- `StackTraceElement[] getStackTrace()` 1.4 gets the trace of the call stack at the time this object was constructed.
- `void addSuppressed(Throwable t)` 7 adds a "suppressed" exception to this exception. This happens in a try-with-resources statement where `t` is an exception thrown by a close method.
- `Throwable[] getSuppressed()` 7 gets all "suppressed" exceptions of this exception. Typically, these are exceptions thrown by a close method in a try-with-resources statement.

### java.lang.Exception 1.0

- `Exception(Throwable cause)` 1.4
- `Exception(String message, Throwable cause)` constructs an Exception with a given cause.

### java.lang.RuntimeException 1.0

- `RuntimeException(Throwable cause)` 1.4
- `RuntimeException(String message, Throwable cause)` 1.4 constructs a `RuntimeException` with a given cause.

### java.lang.StackWalker

- `static StackWalker getInstance()`
- `static StackWalker getInstance(StackWalker.Option option)`
- `static StackWalker getInstance(Set<StackWalker.Option> options)` gets a `StackWalker` instance. The options include `RETAIN_CLASS_REFERENCE`, `SHOW_HIDDEN_FRAMES`, and `SHOW_REFLECT_FRAMES` from the `StackWalker.Option` enumeration.
- `forEach(Consumer<? super StackWalker.StackFrame> action)` carries out the given action on each stack frame, starting with the most recently called method.
- `walk(Function<? super Stream<StackWalker.StackFrame>, ? extends T> function)` applies the given function to the stream of stack frames and returns the result of the function.

### java.lang.StackWalker.StackFrame

- `String getFileName()` gets the name of the source file containing the execution point of this element, or null if the information is not available.
- `int getLineNumber()` gets the line number of the source file containing the execution point of this element, or -1 if the information is not available.
- `String getClassName()` gets the fully qualified name of the class whose method contains the execution point of this element.
- `Class<?> getDeclaringClass()` gets the class object of the method containing the execution point of this element. An exception is thrown if the stack walker was not constructed with the `RETAIN_CLASS_REFERENCE` option.
- `String getMethodName()` gets the name of the method containing the execution point of this element. The name of a constructor is `<init>`. The name of a static initializer is `<clinit>`. You can’t distinguish between overloaded methods with the same name.
- `boolean isNativeMethod()` returns true if the execution point of this element is inside a native method.
- `String toString()` returns a formatted string containing the class and method name and the file name and line number, if available.

### java.lang.StackTraceElement 1.4

- `String getFileName()` gets the name of the source file containing the execution point of this element, or null if the information is not available.
- `int getLineNumber()` gets the line number of the source file containing the execution point of this element, or −1 if the information is not available.
- `String getClassName()` gets the fully qualified name of the class containing the execution point of this element.
- `String getMethodName()` gets the name of the method containing the execution point of this element. The name of a constructor is `<init>`. The name of a static initializer is `<clinit>`. You can't distinguish between overloaded methods with the same name.
- `boolean isNativeMethod()` returns true if the execution point of this element is inside a native method.
- `String toString()` returns a formatted string containing the class and method name and the file name and line number, if available.

## 7.3 Tips for Using Exceptions

There is a certain amount of controversy about the proper use of exceptions. Some programmers believe that all checked exceptions are a nuisance, others can't seem to throw enough of them. I think that exceptions (even checked exceptions) have their place, so I offer you these tips for their proper use.

- 1. Exception handling is not supposed to replace a simple test.

As an example of this, here's code that tries 10,000,000 times to pop an empty stack. It first does this by finding out whether the stack is empty.

```java
if (!s.empty()) s.pop();
```

Next, we force it to pop the stack no matter what and catch the EmptyStackException that tells us we should not have done that.

```java
try
{
    s.pop();
}
catch (EmptyStackException e)
{
}
```

On my test machine, the version that calls `isEmpty` ran in 646 milliseconds. The version that catches the `EmptyStackException` ran in 21,739 milliseconds.

As you can see, it took far longer to catch an exception than to perform a simple test. The moral is: Use exceptions for exceptional circumstances only.

- 2. Do not micromanage exceptions.

Some programmers wrap every statement in a separate `try` block.

```java
PrintStream out;
Stack s;
for (i = 0; i < 100; i++)
{
    try
    {
        n = s.pop();
    }
    catch (EmptyStackException e)
    {
        // stack was empty
    }
    try
    {
        out.writeInt(n);
    }
    catch (IOException e)
    {
        // problem writing to file
    }
}
```

This approach blows up your code dramatically. Think about the task that you want the code to accomplish. Here, we want to pop 100 numbers off a stack and save them to a file. (Never mind why—it is just a toy example.) There is nothing we can do if a problem rears its ugly head. If the stack is
