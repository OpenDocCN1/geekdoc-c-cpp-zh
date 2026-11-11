returns a thread pool that uses the given number of threads to schedule tasks.

+   - `ScheduledExecutorService newSingleThreadScheduledExecutor()` returns an executor that schedules tasks in a single thread.

# `java.util.concurrent.ExecutorService`⁵

+   - `Future<T> submit(Callable<T> task)`

+   - `Future<T> submit(Runnable task, T result)`

+   - `Future<?> submit(Runnable task)` submits the given task for execution.

+   - `void shutdown()` shuts down the service, completing the already submitted tasks but not accepting new submissions.

# `java.util.concurrent.ThreadPoolExecutor`⁵

+   - `int getLargestPoolSize()` returns the largest size of the thread pool during the life of this executor.

# `java.util.concurrent.ScheduledExecutorService`⁵

+   - `ScheduledFuture<V> schedule(Callable<V> task, long time, TimeUnit unit)`