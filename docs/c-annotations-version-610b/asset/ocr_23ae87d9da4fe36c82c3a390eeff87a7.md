to be thrown. An Exception object might support stream-like insertion operations allowing us to do, e.g.,

```
```cpp
if (!lookup(variableName))
    throw Exception() << "Undefined variable " << variableName << "";
```
```

# 10.3.1  The empty ‘throw’ statement

Sometimes it is required to inspect a thrown exception. An exception catcher may decide to ignore the exception, to process the exception, to rethrow it after inspection or to change it into another kind of exception. For example, in a server-client application the client may submit requests to the server by entering them into a queue. Normally every request is eventually answered by the server. The server may reply that the request was successfully processed, or that some sort of error has occurred. On the other hand, the server may have died, and the client should be able to discover this calamity, by not waiting indefinitely for the server to reply.

In this situation an intermediate exception handler is called for. A thrown exception is first inspected at the middle level. If possible it is processed there. If it is not possible to process the exception at the middle level, it is passed on, unaltered, to a more superficial level, where the really tough exceptions are handled.

By placing an empty `throw` statement in the exception handler’s code the received exception is passed on to the next level that might be able to process that particular type of exception. The `rethrow` exception is never handled by one of its neighboring exception handlers; it is always transferred to an exception handler at a more superficial level.

In our server-client situation a function

```
```cpp
initialExceptionHandler(string &exception)
```
```

could be designed to handle the `string` exception. The received message is inspected. If it’s a simple message it’s processed, otherwise the exception is passed on to another level. In `initialExceptionHandler`’s implementation the empty throw statement is used:

```
```cpp
void initialExceptionHandler(string &exception)
{
    if (!plainMessage(exception))
        throw;

    handleTheMessage(exception);
}
```
```

Below (section 10.5), the empty throw statement is used to pass on the exception received by a catch-block. Therefore, a function like `initialExceptionHandler` can be used for a variety of thrown exceptions, as long as their types match `initialExceptionHandler`’s parameter, which is a string.

The next example jumps slightly ahead, using some of the topics covered in chapter 14. The example may be skipped, though, without loss of continuity.

A basic exception handling class can be constructed from which specific exception types are derived. Suppose we have a class `Exception`, having a member function `ExceptionType Exception::severity`. This member function tells us (little wonder!) the severity of a thrown exception. It might be `Info`, `Notice`, `Warning`, `Error` or `Fatal`. The information contained in the exception depends on its severity and is processed by a function handle. In addition, all exceptions support a member function like `textMsg`, returning textual information about the exception in a string.

By defining a polymorphic function handle it can be made to behave differently, depending on the nature of a thrown exception, when called from a basic `Exception` pointer or reference.