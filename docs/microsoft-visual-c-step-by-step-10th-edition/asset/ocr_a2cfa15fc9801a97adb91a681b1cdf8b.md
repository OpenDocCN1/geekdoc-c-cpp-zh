```
Task task = new Task(doWork);
task.ContinueWith(doMoreWork,
    TaskContinuationOptions.NotOnFaulted);
```