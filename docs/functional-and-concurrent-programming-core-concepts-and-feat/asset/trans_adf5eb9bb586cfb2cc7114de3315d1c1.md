

The run ends up using three different threads—the thread pool is unlimited—but there are never more than two tasks active at the same time. The overall run takes about 4 seconds, as before.

## 24.7 Parallel Collections

For a final—and simpler—variant of the runner, recall the discussion of parallel collections in Section 21.4. Indeed, given our assumption that the concurrent invocations of the shared function are independent, parallel collections are a perfect match. You can trivially modify the one-line sequential runner implementation used at the beginning of the chapter to introduce parallelism in the execution of the tasks:

```
Scala
class Runner[A](comp: A => Unit):
    def run(inputs: Seq[A]): Unit = for input <- inputs.par do comp(input)
```

Listing 24.6: Parallel execution: parallel collections.

In Scala, for-do is syntactic sugar for a call to higher-order method foreach, and the body of method run could be written as inputs.par.foreach(comp). On parallel collections, foreach is implemented using a common thread pool.² The runner in Listing 24.6, on the same 2, 1, 3 example, produces an output of the following form:

```
main at XX:XX:26.201: START
scala-execution-context-global-16 at XX:XX:26.275: begin 1
scala-execution-context-global-17 at XX:XX:26.275: begin 3
scala-execution-context-global-15 at XX:XX:26.275: begin 2
scala-execution-context-global-16 at XX:XX:27.276: end 1
scala-execution-context-global-15 at XX:XX:28.276: end 2
scala-execution-context-global-17 at XX:XX:29.277: end 3
main at XX:XX:29.277: END
```

## 24.8 Asynchronous Task Submission Using Conditions

Section 24.7 makes concurrent programming look easy—and it sometimes is. However, you should be ready for scenarios that do not quite fit the canned patterns as nicely.

As an illustration, consider a variation of the runner problem that allows more inputs to be added after a run has started. The Runner type is extended with a method addInput that can be used to add one or more input values to an ongoing run. This small change brings a host of problems and design challenges:

²Mechanisms are available that can make parallel collections run on your own thread pool, but they are a bit awkward in Scala.

- The thread that initiates a computation is stuck inside method run for the duration of the run. Adding tasks can happen only in other threads. Accordingly, runner instances now need to be safe when shared by multiple threads.
- There is an inherent race condition between a finishing run and an attempt to add inputs to this run. A method to test the state of a runner—is it running?—would be useless because of a non-atomic check-then-act: A runner could become passive right after it is checked for being active. Instead, method addInput should be expected to fail to add an input to the current run if it comes too late, and it needs a way to indicate such a failure to its caller.
- Waiting for run completion is harder because new tasks can be added after waiting has begun. In particular, the simple approach used earlier, based on a countdown latch created from a known number of tasks, becomes insufficient.
- If runs are allowed to overlap—a new run can be started by another thread before the previous run is finished—and further inputs are added while multiple runs are ongoing, to which run should they be added?
- Alternatively, overlapping runs can be prohibited by making sure method run is not allowed to start until the previous run is completed. This choice requires that the method behaves differently depending on the state of a runner—active versus passive. All the runners implemented so far have been stateless—not counting the thread pool, which is obviously thread-safe. A stateful runner must be designed more carefully when shared among threads.

This section focuses on implementations that share two design choices. First, runs cannot overlap. Method run blocks until the previous run is terminated, then submits a new set of inputs (and blocks again until this new computation is finished). Second, addInput indicates success or failure by returning a Boolean value. (Some of Java’s concurrent collections use the same approach, such as method offer on queues.)

```
class Runner[A](exec: Executor)(comp: A => Unit):
private var active = 0
private var runs = 0
def run(inputs: Seq[A]): Unit = synchronized {
while active != 0 do wait()
val myRun = runs + 1
runs = myRun
active = inputs.length
}
```

```
for input <- inputs do exec.execute(task(input))
while runs == myRun && active != 0 do wait()
}

def addInput(input: A): Boolean = synchronized {
if active == 0 then false
else
active += 1
exec.execute(task(input))
true
}

private def task(in: A): Runnable = () =>
try comp(in)
finally synchronized {
active -= 1
if active == 0 then notifyAll()
}
```

Listing 24.7: Extensible parallel execution using a single condition.

A variable active is used to count the number of tasks still active in the current run. It is incremented when new tasks are submitted to the executor (inside run and addInput) and decremented by the tasks themselves as they terminate. All accesses to this variable are guarded by using synchronized to lock the runner itself.

When trying to add a new input, the code needs to check whether the current run is still ongoing. If active == 0, method addInput returns false immediately. Variable active needs to be zero to start a new run (first line of method run) and also to complete the current run (last line of method run). The last task of a run, when the active count reaches zero, notifies waiting threads that the run is terminated using notifyAll.

The role of variables runs and myRun is subtle and deserves a detailed explanation. Consider first a simpler but incorrect implementation of method run, without these variables:

```
// DON'T DO THIS!
def run(inputs: Seq[A]): Unit = synchronized {
while active != 0 do wait()
active = inputs.length
for input <- inputs do exec.execute(task(input))
while active != 0 do wait()
}
```

Method run waits for the active count to be zero to start a run, and again to terminate the run. Consider now a scenario in which a thread T1 initiates a run and is blocked waiting for the run to terminate and a thread T2 is blocked at the beginning of method run waiting to start a second run. Both threads wait for active to be zero. When the last task of the first run finishes, both threads are notified. At this point, they compete

to relock the runner so as to continue their execution of method run. If thread T2, which is waiting to start a run, gets the lock first, it will submit new tasks to the executor and make the active count non-zero. It will then release the lock and wait for this second run to finish. Thread T1 can then obtain the lock, but it will test active != 0 to be true and will go back waiting—now waiting for the completion of the second run, instead of simply being done with its own run.

This is a difficulty that is actually not uncommon in concurrent programming. You often need to distinguish between separate repetitions of the same state—here, a runner with a positive count of active tasks. For instance, cyclic barriers face a similar challenge when they need to differentiate between two closed states in a closed-open-closed sequence. A common strategy, used here, is to number iterations as a mechanism to distinguish between states that otherwise would be equivalent: Closed-open-closed becomes closed1-open1-closed2, where closed2 is somehow different from closed1.

In the runner example, each run is assigned a unique number,³ and threads that have started a run wait for the active count of their own run to be zero. If a new run has already started—which implies that the active count must have reached zero—those threads are free to terminate their execution, even if the active count has already become non-zero again.⁴

To conclude this section, I will make two final comments on this implementation. First, locking is necessary to manipulate fields active and runs: You need to read and write them within synchronized blocks. However, it is essential that when the tasks apply the runner’s function, they do it without the lock owned. If the code comp(in) is placed inside the synchronized block, all parallelism is lost.

Second, it is necessary to use notifyAll when you wake waiting threads because you need to notify not only the thread that initiated the run that its run is finished, but also possibly another thread that is waiting to start a new run. Two successive calls to notify won’t work because they might notify two threads waiting to start a run, and not the thread that is finishing. In contrast, by using notifyAll, you can notify all the waiting threads, including multiple threads waiting to start a new run, even though only one of them can initiate a run at a time.

Ideally, you would like to notify the thread waiting for its run to finish as well as one of the threads waiting to start a new run. For this, you need to use two separate conditions, one to start a run and another to finish a run:

³Strictly speaking, runs can wrap and reuse a value, but the number of runs needed is so large that it is not an issue in practice: A run will have terminated long before its number is being reused.

⁴To avoid getting stuck because the active count quickly transitions from non-zero to zero and back to non-zero, you might be tempted to implement method run as follows (assuming inputs is not empty):

```
// DON'T DO THIS!
def run(inputs: Seq[A]): Unit = synchronized {
  while active != 0 do wait()
  active = inputs.length
  for input <- inputs do exec.execute(task(input))
  wait()
}
```

This is incorrect because the JVM allows for spurious wake-ups: A thread blocked on wait may—rarely—unblock and continue without having been notified. For this reason, it is important to always stick to the pattern of invoking wait inside a loop that reevaluates the condition a thread is waiting for.

