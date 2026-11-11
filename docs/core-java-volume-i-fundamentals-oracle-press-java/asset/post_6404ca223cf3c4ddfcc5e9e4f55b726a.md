
```java
List<Callable<T>> tasks = ...;
List<Future<T>> results = executor.invokeAll(tasks);
for (Future<T> result : results)
    processFurther(result.get());
```

In the for loop, the first call `result.get()` blocks until the first result is available. That is not a problem if all tasks finish in about the same time. However, it may be worth obtaining the results in the order in which they are available. This can be arranged with the `ExecutorCompletionService`.

Start with an executor, obtained in the usual way. Then construct an `ExecutorCompletionService`. Submit tasks to the completion service. The service manages a blocking queue of future objects, containing the results of the submitted tasks as they become available. Thus, a more efficient organization for the preceding computation is the following:

```java
var service = new ExecutorCompletionService<T>(executor);
for (Callable<T> task : tasks) service.submit(task);
for (int i = 0; i < tasks.size(); i++)
    processFurther(service.take().get());
```

The program in [Listing 12.8](#) shows how to use callables and executors. In the first computation, we count how many files in a directory tree contain a given word. We make a separate task for each file:

```java
Set<Path> files = descendants(Path.of(start));
var tasks = new ArrayList<Callable<Long>>();
for (Path file : files)
{
    Callable<Long> task = () -> occurrences(word, file);
    tasks.add(task);
}
```

Then we pass the tasks to an executor service:

```java
{
    System.out.println("Search in " + path + " canceled.");
    return null;
}
}
throw new NoSuchElementException();
}
};
}
```

For informational purposes, this program prints out the largest pool size during execution. This information is not available through the ExecutorService interface. For that reason, we had to cast the pool object to the ThreadPoolExecutor class.

![](img/0e7b74ef51a065c077b42cd87b362288_1150_0.png)

> **TIP:**
>
> As you read through this program, you can appreciate how useful executor services are. In your own programs, you should use executor services to manage threads instead of launching threads individually.

### Listing 12.8 `executors/ExecutorDemo.java`

```java
package executors;

import java.io.*;
import java.nio.file.*;
import java.time.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

/**
 * This program demonstrates the Callable interface and
 * executors.
 *
 * @version 1.01 2021-05-30
 * @author Cay Horstmann
 */
public class ExecutorDemo
{
   /**
    * Counts occurrences of a given word in a file.
    * @return the number of times the word occurs in the given file
    */
   public static long occurrences(String word, Path path)
   {
      try (var in = new Scanner(path))
      {
         int count = 0;
         while (in.hasNext())
            if (in.next().equals(word)) count++;
         return count;
      }
      catch (IOException ex)
      {
         return 0;
      }
   }

   /**
    * Returns all descendants of a given directory--see Chapters 1 and 2 of Volume II.
    * @param rootDir the root directory
    * @return a set of all descendants of the root directory
    */
   public static Set<Path> descendants(Path rootDir) throws IOException
   {
      try (Stream<Path> entries = Files.walk(rootDir))
      {
         return entries.filter(Files::isRegularFile)
               .collect(Collectors.toSet());
      }
   }

   /**
    * Yields a task that searches for a word in a file.
    * @param word the word to search
    * @param path the file in which to search
    * @return the search task that yields the path upon
    * success
    */
   public static Callable<Path> searchForTask(String word,
         Path path)
   {
      return () -> {
         try (var in = new Scanner(path))
         {
            while (in.hasNext())
            {
               if (in.next().equals(word)) return path;
               if (Thread.currentThread().isInterrupted())
               {
                  System.out.println("Search in " + path + " canceled.");
                  return null;
               }
            }
            throw new NoSuchElementException();
         }
      };
   }

   public static void main(String[] args)
         throws InterruptedException, ExecutionException, IOException
   {
      try (var in = new Scanner(System.in))
      {
         System.out.print("Enter base directory (e.g. /opt/jdk-src): ");
         String start = in.nextLine();
         System.out.print("Enter keyword (e.g. volatile): ");
         String word = in.nextLine();

         Set<Path> files = descendants(Path.of(start));
         var tasks = new ArrayList<Callable<Long>>();
         for (Path file : files)
         {
            Callable<Long> task = () -> occurrences(word, file);
            tasks.add(task);
         }
         ExecutorService executor =
               Executors.newCachedThreadPool();
         // use a single thread executor instead to see if multiple threads
         // speed up the search
         // ExecutorService executor =
         //       Executors.newSingleThreadExecutor();

         Instant startTime = Instant.now();
         List<Future<Long>> results = executor.invokeAll(tasks);
         long total = 0;
         for (Future<Long> result : results)
            total += result.get();
         Instant endTime = Instant.now();
         System.out.println("Occurrences of " + word + ": " + total);
         System.out.println("Time elapsed: "
               + Duration.between(startTime, endTime).toMillis() + " ms");

         var searchTasks = new ArrayList<Callable<Path>>();
         for (Path file : files)
            searchTasks.add(searchForTask(word, file));
         Path found = executor.invokeAny(searchTasks);
         System.out.println(word + " occurs in: " + found);

         if (executor instanceof ThreadPoolExecutor tpExecutor)
            // the single thread executor isn't
            System.out.println("Largest pool size: "
                  + tpExecutor.getLargestPoolSize());
         executor.shutdown();
      }
   }
}
```

### java.util.concurrent.ExecutorService 5

- `T invokeAny(Collection<Callable<T>> tasks)`
- `T invokeAny(Collection<Callable<T>> tasks, long timeout, TimeUnit unit)`  
  executes the given tasks and returns the result of one of them. The second method throws a `TimeoutException` if a timeout occurs.
- `List<Future<T>> invokeAll(Collection<Callable<T>> tasks)`
- `List<Future<T>> invokeAll(Collection<Callable<T>> tasks, long timeout, TimeUnit unit)`  
  executes the given tasks and returns the results of all of them. The second method throws a `TimeoutException` if a timeout occurs.

### java.util.concurrent.ExecutorCompletionService<V> 5

- `ExecutorCompletionService(Executor e)`  
  constructs an executor completion service that collects the results of the given executor.
- `Future<V> submit(Callable<V> task)`
- `Future<V> submit(Runnable task, V result)`  
  submits a task to the underlying executor.
- `Future<V> take()`  
  removes the next completed result, blocking if no completed results are available.
- `Future<V> poll()`
- `Future<V> poll(long time, TimeUnit unit)`  
  removes and returns the next completed result, or returns `null` if no completed results are available. The second method waits for the given time.

## 12.6.4 The Fork-Join Framework

Some applications use a large number of threads that are mostly idle. An example would be a web server that uses one thread per connection. Other applications use one thread per processor core, in order to carry out computationally intensive tasks, such as image or video processing. The fork-join framework, which appeared in Java 7, is designed to support the latter. Suppose you have a processing task that naturally decomposes into subtasks, like this:

```text
if (problemSize < threshold)
    solve problem directly
else
{
    break problem into subproblems
    recursively solve each subproblem
    combine the results
}
```

One example is image processing. To enhance an image, you can transform the top half and the bottom half. If you have enough idle processors, those operations can run in parallel. (You will need to do a bit of extra work along the strip that separates the two halves, but that’s a technical detail.)

Here, we discuss a simpler example. Suppose we want to count how many elements of an array fulfill a particular property. We cut the array in half, compute the counts of each half, and add them up.
