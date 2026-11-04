# THE EXTENDED ROLE OF TASKFACTORY

The TaskFactory class has many more methods than just StartNew. For most of them, refer to the MSDN documentation. One series of methods I want to point out explicitly, however, is called FromAsync. They enable you to bridge with the Begin/End asynchronous method pair pattern that occurs in quite a few places of the .NET Framework. An example of its use is shown here:

```
var file = File.OpenRead("c:\\temp\\demo.txt");
var buff = new byte[1024];
var task = Task.Factory.FromAsync<byte[], int, int, int>(
    file.BeginRead, file.EndRead, buff, 0, buff.Length, null);
```

The FromAsync factory method overloads take in generic parameters that match the Begin method parameter types and the End method return type. From this, the AsyncCallback and state parameters are omitted because they're always the same in this well-known pattern.

As a result, we get a Task<TResult>, where TResult matches the result type of the imported End method in the asynchronous method pair. The parameters passed to the FromAsync method include delegates to Begin and End methods and the parameters passed to the Begin method. From this point on, the invocation to the asynchronous method is represented as Task<TResult>, which means it can be used in any way the TPL allows.

# Task-Creation Options

Some of the task's constructor overloads and factory's StartNew overloads take in a flags enumeration value of type TaskCreationOptions. Three nontrivial options exist:

+   - LongRunning acts as a hint to the scheduler that the task will be long running. Based on this hint, the scheduler can decide to allocate more worker threads for ad hoc parallelism because the long-running task is there to stay anyway. If this hint is not specified, it takes the scheduler some time to figure out the long-running nature of your task.
+   - AttachedToParent allows for the creation of hierarchical tasks where a parent task can't complete until all of its attached child tasks also complete.
+   - PreferFairness influences scheduling, such that tasks scheduled sooner execute sooner and tasks scheduled later execute later (which is said to be fairer).

Let's focus on the AttachedToParent option for a moment. Here's an example of how a child task can spawn from inside another parent task:

```
var t = Task.Factory.StartNew(() => {
    var s = Task.Factory.StartNew(() => {
        Console.Write("Task " + Task.CurrentId + " waiting for input...");
        return Console.ReadLine();
```