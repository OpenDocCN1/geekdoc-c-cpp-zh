| Exception | Description |
|---|---|
| System.OverflowException | Thrown when an arithmetic operation in a checked context overflows. |
| System.StackOverflowException | Thrown when the execution stack is exhausted by having too many pending method calls; typically indicative of very deep or unbounded recursion. |
| System.TypeInitializationException | Thrown when a static constructor throws an exception, and no catch clauses exists to catch it. |

> **JON SKEET** This table does not list the most commonly encountered exceptions, but rather the exceptions that can occur naturally within the execution environment as the result of C# operations. You should very rarely (if ever) explicitly throw these exceptions yourself. By contrast, the more commonly encountered exceptions such as System.ArgumentException and its subclasses aren't listed here—they're thrown by a higher level of code, whether system libraries or application code.

> **ERIC LIPPERT** I categorize exceptions as *fatal, boneheaded, vexing, and exogenous.*
> 
> *Fatal* exceptions you neither throw nor catch; they include out of memory, thread abort, and so on. You did not cause the problem and you cannot fix it; the exception is just the mechanism by which you are notified that the world is about to end.
> 
> *Boneheaded* exceptions are avoidable and, therefore, are thrown only by buggy programs; they include null dereferenced, invalid argument, and so on. Never catch them; catching a boneheaded exception is hiding someone's bug. Instead, fix the bug.
> 
> *Vexing* exceptions are exceptions that you have to handle because the API is designed to communicate facts via exceptions. For example, previous versions of the framework lacked an "Is this string a legal GUID?" method; to answer that question, you might try to call the GUID constructor and catch the vexing exception to see if it succeeded or failed. Try to not write code that throws vexing exceptions.
> 
> *Exogenous* exceptions are those you must catch because they indicate unexpected facts about the real world: the CD has been removed from the drive, the network router has been unplugged, and so on.