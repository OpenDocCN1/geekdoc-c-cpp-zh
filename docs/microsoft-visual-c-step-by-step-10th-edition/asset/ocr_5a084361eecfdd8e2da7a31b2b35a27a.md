divided into one or more continuations. When these continuations run, they execute on the same thread as the original method call.

+   The await operator specifies a point at which the C# compiler can split the code into a continuation. The await operator itself expects its operand to be an awaitable object. An awaitable object is a type that provides the GetAwait method, which returns an object that turn provides methods for running code and waiting for it to complete. The C# compiler converts your code into statements that use these methods to create an appropriate continuation.

> **Important**
You can use the await operator only in a method marked with async. Outside an async method, the await keyword is treated as an ordinary identifier. (You can create a variable called await, although this is not recommended.)

> Note
Prior to C# 7.1, the Main method could not be marked as async. This restriction has since disappeared. If you're running .NET 6.0 or later, you can tag Main as async and use the await operator to run asynchronous methods. The Main method only terminates when the asynchronous methods complete.

In the current implementation of the await operator, the awaitable object expects you to specify as the operand is a Task object. This means that you must make some modifications to the doFirstLongRunningOperation, doSecondLongRunningOperation, and doThirdLongRunningOperation methods. Specifically, each method must create and run a Task object to perform its work and return a reference to this Task. The following example shows an amended version of the doFirstLongRunningOperation method: