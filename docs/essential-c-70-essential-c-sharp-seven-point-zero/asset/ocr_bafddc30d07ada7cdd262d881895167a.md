```
Parallel.ForEach(files, (fileName) =>
{
	Encrypt(fileName);
});
}
// ... }
```

In this example, we call a method that encrypts each file within the files collection. It does so in parallel, executing as many threads as the TPL determines is efficient.

# ADVANCED TOPIC

# How the TPL Tunes Its Own Performance

The default scheduler within the TPL targets the thread pool, resulting in a variety of heuristics to try to ensure that the right number of threads are executing at any one time. Two of the heuristics it uses are **hill climbing** and **work stealing**.

The hill climbing algorithm involves creating threads to run tasks, and then monitoring the performance of those tasks to try to experimentally determine the point at which adding more threads begins making performance worse. Once that point is reached, the number of threads can then be decreased back to the number that produced the best performance.

The TPL associates top-level tasks that are waiting to be executed with no particular thread. If, however, a task running on a thread itself creates another task, the newly created task is associated with that thread automatically. When the new child task is eventually scheduled to run, it usually runs on the same thread as the task that created it. The work stealing algorithm identifies threads that have an unusually large or unusually small amount of pending work; a thread that has too few tasks associated with it will sometimes “steal” not-yet-executed tasks from threads that have too many tasks waiting to run.

The key feature of these algorithms is that they enable the TPL to dynamically tune its own performance to mitigate processor overscheduling and underscheduling and to balance the work among the available processors.

The TPL generally does a good job of tuning its own performance, but you can help it do a better job by providing hints about the best course of