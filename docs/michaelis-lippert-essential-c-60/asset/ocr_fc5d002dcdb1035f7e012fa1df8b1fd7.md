continuation chain. These values are flags, so they can be combined using the logical OR operator (|). A brief description of some of the possible flag values appears in Table 18.1; see the online MSDN documentation⁵ for more details.

# TABLE 18.1: List of Available TaskContinuationOptions Enums

| Enum | Description |
|---|---|
| None | This is the default behavior. The continuation task will be executed when the antecedent task completes, regardless of its task status. |
| PreferFairness | If two tasks were both asynchronously started, one before the other, there is no guarantee that the one that was started first actually gets to run first. This flag asks the task scheduler to try to increase the likelihood that the first task started is the first task to execute—something that is particularly relevant when the two tasks you describe are created from different thread pool threads. |
| LongRunning | This tells the task scheduler that the task is likely to be an I/O-bound high-latency task. The scheduler can then allow other queued work to be processed rather than starved because of the long-running task. This option should be used sparingly. |
| AttachedToParent | This specifies that a task should attempt to attach to a parent task within the task hierarchy. |
| DenyChildAttach (.NET 4.5) | This throws an exception if creation of a child task is attempted. If code within the continuation tries to use AttachedToParent, it will behave as if there was no parent. |
| NotOnRanToCompletion* | This specifies that the continuation task should not be scheduled if its antecedent ran to completion. This option is not valid for multitask continuations. |
| NotOnFaulted* | This specifies that the continuation task should not be scheduled if its antecedent threw an unhandled exception. This option is not valid for multitask continuations. |
| OnlyOnCanceled* | This specifies that the continuation task should be scheduled only if its antecedent was canceled. This option is not valid for multitask continuations. |

5. MSDN.NET Framework Developer Center, http://msdn.microsoft.com/en-us/library/system.threading.tasks.taskcontinuationoptions(v=vs.110).aspx.