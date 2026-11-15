
{
    try
    {
        // ...
        throw new InvalidOperationException (
            "Arbitrary exception");
        // ...
    }
    catch (NullReferenceException exception)
    {
        // Handle NullReferenceException
    }
    catch (ArgumentException exception)
    {
        // Handle ArgumentException
    }
    catch (InvalidOperationException exception)
    {
        // Handle ApplicationException
    }
    catch (SystemException exception)
    {
        // Handle SystemException
    }
    catch (Exception exception)
    {
        // Handle Exception
    }
    catch
    {
        // Any unhandled exception
    }
}

The general catch block will catch all exceptions, regardless of whether they derive from System.Exception, assuming an earlier catch block does not catch them. The disadvantage of such a block is simply that there is no exception instance to access and, therefore, no way to know the appropriate course of action. It wouldn’t even be possible to recognize the unlikely case where such an exception is innocuous. The best course of action is to handle the exception with some cleanup code before shutting down the application. The catch block could save any volatile data, for example, before shutting down the application or rethrowing the exception.

## ADVANCED TOPIC

### Empty Catch Block Internals

The CIL code corresponding to an empty catch block is, in fact, a catch(object) block. This means that regardless of the type thrown, the empty catch block will catch it. Interestingly, it is not possible to explicitly declare a catch(object) exception block within C# code. Therefore, there is no means of catching a non-System.Exception-derived exception and having an exception instance to scrutinize.

Ironically, unmanaged exceptions from languages such as C++ generally result in System.Runtime.InteropServices.SEHException type exceptions, which derive from the System.Exception type. Therefore, not only can the unmanaged type exceptions be caught using a general catch block, but the non-System.Exception-managed types that are thrown can be caught as well—for instance, types such as string.

### Guidelines for Exception Handling

Exception handling provides much-needed structure to the error-handling mechanisms that preceded it. However, it can still make for some unwieldy results if used haphazardly. The following guidelines offer some best practices for exception handling.

- Catch only the exceptions that you can handle.
  Generally it is possible to handle some types of exceptions but not others. For example, opening a file for exclusive read-write access may throw a System.IO.IOException because the file is already in use. In catching this type of exception, the code can report to the user that the file is in use and allow the user the option of canceling the operation or retrying it. Only exceptions for which there is a known action should be caught. Other exception types should be left for callers higher in the stack.

- Don't hide (bury) exceptions you don't fully handle.
  New programmers are often tempted to catch all exceptions and then continue executing instead of reporting an unhandled exception to the user. However, this may result in a critical system problem going undetected. Unless code takes explicit action to handle an exception or explicitly determines certain exceptions to be innocuous, catch blocks should rethrow exceptions instead of catching them and hiding them from the caller. Predominantly, catch (System.Exception) and general catch blocks should occur higher in the call stack, unless the block ends by rethrowing the exception.

- Use System.Exception and general catch blocks rarely.
  Virtually all exceptions derive from System.Exception. However, the best way to handle some System.Exceptions is to allow them to go unhandled or to gracefully shut down the application sooner rather than later. These exceptions include things such as System.OutOfMemoryException and System.StackOverflowException. In CLR 4, such exceptions were defaulted to nonrecoverable such that catching them without rethrowing them will cause the CLR to rethrow them anyway. These exceptions are runtime exceptions that the developer cannot write code to recover from. Therefore, the best course of action is to shut down the application—something the runtime will force in CLR 4. Code prior to CLR 4 should catch such exceptions only to run cleanup or emergency code (such as saving any volatile data) before shutting down the application or rethrowing the exception with throw;.

- Avoid exception reporting or logging lower in the call stack.
  Often, programmers are tempted to log exceptions or report exceptions to the user at the soonest possible location in the call stack. However, these locations are seldom able to handle the exception fully and they resort to rethrowing the exception. Such catch blocks should not log the exception or report it to a user while in the bowels of the call stack. If the exception is logged and rethrown, the callers higher in the call stack may do the same, resulting in duplicate log entries of the exception. Worse, displaying the exception to the user may not be appropriate for the type of application. (Using System.Console.WriteLine() in a Windows application will never be seen by the user, for example, and displaying a dialog in an unattended command-line process may go unnoticed and freeze the application.) Logging- and exception-related user interfaces should be reserved for high up in the call stack.

- Use throw; rather than throw <exception object> inside a catch block.

  It is possible to rethrow an exception inside a catch block. For example, the implementation of catch(ArgumentNullException exception) could include a call to throw exception. However, rethrowing the exception like this will reset the stack trace to the location of the rethrow call, instead of reusing the original throw point location. Therefore, unless you are rethrowing with a different exception type or intentionally hiding the original call stack, use throw; to allow the same exception to propagate up the call stack.

- Use caution when rethrowing different exceptions.

  From inside a catch block, rethrowing a different exception will not only reset the throw point, it will also hide the original exception. To preserve the original exception set the new exception's InnerException property, generally assignable via the constructor. Rethrowing a different exception should be reserved for the following situations.

  - 1. Changing the exception type clarifies the problem.

    For example, in a call to Logon(User user), rethrowing a different exception type is perhaps more appropriate than propagating System.IO.IOException when the file with the user list is inaccessible.

  - 2. Private data is part of the original exception.

    In the preceding scenario, if the file path is included in the original System.IO.IOException, thereby exposing private security information about the system, the exception should be wrapped. This assumes, of course, that InnerException is not set with the original exception. (Funny enough, a very early version of CLR v1 (pre-alpha even) had an exception that said something like “Security exception: You do not have permission to determine the path of c:\temp\foo.txt”.)

  - 3. The exception type is too specific for the caller to handle appropriately.

    For example, instead of throwing an exception specific to a particular database system, a more generic exception is used so that database-specific code higher in the call stack can be avoided.

### Defining Custom Exceptions

Once throwing an exception becomes the best course of action, it is preferable to use framework exceptions because they are well established and understood. Instead of throwing a custom invalid argument exception, for example, it is preferable to use the System.ArgumentException type. However, if the developers using a particular API will take special action—the exception-handling logic will vary to handle a custom exception type, for instance—it is appropriate to define a custom exception. For example, if a mapping API receives an address for which the ZIP Code is invalid, instead of throwing System.ArgumentException, it may be better to throw a custom InvalidAddressException. The key is whether the caller is likely to write a specific ValidAddressException catch block with special handling rather than just a generic System.ArgumentException catch block. Defining a custom exception simply involves deriving from System.Exception or some other exception type. Listing 10.4 provides an example.

```
LISTING 10.4: Creating a Custom Exception

class DatabaseException : System.Exception
{
    public DatabaseException(
        System.Data.SqlClient.SqlException exception)
    {
        InnerException = exception;
        // ...
    }

    public DatabaseException(
        System.Data.OracleClient.OracleException exception)
    {
        InnerException = exception;
        // ...
    }

    public DatabaseException()
    {
        // ...
    }

    public DatabaseException(string message)
    {
        // ...
    }
}
```
