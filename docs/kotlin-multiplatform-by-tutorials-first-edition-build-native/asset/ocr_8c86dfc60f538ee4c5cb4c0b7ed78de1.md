its current state:

+   - isActive : If it's currently running.

+   - isCompleted : If all of its work, as well as its children, have ended. Moreover, when the current Job gets cancelled — or fails — its value will be true.

+   - isCancelled : When the current job gets cancelled or fails.

The difference between a SupervisorJob and a Job is that they have different policies. In the first one, the children behave independently — if one fails, the others won't be affected — whereas in the second one, if a parent fails, all of its children will be cancelled.

+   - Dispatchers : Define in which thread a coroutine should run:

+   - Default : Uses a shared pool of threads.

+   - Main : Has different behaviors depending on the platform that's currently running. On JVM and Android, Main corresponds to the UI-thread, and should only be used for operations that update the UI. On Native, it's the same as the Default dispatcher.

+   - Unconfined : Doesn't have any associated threading policy. Doesn't switch to any specific thread.

+   - IO : Should be used for long-running and heavy tasks because it's one shared pool of threads, optimized for these types of operations. It's currently not available for iOS.

When you create a coroutine, you have to define the dispatcher where it should run, but you can always switch the context later on its execution by calling withContext with the prepended Dispatcher as an argument.

In the fetchMyGravatar function from FeedPresenter.kt, you're running the coroutine in the main thread, although the only part that is necessary to run are the onSuccess and onFailure calls. You can update the existing function to use the Default thread for the network requests and when the data is available, switch to the Main thread so the UI can be updated:

```
public fun fetchMyGravatar(cb: FeedData) {
    //1
    CoroutineScope(Dispatchers.Default).launch {
    //2
    val profile = feed.invokeGetMyGravatar(
        hash = md5(GRAVATAR_EMAIL)
    )

    //3
    withContext(Dispatchers.Main) {
}
```