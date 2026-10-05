```
Task task = new Task(doWork);
task.ContinueWith(doCancellationWork, TaskContinuationOptions.OnlyOnCanceled);
task.Start();
...
private void doWork()
{
    // The task runs this code when it is started
    ...
}
private void doCancellationWork(Task task)
{
    // The task runs this code when doWork completes
    ...
}
```