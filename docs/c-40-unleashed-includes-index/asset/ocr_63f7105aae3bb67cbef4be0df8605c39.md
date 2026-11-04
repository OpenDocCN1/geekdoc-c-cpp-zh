# Cancellation of Tasks

One thing that has been notoriously difficult in the world of asynchronous code (among other things, such as other threading and synchronization constructs) is the means to cancel an operation. Starting with .NET 4, cancellation has been unified in terms of two concepts: CancellationToken and CancellationTokenSource.

We don't elaborate on the intricacies of the mechanism here but instead focus on the essentials of the feature. Figure 30.6 summarizes the basic interactions with constructs for cancellation.

![](bbox=[0.07, 0.43, 0.9, 0.76])

FIGURE 30.6 Cancellation of a task.

The first key notion is that of a CancellationTokenSource. This class is where a request for cancellation comes in by means of a call to Cancel. The operation being cancelled can check for this situation through a so-called CancellationToken struct, which can be obtained from the token source using the Token get-only property. This lightweight object can be passed in a variety of places across the TPL and System.Threading APIs starting from .NET 4. In the section “Retrieving a Task’s Result,” earlier in this chapter, you saw how the Wait method on a Task accepts a CancellationToken, allowing for cancellation of this operation.

Note that cancellation for tasks is done in a cooperative manner. In contrast to the Thread.Abort method, which throws an asynchronous ThreadAbortException, a cancellation token merely represents a flag the task should check periodically to quit the task’s code when it sees a request for cancellation. It can do so either by using the IsCancellationRequested property or by invoking ThrowIfCancellationRequested, both on the token value. The latter method throws an OperationCanceledException that takes down the task. Obviously, this error can be observed when waiting for the task or from within continuation functions.

When wait operations occur in a task, the same token should be passed to those such that the cancellation can also unblock such wait operations. Because of the cooperative nature