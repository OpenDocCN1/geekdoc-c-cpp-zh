UnauthorizedException. Even the ArgumentException might need treatment in this case because it's not unimaginable for the user to specify an invalid path. As an exercise, implement a few other exception handlers and take a look at the properties available on the various exception types.

# WHERE ARE THE CHECKED EXCEPTIONS?

Some other programming languages have the concept of checked exceptions by which a method declares the exceptions it may throw, forcing the caller either to catch the exception or propagate it to its caller:

```
```
string[] ReadAllLines(string path) throws FileNotFoundException /* and more */
```
```

Although this is a nice way to ensure proper exception handling, there are a couple of practical issues.

First, using checked exceptions on interface declarations is rather fragile. A practical implementation of the interface may require other exceptions to be thrown. For example, a GetUser interface method may be implemented based on file access (IOException being a reasonable error condition) or based on database access (where a SqlException may occur). And changing the interface after its initial release is a big no-no because you'll break everything that depends on it: Adding an exception type to a throws clause requires callers to handle or propagate it, so you end up breaking everything that already used the interface: You have a version issue at this point:

```
```
interface IUserManagementService
{
    User GetUser(string username) throws UserNotFoundException;
}
```
```

Second, use of checked exceptions can be very annoying because the compiler starts complaining about unhandled exception types all the time. In lots of cases, you find yourself in a project phase where you want to throw something together quickly, in a mindset of "I'll patch parts up later." The simplest way to get around excessive compiler warnings is either to catch and swallow exceptions on the spot ("oh, this will never happen") or propagate all of them by adding a throws Exception clause (that is, throwing the mother type of all exceptions accommodating for everything inside):

```
```
void Foo() throws Exception
{
    // Every checked exception is propagate unnoticed here.
}
```
```

You've effectively just suppressed the whole feature. Exceptions are unfortunately something you have to think about all the time, severely impairing your development productivity at times. It's not clear whether checked exceptions are worth the trouble because of those hidden rat holes. Therefore, C# (and many CLR languages) go for a more minimalist approach without checked exceptions.