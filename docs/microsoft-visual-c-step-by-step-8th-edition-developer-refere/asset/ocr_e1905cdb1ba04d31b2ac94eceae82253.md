# Graph Demo

Plot Graph

Duration (ms):
1560

Cancel

Status of tasks is RanToCompletion, RanToCompletion

This behavior occurs because although you sent a cancellation request to each task by using the cancellation token, the methods they were running simply returned. The .NET Framework runtime does not know whether the tasks were actually canceled or whether they were allowed to run to completion, and it simply ignored the cancellation requests.

7. Return to Visual Studio and stop debugging.

So, how do you indicate that a task has been canceled rather than allowed to run to completion? The answer lies in the CancellationToken object passed as a parameter to the method that the task is running. The CancellationToken class provides a method called ThrowIfCancellationRequested. This method tests the IsCancellationRequested property of a cancellation token; if it is true, the method throws an OperationCanceledException exception and aborts the method that the task is running.

The application that started the thread should be prepared to catch and handle this exception, but this leads to another question. If a task terminates by throwing an exception, it actually reverts to the Faulted state. This is true even if the exception is an OperationCanceledException exception. A task enters the Canceled state only if it is canceled without throwing an exception. So, how does a task throw an OperationCanceledException without it being treated as an exception?

This time, the answer lies in the task itself. For a task to recognize that an OperationCanceledException exception is the result of canceling the task in a controlled manner and not just an exception caused by other circumstances, it has