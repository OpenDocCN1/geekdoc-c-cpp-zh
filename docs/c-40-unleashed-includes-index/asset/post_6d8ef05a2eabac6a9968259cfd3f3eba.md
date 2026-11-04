
UnauthorizedException. Even the ArgumentException might need treatment in this case because it's not unimaginable for the user to specify an invalid path. As an exercise, implement a few other exception handlers and take a look at the properties available on the various exception types.

## WHERE ARE THE CHECKED EXCEPTIONS?

Some other programming languages have the concept of checked exceptions by which a method declares the exceptions it may throw, forcing the caller either to catch the exception or propagate it to its caller:

```
string[] ReadAllLines(string path) throws FileNotFoundException /* and more */
```

Although this is a nice way to ensure proper exception handling, there are a couple of practical issues.

First, using checked exceptions on interface declarations is rather fragile. A practical implementation of the interface may require other exceptions to be thrown. For example, a GetUser interface method may be implemented based on file access (IOException being a reasonable error condition) or based on database access (where a SqlException may occur). And changing the interface after its initial release is a big no-no because you'll break everything that depends on it: Adding an exception type to a throws clause requires callers to handle or propagate it, so you end up breaking everything that already used the interface: You have a version issue at this point:

```
interface IUserManagementService
{
    User GetUser(string username) throws UserNotFoundException;
}
```

Second, use of checked exceptions can be very annoying because the compiler starts complaining about unhandled exception types all the time. In lots of cases, you find yourself in a project phase where you want to throw something together quickly, in a mindset of "I'll patch parts up later." The simplest way to get around excessive compiler warnings is either to catch and swallow exceptions on the spot ("oh, this will never happen") or propagate all of them by adding a throws Exception clause (that is, throwing the mother type of all exceptions accommodating for everything inside):

```
void Foo() throws Exception
{
    // Every checked exception is propagated unnoticed here.
}
```

You've effectively just suppressed the whole feature. Exceptions are unfortunately something you have to think about all the time, severely impairing your development productivity at times. It's not clear whether checked exceptions are worth the trouble because of those hidden rat holes. Therefore, C# (and many CLR languages) go for a more minimalist approach without checked exceptions.

## Throwing Exceptions

Time for a more structured look at working with exceptions. We'll start with the act of throwing exceptions to signal an error condition. Not surprisingly, throwing an exception is done using the throw keyword, specifying an instance of an exception type. For example:

```
void DisplayUserProfile(string user)
{
    if (user == null)
        throw new ArgumentNullException("user");

    if (user == "")
        throw new ArgumentException("exception");

    if (!Profiles.Exists(user))
        throw new UserNotFoundException(user);

    // Do real work here.
}
```

The third exception type used here is a custom exception type, something we explore later. What matters here is the syntax of the throw statement, which is, as you can see, very straightforward. That said, I sometimes make the silly mistake of thinking throw also creates an instance:

```
throw /* don't forget new here */ ArgumentException("user")
```

So you might be getting your exception instance from elsewhere rather than by using a new expression in conjunction with the throw statement. This instance could be instantiated upfront (like OutOfMemoryException's single instance is in the runtime) or be retrieved by calling some method. The latter technique is often handy when exception messages have to be localized, which can be taken care of by custom logic in the exception creator method.

## Handling Exceptions

Handling exceptions is done by protecting a certain block of code using try and having an exception handler associated with it using catch. You saw examples of this earlier, but let's take a closer look:

```
try
{
    PrintFile(path);
}
catch (FileNotFoundException ex)
{
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine(ex.Message);
    Console.ResetColor();
}
```

Here we're protecting the call to PrintFile against the FileNotFoundException. Of course, the protected block of code (following the try keyword) can consist of more than one line of code, but it's a good practice not to protect too much code if you're only after catching an exception from a specific call somewhere in there.

### CURLY BRACES REQUIRED

Sometimes there are those unexplainable asymmetries in languages. Even though statements such as if, while, for, and so on enable you to omit curly braces if the embedded statement is just a one liner, try and its friends don't. Because I love curly braces (because the C# language lacks whitespace sensitivity), I'm not offended by this asymmetry.

Notice in the preceding code that the PrintFile method doesn't throw FileNotFoundException itself; instead, one of the methods it calls, ReadAllLines, does. This illustrates the intimate coupling that exists between exception propagation and the call stack. Contrast this to manual HRESULT-checking code, where it's the user's responsibility to propagate errors by hand all over the place.

In fact, it's not even the ReadAllLines method that executes the throw statement for this exception type. Internally, the ReadAllLines method calls into many more helper methods, and one of those will detect the problem and throw the exception. To illustrate this, first disable the Just My Code feature via Tools, Options, Debugging, General, as shown in Figure 8.8.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_453_0.png)

FIGURE 8.8 Disabling Just My Code.

Just My Code hides code you haven't written from various places like the Call Stack window. Because we're already handling the exception, simply executing the code won't enable us to observe the point where the exception is thrown. One way to get to see this is by inspecting the stack trace through the exception object's StackTrace property. You can try this by setting a breakpoint inside the exception-handler block and inspecting the ex local variable when the breakpoint is hit. Visual Studio also has an exception helper tool that can show you the exception that was caught (see Figure 8.9). After opening the exception helper, click View Detail to inspect the exception object.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_454_0.png)

FIGURE 8.9 The exception helper in the debugger.

There's another way for you to see precisely where an exception occurred, even though it's caught by the code. From the time an exception is thrown until it's caught (or not, depending on the situation), lots of things happen. The whole exception system in the runtime is quite complicated, but in essence there are different phases:

- When the exception is thrown, a first-chance exception notification is sent out. This can be seen in a debugger, as you see shortly.
- Next, the runtime walks the call stack looking for a protected block that has an associated handler willing to handle the exception based on its type.
- The next thing on the runtime's checklist is to unwind the stack until it finds an exception handler or all the way back to the entry point if no handler exists.
- Finally, control is transferred to the found handler, supplying the exception object to the handler's catch block.

To observe an exception as it gets raised, you can enable first-chance exception notifications under the debugger. In Visual Studio, you can do so through a dialog under Debug, Exceptions, as shown in Figure 8.10.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_454_1.png)

FIGURE 8.10 Enabling first-chance exceptions.
