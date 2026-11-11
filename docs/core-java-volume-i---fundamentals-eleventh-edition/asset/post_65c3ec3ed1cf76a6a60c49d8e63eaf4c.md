
- 4. **A logging proxy** is an object of a subclass that intercepts method calls, logs them, and then calls the superclass. For example, if you have trouble with the `nextDouble` method of the `Random` class, you can create a proxy object as an instance of an anonymous subclass:

```java
var generator = new Random()
{
    public double nextDouble()
    {
        double result = super.nextDouble();
        Logger.getGlobal().info("nextDouble: " + result);
        return result;
    }
};
```

Whenever the nextDouble method is called, a log message is generated.

To find out who called the method, generate a stack trace.

- 5. You can get a stack trace from any exception object with the `printStackTrace` method in the `Throwable` class. The following code catches any exception, prints the exception object and the stack trace, and rethrows the exception so it can find its intended handler.

```java
try
{
    . . .
}
catch (Throwable t)
{
    t.printStackTrace();
    throw t;
}
```

You don’t even need to catch an exception to generate a stack trace. Simply insert the statement

```java
Thread.dumpStack();
```

anywhere into your code to get a stack trace.

- 6. Normally, the stack trace is displayed on `System.err`. If you want to log or display the stack trace, here is how you can capture it into a string:

```java
var out = new StringWriter();
new Throwable().printStackTrace(new PrintWriter(out));
String description = out.toString();
```

- 7. It is often handy to trap program errors in a file. However, errors are sent to `System.err`, not `System.out`. Therefore, you cannot simply trap them by running

```
java MyProgram > errors.txt
```

Instead, capture the error stream as

```
java MyProgram 2> errors.txt
```

To capture both System.err and System.out in the same file, use

```
java MyProgram 1> errors.txt 2>&1
```

This works in bash and the Windows shell.

- 8. Having the stack traces of uncaught exceptions show up in System.err is not ideal. These messages are confusing to end users if they happen to see them, and they are not available for diagnostic purposes when you need them. A better approach is to log them to a file. You can change the handler for uncaught exceptions with the static `Thread.setDefaultUncaughtExceptionHandler` method:

```java
Thread.setDefaultUncaughtExceptionHandler(
    new Thread.UncaughtExceptionHandler()
    {
        public void uncaughtException(Thread t, Throwable e)
        {
            save information in log file
        }
    });
```

- 9. To watch class loading, launch the Java virtual machine with the `-verbose` flag. You will get a printout such as the following:

```
[0.012s][info][class,load] opened: /opt/jdk-11.0.1/lib/modules
[0.034s][info][class,load] java.lang.Object source: jrt:/java.base
[0.035s][info][class,load] java.io.Serializable source: jrt:/java.base
[0.035s][info][class,load] java.lang.Comparable source: jrt:/java.base
[0.035s][info][class,load] java.lang.CharSequence source: jrt:/java.base
[0.035s][info][class,load] java.lang.String source: jrt:/java.base
[0.035s][info][class,load] java.lang.constant.Constable source: jrt:/java.base
[0.036s][info][class,load] java.lang.reflect.GenericDeclaration source: jrt:/java.base
[0.036s][info][class,load] java.lang.reflect.Type source: jrt:/java.base
[0.036s][info][class,load] java.lang.Class source: jrt:/java.base
[0.036s][info][class,load] java.lang.Cloneable source: jrt:/java.base
[0.037s][info][class,load] java.lang.ClassLoader source: jrt:/java.base
[0.037s][info][class,load] java.lang.System source: jrt:/java.base
[0.037s][info][class,load] java.lang.Throwable source: jrt:/java.base
[0.037s][info][class,load] java.lang.Error source: jrt:/java.base
[0.037s][info][class,load] java.lang.Thread source: jrt:/java.base
[0.037s][info][class,load] java.lang.Exception source: jrt:/java.base
[0.037s][info][class,load] java.lang.RuntimeException source: jrt:/java.base
[0.038s][info][class,load] java.lang.SecurityManager source: jrt:/java.base
. . . . .
```

This can occasionally be helpful to diagnose class path problems.

- 10. The `-Xlint` option tells the compiler to spot common code problems. For example, if you compile with the command

```
javac -Xlint sourceFiles
```

The compiler will report missing break statements in switch statements. (The term “lint” originally described a tool for locating potential problems in C programs, but is now generically applied to any tools that flag constructs that are questionable but not illegal.)

You will get messages such as

```
warning: [fallthrough] possible fall-through into case
```

The string in square brackets identifies the warning category. You can enable and disable each category. Since most of them are quite useful, it seems best to leave them all in place and disable only those that you don’t care about, like this:

```
javac -Xlint:all,-fallthrough,-serial sourceFiles
```

You get a list of all warnings from the command

```
javac --help -X
```

- 11. The Java VM has support for *monitoring and management* of Java applications, allowing the installation of agents in the virtual machine that track memory consumption, thread usage, class loading, and so on. This feature is particularly important for large and long-running Java programs, such as application servers. As a demonstration of these capabilities, the JDK ships with a graphical tool called jconsole that displays statistics about the performance of a virtual machine (see Figure 7.3). Start your program, then start jconsole and pick your program from the list of running Java programs.

The console gives you a wealth of information about your running program. See www.oracle.com/technetwork/articles/java/jconsole-1564139.html for more information.

- 12. Java Mission Control is a professional-level profiling and diagnostics tool that is included with the Oracle JDK and is free to use for development purposes. A commercial license is required for use in production. An open source version will be a part of the OpenJDK at some point. Like jconsole, Java Mission Control can attach to a running virtual machine. It can also analyze the output from Java Flight Recorder, a tool that collects diagnostic and profiling data from a running Java application. See https://docs.oracle.com/javacomponents/index.html for more information about these tools.

![](img/127bccebb2cfadea3f02579edaad63c3_456_0.png)

**Figure 7.3** The jconsole program

This chapter introduced you to exception handling and logging. You also saw useful hints for testing and debugging. The next two chapters cover generic programming and its most important application: the Java collections framework.

## CHAPTER 8: Generic Programming

### In this chapter

- 8.1 Why Generic Programming? page 432
- 8.2 Defining a Simple Generic Class, page 434
- 8.3 Generic Methods, page 437
- 8.4 Bounds for Type Variables, page 438
- 8.5 Generic Code and the Virtual Machine, page 441
- 8.6 Restrictions and Limitations, page 447
- 8.7 Inheritance Rules for Generic Types, page 457
- 8.8 Wildcard Types, page 459
- 8.9 Reflection and Generics, page 467

Generic classes and methods have type parameters. This allows them to describe precisely what should happen when they are instantiated with specific types. Prior to generic classes, programmers had to use the `Object` for writing code that works with multiple types. This was both cumbersome and unsafe.

With the introduction of generics, Java has an expressive type system that allows designers to describe in detail how types of variables and methods should vary. In straightforward situations, you will find it simple to implement generic code. In more advanced cases, it can get quite complex—for implementors. The goal is to provide classes and methods that other programmers can use without surprises.

The introduction of generics in Java 5 constitutes the most significant change in the Java programming language since its initial release. A major design goal was to be backwards compatible with earlier releases. As a result, Java generics have some uncomfortable limitations. You will learn about the benefits and challenges of generic programming in this chapter.

### 8.1 Why Generic Programming?

*Generic programming* means writing code that can be reused for objects of many different types. For example, you don’t want to program separate classes to collect String and File objects. And you don’t have to—the single class `ArrayList` collects objects of any class. This is one example of generic programming.

Actually, Java had an ArrayList class before it had generic classes. Let us investigate how the mechanism for generic programming has evolved, and what that means for users and implementors.

#### 8.1.1 The Advantage of Type Parameters

Before generic classes were added to Java, generic programming was achieved with *inheritance*. The `ArrayList` class simply maintained an array of `Object` references:

```java
public class ArrayList // before generic classes
{
    private Object[] elementData;

    public Object get(int i) { . . . }
    public void add(Object o) { . . . }
}
```

This approach has two problems. A cast is necessary whenever you retrieve a value:

```java
ArrayList files = new ArrayList();
. . .
String filename = (String) files.get(0);
```

Moreover, there is no error checking. You can add values of any class:

```java
files.add(new File(". . ."));
```

This call compiles and runs without error. Elsewhere, casting the result of `get` to a String will cause an error.
