
# Working with Tasks

The Parallel provides uniquely simple declarative units of work to be run concurrently. The Invoke method and loops are really useful in many situations, but there are scenarios where algorithms cannot be composed so easily. This is where tasks come into the picture.

The name "Task Parallel Library" obviously refers to a task as the most important abstraction in the approach to parallelism. Developers using traditional multi-threading have to think in "path of execution" when programming parallel algorithms. A majority of their efforts tend to be spent on organizing large amount of plumbing code wrapping around relatively small amount of real code related to the algorithm itself. The mission of tasks is to free developers from the "path of execution" thinking, and change their mindset toward the "unit of work" paradigm.

"Unit of work" means that algorithms are gradually decomposed into smaller pieces (units) that run their bodies sequentially. Dependencies among these units are mapped, so that units available for parallel working could be discovered. Figure 10-16 shows an example of this decomposition.

![](img/b5597c749e848b27b0d305153ae16106_481_0.png)

FIGURE 10-16: Decomposing a task to units

The algorithm shown in Figure 10-16 can be decomposed to an Initialization task at the beginning and Consolidation task at the end. The body of the algorithm uses two calculations, Task A and Task B, that are independent and their partial results are combined to the final result in the Consolidation task. These high-level tasks are individually split into smaller units. Arrows show the control flow among them.

When you see this net of tasks, you simply find that can run parallel. It is obvious that Task A and Task B can run side-by-side, and even within them (just as in Initialization and Consolidation), you can easily discover the units that are good candidates for concurrent execution (such as Task I1 and Task I2, Task A1 and Task A2, and the others).

The concept of a task TPL allows you to make the same kind of decomposition programmatically.

> Sometimes it is not obvious how to transform a sequential algorithm into a parallel one, especially when sequential algorithms contain loops where iterations depend on the preceding one. If you do not have the appropriate background in algorithm theory, you can use the web to search for parallel solutions. If you have a concurrent version of an algorithm, you can use the "unit of work" approach to describe it with TPL.

# Creating and Starting Tasks

The TPL is very strong in describing tasks and control flow. Listing 10-14 demonstrates this statement by programmatically defining the task visualized in Figure 10-16. You will get a detailed explanation about this code and the concepts used within, but before getting to, examine the code listing thoroughly, compare it with Figure 10-16, and try to understand it. You'll see it's intuitive.

LISTING 10-14: Describing Tasks in Figure 10-15 with TPL

# LISTING 10-14 (continued)

```
taskB.Start();
Task.WaitAll(taskA, taskB);
Console.WriteLine("Task A' and 'Task B' finished.");
```

```
// Consolidation
var taskConsolidation = Task.Factory.StartNew(() => {
    Console.WriteLine("Prepare to run Task Consolidation");
    var taskC1 = Task.Factory.StartNew(() => {
        Console.WriteLine("Executing Task C1");
        TaskCreationOptions.AttachedToParent
    });
    var taskC2 = Task.Factory.StartNew(() => {
        Console.WriteLine("Executing Task C2");
        TaskCreationOptions.AttachedToParent
    });
});
taskConsolidation.Wait();
Console.WriteLine("Consolidation' finished.");
Console.WriteLine("Press Enter to exit...");
Console.ReadLine();
```

```
}}
```

> Code file [Program.cs] available for download at Wrox.com

When you run this code, it generates output similar to Figure 10-17.

![](img/b5597c749e848b27b0d305153ae16106_484_0.png)

FIGURE 10-17: Output of running the code of Listing 10-14

In Figure, you can see that Task A and Task B run concurrently, because child tasks belonging to Task A and Task B are combed. According to the control flow definition, the last running child of Task A is Task A4, and the last running child of Task B is Task B5.

Now, let's dive into the details of the code.

The most important type in this declaration is the Task class. An instance of this class can be used to represent a task, or its static Factory property can be used to instantiate tasks. With a few exceptions in the sample code, all the tasks are instantiated with the Task.Factory.StartNew() method:

```
var taskA = Task.Factory.StartNew(() =>
{
    Console.WriteLine("Prepare to run 'Task A'");
});
```

StartNew takes an Action as its input parameter (the code uses lambda expressions to represent these action instances), creates a task and immediately starts it. This method has a few overriding other parameters like a CancellationToken, a TaskScheduler, or a TaskCreationOptions instance — these overrides the variety of Task constructors.

Instantiating and starting a task can be separated into two steps:

```
var taskB = new Task(() =>
{
    Console.WriteLine("Prepare to run 'Task B'");
});
taskB.Start();
```

# Defining Control Flow

TPL uses the concept of parent task and child tasks to describe a task hierarchy. "Hierarchy" means a parent task is terminated only when all children complete their activities. You can attach a task to its parent by passing TaskCreationOptions.AttachedToParent to the construction method initializing a task:

```
var taskA = Task.Factory.StartNew(() =>
{
    //
    var task1 = Task.Factory.StartNew(() =>
    {
        Console.WriteLine("Executing 'Task A1'");
    }, TaskCreationOptions.AttachedToParent);
}
});
```

TaskCreationOptions also has other flags influencing how the scheduler should handle the related task (PreferFairness and LongRunning), which can be combined with AttachedToParent.

It is very important to use the AttachedToParent value to mark a child task. Should you miss this markup, the task will be a simple task created within the body of another. In this case, the wrapping task can be finished without waiting for the finalization of the task.

# LISTING 10-15: Tasks without Parent-Child Relationship

When you run this code, you can see that Initialization is finished before task1 and task2.

![](img/b5597c749e848b27b0d305153ae16106_486_0.png)

**Figure 10-18: Main tasks finish before subtasks**

Moreover, if you omit the Thread.Sleep(1000) statement from the code, you will not see task1 and task2 execute, because the application closes.

At a certain point, concurrently running tasks must meet before one. For example, both Task A and Task B must be finished before Consolidation can run; the following code is used:

```
var taskA = Task.Factory.StartNew(() => { });
var taskB = new Task(() => { });
taskB.Start();
task.WaitAll(taskA, taskB);
```

Task 3 uses the Wait method before Task 4 is:

```
Task.Factory.StartNew(() =>
  Console.WriteLine("Exec A3");
  TaskCreationOptions.AttachedToParent).Wait();
Task.Factory.StartNew(() =>
  Console.WriteLine("Exec A4");
  TaskCreationOptions.AttachedToParent);
```

Looking back at List 10-14 you can see that neither Initialization nor Wait or WaitAll for their concurrently running Task 11, Task 12 and TaskC1, C2 pairs. Because they are children, their parents will wait for their completion.

The sequential relationship between tasks (or among a chain of tasks) between B1 and B3 is handled with the ContinueWith method. Of course, you could use Wait instead of ContinueWith:

```
var taskB1 = Task.Factory.StartNew(() => { ... });
taskB1.Wait();
var taskB3 = Task.Factory.StartNew(() => { ... });
```

# Tasks with Results

In many cases, tasks are to compute a certain value or a complex structure - for example a customer account report. You can use the Task<TResult> type for this purpose. Task<TResult> is
