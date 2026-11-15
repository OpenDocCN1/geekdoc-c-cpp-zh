# OUTPUT 19.6:

```
Application started....
Starting thread....
DoWork() started....
Waiting while thread executes....
DoWork() ending...
Thread completed.
Application shutting down....
```

Listing 19.9 begins by instantiating and starting a new Task. Table 19.3 shows the execution path in which each column represents a thread. In cases where code appears on the same row, it is indeterminate which side executes first.

# TABLE 19.3: Execution Path with ManualResetEvent Synchronization

| Main() | DoWork() |
| :--- | :--- |
| ... | |
| Console.WriteLine("Application started...."); | |
| Task task = new Task(DoWork); | |
| Console.WriteLine("Starting thread...."); | |
| task.Start(); | |
| DoWorkSignaledResetEvent.Wait(); | Console.WriteLine("DoWork() started....");<br>DoWorkSignaledResetEvent.Set(); |
| Console.WriteLine("Thread executing..."); | MainSignaledResetEvent.Wait(); |
| MainSignaledResetEvent.Set(); | |
| task.Wait(); | Console.WriteLine("DoWork() ending...."); |