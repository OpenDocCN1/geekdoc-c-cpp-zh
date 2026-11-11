
```java
try
{
    access the database
}
catch (SQLException original)
{
    var e = new ServletException("database error");
    e.initCause(original);
    throw e;
}
```

When the exception is caught, the original exception can be retrieved:

```java
Throwable original = caughtException.getCause();
```

This wrapping technique is highly recommended. It allows you to throw high-level exceptions in subsystems without losing the details of the original failure.

![](img/0e7b74ef51a065c077b42cd87b362288_577_0.png)

**TIP:**

The wrapping technique is also useful if a checked exception occurs in a method that is not allowed to throw a checked exception. You can catch the checked exception and wrap it into a runtime exception.

Sometimes, you just want to log an exception and rethrow it without any change:

```java
try
{
    access the database
}
catch (Exception e)
{
    logger.log(level, message, e);
    throw e;
}
```

Before Java 7, there was a problem with this approach. Suppose the code is inside a method

```java
public void updateRecord() throws SQLException
```

The Java compiler looked at the `throw` statement inside the `catch` block, then at the type of `e`, and complained that this method might throw any `Exception`, not just a `SQLException`. This has now been improved. The compiler now tracks the fact that `e` originates from the `try` block. Provided that the only checked exceptions in that block are `SQLException` instances, and provided that `e` is not changed in the `catch` block, it is valid to declare the enclosing method as `throws SQLException`.

### 7.2.4 The finally Clause

When your code throws an exception, it stops processing the remaining code in your method and exits the method. This is a problem if the method has acquired some local resource, which only this method knows about, and that resource must be cleaned up. One solution is to catch all exceptions, carry out the cleanup, and rethrow the exceptions. But this solution is tedious because you need to clean up the resource allocation in two places—in the normal code and in the exception code. The `finally` clause can solve this problem.

![](img/0e7b74ef51a065c077b42cd87b362288_578_0.png)

**NOTE:**

Since Java 7, there is a more elegant solution, the `try-with-resources` statement that you will see in the following section. We discuss the `finally` mechanism in detail because it is the conceptual foundation. But in practice, you will probably use `try-with-resources` statements more often than `finally` clauses.

The code in the `finally` clause executes whether or not an exception was caught. In the following example, the program will close the input stream *under all circumstances*:

```java
var in = new FileInputStream(...);
try
{
    // 1
    *code that might throw exceptions*
    // 2
}
catch (IOException e)
{
    // 3
    *show error message*
    // 4
}
finally
{
    // 5
    in.close();
}
// 6
```

Let us look at the three possible situations in which the program will execute the `finally` clause.

- 1. The code throws no exceptions. In this case, the program first executes all the code in the `try` block. Then, it executes the code in the `finally` clause. Afterwards, execution continues with the first statement after the `finally` clause. In other words, execution passes through points 1, 2, 5, and 6.
- 2. The code throws an exception that is caught in a `catch` clause—in our case, an `IOException`. For this, the program executes all code in the `try` block, up to the point at which the exception was thrown. The remaining code in the `try` block is skipped. The program then executes the code in the matching `catch` clause, and then the code in the `finally` clause. If the `catch` clause does not throw an exception, the program executes the first line after the `finally` clause. In this scenario, execution passes through points 1, 3, 4, 5, and 6. If the `catch` clause throws an exception, then the exception is thrown back to the caller of this method, and execution passes through points 1, 3, and 5 only.
- 3. The code throws an exception that is not caught in any `catch` clause. Here, the program executes all code in the `try` block until the exception is thrown. The remaining code in the `try` block is skipped. Then, the code in the `finally` clause is executed, and the exception is thrown back to the caller of this method. Execution passes through points 1 and 5 only.

You can use the `finally` clause without a `catch` clause. For example, consider the following `try` statement:

```java
InputStream in = ...;
try
{
    code that might throw exceptions
}
finally
{
    in.close();
}
```

The `in.close()` statement in the `finally` clause is executed whether or not an exception is encountered in the `try` block. Of course, if an exception is encountered, it is rethrown and must be caught in another `catch` clause.

```java
InputStream in = ...;
try
{
    try
    {
        code that might throw exceptions
    }
    finally
    {
        in.close();
    }
}
catch (IOException e)
{
    show error message
}
```

The inner `try` block has a single responsibility: to make sure that the input stream is closed. The outer `try` block has a single responsibility: to ensure that errors are reported. Not only is this solution clearer, it is also more functional: Errors in the `finally` clause are reported.

**CAUTION:**

A `finally` clause can yield unexpected results when it contains `return` statements. Suppose you exit the middle of a `try` block with a `return` statement. Before the method returns, the `finally` block is executed. If the `finally` block also contains a `return` statement, then it masks the original return value. Consider this example:

```java
public static int parseInt(String s)
{
    try
    {
        return Integer.parseInt(s);
    }
    finally
    {
        return 0; // ERROR
    }
}
```

It looks as if in the call `parseInt("42")`, the body of the try block returns the integer 42. However, the `finally` clause is executed before the method actually returns and causes the method to return 0, ignoring the original return value.

And it gets worse. Consider the call `parseInt("zero")`. The `Integer.parseInt` method throws a `NumberFormatException`. Then the `finally` clause is executed, and the return statement swallows the exception!

The body of the finally clause is intended for cleaning up resources. Don’t put statements that change the control flow (`return`, `throw`, `break`, `continue`) inside a finally clause.

### 7.2.5 The try-with-Resources Statement

As of Java 7, there is a useful shortcut to the code pattern

```
open a resource
try
{
    work with the resource
}
finally
{
    close the resource
}
```

provided the resource belongs to a class that implements the `AutoCloseable` interface. That interface has a single method

```java
void close() throws Exception
```

> **NOTE:**
> There is also a `Closeable` interface. It is a subinterface of `AutoCloseable`, also with a single `close` method. However, that method is declared to throw an `IOException`.

In its simplest variant, the try-with-resources statement has the form

```java
try (Resource res = . . .)
{
    work with res
}
```

When the try block exits, then `res.close()` is called automatically. Here is a typical example—reading all words of a file:

```java
try (var in = new Scanner(Path.of("in.txt"),
    StandardCharsets.UTF_8))
{
    while (in.hasNext())
        System.out.println(in.next());
}
```

When the block exits normally, or when there was an exception, the `in.close()` method is called, exactly as if you had used a `finally` block.

You can specify multiple resources. For example,

```java
try (var in = new Scanner(Path.of("in.txt"),
    StandardCharsets.UTF_8);
        var out = new PrintWriter("out.txt",
            StandardCharsets.UTF_8))
{
    while (in.hasNext())
```
