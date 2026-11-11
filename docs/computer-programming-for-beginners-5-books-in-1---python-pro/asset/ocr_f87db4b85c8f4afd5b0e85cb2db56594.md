# Chapter 17: The Process of Handling Exceptions

Applications usually encounter errors during execution. After the occurrence of an error, the program throws an exception with more information regarding the error. Exceptions should be handled to prevent a program from crashing.

In C#, exceptions are handled using 4 main keywords:

+   1. try- this keyword identifies the block of code in which particular exceptions have been activated. It is then followed by either one or more *catch* blocks.
+   2. catch- a program should catch an exception with an exception handler at a place within the program where you need to handle the problem. The *catch* is a keyword that indicates a place where the exception will be caught.
+   3. finally- the finally block is used for executing a set of statements regardless of whether an exception has been thrown or not. For example, a file must be closed after being opened, whether an exception is thrown or not.
+   4. throw- an exception is normally thrown after the occurrence of a problem. This is done via the *throw* keyword.

A combination of *try* and *catch* is used for catching exceptions. The try/catch block has to be placed around a code that may raise an exception. Such code is said to be *protected*, and here is the syntax for using these keywords:

```
```csharp
try {
  // statements raising the exception
} catch( ExceptionName exception1 ) {
  // The error handling code
} catch( ExceptionName exception2 ) {
  // The error handling code
} catch( ExceptionName eexceptionN ) {
  // The error handling code
} finally {
  // statements to execute
}
```
```