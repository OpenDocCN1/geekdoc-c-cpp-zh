# Chapter 6

Continuation is good for tasks that should be executed only after a certain task is done.
For example, if we have two tasks where the second task must be the result of the first task, then when you use the ContinueWith method, the dispatcher reallocates the thread to continue with the
address supplied by the argument of the ContinueWith method. The code follows:

```
static System::Void StartAddress(Object^ parameter);
static System::Void ContinueAddress(Task^ task);

Task^ task = gcnew(Task(Object^)(&StartAddress), this);
task->Start();
Task^ continueTask = task->ContinueWith(gcnew(Task^>(
&ContinueAddress));
```

The ContinueWith method has many overloads, and you can use it with different values,
such as TaskContinuationOptions, TaskScheduler, or TaskCreationOptions.
More information can be found on MSDN (http://ms.microsoft.com/en-us/
library/system.threading.tasks.continuationoptions%28vs=110%29.
asaspx?7cs-save-lang=6cs-lang=cpp-snippet-1). By the variety of benefits,
The Task object provides the WaitAll and WaitAny methods that are similar to the
WaitForObject and WaitForMultipleObjects APIs.

# Non-blocking synchronization

Many features of .NET programmers must be aware of certain CLR
behavior so as to avoid mistakes when using multiple threads. Both, the Microsoft CLI/
C++ compiler as well as CLR can reorder certain statements at runtime for the sake of
improving efficiency or caching optimizations. For these reasons, it is not always enough
to organize the code, it must be protected as well. That's why .NET provides the
MemoryBarrier class that prevents the effects of instruction reordering and read/write
caching, as in the following class:

```
ref class TestClass
{
public:
TestClass()
{
bState = false;
iValue = 0;
}
static void SetMethod())
{
niValue = 5;
}
```

![](bbox=[0.763, 0.833, 0.823, 0.846])