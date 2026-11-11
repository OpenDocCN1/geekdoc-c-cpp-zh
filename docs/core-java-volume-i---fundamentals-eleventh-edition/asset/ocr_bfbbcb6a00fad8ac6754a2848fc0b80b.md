**java.util.concurrent.Executors** 5 *(Continued)*

- `ScheduledExecutorService newScheduledThreadPool(int threads)`  
  returns a thread pool that uses the given number of threads to schedule tasks.
- `ScheduledExecutorService newSingleThreadScheduledExecutor()`  
  returns an executor that schedules tasks in a single thread.

**java.util.concurrent.ExecutorService** 5

- `Future<T> submit(Callable<T> task)`
- `Future<T> submit(Runnable task, T result)`
- `Future<?> submit(Runnable task)`  
  submits the given task for execution.
- `void shutdown()`  
  shuts down the service, completing the already submitted tasks but not accepting new submissions.

**java.util.concurrent.ThreadPoolExecutor** 5

- `int getLargestPoolSize()`  
  returns the largest size of the thread pool during the life of this executor.

**java.util.concurrent.ScheduledExecutorService** 5

- `ScheduledFuture<?> schedule(Callable<V> task, long time, TimeUnit unit)`
- `ScheduledFuture<?> schedule(Runnable task, long time, TimeUnit unit)`  
  schedules the given task after the given time has elapsed.
- `ScheduledFuture<?> scheduleAtFixedRate(Runnable task, long initialDelay, long period, TimeUnit unit)`  
  schedules the given task to run periodically, every period units, after the initial delay has elapsed.
- `ScheduledFuture<?> scheduleWithFixedDelay(Runnable task, long initialDelay, long delay, TimeUnit unit)`  
  schedules the given task to run periodically, with delay units between completion of one invocation and the start of the next, after the initial delay has elapsed.