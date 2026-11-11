
```java
for (Path file : files)
{
    Callable<Long> task = () -> occurrences(word, file);
    tasks.add(task);
}
```

Then we pass the tasks to an executor service:

```java
ExecutorService executor = Executors.newCachedThreadPool();
List<Future<Long>> results = executor.invokeAll(tasks);
```

To get the combined count, we add all results, blocking until they are available:

```java
long total = 0;
for (Future<Long> result : results)
    total += result.get();
```

The program also displays the time spent during the search. Unzip the source code for the JDK somewhere and run the search. Then replace the executor service with a single-thread executor and try again to see whether the concurrent computation was faster.

In the second part of the program, we search for the first file that contains the given word. We use invokeAny to parallelize the search. Here, we have to be more careful about formulating the tasks. The invokeAny method terminates as soon as any task returns. So we cannot have the search tasks return a boolean to indicate success or failure. We don't want to stop searching when a task failed. Instead, a failing task throws a NoSuchElementException. Also, when one task has succeeded, the others are canceled. Therefore, we monitor the interrupted status. If the underlying thread is interrupted, the search task prints a message before terminating, so that you can see that the cancellation is effective.

```java
public static Callable<Path> searchForTask(String word, Path path)
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
```

For informational purposes, this program prints out the largest pool size during execution. This information is not available through the ExecutorService interface. For that reason, we had to cast the pool object to the ThreadPoolExecutor class.

> **TIP:** As you read through this program, you can appreciate how useful executor services are. In your own programs, you should use executor services to manage threads instead of launching threads individually.

## Listing 12.8 `executors/ExecutorDemo.java`

```java
package executors;

import java.io.*;
import java.nio.file.*;
import java.time.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

/**
 * This program demonstrates the Callable interface and executors.
 * @version 1.0 2018-01-04
 * @author Cay Horstmann
 */
public class ExecutorDemo
{
   /**
    * Counts occurrences of a given word in a file.
    * @return the number of times the word occurs in the given word
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
    * @return the search task that yields the path upon success
    */
   public static Callable<Path> searchForTask(String word, Path path)
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
```

_(Continues)_

### Listing 12.8 (Continued)

```java
75 public static void main(String[] args)
76     throws InterruptedException, ExecutionException, IOException
77 {
78     try (var in = new Scanner(System.in))
79     {
80         System.out.print("Enter base directory (e.g. /opt/jdk-9-src): ");
81         String start = in.nextLine();
82         System.out.print("Enter keyword (e.g. volatile): ");
83         String word = in.nextLine();
84 
85         Set<Path> files = descendants(Path.of(start));
86         var tasks = new ArrayList<Callable<Long>>();
87         for (Path file : files)
88         {
89             Callable<Long> task = () -> occurrences(word, file);
90             tasks.add(task);
91         }
92         ExecutorService executor = Executors.newCachedThreadPool();
93         // use a single thread executor instead to see if multiple threads
94         // speed up the search
95         // ExecutorService executor = Executors.newSingleThreadExecutor();
96 
97         Instant startTime = Instant.now();
98         List<Future<Long>> results = executor.invokeAll(tasks);
99         long total = 0;
100        for (Future<Long> result : results)
101            total += result.get();
102        Instant endTime = Instant.now();
103        System.out.println("Occurrences of " + word + ": " + total);
104        System.out.println("Time elapsed: "
105            + Duration.between(startTime, endTime).toMillis() + " ms");
106 
107        var searchTasks = new ArrayList<Callable<Path>>();
108        for (Path file : files)
109            searchTasks.add(searchForTask(word, file));
110        Path found = executor.invokeAny(searchTasks);
111        System.out.println(word + " occurs in: " + found);
112 
113        if (executor instanceof ThreadPoolExecutor) // the single thread executor isn't
114            System.out.println("Largest pool size: "
115                + ((ThreadPoolExecutor) executor).getLargestPoolSize());
116        executor.shutdown();
117    }
118 }
119 }
```

```java
        break problem into subproblems
        recursively solve each subproblem
        combine the results
    }
```

One example is image processing. To enhance an image, you can transform the top half and the bottom half. If you have enough idle processors, those operations can run in parallel. (You will need to do a bit of extra work along the strip that separates the two halves, but that’s a technical detail.)

Here, we discuss a simpler example. Suppose we want to count how many elements of an array fulfill a particular property. We cut the array in half, compute the counts of each half, and add them up.

To put the recursive computation in a form that is usable by the framework, supply a class that extends `RecursiveTask<T>` (if the computation produces a result of type `T`) or `RecursiveAction` (if it doesn't produce a result). Override the `compute` method to generate and invoke subtasks, and to combine their results.

```java
class Counter extends RecursiveTask<Integer>
{
    ...
    protected Integer compute()
    {
        if (to - from < THRESHOLD)
        {
            solve problem directly
        }
        else
        {
            int mid = (from + to) / 2;
            var first = new Counter(values, from, mid, filter);
            var second = new Counter(values, mid, to, filter);
            invokeAll(first, second);
            return first.join() + second.join();
        }
    }
}
```

Here, the `invokeAll` method receives a number of tasks and blocks until all of them have completed. The `join` method yields the result. Here, we apply `join` to each subtask and return the sum.

> **NOTE:** There is also a `get` method for getting the current result, but it is less attractive since it can throw checked exceptions that we are not allowed to throw in the `compute` method.
