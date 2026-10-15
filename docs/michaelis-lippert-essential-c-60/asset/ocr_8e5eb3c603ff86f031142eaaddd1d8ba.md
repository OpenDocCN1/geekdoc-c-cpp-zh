H
HideScheduler enum, 759
Hill climbing, 802-803
Hot tasks, 752

I
Id property, 755
IDisposable, 774
In type parameter, 526
InnerExceptions property, 764, 780, 804
IProducerConsumerCollection<T>, 840
IsCancellationRequested property, monitoring, 770-771
IsCompleted property, 754

L
LazyCancellation enum, 759
LINQ queries, running in parallel, 594-595
LongRunning enum, 758
Long-running tasks, 773-774

M
MaxDegreeOfParallelism property, 807
Member names, retrieving, 729
Methods, calling
  applicable calls, 201
  compatible calls, 201
Multithreading, asynchronous tasks
  AggregateException.Handle() method, 764
  antecedent tasks, 757
  associating data with tasks, 755
  asynchronous continuations, 756-762
  AsyncState, 755
  chaining tasks, 757
  cold tasks, 752
  composing large tasks from smaller one, 756-758
  continuation tasks, 757
  ContinueWith() method, 756-758, 760-761, 764-765
  control flow, 755
  creating threads and tasks, 750-751
  hot tasks, 752
  Id property, 755
  introduction, 751-755
  invoking, 751-753
  IsCompleted property, 754
  multithreaded programming complexities, 749-750
observing unhandled exceptions, 764-765
polling a Task<T>, 753-754
registering for notification of task behavior, 760-761
registering for unhandled exceptions, 766-768
Result property, 754
Status property, 754
synchronous delegates, 751
task continuation, 755-762
task identification, 755
task scheduler, 750-751
task status, getting, 754
TaskContinuationOptions enums, 758-759
tasks, definition, 750
tasks vs. delegates, 751
unhandled exception handling with AggregateException, 762-765
unhandled exceptions on a thread, 765-768
UnhandledException event, 766
Multithreading, canceling tasks
CancellationToken object, 769-772
CancellationTokenSource.Cancel() method, 770-771
cooperative cancellation, definition, 769
disposable tasks, 774
IDisposable, 774
IsCancellationRequested property, monitoring, 770-771
long-running tasks, 773-774
obtaining a task, 772-773
TaskCreationOptions.LongRunning option, 773-774
Task.Factory.StartNew() method, 772-773
Task.Run() method, 772-773
WaitHandle, 774
Multithreading, guidelines
long-running tasks, 773-774
parallel loops, 801
unhandled exceptions, 768
Multithreading, parallel loop iterations
Break() method, 808
breaking, 808
canceling, 805-806
exception handling with AggregateException, 803-804
hill climbing, 802-803