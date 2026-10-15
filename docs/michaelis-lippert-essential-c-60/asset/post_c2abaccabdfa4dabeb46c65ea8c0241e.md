
catch(object) exception block within C# code. Therefore, there is no means of catching a non-System.Exception-derived exception and having an exception instance to scrutinize.

In fact, unmanaged exceptions from languages such as C++ generally result in System.Runtime.InteropServices.SEHException-type exceptions, which derive from the System.Exception type. Therefore, not only can the unmanaged type exceptions be caught using a general catch block, but the non-System.Exception-managed types that are thrown can be caught as well—for instance, types such as string.

## Guidelines for Exception Handling

Exception handling provides much-needed structure to the error-handling mechanisms that preceded it. However, it can still lead to some unwieldy results if used haphazardly. The following guidelines offer some best practices for exception handling.

- *Catch only the exceptions that you can handle.*

  Generally it is possible to handle some types of exceptions but not others. For example, opening a file for exclusive read-write access may throw a System.IO.IOException because the file is already in use. In catching this type of exception, the code can report to the user that the file is in use and allow the user the option of canceling the operation or retrying it. Only exceptions for which there is a known action should be caught. Other exception types should be left for callers higher in the stack.

- *Don’t hide (bury) exceptions you don’t fully handle.*

  New programmers are often tempted to catch all exceptions and then continue executing instead of reporting an unhandled exception to the user. However, this practice may result in a critical system problem going undetected. Unless code takes explicit action to handle an exception or explicitly determines certain exceptions to be innocuous, catch blocks should rethrow exceptions instead of catching them and hiding them from the caller. In most cases, catch(System.Exception) and general catch blocks should occur higher in the call stack, unless the block ends by rethrowing the exception.

## Chapter 10: Exception Handling

- *Use `System.Exception` and general catch blocks rarely.* Almost all exceptions derive from `System.Exception`. However, the best way to handle some `System.Exception`s is to allow them to go unhandled or to gracefully shut down the application sooner rather than later. These exceptions include things such as `System.OutOfMemoryException` and `System.StackOverflowException`. In CLR 4, such exceptions defaulted to nonrecoverable, such that catching them without rethrowing them would cause the CLR to rethrow them anyway. These exceptions are runtime exceptions that the developer cannot write code to recover from. Therefore, the best course of action is to shut down the application—something the runtime will force in CLR 4 and later. Code prior to CLR 4 should catch such exceptions only to run cleanup or emergency code (such as saving any volatile data) before shutting down the application or rethrowing the exception with `throw;`.

- *Avoid exception reporting or logging lower in the call stack.* Often, programmers are tempted to log exceptions or report exceptions to the user at the soonest possible location in the call stack. However, these locations are seldom able to handle the exception fully; instead, they resort to rethrowing the exception. Such catch blocks should not log the exception or report it to a user while in the bowels of the call stack. If the exception is logged and rethrown, the callers higher in the call stack may do the same, resulting in duplicate log entries of the exception. Worse, displaying the exception to the user may not be appropriate for the type of application. (Using `System.Console.WriteLine()` in a Windows application will never be seen by the user, for example, and displaying a dialog in an unattended command-line process may go unnoticed and freeze the application.) Logging- and exception-related user interfaces should be reserved for use higher up in the call stack.

- *Use `throw;` rather than `throw <exception object>` inside a catch block.* It is possible to rethrow an exception inside a catch block. For example, the implementation of `catch(ArgumentNullException exception)` could include a call to `throw exception`. However, rethrowing the exception like this will reset the stack trace to the location of the rethrown call, instead of reusing the original throw point location. Therefore, unless you are rethrowing with a different

exception type or intentionally hiding the original call stack, use throw; to allow the same exception to propagate up the call stack.

- *Avoid throwing exceptions from exception conditionals.*

  When providing an exception conditional, avoid code that throws an exception. Doing so will result in a false condition and the exception occurrence will be ignored. For this reason, consider placing complicated conditional checks into a separate method that is wrapped in a try/catch block that handles the exception explicitly.

- *Avoid exception conditionals that might change over time.*

  If an exception conditional evaluates conditions such as exception messages that could potentially change with localization or changed message, the expected exception condition will not get caught, unexpectedly changing the business logic. For this reason, ensure exception conditions are valid over time.

- *Use caution when rethrowing different exceptions.*

  From inside a catch block, rethrowing a different exception will not only reset the throw point, but also hide the original exception. To preserve the original exception, set the new exception’s InnerException property, generally assignable via the constructor. Rethrowing a different exception should be reserved for the following situations:

  1. Changing the exception type clarifies the problem.

     For example, in a call to Logon(User user), rethrowing a different exception type is perhaps more appropriate than propagating System.IO.IOException when the file with the user list is inaccessible.

  2. Private data is part of the original exception.

     In the preceding scenario, if the file path is included in the original System.IO.IOException, thereby exposing private security information about the system, the exception should be wrapped. This assumes, of course, that InnerException is not set with the original exception. (Funnily enough, a very early version of CLR v1 [pre-alpha, even] had an exception that said something like “Security exception: You do not have permission to determine the path of c:\temp\foo.txt”.)

  3. The exception type is too specific for the caller to handle appropriately.

     For example, instead of throwing an exception specific to a particular database system, a more generic exception is used so that database-specific code higher in the call stack can be avoided.

## Guidelines

- **AVOID** exception reporting or logging lower in the call stack.
- **DO NOT** over-catch. Exceptions should be allowed to propagate up the call stack unless it is clearly understood how to programmatically address those errors lower in the stack.
- **CONSIDER** catching a specific exception when you understand why it was thrown in a given context and can respond to the failure programmatically.
- **AVOID** catching System.Exception or System.SystemException except in top-level exception handlers that perform final cleanup operations before rethrowing the exception.
- **DO** use throw rather than throw <exception object> inside a catch block.
- **DO** use caution when rethrowing different exceptions.
- **DO NOT** throw a NullReferenceException, favoring ArgumentNullException instead when a value is unexpectedly null.
- **AVOID** throwing exceptions from exception conditionals.
- **AVOID** exception conditionals that might change over time.

## Defining Custom Exceptions

Once throwing an exception becomes the best course of action, it is preferable to use framework exceptions because they are well established and understood. Instead of throwing a custom invalid argument exception, for example, it is preferable to use the System.ArgumentException type. However, if the developers using a particular API will take special action—the exception-handling logic will vary to handle a custom exception type, for instance—it is appropriate to define a custom exception. For example, if a mapping API receives an address for which the ZIP code is invalid, instead of throwing System.ArgumentException, it may be better to throw a custom InvalidAddressException. The key is whether the caller is likely to write a specific InvalidAddressException catch block with special handling rather than just a generic System.ArgumentException catch block.
